# ENV Variables

{% hint style="info" %}
This table is horizontally scrollable, version information is located in the last column.
{% endhint %}

{% hint style="info" %}
Additional information related to certain variables is available on the [ansible deployment](../ansible-deployment/) page.
{% endhint %}

* To set variables using the CLI, use the export command. For example:

  ```bash
  $ export ETHEREUM_JSONRPC_VARIANT=parity
  $ export COIN=POA
  $ export NETWORK=POA
  ```

| Variable | Required | Description | Default | Version | Need recompile | Deprecated in Version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `NETWORK` | ✅ | Environment variable for the main EVM network such as Ethereum Network or POA Network | POA Network | all |  |  |
| `SUBNETWORK` | ✅ | Environment variable for the subnetwork such as Core or Sokol Network | Sokol Testnet | all |  |  |
| `NETWORK_ICON` | ✅ | Environment variable for the main network icon or testnet icon. Two options are  `_test_network_icon.html` and `_network_icon.html` | `_test_network_icon.html` | all |  |  |
| `LOGO` | ✅ | Environment variable for the header logo image location. The logo files names for different chains can be found [here](https://github.com/poanetwork/blockscout/tree/master/apps/block_scout_web/assets/static/images) | /images/blockscout\_logo.svg | all |  |  |
| `LOGO_FOOTER` | ✅ | Environment variable for the footer logo image location. The logo files names for different chains can be found [here](https://github.com/poanetwork/blockscout/tree/master/apps/block_scout_web/assets/static/images) | /images/blockscout\_logo.svg |  |  |  |
| `ETHEREUM_JSONRPC_VARIANT` | ✅ | Tells the application which RPC Client the node is using \(i.e. Geth, Parity, or Ganache\) \([See Client Settings for more info](client-settings-parity-geth-ganache.md)\) | parity | all |  |  |
| `ETHEREUM_JSONRPC_HTTP_URL` | ✅ | The RPC endpoint used to fetch blocks, transactions, receipts, tokens. | localhost:8545 | all |  |  |
| `ETHEREUM_JSONRPC_TRACE_URL` |  | The RPC endpoint specifically for the Geth/Parity client used by trace\_block and trace\_replayTransaction. This can be used to designate a tracing node. | localhost:8545 | all |  |  |
| `ETHEREUM_JSONRPC_WS_URL` | ✅ | The WebSockets RPC endpoint used to subscribe to the `newHeads` subscription alerting the indexer to fetch new blocks. | ws://localhost:8546 | all |  |  |
| `ETHEREUM_JSONRPC_TRANSPORT` |  | Specifies the transport for blockscout to connect to the Ethereum Node. Available transports are `http` and `ipc`. If `ipc` is selected, also set `IPC_PATH` variable | http | master |  |  |
| `ETHEREUM_JSONRPC_JSON_RPC_TRANSPORT` |  | Specifies the transport for blockscout to connect to the Ethereum Node. Available transports are `http` and `ipc`. If `ipc` is selected, also set `IPC_PATH` variable | `http` | v2.1.1+ |  | master |
| `IPC_PATH` |  | Path to the ipc file of the running node |  | v2.1.1+ |  |  |
| `NETWORK_PATH` |  | Used to set a network path other than what is displayed in the root directory. An example would be to add /eth/mainnet/ to the root directory. | \(empty\) | all |  |  |
| `SECRET_KEY_BASE` | ✅ | Use mix phx.gen.secret to generate a new Secret Key Base string to protect production assets. | \(empty\) | all |  |  |
| `CHECK_ORIGIN` |  | Used to check the origin of requests when the origin header is present. It defaults to false. In case of true, it will check against the host value. | false | all |  |  |
| `PORT` | ✅ | Default port the application runs on is 4000 | 4000 | all |  |  |
| `COIN` | ✅ | The coin here is checked via the CoinGecko API to obtain USD prices on graphs and other areas of the UI | POA | all |  |  |
| `METADATA_CONTRACT` |  | This environment variable is specifically used by POA Network to obtain Validators information to display in the UI. | \(empty\) | all |  |  |
| `VALIDATORS_CONTRACT` |  | This environment variable is specifically used by POA Network to obtain the list of current validators. | \(empty\) | all |  |  |
| `SUPPLY_MODULE` |  | This environment variable is used by the xDai Chain in order to tell the application how to calculate the total supply of the chain. | false | all |  |  |
| `SOURCE_MODULE` |  | This environment variable is used to calculate the exchange rate and is specifically used by the xDai Chain. | false | all |  |  |
| `DATABASE_URL` |  | Production environment variable to define the Database endpoint. | \(empty\) | all |  |  |
| `POOL_SIZE` |  | Production environment variable to define the number of database connections allowed. | 20 | all |  |  |
| `ECTO_USE_SSL` |  | Production environment variable to use SSL on Ecto queries. | true | all |  |  |
| `DATADOG_HOST` |  | Host configuration setting for [Datadog integration](https://docs.datadoghq.com/integrations/) | \(empty\) | all |  |  |
| `DATADOG_PORT` |  | Port configuration setting for [Datadog integration](https://docs.datadoghq.com/integrations/). | \(empty} | all |  |  |
| `SPANDEX_BATCH_SIZE` |  | [Spandex](https://github.com/spandex-project/spandex) and Datadog configuration setting. | \(empty\) | all |  |  |
| `SPANDEX_SYNC_THRESHOLD` |  | [Spandex](https://github.com/spandex-project/spandex) and Datadog configuration setting. | \(empty\) | all |  |  |
| `HEART_BEAT_TIMEOUT` |  | Production environment variable to restart the application in the event of a crash. | 30 | all |  |  |
| `HEART_COMMAND` |  | Production environment variable to restart the application in the event of a crash. | systemctl restart explorer.service | all |  |  |
| `BLOCKSCOUT_VERSION` |  | Added to the footer to signify the current BlockScout version. | \(empty\) | v1.3.4+ |  |  |
| `RELEASE_LINK` |  | The link to Blockscout release notes in the footer. | https: //github.com/poanetwork/  blockscout/releases/   tag/${BLOCKSCOUT\_VERSION} | v1.3.5+ |  |  |
| `ELIXIR_VERSION` |  | Elixir version to install on the node before Blockscout deploy. | \(empty\) | all |  |  |
| `BLOCK_TRANSFORMER` |  | Transformer for blocks: base or clique. | base | v1.3.4+ |  |  |
| `GRAPHIQL_TRANSACTION` |  | Default transaction in query to GraphiQL. | \(empty\) | v1.2.0+ | ✅ |  |
| `FIRST_BLOCK` |  | The block number, where indexing begins from. | 0 | v1.3.8+ |  |  |
| `LAST_BLOCK` |  | The block number, where indexing stops. | \(empty\) | v2.0.3+ |  |  |
| `TXS_COUNT_CACHE_PERIOD` |  | Interval in seconds to restart the task, which calculates the total txs count. | 60  _60_  2 | v1.3.9+ |  |  |
| `ADDRESS_WITH_BALANCES`   `_UPDATE_INTERVAL` |  | Interval in seconds to restart the task, which calculates addresses with balances. | 30 \* 60 | v1.3.9+ |  |  |
| `LINK_TO_OTHER_EXPLORERS` |  | true/false. If true, links to other explorers are added in the footer | \(empty\) | v1.3.0+ |  |  |
| `COINMARKETCAP_PAGES` |  | the number of pages on coinmarketcap to list in order to find token's price | 10 | v1.3.10+ |  | v2.0.4 |
| `SUPPORTED_CHAINS` |  | Array of supported chains that displays in the footer and in the chains dropdown. This var was introduced in this PR [\#1900](https://github.com/poanetwork/blockscout/pull/1900) and looks like an array of JSON objects. | \(empty\) | v2.0.0+ |  |  |
| `BLOCK_COUNT_CACHE_PERIOD` |  | time to live of blocks with consensus count cache in seconds. This var was introduced in [\#1876](https://github.com/poanetwork/blockscout/pull/1876) | 600 | v2.0.0+ |  |  |
| `ADDRESS_SUM_CACHE_PERIOD` |  | time to live of addresses sum \(except burn address\) cache in seconds. This var was introduced in [\#2862](https://github.com/poanetwork/blockscout/pull/2862) | 3600 | v2.1.1+ |  |  |
| `ADDRESS_COUNT_CACHE_PERIOD` |  | time to live of cache in seconds. This var was introduced in [\#2822](https://github.com/poanetwork/blockscout/pull/2822) | 60  _60_  2 | v2.1.1+ |  |  |
| `ALLOWED_EVM_VERSIONS` |  | the comma-separated list of allowed EVM versions for contracts verification. This var was introduced in [\#1964](https://github.com/poanetwork/blockscout/pull/1964) | "homestead, tangerineWhistle, spuriousDragon, byzantium, constantinople, petersburg" | v2.0.0+ |  |  |
| `UNCLES_IN_AVERAGE_BLOCK_TIME` |  | Include or exclude nonconsensus blocks in avg block time calculation. Exclude if `false`. | false | v2.0.1+ |  |  |
| `AVERAGE_BLOCK_CACHE_PERIOD` |  | Update of average block period cache, in seconds | 30 minutes | v2.0.2+ |  |  |
| `MARKET_HISTORY_CACHE_PERIOD` |  | Update of market history cache, in seconds | 6 hours | v2.0.2+ |  |  |
| `DISABLE_WEBAPP` |  | If `true`, endpoints to webapp are hidden \(compile-time\). Also, enabling it makes notifications go through `db_notify` | `false` | v2.0.3+ | ✅ |  |
| `DISABLE_READ_API` |  | If `true`, read-only endpoints to API are hidden \(compile-time\) | `false` | v2.0.3+ | ✅ |  |
| `DISABLE_WRITE_API` |  | If `true`, write endpoints to API are hidden \(compile-time\) | `false` | v2.0.3+ | ✅ |  |
| `DISABLE_INDEXER` |  | If `true`, indexer application doesn't run | `false` | v2.0.3+ | ✅ |  |
| `WEBAPP_URL` |  | Link to web application instance, e.g. `http://host/path` | \(empty\) | v2.0.3+ |  |  |
| `API_URL` |  | Link to API instance, e.g. `http://host/path` | \(empty\) | v2.0.3+ |  |  |
| `CHAIN_SPEC_PATH` |  | Chain specification path \(absolute file system path or url\) to import block emission reward ranges and genesis account balances from | \(empty\) | v2.0.4+ |  |  |
| `COIN_GECKO_ID` |  | CoinGecko coin id required for fetching an exchange rate | poa-network | v2.0.4+ |  | v2.1.0+ |
| `EMISSION_FORMAT` |  | Should be set to `POA` if you have block emission indentical to POA Network. This env var is used only if `CHAIN_SPEC_PATH` is set | `STANDARD` | v2.0.4+ |  |  |
| `REWARDS_CONTRACT_ADDRESS` |  | Emission rewards contract address. This env var is used only if `EMISSION_FORMAT` is set to `POA` | `0xeca443e8e1ab29971a45a9c57a6a9875701698a5` | v2.0.4+ |  |  |
| `SHOW_ADDRESS_MARKETCAP_PERCENTAGE` |  | Configures marketcap percentage column on the top accounts page | `true` | v2.1.1+ |  |  |
| `BLOCKSCOUT_HOST` |  | Host for API endpoint examples | \(empty\) | v2.1.0+ |  |  |
| `BLOCKSCOUT_PROTOCOL` |  | Url scheme for blockscout | in prod env `https` is used, in dev env `http` is used | v2.1.0+ |  |  |
| `SOCKET_ROOT` |  | Custom websocket url | empty string by default | v3.0.0+ |  |  |
| `API_PATH` |  | PATH in API endpoint URL on API docs page | / | master |  |  |
| `CHECKSUM_ADDRESS_HASHES` |  | If set to `true`, redirects to checksummed version of address hashes | true | master |  |  |
| `CHECKSUM_FUNCTION` |  | Defines checksum address function. 2 available values: "rsk", "eth" | eth | v2.0.1+ |  |  |



