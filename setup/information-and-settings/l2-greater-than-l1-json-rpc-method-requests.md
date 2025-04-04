# L2 -> L1 JSON-RPC Method Requests

Layer 2 (L2) chains interact with their Layer 1 (L1) counterparts in different ways depending on the rollup type and information required.

* [zkSync Rollups](l2-greater-than-l1-json-rpc-method-requests.md#zksync-rollups)
* [Arbitrum Rollups](l2-greater-than-l1-json-rpc-method-requests.md#arbitrum-rollups)
* Optimism Rollups (in process)

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

## Arbitrum Rollups

### **L1 interaction process**

Blockscout's Arbitrum-specific fetchers interact with the Layer 1 (L1) node to gather information crucial for tracking the rollup's state, batches, confirmations, and cross-chain messages.&#x20;

### **L1 interaction summary**

| L1 JSON-RPC Method         | Trigger / Frequency                                                                  | Purpose                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| `eth_getLogs`              | Periodic Polling (configurable interval) & On-Demand (AnyTrust Keyset)               | Discover L1 events (Batches, Confirmations, Executions, Messages, Keysets) |
| `eth_getBlockByNumber`     | Event-Triggered (Batched), Periodic Polling (`latest`/`safe`), Initialization (Once) | Get L1 Block Timestamps, Chain Head/Safe Block info                        |
| `eth_getTransactionByHash` | Event-Triggered (Batched)                                                            | Get L1 Tx Calldata (Batches), Get L1 Tx Originator (L1->L2 Messages)       |
| `eth_call`                 | On-Demand (AnyTrust Keyset processing)                                               | Get Keyset Creation Block from `SequencerInbox` contract                   |

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

_in process_
