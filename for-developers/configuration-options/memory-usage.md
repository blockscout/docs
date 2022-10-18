# Memory Usage

The work queues for building the index of all blocks, balances (coin and token), and internal transactions can grow quite large. By default, the soft-limit is 1 GiB, which can be changed via the  `INDEXER_MEMORY_LIMIT` ENV which is used in runtime config:

[https://github.com/blockscout/blockscout/blob/174bccc7038de5f699109f9ae0c718eefee18142/config/runtime.exs#L15](https://github.com/blockscout/blockscout/blob/174bccc7038de5f699109f9ae0c718eefee18142/config/runtime.exs#L15)

For example, to increase the soft limit to 3GiB:

```
INDEXER_MEMORY_LIMIT=3
```

This configuration utilizes Bitwise which in our case calculates the result of an [arithmetic left bitshift](../indexing/how-do-i-update-memory-consumption-to-fix-indexer-memory-errors.md#left-bitshift-conversion-table). The recommended minimum Memory to index Ethereum Mainnet is 30 GiB.

Memory usage is checked once per minute. If the soft-limit is reached, the shrinkable work queues will shed half their load. The shed load will be restored from the database, the same as when a restart of the server occurs, so rebuilding the work queue will be slower, but use less memory.

If all queues are at their minimum size, then no more memory can be reclaimed and an error will be logged.

