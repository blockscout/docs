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
8. Run the test suite inside the umbrella application: `mix cmd --app block_scout_web mix test`.&#x20;

### **Parity**

**Mox**

**This is the default setup. `mix test --no-start` will work on its own, but to be explicit, use the following setup**:

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Parity.Mox \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Mox \
mix test --no-start --exclude no_parity
```

**HTTP / WebSocket**

```
ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Parity.HTTPWebSocket \
ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Parity \
mix test --no-start --exclude no_parity
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
