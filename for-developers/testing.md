# Testing

### Requirements

* Install `chromedriver` . It is required to run tests from `./apps/block_scout_web` of the Umbrella application.
*   This set of environment variables is required for each run of the test (`mix test`) suite:

    ```
    export MIX_ENV=test
    export POSTGRES_DB=explorer_test
    export POSTGRES_PASSWORD=postgres
    export POSTGRES_USER=postgres
    export CHAIN_ID=77
    ```

### Running tests

1. Build assets. `cd apps/block_scout_web/assets && npm run build; cd -`
2. Format Elixir code. `mix format`
3. Lint Elixir code. `mix credo --strict`
4. Run the dialyzer. `mix dialyzer --halt-exit-status`
5. Check the Elixir code for vulnerabilities. `cd apps/explorer && mix sobelow --config; cd -` `cd apps/block_scout_web && mix sobelow --config; cd -`
6. Lint JavaScript code. `cd apps/block_scout_web/assets && npm run eslint; cd -`
7. Test JavaScript code. `cd apps/block_scout_web/assets && npm run test; cd -`
8. Run separate test suites for the Umbrella application\
   \- `indexer`\
   `mix do ecto.create --quiet, ecto.migrate && cd apps/indexer && mix do compile, test --no-start && cd -` \
   \
   \- `explorer`\
   `mix do ecto.create --quiet, ecto.migrate && cd apps/explorer && mix do compile, test --no-start && cd -`  \
   \
   \- `block_scout_web`\
   `mix do ecto.create --quiet, ecto.migrate && cd apps/block_scout_web && mix do compile, test --no-start && cd -`\
   \
   &#x20;\- `ethereum_jsonrpc`\
   `mix do ecto.create --quiet, ecto.migrate && cd apps/ethereum_jsonrpc && mix do compile, test --no-start && cd -`

### **Nethermind**

**Mox**

**This is the default setup. `mix test --no-start` will work on its own, but to be explicit, use the following setup**:

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Nethermind.Mox \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Mox \
mix test --no-start --exclude no_nethermind
```

**HTTP / WebSocket**

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Nethermind.HTTPWebSocket \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Nethermind \
mix test --no-start --exclude no_nethermind
```

| Protocol  | URL                     |
| --------- | ----------------------- |
| HTTP      | `http://localhost:8545` |
| WebSocket | `ws://localhost:8546`   |

### **Geth**

**Mox**

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Geth.Mox \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Mox \
mix test --no-start --exclude no_geth
```

**HTTP / WebSocket**

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Geth.HTTPWebSocket \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Geth \
mix test --no-start --exclude no_geth
```

| Protocol  | URL                                               |
| --------- | ------------------------------------------------- |
| HTTP      | `https://mainnet.infura.io/8lTvJTKmHPCHazkneJsY`  |
| WebSocket | `wss://mainnet.infura.io/ws/8lTvJTKmHPCHazkneJsY` |
