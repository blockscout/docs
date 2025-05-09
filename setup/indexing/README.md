# Indexing

{% hint style="success" %}
🚗  [Autoscout is now available](../../using-blockscout/autoscout.md), providing a simple one-click explorer deployment with Blockscout's optimized hosting infrastructure. Use it for early testing, modifications, and launching a full production-grade explorer. [**Get Started Now**](../../using-blockscout/autoscout.md) **and have your explorer up-and-running in minutes.**
{% endhint %}

BlockScout can take some time to fully index a chain. Larger chains require more time. Indexing starts from the head of the chain (the current block) and goes backwards towards the genesis block. The genesis block is the final block indexed during this process.

### Messages during indexing

1. **n% Blocks Indexed - We're indexing this chain right now. Some of the counts may be inaccurate.** This means blocks are still being collected and processed by BlockScout. The message should disappear once the genesis block is indexed.
2. **Blocks With Internal Transactions Indexed - We're indexing this chain right now. Some of the counts may be inaccurate.** This means BlockScout has collected all blocks but is still indexing internal transactions using the archive node tracing api. This message will disappear when `INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER=true` is provided.

### Monitoring indexing processes

#### Monitoring blocks/transactions indexing

1. Block count should be close to the number of the blocks in the chain. Query using `SELECT COUNT(1) FROM blocks;` \~= num of blocks in the chain.
2. The number of missing blocks in the chain can be monitored with this query:

```
SELECT COUNT(DISTINCT b1.number)
FROM generate_series(0, (SELECT MAX(number) FROM blocks)) AS b1(number)
WHERE NOT EXISTS (
    SELECT 1 FROM blocks b2 WHERE b2.number=b1.number AND b2.consensus
);
```

#### Monitoring internal transactions indexing

Internal transaction fetching can be monitored with this query: `SELECT COUNT(1) FROM pending_block_operations;` It should move towards zero during internal transaction processing.
