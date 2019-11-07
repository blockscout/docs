# Testing

### Requirements

* PhantomJS \(for wallaby\)

### Running tests

1. Build assets. `cd apps/block_scout_web/assets && npm run build; cd -`
2. Format Elixir code. `mix format`
3. Run the test suite with coverage for whole umbrella project. This step can be run with different configuration outlined below. `mix coveralls.html --umbrella`
4. Lint Elixir code. `mix credo --strict`
5. Run the dialyzer. `mix dialyzer --halt-exit-status`
6. Check the Elixir code for vulnerabilities. `cd apps/explorer && mix sobelow --config; cd -` `cd apps/block_scout_web && mix sobelow --config; cd -`
7. Lint JavaScript code. `cd apps/block_scout_web/assets && npm run eslint; cd -`
8. Test JavaScript code. `cd apps/block_scout_web/assets && npm run test; cd -`

### **Parity**

**Mox**

**This is the default setup. `mix coveralls.html --umbrella` will work on its own, but to be explicit, use the following setup**:

```text
export ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Parity.Moxexport ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Moxmix coveralls.html --umbrella --exclude no_parity
```

**HTTP / WebSocket**

```text
export ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Parity.HTTPWebSocketexport ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Paritymix coveralls.html --umbrella --exclude no_parity
```

| Protocol | URL |
| :--- | :--- |
| HTTP | `http://localhost:8545` |
| WebSocket | `ws://localhost:8546` |

### **Geth**

**Mox**

```text
export ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Geth.Moxexport ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Moxmix coveralls.html --umbrella --exclude no_geth
```

**HTTP / WebSocket**

```text
export ETHEREUM_JSONRPC_CASE=EthereumJSONRPC.Case.Geth.HTTPWebSocketexport ETHEREUM_JSONRPC_WEB_SOCKET_CASE=EthereumJSONRPC.WebSocket.Case.Gethmix coveralls.html --umbrella --exclude no_geth
```

| Protocol | URL |
| :--- | :--- |
| HTTP | `https://mainnet.infura.io/8lTvJTKmHPCHazkneJsY` |
| WebSocket | `wss://mainnet.infura.io/ws/8lTvJTKmHPCHazkneJsY` |

