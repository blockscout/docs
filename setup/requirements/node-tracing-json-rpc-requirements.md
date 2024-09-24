# Node Tracing / JSON RPC Requirements

### Standard JSON RPC Requirements

* Archive node with JSON RPC interface should strictly follow input/output interface described in [https://ethereum.github.io/execution-apis/api-documentation/](https://ethereum.github.io/execution-apis/api-documentation/)
* WebSocket interface (optional/highly recommended to enable) is used to subscribe to new block heads. Otherwise, Blockscout will trigger new blocks fetching by periodical polling the JSON RPC `eth_blockNumber` method.
* Support for the following standard Ethereum JSON RPC methods (documented at [https://ethereum.github.io/execution-apis/api-documentation/](https://ethereum.github.io/execution-apis/api-documentation/))
  * `eth_blockNumber`
  * `eth_call`
  * `eth_getBalance`
  * `eth_getCode`
  * `eth_getBlockByHash`
  * `eth_getBlockByNumber`
  * `eth_getTransactionByHash`
  * `eth_getTransactionByBlockHashAndIndex`
  * `eth_getTransactionByBlockNumberAndIndex`
  * `eth_getTransactionReceipt`
  * `eth_getUncleByBlockHashAndIndex`
  * `eth_getLogs`

### **Fetching Pending Transactions**

| Client                                      | Method                       |
| ------------------------------------------- | ---------------------------- |
| <p>Erigon<br>Nethermind<br>OpenEthereum</p> | `parity_pendingTransactions` |
| Geth                                        | `txpool_content`             |

### Enable Tracing to Fetch Internal Transactions

| Client                                      | Method                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Erigon<br>Nethermind<br>OpenEthereum</p> | <ul><li><code>trace_replayBlockTransactions</code> (fetching of internal transactions)</li><li><code>trace_block</code> (fetching of block rewards)</li></ul>                                                                                                                                                                                                                                                                     |
| Geth                                        | <ul><li><code>debug_traceBlockByNumber</code></li><li>or <code>debug_traceTransaction</code></li></ul><p><code>callTracer</code> is used by default, starting from the Blockscout 5.1.0 release. To switch to a custom JS tracer, the Blockscout maintainer should set the <code>export INDEXER_INTERNAL_TRANSACTIONS_TRACER_TYPE=js</code> environment variable. Prior to the 5.1.0 release, js tracer was a default option.</p> |

### JSON RPC Performance Benchmarks

Time measures for response time of crucial JSON RPC methods for indexing in Blockscout. [Ways to improve speed](../../faqs/faqs.md#how-do-i-speed-up-my-self-hosted-instance).

1. `eth_getBlockByNumber` without transaction receipts for a block with 15 transactions: Desired response time is < 0.5s. For instance, in case of the Gnosis chain archive node, the response time for the block with \~20 transactions is \~0.4s.
2. `eth_getTransactionReceipt` for random transactions desired response time is < 0.5s. For the Gnosis chain archive node the response time is \~0.3 - 0.4s.
3. Batched `eth_getTransactionReceipt` for 15 transactions acceptable response time is Less than 1s. For the Gnosis chain archive node, it is \~0.6 - 0.7s

### Rate Limit

The desired rate limit for RPC endpoint is 200 req/sec for the indexing phase and 100 req/sec for the indexed chain.

## EVM Requirements & Clients

* All EVM chains must [define these variables](../env-variables/#all-chains-must-define-the-following-minimum-set-of-env-variables) during configuration.
* BlockScout currently supports Erigon, Geth, Nethermind, Hyperledger Besu, and Ganache clients. Define the node variant using the `ETHEREUM_JSONRPC_VARIANT` environment variable. [More information](client-settings.md)
