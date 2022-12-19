# Indexing

BlockScout can take some time to fully index a chain. Larger chains require more time. Indexing starts from the head of the chain \(the current block\) and goes backwards towards the genesis block. The genesis block is the final block indexed during this process.

### Messages during indexing 

1. **n% Blocks Indexed - We're indexing this chain right now. Some of the counts may be inaccurate.** This means blocks are still being collected and processed by BlockScout. The message should disappear once the genesis block is indexed.
2. **Indexing Internal Transactions - We're indexing this chain right now. Some of the counts may be inaccurate.** This means BlockScout has collected all blocks but is still indexing internal transactions using the archive node tracing api. This message will disappear when `INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER=true` is provided.

### Monitoring indexing processes

1. Block count should be close to the number of the blocks in the chain. Query using  `SELECT COUNT(1) FROM blocks;` ~= num of blocks in the chain.
2. Internal transaction fetching can be monitored with this query: `SELECT COUNT(1) FROM pending_block_operations;`  It should move towards zero during internal transaction processing.

