# Resource Requirements

Resource requirements may vary based on chain size and other parameters. This mainly impacts [database storage](../for-developers/information-and-settings/database-storage-requirements.md) requirements. Basic [prerequisites ](../for-developers/information-and-settings/requirements.md)and settings can be found throughout the [Information and Settings](../for-developers/information-and-settings/) section for developers.

## Recommended Hardware

EVM chains can differ in size and requirements, these are the recommendations for optimal performance.

| CPU | 16 core, 32 thread |
| --- | ------------------ |
| RAM | 128GB              |

## Hosting Requirements

Minimums are listed for an AWS Cloud instance and can be inferred to other hosting providers.

|                               |                                                                                                                                            |   |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | - |
| Application                   | <ul><li>1x EC2 t3.Medium instance running Linux</li><li>8GB of EBS General Purpose SSD (NVMe)</li></ul>                                    |   |
| Database                      | <ul><li>1x RDS Database running on db.t3.Medium using PostgreSQL</li><li> 500GB of General Purpose SSD (depending on chain size)</li></ul> |   |
| Amazon Elastic Load Balancing | Average 100 **** new connections/sec per Elastic Load Balancer                                                                             |   |

## Node Tracing Requirements

* Archive node with JSON RPC interface should strictly follow input/output interface described in [https://eth.wiki/json-rpc/API](https://eth.wiki/json-rpc/API).
* WebSocket interface (optional/highly recommended to enable) is used to subscribe to new block heads. Otherwise, Blockscout will trigger new blocks fetching by periodical polling of JSON RPC **** `eth_blockNumber` method.
* Support for the following standard Ethereum JSON RPC methods:&#x20;
  * ``[`eth_blockNumber`](https://eth.wiki/json-rpc/API#eth\_blocknumber)
  * [ `eth_cal`](https://eth.wiki/json-rpc/API#eth\_call)``
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

| Client                            | Method                                             |
| --------------------------------- | -------------------------------------------------- |
| <p>OpenEthereum<br>Nethermind</p> | `parity_pendingTransactions`                       |
| Geth                              | `txpool_content` (for parity\_pendingTransactions) |

### Enable Tracing to Fetch internal Transactions

| Client                            | Method                                                                                                              |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <p>OpenEthereum<br>Nethermind</p> | <ul><li><code>trace_replayBlockTransactions</code></li><li><code>trace_block</code> (fetch block rewards)</li></ul> |
| Geth                              | `debug_traceTransactions`  (for trace\_replayBlockTransactions)                                                     |

### JSON RPC Performance Benchmarks

Time measures for response time of crucial JSON RPC methods for indexing in Blockscout. [Ways to improve speed](../for-developers/developer-faqs/how-do-i-speed-up-my-hosted-blockscout-instance.md).

1. `eth_getBlockByNumber` without transaction receipts for a block with 15 transactions:  Desired response time is < 0.5s. For instance, in case of the Gnosis chain archive node, the response time for the block with \~20 transactions is \~0.4s.
2. `eth_getTransactionReceipt` for random transactions desired response time is < 0.5s. For the Gnosis chain archive node the response time is \~0.3 - 0.4s.
3. Batched `eth_getTransactionReceipt` for 15 transactions acceptable response time is Less than 1s. For the Gnosis chain archive node, it is \~0.6 - 0.7s
