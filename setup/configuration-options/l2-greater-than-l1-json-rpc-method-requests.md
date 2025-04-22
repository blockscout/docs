# L2 -> L1 JSON-RPC Method Requests

Layer 2 (L2) chains interact with their Layer 1 (L1) counterparts in different ways depending on the rollup type and information required. Blockscout's chain-specific fetchers interact with the L1 node to gather information crucial for tracking the rollup's state, batches, confirmations, and cross-chain messages.&#x20;

* [Arbitrum](l2-greater-than-l1-json-rpc-method-requests.md#arbitrum-rollups)
* [Optimism](l2-greater-than-l1-json-rpc-method-requests.md#optimism-rollups)
* [Scroll](l2-greater-than-l1-json-rpc-method-requests.md#scroll-l1-fetchers)
* [Shibarium](l2-greater-than-l1-json-rpc-method-requests.md#shibarium-l1-fetchers)
* [zkSync](l2-greater-than-l1-json-rpc-method-requests.md#zksync-rollups)
* [Polygon zkEVM](l2-greater-than-l1-json-rpc-method-requests.md#polygon-zkevm-l1-fetchers)

The following standard L1 JSON-RPC methods are utilized. Frequency and triggers for these calls are described for each chain below.

| L1 JSON-RPC Method         | Purpose                                                                                               |
| -------------------------- | ----------------------------------------------------------------------------------------------------- |
| `eth_getLogs`              | Discover L1 events (Batches, Confirmations, Executions, Messages, Keysets)                            |
| `eth_getBlockByNumber`     | Get L1 Block Timestamps, Chain Head/Safe Block info                                                   |
| `eth_getTransactionByHash` | Get L1 Tx Calldata (Batches), Get L1 Tx Originator (L1->L2 Messages)                                  |
| `eth_call`                 | Get Keyset Creation Block from `SequencerInbox` contract (Used infrequently for Arbitrum chains only) |

***

## Arbitrum Rollups

### L1 JSON-RPC method details

#### Method: `eth_getLogs`

Used periodically to poll for specific L1 events emitted by Arbitrum contracts. The polling intervals are generally configurable (`INDEXER_ARBITRUM_BATCHES_TRACKING_RECHECK_INTERVAL` and `INDEXER_ARBITRUM_TRACKING_MESSAGES_ON_L1_RECHECK_INTERVAL` for new events, faster polling for historical catch-up).

* **Events Polled:**
  * `SequencerBatchDelivered` (from `SequencerInbox` contract): To discover new L1 batches containing L2 block data. Polled periodically by the batch tracking worker (`TrackingBatchesStatuses`).
  * `SendRootUpdated` (from `Outbox` contract): To discover L2 block confirmations. Polled periodically by the batch tracking worker.
  * `OutBoxTransactionExecuted` (from `Outbox` contract): To discover L2-to-L1 message executions on L1. Polled periodically by the batch tracking worker.
  * `MessageDelivered` (from `Bridge` contract): To discover L1-to-L2 message initiations on L1. Polled periodically by the L1 message tracking worker (`TrackingMessagesOnL1`).
  * `SetValidKeyset` (from `SequencerInbox` contract): To retrieve details about AnyTrust Data Availability Committee keysets. This is triggered **on-demand** when processing an AnyTrust batch that references a keyset hash not yet seen in the database.

***

#### Method: `eth_getBlockByNumber`

* **Fetching Timestamps:**&#x20;
  * Called frequently **in response to processing events** found via `eth_getLogs`. When a relevant event (like batch delivery, confirmation, or message execution) is found in a log, this method is called for the corresponding L1 block number to get its timestamp. This happens in batches triggered by the periodic log polling.
* **Fetching Chain Head/Safe Block:**
  * Called periodically (driven by `recheck_interval`) with tags `"latest"` and `"safe"` to determine the current L1 chain head and the safe block for reorg protection and determining finality. Used by batch, confirmation, and execution workers.
  * Called once during initialization to determine the starting point if not explicitly configured.

***

Method: `eth_getTransactionByHash`

Called **in response to processing events** found via `eth_getLogs`:

* **Fetching Batch Calldata:**&#x20;
  * When a `SequencerBatchDelivered` event is processed, this method is called for the L1 transaction hash associated with the event to retrieve the transaction's `input` data (calldata). This calldata contains essential batch information, especially for non-blob batches.
* **Fetching L1->L2 Message Originator:**&#x20;
  * When a `MessageDelivered` event (for an L1->L2 message) is processed, this method is called for the L1 transaction hash to retrieve the originator (`from`) address.

***

Method: `eth_call`

Used less frequently than the other calls.

* **Fetching Keyset Creation Block:**&#x20;
  * When processing an AnyTrust batch referencing a previously unknown keyset hash, an `eth_call` is made to the `SequencerInbox` contract's `getKeysetCreationBlock` function to determine the L1 block where the keyset became active. This is triggered **on-demand** during batch processing.

***

## Optimism Rollups

### Optimism L1 fetchers

Method calls are described for each of the Optimism-based fetchers including Deposit, DisputeGame, OutputRoot, TransactionBatch and WithdrawalEvent.

#### Indexer.Fetcher.Optimism.Deposit

* `eth_getLogs` (driven by `INDEXER_OPTIMISM_L1_ETH_GET_LOGS_RANGE_SIZE` for catchup mode) - one request per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` response to get block timestamp. Batch request is used, so one batch request per one `eth_getLogs` call

#### Indexer.Fetcher.Optimism.DisputeGame

* call to `OptimismPortal`'s `respectedGameType()` public getter (every 60 seconds)
* call to `DisputeGameFactory`'s `gameCount` public getter (every 60 seconds)
* call to `DisputeGameFactory`'s `gameAtIndex` public getter (max 50 items per batch request) and the corresponding batch calls to `extraData`, `resolvedAt`, `status` public getters for each dispute game
* call to `DisputeGameFactory`'s `resolvedAt` public getter (max 50 items per batch request) for max 1000 last unresolved games
* call to `DisputeGameFactory`'s `status` public getter (max 50 items per batch request) for max 1000 last resolved games

#### Indexer.Fetcher.Optimism.OutputRoot

* `eth_getLogs` (driven by `INDEXER_OPTIMISM_L1_ETH_GET_LOGS_RANGE_SIZE` for catchup mode) - one request per block in realtime mode

#### Indexer.Fetcher.Optimism.TransactionBatch

* `eth_getBlockByNumber` (batch RPC calls containing up to `INDEXER_OPTIMISM_L1_BATCH_BLOCKS_CHUNK_SIZE` requests per batch in catchup mode starting from the start block defined in `SystemConfig` contract) - one request per block in realtime mode

#### Indexer.Fetcher.Optimism.WithdrawalEvent

* `eth_getLogs` (driven by `INDEXER_OPTIMISM_L1_ETH_GET_LOGS_RANGE_SIZE` for catchup mode) - one request per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` response to get block timestamp. Batch request is used, so one batch request per one `eth_getLogs` call

***

## zkSync Rollups

### **L1 interaction process**

Blockscout's zkSync-specific fetchers verify zkSync batch status and transitions (Committed, Proven, Executed) recorded on the L1.

### **L1 interaction summary**

L1 calls are infrequent and only triggered to confirm L1 state transitions suggested by the L2 node.

* L1 interaction is driven by the `BatchesStatusTracker`. This tracker performs periodic checks based on the `INDEXER_ZKSYNC_BATCHES_STATUS_RECHECK_INTERVAL` ENV variable setting.
* Each check phase (`:check_committed`, `:check_proven`, `:check_executed`) _first_ queries the L2 node via RPC (`zks_getL1BatchDetails`).
* If (_and only if)_ the L2 query indicates a new L1 transaction hash associated with a batch's status change (commit, prove, or execute), the corresponding L1 RPC method (`eth_getTransactionReceipt` or `eth_getTransactionByHash`) is called for that _specific_ transaction hash.&#x20;

### L1 JSON-RPC method details

#### Method: `eth_getTransactionReceipt`

**Purpose**: Retrieves the receipt of an L1 transaction suspected of changing a batch's status (commit or execute). The fetcher specifically looks for event logs within the receipt (`BlockCommit` or `BlockExecution` events) to confirm which batches were affected by that single L1 transaction.

**Frequency:**

* Called conditionally by the `BatchesStatusTracker` process.&#x20;
* This tracker runs in a loop with a configurable `INDEXER_ZKSYNC_BATCHES_STATUS_RECHECK_INTERVAL`.&#x20;
* Within this loop, it first checks the L2 RPC (`zks_getL1BatchDetails`) for the oldest uncommitted/unexecuted batch.&#x20;
* If the L2 RPC response indicates a new commit or execute L1 transaction hash associated with that batch, _then_ `eth_getTransactionReceipt` is called on the L1 node for that specific transaction hash.&#x20;
* It does _not_ poll L1 constantly; the call is triggered only when a potential status change is detected via L2 RPC data during the periodic check.

***

#### Method: `eth_getTransactionByHash`

**Purpose:** Retrieves the details of an L1 transaction suspected of proving one or more zkSync batches. The fetcher needs the transaction's `input` (calldata) to decode the list of batches proven in that single L1 transaction.

**Frequency**:&#x20;

* Called conditionally by the `BatchesStatusTracker` process, similar to `eth_getTransactionReceipt`. It also runs within the tracker's periodic `INDEXER_ZKSYNC_BATCHES_STATUS_RECHECK_INTERVAL`.&#x20;
* The tracker checks the L2 RPC (`zks_getL1BatchDetails`) for the oldest unproven batch. If the L2 RPC response indicates a new prove L1 transaction hash, _then_ `eth_getTransactionByHash` is called on the L1 node for that specific transaction hash to retrieve its calldata.&#x20;
* Like the receipt fetch, this is triggered by potential changes detected via L2 RPC during the periodic check, not through constant L1 polling.

***

## Polygon zkEVM L1 fetchers

Method calls are described for each of the zkEVM-based fetchers including BridgeL1, BridgeL1Tokens, and TransactionBatch.

#### Indexer.Fetcher.PolygonZkevm.BridgeL1

* `eth_getLogs` (max 1000 blocks in a range per request for catchup mode) - one request per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` response to get block timestamp (batch request is used with max 50 items per request)
* `eth_getBlockByNumber` to get latest block (every block time in seconds, divided by 2)
* one batch request (with calls to `symbol()` and `decimals()` getters of token contracts) per one `eth_getLogs` call

#### Indexer.Fetcher.PolygonZkevm.BridgeL1Tokens

* one batch request (with calls to `symbol()` and `decimals()` getters of token contracts) per one set of logs taken in realtime mode from the L2 block

#### Indexer.Fetcher.PolygonZkevm.TransactionBatch

* a batch call of `zkevm_batchNumber`, `zkevm_virtualBatchNumber`, `zkevm_verifiedBatchNumber` requests per `INDEXER_POLYGON_ZKEVM_BATCHES_RECHECK_INTERVAL` seconds
* a batch call of `zkevm_getBatchByNumber` requests per `INDEXER_POLYGON_ZKEVM_BATCHES_CHUNK_SIZE` zkEVM batches

***

## Scroll L1 fetchers

Method calls are described for each of the Scroll-based fetchers including Batch and BridgeL1.

#### Indexer.Fetcher.Scroll.Batch

* `eth_getLogs` (driven by `INDEXER_SCROLL_L1_ETH_GET_LOGS_RANGE_SIZE` for catchup mode) - one request per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` response to get block timestamp (batch request is used with max 50 items per request)
* `eth_getBlockByNumber` to get latest block (every block time in seconds, divided by 2)

#### Indexer.Fetcher.Scroll.BridgeL1

* `eth_getLogs` (driven by `INDEXER_SCROLL_L1_ETH_GET_LOGS_RANGE_SIZE` for catchup mode) - one request per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` response (taking into account `SentMessage` events only) to get block timestamp (batch request is used with max 50 items per request)
* `eth_getBlockByNumber` to get latest block (every block time in seconds, divided by 2)

## Shibarium L1 fetchers

Method calls are described for each of the Scroll-based fetchers including L1 and RollupL1ReorgMonitor.

#### Indexer.Fetcher.Shibarium.L1

* three `eth_getLogs` requests per chunk for catchup mode (max 1000 blocks in a chunk) - three requests per block in realtime mode
* `eth_getBlockByNumber` for each block within `eth_getLogs` responses (taking into account deposit events only) to get block timestamp (batch request is used with max 50 items per request)
* `eth_getBlockByNumber` to get latest block (every block time in seconds, divided by 2)

#### Indexer.Fetcher.RollupL1ReorgMonitor

* `eth_getBlockByNumber` to get latest block (every block time in seconds, divided by 2)
