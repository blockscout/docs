---
description: 'Adjust # of files and max size to impact disc space'
---

# Logger Configs

Each [umbrella app](../information-and-settings/untitled.md) (indexer, explorer, block\_scout\_web, ethereum\_json\_rpc) contains a log rotation config in the `prod.exs` file.

{% hint style="info" %}
_Example:_ [_https://github.com/blockscout/blockscout/blob/master/apps/explorer/config/prod.exs#L36-L51_](https://github.com/blockscout/blockscout/blob/master/apps/explorer/config/prod.exs#L36-L51.)__
{% endhint %}

```
config :logger, :explorer,
  level: :info,
  path: Path.absname("logs/prod/explorer.log"),
  rotate: %{max_bytes: 52_428_800, keep: 19}

config :logger, :reading_token_functions,
  level: :debug,
  path: Path.absname("logs/prod/explorer/tokens/reading_functions.log"),
  metadata_filter: [fetcher: :token_functions],
  rotate: %{max_bytes: 52_428_800, keep: 19}
```

&#x20;`config :logger` defines several variables including:&#x20;

* **level**: (`info`, `debug`, `error`) log level of detail
* **rotate**:  {max bytes:  `52,428,800`  max size in bytes for each file, keep:  `19` max number of files to store}

If you are having issues with disc space, change the level, default number of files, and max bytes to consume less space with logs.

Additional log rotation configs for `ecto.log` (DB interactions wrapper) and `error.log` are located in the common config file [https://github.com/blockscout/blockscout/blob/master/config/config.exs#L47-L61](https://github.com/blockscout/blockscout/blob/master/config/config.exs##L47-L61)



