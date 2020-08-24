# Deprecated ENV Variables

{% hint style="info" %}
This table is horizontally scrollable, version information is located in the last column.
{% endhint %}

| Variable | Required | Description | Default | Version | Need recompile | Deprecated in Version |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `ETHEREUM_JSONRPC_JSON_RPC_TRANSPORT` |  | Specifies the transport for blockscout to connect to the Ethereum Node. Available transports are `http` and `ipc`. If `ipc` is selected, also set `IPC_PATH` variable. Replaced with `ETHEREUM_JSONRPC_TRANSPORT` | `http` | v2.1.1+ |  | v3.1.0 |
| `COINMARKETCAP_PAGES` |  | the number of pages on coinmarketcap to list in order to find token's price | 10 | v1.3.10+ |  | v2.0.4 |
| `COIN_GECKO_ID` |  | CoinGecko coin id required for fetching an exchange rate | poa-network | v2.0.4+ |  | v2.1.0+ |
| `NETWORK_ICON` |  | Environment variable for the main network icon or testnet icon. Two options are `_test_network_icon.html` and `_network_icon.html` | \_network\_icon.html | All |  | v2.0.0+ |
| `REWARDS_CONTRACT_ADDRESS` |  | Emission rewards contract address. This env var is used only if `EMISSION_FORMAT` is set to `POA` . Replaced with `REWARDS_CONTRACT` | `0xeca443e8e1ab29971a45a9c57a6a9875701698a5` | v2.0.4+ |  | v3.1.0 |



