# How do I fix indexer timeouts?

BlockScout utilizes two separate indexers in order to index the network history as well as keep up with new incoming blocks. Due to this process, a node may become overloaded and not respond to BlockScout's RPC requests within the designated timeout period.

The indexer umbrella application can be tweaked to meet your node's size and responsiveness. Outlined below are the locations and adjustments that can be made to each fetcher.

| Fetcher | Description | Default Values |
| :--- | :--- | :--- |
| [Catchup Block Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/block/catchup/fetcher.ex#L24) | This fetcher indexes blocks, transactions and receipts starting from the tip of the chain working backward to the Genesis block. | Batch Size: 10, Concurrency: 10 |
| [Internal Transaction Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/internal_transaction/fetcher.ex#L20) | This fetcher indexes internal transactions. For the real-time fetcher this process is done synchronously and for the catchup fetcher, this process is done asynchronously. | Batch Size: 10, Concurrency: 4 |
| [Coin Balance Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/coin_balance/fetcher.ex#L22) | This fetcher indexes each coin balance at the block height the address was interacted with. | Batch Size: 500, Concurrency: 4 |
| [Uncle Block Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/block/uncle/fetcher.ex#L22) | This fetcher indexes non-consensus blocks, transactions, and receipts. | Batch Size: 10, Concurrency: 10 |
| [Token Balance Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/token_balance/fetcher.ex#L29) | This fetcher indexes token balances. Note you may experience some token balances that cannot be fetched due to a malformed smart contract or other functions that do not allow a balance to be fetched. | Batch Size: 100, Concurrency: 10 |
| [Token Fetcher](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/indexer/lib/indexer/token/fetcher.ex#L18) | This indexer fetches the metadata for a token contract | Batch Size: 1, Concurrency: 10 |

## Understanding Errors and Timeouts

`application=indexer fetcher=coin_balance count=500 error_count=500 [error] failed to fetch: :timeout`

In the error provided above, we can tell that the **indexer** application failed to fetch **500** **coin balances** due to a **timeout** error. Usually, when an indexer starts to receive timeouts, many more timeouts from other fetchers will occur as well.

### Resolving Timeout Issues

The best action to take when fetchers start to receive timeouts is to lower the batch size and concurrency of a few fetchers which will put less pressure on the node.

The two indexers that cause the most strain to the node are the block fetcher and the internal transactions fetcher. It would be advised to cut these fetchers values in half and restart the application. A restart of the node may also be required.

### Other  Actions

BlockScout comes equipped with functionality to automatically stop sending requests for `n` seconds if timeouts are detected. You may adjust these settings by setting a different value for `wait_per_timeout`.

[https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/ethereum\_jsonrpc/config/config.exs\#L3-L9](https://github.com/poanetwork/blockscout/blob/1475e3bfd002d9397efd0f0cc29c20f39a70d023/apps/ethereum_jsonrpc/config/config.exs#L3-L9)

{% hint style="success" %}
Content moved from [https://forum.poa.network/t/faq-how-do-i-fix-indexer-timeouts/1829](https://forum.poa.network/t/faq-how-do-i-fix-indexer-timeouts/1829)
{% endhint %}

