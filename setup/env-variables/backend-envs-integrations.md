# Backend ENVs: Integrations

{% hint style="info" %}
The following ENVs are used for different integrations. Some work with various microservices (when the variable begins with MICROSERVICE) while others are contained within the application.

More info on Blockscout Rust MicroServices is available in the [blockscout-rs Github Repo](https://github.com/blockscout/blockscout-rs/tree/main).
{% endhint %}

## Time format

Can be set in format `1h` for 1 hour, `1m` for 1 minute, `1s` or `1` for 1 second, `1ms` for 1 millisecond

{% hint style="warning" %}
_**Note**_**: Before release 5.1.2, all environment variables of time format supported only integers in seconds (without dimensions) as values.**
{% endhint %}

## <mark style="background-color:orange;">Smart-contract verifier / Eth Bytecode DB</mark>

{% hint style="info" %}
Connecting to the smart contract verification service
{% endhint %}

| Variable                                                | Description                                                                                                                                                                                                                                                                               | Parameters                                                                                                             |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `MICROSERVICE_SC_VERIFIER_ENABLED`                      | If `true`, integration with [Rust smart-contract verifier](https://github.com/blockscout/blockscout-rs/tree/main/smart-contract-verifier) is enabled. `true` is the default value starting from version 6.4.0. Implemented in [#5860](https://github.com/blockscout/blockscout/pull/5860) | <p>Version: v5.1.3+<br>Default: <code>true</code><br>Applications: API</p>                                             |
| `MICROSERVICE_SC_VERIFIER_URL`                          | URL of Rust smart-contract verifier. Implemented in [#5860](https://github.com/blockscout/blockscout/pull/5860)                                                                                                                                                                           | <p>Version: v5.1.3+<br>Default: <code>https://eth-bytecode-db.services.blockscout.com/</code><br>Applications: API</p> |
| `MICROSERVICE_ETH_BYTECODE_DB_INTERVAL_BETWEEN_LOOKUPS` | Minimal time after unsuccessful check of smart contract's sources in Eth Bytecode DB. Implemented in [#7187](https://github.com/blockscout/blockscout/pull/7187).                                                                                                                         | <p>Version: v5.1.3+<br>Default: <code>10m</code><br>Applications: API</p>                                              |
| `MICROSERVICE_SC_VERIFIER_TYPE`                         | Type of smart contract microservice could be either `eth_bytecode_db` or `sc_verifier`. Implemented in [#7187](https://github.com/blockscout/blockscout/pull/7187)                                                                                                                        | <p>Version: v5.1.3+<br>Default: <code>sc_verifier</code><br>Applications: API</p>                                  |
| `MICROSERVICE_ETH_BYTECODE_DB_MAX_LOOKUPS_CONCURRENCY`  | Maximum amount of concurrent requests for fetching smart contract's sources in Eth Bytecode DB. Implemented in [#8472](https://github.com/blockscout/blockscout/pull/8472)                                                                                                                | <p>Version: v5.3.0+<br>Default: <code>10</code><br>Applications: API</p>                                               |
| `MICROSERVICE_SC_VERIFIER_API_KEY`                      | API key for verification that metadata sent to verifier microservice from a trusted source. Implemented in [#8750](https://github.com/blockscout/blockscout/pull/8750)                                                                                                                    | <p>Version: v5.3.2+<br>Default: (empty)<br>Applications: API</p>                                                       |

## <mark style="background-color:orange;">Sol2Uml</mark>

{% hint style="info" %}
Sol2Uml is a visualization tool for Solidity contracts.
{% endhint %}

<figure><img src="../../../.gitbook/assets/view-UML.png" alt=""><figcaption><p>Scroll down on the contract page to find the View UML diagram link</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/visualizer-1.png" alt=""><figcaption><p>Contract visualization example</p></figcaption></figure>

| Variable                                 | Description                                                                                                                                                                                                    | Parameters                                                       |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `MICROSERVICE_VISUALIZE_SOL2UML_ENABLED` | If `true`, integration with [Rust sol2uml visualizer](https://github.com/blockscout/blockscout-rs/tree/main/visualizer) is enabled. Implemented in [#6401](https://github.com/blockscout/blockscout/pull/6401) | <p>Version: v5.1.3+<br>Default: (empty)<br>Applications: API</p> |
| `MICROSERVICE_VISUALIZE_SOL2UML_URL`     | URL of Rust visualizer. Implemented in [#6401](https://github.com/blockscout/blockscout/pull/6401)                                                                                                             | <p>Version: v5.1.3+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Sig-provider</mark>

{% hint style="info" %}
The Sig-provider microservice is used by Blockscout to display decoded transaction data on transaction pages and to determine transaction actions
{% endhint %}

| Variable                            | Description                                                                                                                                                                                                        | Parameters                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| `MICROSERVICE_SIG_PROVIDER_ENABLED` | If `true`, integration with [Rust sig-provider service](https://github.com/blockscout/blockscout-rs/tree/main/sig-provider) is enabled. Implemented in [#6541](https://github.com/blockscout/blockscout/pull/6541) | <p>Version: v5.1.3+<br>Default: (empty)<br>Applications: API</p> |
| `MICROSERVICE_SIG_PROVIDER_URL`     | URL of Rust sig-provider service. Implemented in [#6541](https://github.com/blockscout/blockscout/pull/6541)                                                                                                       | <p>Version: v5.1.3+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Blockscout ENS</mark>

{% hint style="info" %}
Blockscout ENS provides indexed data of domain name service for blockscout instances. [Learn more](https://github.com/blockscout/blockscout-rs/tree/main/blockscout-ens).
{% endhint %}

| Variable                    | Description                                                                                                                                                                                                       | Parameters                                                       |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `MICROSERVICE_BENS_ENABLED` | If `true`, integration with [Blockscout ENS service](https://github.com/blockscout/blockscout-rs/tree/main/blockscout-ens) is enabled. Implemented in [#8972](https://github.com/blockscout/blockscout/pull/8972) | <p>Version: v5.4.0+<br>Default: (empty)<br>Applications: API</p> |
| `MICROSERVICE_BENS_URL`     | URL of Blockscout ENS service. Implemented in [#8972](https://github.com/blockscout/blockscout/pull/8972)                                                                                                         | <p>Version: v5.4.0+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Blockscout Account Abstraction</mark>

{% hint style="info" %}
Enables the [User Ops Indexer](https://github.com/blockscout/blockscout-rs/tree/main/user-ops-indexer), a service designed to index, decode and serve user operations as per the ERC-4337 standard
{% endhint %}

| Variable                                   | Description                                                                                                                                                                                                                         | Parameters                                                       |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `MICROSERVICE_ACCOUNT_ABSTRACTION_ENABLED` | If `true`, integration with [Blockscout Account Abstraction service](https://github.com/blockscout/blockscout-rs/tree/main/user-ops-indexer) is enabled. Implemented in [#9145](https://github.com/blockscout/blockscout/pull/9145) | <p>Version: v6.1.0+<br>Default: (empty)<br>Applications: API</p> |
| `MICROSERVICE_ACCOUNT_ABSTRACTION_URL`     | URL of Blockscout ENS service. Implemented in [#9145](https://github.com/blockscout/blockscout/pull/9145)                                                                                                                           | <p>Version: v6.1.0+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Tx Interpreter (Summary) Service</mark>

| Variable                                          | Description                                                                                                                               | Parameters                                                       |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `MICROSERVICE_TRANSACTION_INTERPRETATION_ENABLED` | If `true`, integration with Tx Interpreter Service is enabled. Implemented in [#8957](https://github.com/blockscout/blockscout/pull/8957) | <p>Version: v5.4.0+<br>Default: (empty)<br>Applications: API</p> |
| `MICROSERVICE_TRANSACTION_INTERPRETATION_URL`     | URL of Tx Interpreter Service. Implemented in [#8957](https://github.com/blockscout/blockscout/pull/8957)                                 | <p>Version: v5.4.0+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Metadata Service</mark>

| Variable                                       | Description                                                                                                                                 | Parameters                                                               |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| `MICROSERVICE_METADATA_ENABLED`                | If `true`, integration with Metadata Service is enabled. Implemented in [#9706](https://github.com/blockscout/blockscout/pull/9706)         | <p>Version: v6.4.0+<br>Default: (empty)<br>Applications: API</p>         |
| `MICROSERVICE_METADATA_URL`                    | URL of Metadata Service. Implemented in [#9706](https://github.com/blockscout/blockscout/pull/9706)                                         | <p>Version: v6.4.0+<br>Default: (empty)<br>Applications: API</p>         |
| `MICROSERVICE_METADATA_PROXY_REQUESTS_TIMEOUT` | Timeout for request forwarding from `/api/v2/proxy/metadata/`. Implemented in [#11656](https://github.com/blockscout/blockscout/pull/11656) | <p>Version: v7.0.0+<br>Default: <code>30s</code><br>Applications: API</p> |

## <mark style="background-color:orange;">Multichain Search Service</mark>

{% hint style="info" %}
Multichain Search is the single point of search of the data in the all blockchains.
{% endhint %}

| Variable                                          | Description                                                                                                                                                                        | Parameters                                                                 |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `MICROSERVICE_MULTICHAIN_SEARCH_URL`              | Multichain Search Service API URL. Integration is enabled, if this variable value contains valid URL. Implemented in [#11139](https://github.com/blockscout/blockscout/pull/11139) | <p>Version: v6.10.0+<br>Default: (empty)<br>Applications: API, Indexer</p> |
| `MICROSERVICE_MULTICHAIN_SEARCH_API_KEY`          | Multichain Search Service API key. Implemented in [#11139](https://github.com/blockscout/blockscout/pull/11139)                                                                    | <p>Version: v6.10.0+<br>Default: (empty)<br>Applications: API, Indexer</p> |
| `MICROSERVICE_MULTICHAIN_SEARCH_ADDRESSES_CHUNK_SIZE`          | Chunk size of addresses while exporting to Multichain Search DB. Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377)                                                                    | <p>Version: v8.1.0+<br>Default: 7000<br>Applications: API, Indexer</p> |
| `MIGRATION_BACKFILL_MULTICHAIN_SEARCH_BATCH_SIZE` | Batch size of backfilling Multichain Search Service DB. Implemented in [#11139](https://github.com/blockscout/blockscout/pull/11139)                                               | <p>Version: v6.10.0+<br>Default: 10<br>Applications: Indexer</p>      |
| `INDEXER_DISABLE_MULTICHAIN_SEARCH_DB_EXPORT_MAIN_QUEUE_FETCHER`             | If `true`, multichain DB main (blocks, transactions, addresses) export fetcher doesn't run. Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377).                  | <p>Version: v9.0.0+<br>Default: <code>false</code><br>Applications: Indexer</p>                                      |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_MAIN_QUEUE_BATCH_SIZE`                                 | Batch size for multichain DB main (blocks, transactions, addresses) export fetcher. Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377).                       | <p>Version: v9.0.0+<br>Default: <code>1000</code><br>Applications: Indexer</p>                                        |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_MAIN_QUEUE_CONCURRENCY`                                | Concurrency for multichain DB main (blocks, transactions, addresses) export fetcher. Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377).     | <p>Version: v9.0.0+<br>Default: <code>10</code><br>Applications: Indexer</p>                                         |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_MAIN_QUEUE_ENQUEUE_BUSY_WAITING_TIMEOUT`                                | Timeout before new attempt to append item to multichain DB main (blocks, transactions, addresses) export queue if it's full. [Time format](backend-env-variables.md#time-format). Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377).     | <p>Version: v9.0.0+<br>Default: <code>1s</code><br>Applications: Indexer</p>   |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_MAIN_QUEUE_MAX_QUEUE_SIZE`                                | Maximum size of multichain DB main (blocks, transactions, addresses) export queue. Implemented in [#12377](https://github.com/blockscout/blockscout/pull/12377).     | <p>Version: v9.0.0+<br>Default: <code>1000</code><br>Applications: Indexer</p>   |
| `INDEXER_DISABLE_MULTICHAIN_SEARCH_DB_EXPORT_BALANCES_QUEUE_FETCHER`             | If `true`, multichain DB balances export fetcher doesn't run. Implemented in [#12580](https://github.com/blockscout/blockscout/pull/12580).                  | <p>Version: v9.0.0+<br>Default: <code>false</code><br>Applications: Indexer</p>                                      |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_BALANCES_QUEUE_BATCH_SIZE`                                 | Batch size for multichain DB balances export fetcher. Implemented in [#12580](https://github.com/blockscout/blockscout/pull/12580).                       | <p>Version: v9.0.0+<br>Default: <code>1000</code><br>Applications: Indexer</p>                                        |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_BALANCES_QUEUE_CONCURRENCY`                                | Concurrency for multichain DB balances export fetcher. Implemented in [#12580](https://github.com/blockscout/blockscout/pull/12580).     | <p>Version: v9.0.0+<br>Default: <code>10</code><br>Applications: Indexer</p>                                         |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_BALANCES_QUEUE_ENQUEUE_BUSY_WAITING_TIMEOUT`                                | Timeout before new attempt to append item to multichain DB balances export queue if it's full. [Time format](backend-env-variables.md#time-format). Implemented in [#12580](https://github.com/blockscout/blockscout/pull/12580).     | <p>Version: v9.0.0+<br>Default: <code>1s</code><br>Applications: Indexer</p>   |
| `INDEXER_MULTICHAIN_SEARCH_DB_EXPORT_BALANCES_QUEUE_MAX_QUEUE_SIZE`                                | Maximum size of multichain DB balances export queue. Implemented in [#12580](https://github.com/blockscout/blockscout/pull/12580).     | <p>Version: v9.0.0+<br>Default: <code>1000</code><br>Applications: Indexer</p>   |

## <mark style="background-color:orange;">TAC Operation Lifecycle Service</mark>

| Variable                                          | Description                                                                                                                                                                                            | Parameters                                                                 |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| `MICROSERVICE_TAC_OPERATION_LIFECYCLE_URL`        | TAC Operation Lifecycle Service API URL. Integration is enabled, if this variable value contains valid URL. Implemented in [#12367](https://github.com/blockscout/blockscout/pull/12367)               | <p>Version: v8.1.0+<br>Default: (empty)<br>Applications: API</p>            |
| `MICROSERVICE_TAC_OPERATION_LIFECYCLE_ENABLED`    | If `false`, TAC Operation Lifecycle Service integration is disabled despite `MICROSERVICE_TAC_OPERATION_LIFECYCLE_URL`. Implemented in [#12367](https://github.com/blockscout/blockscout/pull/12367)   | <p>Version: v8.1.0+<br>Default: <code>true</code><br>Applications: API</p>  |

## <mark style="background-color:orange;">Sourcify</mark>

{% hint style="info" %}
Allows for contract verification via [Sourcify](https://sourcify.dev/)
{% endhint %}

| Variable                       | Description                                                     | Parameters                                                                                                                                                                                |
| ------------------------------ | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SOURCIFY_INTEGRATION_ENABLED` | Enables or disables verification of contracts through Sourcify. | <p>Version: v5.1.3+<br>Default: <code>false</code><br>Applications: API</p>                                                                                                               |
| `SOURCIFY_SERVER_URL`          | URL to Sourcify backend.                                        | <p>Version: v3.7.0+<br>Default: <code>https://sourcify.dev/server</code><br>Applications: API</p>                                                                                         |
| `SOURCIFY_REPO_URL`            | URL to Sourcify repository with fully verified contracts.       | <p>Version: v3.7.0+<br>Default: <code>https://repo.sourcify.dev/contracts/</code><br>Before v3.7.1: <code>https://repo.sourcify.dev/contracts/full_match/</code><br>Applications: API</p> |

## <mark style="background-color:orange;">Tenderly</mark>

| Variable              | Description                                                                                                                                                                                                                                                                   | Parameters                                                       |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `SHOW_TENDERLY_LINK`  | if `true`, Open in Tenderly" button is displayed on the transaction page. Implemented in [#4656](https://github.com/blockscout/blockscout/pull/4656)                                                                                                                          | <p>Version: v4.0.0+<br>Default: (empty)<br>Applications: API</p> |
| `TENDERLY_CHAIN_PATH` | Chain path to the transaction in Tenderly. For instance, for transactions in xDai, Tenderly link looks like this `https://dashboard.tenderly.co/tx/xdai/0x...`, then `TENDERLY_CHAIN_PATH =/xdai.` Implemented in [#4656](https://github.com/blockscout/blockscout/pull/4656) | <p>Version: v4.0.0+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Datadog</mark>

{% hint style="info" %}
Integration with the Datadog monitoring and analytics tools
{% endhint %}

| Variable       | Description                                                                                     | Parameters                                                   |
| -------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `DATADOG_HOST` | Host configuration setting for [Datadog integration](https://docs.datadoghq.com/integrations/). | <p>Version: all<br>Default: (empty)<br>Applications: API</p> |
| `DATADOG_PORT` | Port configuration setting for [Datadog integration](https://docs.datadoghq.com/integrations/). | <p>Version: all<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Spandex</mark>

{% hint style="info" %}
Spandex is a library for tracing Elixir applications
{% endhint %}

| Variable                 | Description                                                                              | Parameters                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `SPANDEX_BATCH_SIZE`     | [Spandex](https://github.com/spandex-project/spandex) and Datadog configuration setting. | <p>Version: all<br>Default: (empty)<br>Applications: API</p> |
| `SPANDEX_SYNC_THRESHOLD` | [Spandex](https://github.com/spandex-project/spandex) and Datadog configuration setting. | <p>Version: all<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Analytics</mark>

{% hint style="info" %}
Variables for adding Mixpanel and/or amplitude for visitor analytics.&#x20;
{% endhint %}

| Variable            | Description                                                                                                                              | Parameters                                                                              |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `MIXPANEL_TOKEN`    | [Mixpanel](https://mixpanel.com/) project token.                                                                                         | <p>Needs Recompile: ☑️<br>Version: v5.0.0+<br>Default: (empty)<br>Applications: API</p> |
| `MIXPANEL_URL`      | Url to use Mixpanel with proxy ([Collection via Proxy](https://developer.mixpanel.com/docs/collection-via-a-proxy)).                     | <p>Needs Recompile: ☑️<br>Version: v5.0.0+<br>Default: (empty)<br>Applications: API</p> |
| `AMPLITUDE_API_KEY` | [Amplitude](https://amplitude.com/) API key.                                                                                             | <p>Needs Recompile: ☑️<br>Version: v5.0.0+<br>Default: (empty)<br>Applications: API</p> |
| `AMPLITUDE_URL`     | Url to use Amplitude with proxy ([Use Domain Proxy to Relay Events](https://www.docs.developers.amplitude.com/analytics/domain-proxy/)). | <p>Needs Recompile: ☑️<br>Version: v5.0.0+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Solidityscan</mark>

{% hint style="info" %}
Enables security scoring for smart contracts
{% endhint %}

<figure><img src="../../../.gitbook/assets/solidity-scan.png" alt=""><figcaption></figcaption></figure>

| Variable                   | Description                                                                                                                                                                                                                                                | Parameters                                                       |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| `SOLIDITYSCAN_PLATFORM_ID` | Internal platform id in [Solidityscan](https://apidoc.solidityscan.com/solidityscan-security-api/solidityscan-other-apis/quickscan-api-v1). Implemented in [#10473](https://github.com/blockscout/blockscout/pull/10473)                                   | <p>Version: v6.8.0+<br>Default: 16<br>Applications: API</p>      |
| `SOLIDITYSCAN_CHAIN_ID`    | Internal chain id in [Solidityscan](https://apidoc.solidityscan.com/solidityscan-security-api/solidityscan-other-apis/quickscan-api-v1). It may not match with actual chain ID. Implemented in [#8908](https://github.com/blockscout/blockscout/pull/8908) | <p>Version: v5.3.3+<br>Default: (empty)<br>Applications: API</p> |
| `SOLIDITYSCAN_API_TOKEN`   | API token for usage of [Solidityscan API](https://apidoc.solidityscan.com/solidityscan-security-api/solidityscan-other-apis/quickscan-api-v1).                                                                                                             | <p>Version: v5.3.3+<br>Default: (empty)<br>Applications: API</p> |

## <mark style="background-color:orange;">Noves.fi</mark>

{% hint style="info" %}
Adds additional transaction details such as summaries and asset flows. [More info here](https://www.blog.blockscout.com/better-blockchain-data-with-noves/).
{% endhint %}

| Variable                | Description                                                                                                                                            | Parameters                                                                                        |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- |
| `NOVES_FI_BASE_API_URL` | [Noves.fi API](https://blockscout.noves.fi/swagger/index.html) base URL. Implemented in [#9056](https://github.com/blockscout/blockscout/pull/9056).   | <p>Version: v6.1.0+<br>Default: <code>https://blockscout.noves.fi</code><br>Applications: API</p> |
| `NOVES_FI_CHAIN_NAME`   | [Noves.fi API](https://blockscout.noves.fi/swagger/index.html) chain name. Implemented in [#9056](https://github.com/blockscout/blockscout/pull/9056). | <p>Version: v6.1.0+<br>Default: (empty)<br>Applications: API</p>                                  |
| `NOVES_FI_API_TOKEN`    | [Noves.fi API](https://blockscout.noves.fi/swagger/index.html) token. Implemented in [#9056](https://github.com/blockscout/blockscout/pull/9056).      | <p>Version: v6.1.0+<br>Default: (empty)<br>Applications: API</p>                                  |

## <mark style="background-color:orange;">MUD framework</mark>

{% hint style="info" %}
[The MUD framework](https://mud.dev/introduction) provides standardized tools for data retrieval, libraries and more.
{% endhint %}

| Variable              | Description                                                                                                                                                                                               | Parameters                                                                                    |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `MUD_INDEXER_ENABLED` | If `true`, integration with [MUD](https://mud.dev/services/indexer#schemaless-indexing-with-postgresql-via-docker) is enabled. Implemented in [#9869](https://github.com/blockscout/blockscout/pull/9869) | <p>Version: v6.6.0+<br>Default: (empty)<br>Applications: API</p>                              |
| `MUD_DATABASE_URL`    | MUD indexer DB connection URL.                                                                                                                                                                            | <p>Version: v6.6.0+<br>Default: value from <code>DATABASE_URL</code><br>Applications: API</p> |
| `MUD_POOL_SIZE`       | MUD indexer DB `pool_size`                                                                                                                                                                                | <p>Version: v6.6.0+<br>Default: <code>50</code><br>Applications: API</p>                      |

## <mark style="background-color:orange;">Xname app</mark>

{% hint style="info" %}
Enables Xname app integration, which includes humanity score displayment.
{% endhint %}

| Variable             | Description                                                                                                             | Parameters                                                                                      |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `XNAME_BASE_API_URL` | [Xname API](https://xname.app/) base URL. Implemented in [#11010](https://github.com/blockscout/blockscout/pull/11010). | <p>Version: v6.9.2+<br>Default: <code>https://gateway.xname.app</code><br>Applications: API</p> |
| `XNAME_API_TOKEN`    | [Xname API](https://xname.app/) token. Implemented in [#11010](https://github.com/blockscout/blockscout/pull/11010).    | <p>Version: v6.9.2+<br>Default: (empty)<br>Applications: API</p>                                |

## <mark style="background-color:orange;">Stylus contract verifier</mark>

{% hint style="info" %}
Connecting to the Stylus smart contract verification service
{% endhint %}

| Variable                           | Description                                                                                                                                                                                                                                                            | Parameters                                                        |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `MICROSERVICE_STYLUS_VERIFIER_URL` | URL of Stylus verifier. If set valid url and `CHAIN_TYPE=arbitrum`, integration with [Stylus verifier](https://github.com/blockscout/blockscout-rs/tree/main/stylus-verifier) is enabled. Implemented in [#11183](https://github.com/blockscout/blockscout/pull/11183) | <p>Version: v6.10.0+<br>Default: (empty)<br>Applications: API</p> |
