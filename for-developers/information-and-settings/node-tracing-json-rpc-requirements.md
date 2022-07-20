# Node Tracing / JSON RPC Requirements

### Standard JSON RPC Requirements

* Archive node with JSON RPC interface should strictly follow input/output interface described in [https://eth.wiki/json-rpc/API](https://eth.wiki/json-rpc/API).
* WebSocket interface (optional/highly recommended to enable) is used to subscribe to new block heads. Otherwise, Blockscout will trigger new blocks fetching by periodical polling of JSON RPC **** `eth_blockNumber` method.
* Support for the following standard Ethereum JSON RPC methods:&#x20;
  * ``[`eth_blockNumber`](https://eth.wiki/json-rpc/API#eth\_blocknumber)
  * [ `eth_call`](https://eth.wiki/json-rpc/API#eth\_call)
  * ``[`eth_getBalance`](https://eth.wiki/json-rpc/API#eth\_getbalance)``
  * ``[`eth_getCode`](https://eth.wiki/json-rpc/API#eth\_getcode)``
  * ``[`eth_getBlockByHash`](https://eth.wiki/json-rpc/API#eth\_getblockbyhash)``
  * ``[`eth_getBlockByNumber`](https://eth.wiki/json-rpc/API#eth\_getblockbynumber)``
  * ``[`eth_getTransactionByHash`](https://eth.wiki/json-rpc/API#eth\_gettransactionbyhash)``
  * ``[`eth_getTransactionByBlockHashAndIndex`](https://eth.wiki/json-rpc/API#eth\_gettransactionbyblockhashandindex)``
  * ``[`eth_getTransactionByBlockNumberAndIndex`](https://eth.wiki/json-rpc/API#eth\_gettransactionbyblocknumberandindex)``
  * ``[`eth_getTransactionReceipt`](https://eth.wiki/json-rpc/API#eth\_gettransactionreceipt)``
  * ``[`eth_getUncleByBlockHashAndIndex`](https://eth.wiki/json-rpc/API#eth\_getunclebyblockhashandindex)``
  * ``[`eth_getLogs`](https://eth.wiki/json-rpc/API#eth\_getlogs)``

### **Fetching Pending Transactions**

| Client                            | Method                                                                         |
| --------------------------------- | ------------------------------------------------------------------------------ |
| <p>OpenEthereum<br>Nethermind</p> | <ul><li><code>parity_pendingTransactions</code></li></ul>                      |
| Geth                              | <ul><li><code>txpool_content</code> (for parity_pendingTransactions)</li></ul> |

### Enable Tracing to Fetch internal Transactions

| Client                            | Method                                                                                                              |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <p>OpenEthereum<br>Nethermind</p> | <ul><li><code>trace_replayBlockTransactions</code></li><li><code>trace_block</code> (fetch block rewards)</li></ul> |
| Geth                              | <ul><li><code>debug_traceTransactions</code>  (for trace_replayBlockTransactions)</li></ul>                         |

### JSON RPC Performance Benchmarks

Time measures for response time of crucial JSON RPC methods for indexing in Blockscout. [Ways to improve speed](../developer-faqs/how-do-i-speed-up-my-hosted-blockscout-instance.md).

1. `eth_getBlockByNumber` without transaction receipts for a block with 15 transactions:  Desired response time is < 0.5s. For instance, in case of the Gnosis chain archive node, the response time for the block with \~20 transactions is \~0.4s.
2. `eth_getTransactionReceipt` for random transactions desired response time is < 0.5s. For the Gnosis chain archive node the response time is \~0.3 - 0.4s.
3. Batched `eth_getTransactionReceipt` for 15 transactions acceptable response time is Less than 1s. For the Gnosis chain archive node, it is \~0.6 - 0.7s

## EVM Requirements & Clients

* All EVM chains must [define these variables](deployment-differences-between-chains.md) during configuration.&#x20;
* BlockScout currently supports Parity, OpenEthereum, Geth, Nethermind, Hyperledger Besu, and Ganache clients. Define the node variant using the `ETHEREUM_JSONRPC_VARIANT` environment variable. [More information](client-settings-parity-geth-ganache.md)
