---
description: ShareLock is the row-level locking mechanism used internally by PostgreSQL.
---

# ShareLock

### Deadlocks and prevention

When several DB transactions are acting on multiple rows of the same table, it's possible to incur in a deadlock and so into an error. This can be prevented by enforcing the same consistent order of lock acquisition on _all_ the transactions performing `INSERT`, `UPDATE` or `DELETE` on a given table.

On top of this, if multiple DB transactions act on multiple tables a deadlock will occur, even if they follow the order on each table described above, if they acquire locks on said tables in a different order. This can also be prevented by using a consistent order of lock acquisition _between_ different tables.

### Imposing the lock acquisition order on a table with Ecto

When `INSERT`ing a list of rows Postgres will respect the order in which they appear in the query, so the reordering can happen beforehand.

For example, this will work:

```elixir
entries = [...]

ordered_entries = Enum.sort_by(entries, & &1.id)

Repo.insert_all(__MODULE__, ordered_entries)
```

Performing `UPDATE`s is trickier because there is no `ORDER BY` clause. The solution to this is to `JOIN` on a subquery that `SELECT`s with the option `FOR UPDATE`.

Using Ecto this can be done, for example, like this:

```elixir
query =
  from(
    entry in Entry,
    where: not is_nil(entry.value),
    order_by: entry.id,
    lock: "FOR UPDATE"
  )

Repo.update_all(
  from(e in Entry, join: s in subquery(query), on: e.id == s.id),
  [set: [value: nil]],
  timeout: timeout)
```

`DELETE` has the same quirks as `UPDATE` and it is too solved in the same way.

For example:

```elixir
query =
  from(
    entry in Entry,
    where: is_nil(entry.value),
    order_by: entry.id,
    lock: "FOR UPDATE"
  )

Repo.delete_all(from(e in Entry, join: s in subquery(query), on: e.id == s.id))
```

### Imposing the lock acquisition order between tables with Ecto

When using an `Ecto.Multi` to perform `INSERT`, `UPDATE` or `DELETE` on multiple tables the order to keep is between different operation. For example, supposing `EntryA` was established to be modified before `EntryB`, this is not correct:

```elixir
Multi.new()
|> Multi.run(:update_b, fn repo, _ ->
  # operations with ordered locks on `EntryB`
end)
|> Multi.run(:update_a, fn repo, _ ->
  # operations with ordered locks on `EntryA`
end)
|> Repo.transaction()
```

When possible, the simple solution is to move `:update_a` to be before `:update_b`. When not possible, for instance if `:update_a` depends on the result of `:update_b`, this can be solved by acquiring the locks in a separate operation.

For example:

```elixir
Multi.new()
|> Multi.run(:acquire_a, fn repo, _ ->
  # acquire locks in order on `EntryA`
end)
|> Multi.run(:update_b, fn repo, _ ->
  # operations with ordered locks on `EntryB`
end)
|> Multi.run(:update_a, fn repo, %{acquire_a: values} ->
  # operations (no need to enforce order again) on `EntryA`
end)
|> Repo.transaction()
```

Note also that for the same reasons multiple operations on the same table in the same transaction are not safe to perform if they each acquire locks in order, because locks are not released until the transaction is committed.

### Order used for Explorer's tables

This is a complete list of the ordering currently in use on each table. It also specifies the order between tables in the same transaction: locks for a table on top need to be acquired before those from a table on the bottom.

Note that this should always be enforced because as long as there is one DB transaction performing in a different order there is the possibility of a deadlock.

