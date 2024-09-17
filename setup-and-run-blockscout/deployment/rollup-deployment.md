---
icon: circle
---

# Rollup Deployment

Rollup deployments require different backend setups depending on the rollup type. Below we provide information and examples for [Arbitrum](rollup-deployment.md#arbitrum) and [Optimism](rollup-deployment.md#optimism).

## Arbitrum

Variables are linked below and supported with `CHAIN_TYPE=arbitrum.`Default values are set for many variables and typically do not need adjustment for common setups.

{% hint style="info" %}
[Arbitrum environment variables](../env-variables/backend-envs-chain-specific.md#arbitrum-rollup-management)
{% endhint %}

Example Configuration using Ethereum as the settlement layer:

```
INDEXER_ARBITRUM_ROLLUP_CHUNK_SIZE=20
INDEXER_ARBITRUM_L1_RPC=...
INDEXER_ARBITRUM_L1_RPC_HISTORICAL_BLOCKS_RANGE=1000
INDEXER_ARBITRUM_L1_RPC_CHUNK_SIZE=20
INDEXER_ARBITRUM_L1_ROLLUP_CONTRACT="..."
INDEXER_ARBITRUM_L1_ROLLUP_INIT_BLOCK=...
INDEXER_ARBITRUM_BRIDGE_MESSAGES_TRACKING_ENABLED='true'
INDEXER_ARBITRUM_MISSED_MESSAGES_RECHECK_INTERVAL=1h
INDEXER_ARBITRUM_TRACKING_MESSAGES_ON_L1_RECHECK_INTERVAL=30s
INDEXER_ARBITRUM_BATCHES_TRACKING_ENABLED='true'
INDEXER_ARBITRUM_BATCHES_TRACKING_RECHECK_INTERVAL=30s
INDEXER_ARBITRUM_NEW_BATCHES_LIMIT=1
INDEXER_ARBITRUM_CONFIRMATIONS_TRACKING_FINALIZED='true'
INDEXER_ARBITRUM_BATCHES_TRACKING_L1_FINALIZATION_CHECK_ENABLED='true'
```

### Arbitrum ENV Notes

#### `INDEXER_ARBITRUM_L1_RPC`&#x20;

Set to the settlement layer RPC node. In the case above it would be set to your choice of Ethereum RPC nodes such as [https://rpc.ankr.com/eth](https://rpc.ankr.com/eth) or another one of your choice [from this list](https://www.alchemy.com/chain-connect/chain/ethereum). If the rollup settles to a testnet, such as Arbitrum Sepolia, then it would be set to [https://arbitrum-sepolia.blockscout.com/](https://arbitrum-sepolia.blockscout.com/) ( [info retrieved here](https://docs.arbitrum.io/build-decentralized-apps/reference/node-providers))

#### `INDEXER_ARBITRUM_L1_ROLLUP_INIT_BLOCK`&#x20;

Retrieved using the block explorer for the settlement layer chain. Search the rollup contract address and find the transaction and block where the contract was deployed. Use that block number as the value for this env.&#x20;

<div>

<figure><img src="../../.gitbook/assets/arb-get-tx.png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../../.gitbook/assets/2-arb-get-block.png" alt=""><figcaption></figcaption></figure>

</div>

#### `INDEXER_ARBITRUM_L1_RPC_HISTORICAL_BLOCKS_RANGE`

The RPC historical blocks range depends on the following factors:

* Batch production rate for the rollup. This can be identified by looking at how fast the `SequencerInbox` contract is called using the method `addSequencerL2BatchFromOrigin`. The transactions to the contract can be found on the contract page of of the block explorer.

<figure><img src="../../.gitbook/assets/example-arb-contract-calls.png" alt=""><figcaption></figcaption></figure>

* Block production rate for the settlement layer.
* The limits of the L1 RPC node. Specifically, the maximum block range for the `eth_getLogs` operation is needed. This can be identified empirically or by contacting the node admin.

**Recommendations based on these factors:**

1. If the block production rate on the settlement layer is low (like one block per 12 secs for Ethereum Mainnet), choose a block range that will cover 1 or 2 batches.
2. If the block production rate is high (if another rollup is used as a settlement layer), use the minimum amount of settlement layer blocks produced during the time required to produce 2 rollup batches and the block range limit to get logs from the L1 RPC node. For example, if 5000 settlement layer blocks are produced during the time when two subsequent batches are sent to the settlement layer and the RPC node block range limit is 3000, the smaller 3000 value must be used.

#### `INDEXER_ARBITRUM_BATCHES_TRACKING_RECHECK_INTERVAL` `INDEXER_ARBITRUM_TRACKING_MESSAGES_ON_L1_RECHECK_INTERVAL`

Tracking intervals depend on the block production rate on the settlement layer. Do not set them lower than the average block time. Higher values will cause latency in batches/messages identification. The default for L1 batches and messages re-check is 20 seconds.

#### `INDEXER_ARBITRUM_ROLLUP_CHUNK_SIZE` `INDEXER_ARBITRUM_L1_RPC_CHUNK_SIZE`

Chunk sizes depend on the RPC nodes' rate limits. Larger chunks may cause rate limit errors and smaller chunks introduce additional network-related delays.`INDEXER_ARBITRUM_ROLLUP_CHUNK_SIZE` configures the chunk size for the rollup RPC node and`INDEXER_ARBITRUM_L1_RPC_CHUNK_SIZE` configures the chunk size for the settlement layer (L1) RPC node.

#### `INDEXER_ARBITRUM_BATCHES_TRACKING_MESSAGES_TO_BLOCKS_SHIFT`

{% hint style="warning" %}
The only chain identified so far where this variable is required is the **Arbitrum One** chain.
{% endhint %}

This variable must be configured for chains where the message counters in the call `addSequencerL2BatchFromOrigin` of the `SequencerInbox` contract do not correspond directly to the rollup block numbers.&#x20;

## Optimism

{% hint style="danger" %}
More info coming soon
{% endhint %}

Variables are linked below and supported with `CHAIN_TYPE=optimism`

{% hint style="info" %}
[Optimism environment variables](../env-variables/backend-envs-chain-specific.md#optimism-rollup-management)
{% endhint %}

