# How do I update memory consumption to fix indexer memory errors?

During the indexing phase, many fetching processes are run asynchronously due to the load placed on trying to fetch all of the block content at once. These processes are stored in memory to be fetched at set intervals defined in each asynchronous fetcher.

`Indexer.Memory.Monitor` checks if the BEAM memory usage exceeds a set limit (defaults to 1 GiB) and if it does, it asks the process with the most memory that is registered as shrinkable to shrink.

Memory usage is checked once per minute. If the soft-limit is reached, the shrinkable work queues will shed half their load. The shed load will be restored from the database, the same as when a restart of the server occurs, so rebuilding the work queue will be slower, but use less memory.

If all queues are at their minimum size, then no more memory can be reclaimed and an error will be logged.

### Future Work

As mentioned above, future work is entered into memory to be processed later. These same processes are imported into the database to be checked on a server restart and reentered into memory to be processed.

### Updating Memory Consumption

The default Memory limit is 1 GiB and can be edited by setting `INDEXER_MEMORY_LIMIT` environment variable. See [Memory Usage](../configuration-options/memory-usage.md) for more info.

### Left Bitshift Conversion Table

To perform a left bitshift conversion yourself open the interactive shell.&#x20;

1\. `iex`&#x20;

2\. `import Bitwise`&#x20;

3\. `1 <<< 30` //1073741824

| `INDEXER_MEMORY_LIMIT` environment variable value          | Left Bitshift    | Bytes       | GiB   |
| ---------------------------------------------------------- | ---------------- | ----------- | ----- |
| `1` or `1gb` or `1g` regardless of the case of the letters | `1 <<< 30`       | 1073741824  | 1     |
| `5` or `5gb` or `5g`                                       | `5 <<< 30`       | 5368709120  | 5.3   |
| `10` or `10gb` or `10g`                                    | `10 <<< 30`      | 10737418240 | 10.7  |
| `15` or `15gb` or `15g`                                    | `15 <<< 30`      | 16106127360 | 16.1  |
| `20` or `20gb` or `20g`                                    | `20 <<< 30`      | 21474836480 | 21.4  |
| `25` or `25gb` or `25g`                                    | `25 <<< 30`      | 26843545600 | 26.8  |
| `30` or `30gb` or `30g`                                    | `30 <<< 30`      | 32212254720 | 32.2  |
| `35` or `35gb` or `35g`                                    | `35 <<< 30`      | 37580963840 | 37.6  |
| `40` or `40gb` or `40g`                                    | `40 <<< 30`      | 42949672960 | 43    |
| `45` or `45gb` or `45g`                                    | `45 <<< 30`      | 48318382080 | 48.3  |
| `50` or `50gb` or `50g`                                    | `50 <<< 30`      | 53687091200 | 53.7  |
| `100mb` or `100m` regardless of the case of the letters    | `100 <<< 20`     | 104857600   | 0.105 |
| `500mb` or `500m`                                          | `500 <<< 20`     | 524288000   | 0.52  |
| `1500mb` or `1500m`                                        | `1500 <<< 20`    | 1572864000  | 1.57  |
| `9536mb` or `9536m`                                        | `9536 <<< 20`    | 9999220736  | ~10   |
| `28610mb` or `28610m`                                      | `28610 <<< 20`   | 29999759360 | ~30   |
