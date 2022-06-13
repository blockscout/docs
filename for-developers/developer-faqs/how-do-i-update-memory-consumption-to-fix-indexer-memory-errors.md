# How do I update memory consumption to fix indexer memory errors?

During the indexing phase, many fetching processes are run asynchronously due to the load placed on trying to fetch all of the block content at once. These processes are stored in memory to be fetched at set intervals defined in each asynchronous fetcher.

`Indexer.Memory.Monitor` checks if the BEAM memory usage exceeds a set limit (defaults to 1 GiB) and if it does, it asks the process with the most memory that is registered as shrinkable to shrink.

Memory usage is checked once per minute. If the soft-limit is reached, the shrinkable work queues will shed half their load. The shed load will be restored from the database, the same as when a restart of the server occurs, so rebuilding the work queue will be slower, but use less memory.

If all queues are at their minimum size, then no more memory can be reclaimed and an error will be logged.

### Future Work

As mentioned above, future work is entered into memory to be processed later. These same processes are imported into the database to be checked on a server restart and reentered into memory to be processed.

### Updating Memory Consumption

The default Memory limit is 1 GiB and can be edited by setting `INDEXER_MEMORY_LIMIT` environment variable, which is used in runtime config:

[https://github.com/blockscout/blockscout/blob/174bccc7038de5f699109f9ae0c718eefee18142/config/runtime.exs#L15](https://github.com/blockscout/blockscout/blob/174bccc7038de5f699109f9ae0c718eefee18142/config/runtime.exs#L15)

This configuration utilizes Bitwise which in our case calculates the result of an arithmetic left bitshift. The recommended minimum Memory to index Ethereum Mainnet is 30 GiB.

### Left Bitshift Conversion Table

To perform a left bitshift conversion yourself open the interactive shell.&#x20;

1\. `iex`&#x20;

2\. `import Bitwise`&#x20;

3\. `1 <<< 30` //1073741824

| Left Bitshift | Bytes       | GiB  |
| ------------- | ----------- | ---- |
| `1 <<< 30`    | 1073741824  | 1    |
| `5 <<< 30`    | 5368709120  | 5.3  |
| `10 <<< 30`   | 10737418240 | 10.7 |
| `15 <<< 30`   | 16106127360 | 16.1 |
| `20 <<< 30`   | 21474836480 | 21.4 |
| `25 <<< 30`   | 26843545600 | 26.8 |
| `30 <<< 30`   | 32212254720 | 32.2 |
| `35 <<< 30`   | 37580963840 | 37.6 |
| `40 <<< 30`   | 42949672960 | 43   |
| `45 <<< 30`   | 48318382080 | 48.3 |
| `50 <<< 30`   | 53687091200 | 53.7 |

{% hint style="success" %}
Content moved from [https://forum.poa.network/t/faq-indexer-memory-errors/1857](https://forum.poa.network/t/faq-indexer-memory-errors/1857)
{% endhint %}