| schema module | table name | ordered by |
| :--- | :--- | :--- |
| Explorer.Chain.Address | addresses | \[asc: :hash\] |
| Explorer.Chain.Address.Name | address\_names | \[asc: :address\_hash, asc: :name\] |
| Explorer.Chain.Address.CoinBalance | address\_coin\_balances | \[asc: :address\_hash, asc: :block\_number\] |
| Explorer.Chain.Block | blocks | \[asc: :hash\] |
| Explorer.Chain.Block.SecondDegreeRelation | block\_second\_degree\_relations | \[asc: :nephew\_hash, asc: :uncle\_hash\] |
| Explorer.Chain.Block.Reward | block\_rewards | \[asc: :address\_hash, asc: :address\_type, asc: :block\_hash\] |
| Explorer.Chain.Block.EmissionReward | emission\_rewards | \[asc: :block\_range\] |
| Explorer.Chain.Transaction | transactions | \[asc: :hash\] |
| Explorer.Chain.Transaction.Fork | transaction\_forks | \[asc: :uncle\_hash, asc: :index\] |
| Explorer.Chain.Log | logs | \[asc: :transaction\_hash, asc: :index\] |
| Explorer.Chain.InternalTransaction | internal\_transactions | \[asc: :transaction\_hash, asc: :index\] |
| Explorer.Chain.Token | tokens | \[asc: :contract\_address\_hash\] |
| Explorer.Chain.TokenTransfer | token\_transfers | \[asc: :transaction\_hash, asc: :log\_index\] |
| Explorer.Chain.TransactionAction | transaction\_actions | \[asc: :hash, asc: :log\_index\] |
| Explorer.Chain.PolygonEdge.Deposit | polygon\_edge\_deposits | \[asc: :msg\_id\] |
| Explorer.Chain.PolygonEdge.DepositExecute | polygon\_edge\_deposit\_executes | \[asc: :msg\_id\] |
| Explorer.Chain.PolygonEdge.Withdrawal | polygon\_edge\_withdrawals | \[asc: :msg\_id\] |
| Explorer.Chain.PolygonEdge.WithdrawalExit | polygon\_edge\_withdrawal\_exits | \[asc: :msg\_id\] |
| Explorer.Chain.Optimism.OutputRoot | op\_output\_roots | \[asc: :l2\_output\_index\] |
| Explorer.Chain.Optimism.TxnBatch | op\_transaction\_batches | \[asc: :l2\_block\_number\] |
| Explorer.Chain.Optimism.Deposit | op\_deposits | \[asc: :l2\_transaction\_hash\] |
| Explorer.Chain.Optimism.DisputeGame | op\_dispute\_games | \[asc: :index\] |
| Explorer.Chain.Optimism.FrameSequence | op\_frame\_sequences | \[asc: :id\] |
| Explorer.Chain.Optimism.FrameSequenceBlob | op\_frame\_sequence\_blobs | \[asc: :id\] |
| Explorer.Chain.Optimism.WithdrawalEvent | op\_withdrawal\_events | \[asc: :withdrawal\_hash, asc: :l1\_event\_type\] |
| Explorer.Chain.Optimism.Withdrawal | op\_withdrawals | \[asc: :msg\_nonce\] |
| Explorer.Chain.Optimism.EIP1559ConfigUpdate | op\_eip1559\_config\_updates | \[asc: :l2\_block\_number\] |
| Explorer.Chain.Optimism.InteropMessage | op\_interop\_messages | \[asc: :nonce, asc: :init\_chain\_id\] |
| Explorer.Chain.Address.TokenBalance | address\_token\_balances | \[asc: :address\_hash, asc: :token\_contract\_address\_hash, asc: :block\_number\] |
| Explorer.Chain.Address.CurrentTokenBalance | address\_current\_token\_balances | \[asc: :token\_contract\_address\_hash, asc: :token\_id, asc: :address\_hash\] |
| Explorer.Chain.Scroll.Batch | scroll\_batches | \[asc: number\] |
| Explorer.Chain.Scroll.BatchBundle | scroll\_batch\_bundles | \[asc: final\_batch\_number\] |
| Explorer.Chain.Scroll.Bridge | scroll\_bridge | \[asc: :type, asc: message\_hash\] |
| Explorer.Chain.Scroll.L1FeeParam | scroll\_l1\_fee\_params | \[asc: :block\_number, asc: tx\_index, asc: name\] |
| Explorer.Chain.Shibarium.Bridge | shibarium\_bridge | \[asc: :operation_hash, asc: l1\_transaction\_hash, asc: l2\_transaction\_hash\] |
| Explorer.Chain.StakingPool | staking\_pools | \[asc: :staking\_address\_hash\] |
| Explorer.Chain.StakingPoolsDelegator | staking\_pools\_delegators | \[asc: :delegator\_address\_hash, asc: :pool\_address\_hash\] |
| Explorer.Chain.ContractMethod | contract\_methods | \[asc: :identified, asc: :abi\] |
| Explorer.Market.MarketHistory | market\_history | \[asc: :date\] |
| Explorer.Chain.Withdrawal | withdrawals | \[asc: :index\] |
| Explorer.Chain.Zkevm.TransactionBatch | zkevm\_transaction\_batches | \[asc: :number\] |
| Explorer.Chain.Zkevm.BatchTransaction | zkevm\_batch\_l2\_transactions | \[asc: :hash\] |
| Explorer.Chain.Zkevm.LifecycleTransaction | zkevm\_lifecycle\_l1\_transactions | \[asc: :id\] |
| Explorer.Chain.Zkevm.Bridge | zkevm\_bridge | \[asc: :type, asc: :index\] |
| Explorer.Chain.Zkevm.BridgeL1Token | zkevm\_bridge\_l1\_tokens | \[asc: :address\] |
| Explorer.Chain.ZkSync.TransactionBatch | zksync\_transaction\_batches | \[asc: :number\] |
| Explorer.Chain.ZkSync.BatchBlock | zksync\_batch\_blocks | \[asc: :hash\] |
| Explorer.Chain.ZkSync.BatchTransaction | zksync\_batch\_transactions | \[asc: :hash\] |
| Explorer.Chain.ZkSync.LifecycleTransaction | zksync\_lifecycle\_transactions | \[asc: :id\] |
| Explorer.Chain.Celo.EpochReward | celo\_epoch\_rewards | \[asc: :block\_hash\] |
| Explorer.Chain.Celo.PendingEpochBlockOperation | celo\_pending\_epoch\_block\_operations | \[asc: :block\_hash\] |
| Explorer.Chain.Celo.ValidatorGroupVote | celo\_epoch\_validator\_group\_votes | \[asc: :transaction\_hash, asc: :account\_address\_hash, asc: :group\_address\_hash\] |
| Explorer.Chain.Celo.ElectionReward | celo\_election\_rewards | \[asc: :block\_hash, asc: type, asc: :account\_address\_hash, asc: :associated\_account\_address\_hash\] |
| Explorer.Chain.Zilliqa.QuorumCertificate | zilliqa\_quorum\_certificates | \[asc: :block\_hash\] |
| Explorer.Chain.Zilliqa.AggregateQuorumCertificate | zilliqa\_aggregate\_quorum\_certificates | \[asc: :block\_hash\] |
| Explorer.Chain.Zilliqa.NestedQuorumCertificate | zilliqa\_nested\_quorum\_certificates | \[asc: :block\_hash, asc: proposed\_by\_validator\_index] |
| Explorer.Chain.Filecoin.PendingAddressOperation | filecoin\_pending\_address\_operations | \[asc: :address\_hash] |
