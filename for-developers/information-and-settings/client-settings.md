# JSON RPC Client Setting Requirements

## Supported JSON RPC Clients

BlockScout currently supports [Geth](https://github.com/ethereum/go-ethereum), [Erigon](https://github.com/erigontech/erigon), [Nethermind](https://github.com/NethermindEth/nethermind), [Reth](https://github.com/paradigmxyz/reth), [Besu](https://github.com/hyperledger/besu), [RSKj](https://github.com/rsksmart/rskj), [Lotus](https://github.com/filecoin-project/lotus), and [Ganache](https://archive.trufflesuite.com/ganache/) JSON RPC clients. To define the JSON RPC node variant, it's advised to define the `ETHEREUM_JSONRPC_VARIANT` environment variable*. Correct values include:

| JSON RPC Client | Value          | Note                                                                              |
| --------------- | -------------- | --------------------------------------------------------------------------------- |
| Geth      | \`geth\`       | Default. This value is applicable for both Geth and Reth JSON RPC clients                  |
| Erigon    | \`erigon\`     |  It is suggested to use `erigon` variant for Reth JSON RPC client.                                                                                 |
| Nethermind      | \`nethermind\` | This value is applicable for Reth and deprecated OpenEthereum (aka Parity) JSON RPC clients |
| Besu            | \`besu\`       |                                                                                   |
| RSKj            | \`rsk\`        |                                                                                   |
| Lotus           | \`filecoin\`   |                                                                                   |
| Ganache         | \`ganache\`    |                                                                                   |

*If the variable is not set, JSON RPC variant will be chosen based on `CHAIN_TYPE` variable according to the mapping https://github.com/blockscout/blockscout/blob/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/ethereum_jsonrpc/lib/ethereum_jsonrpc/variant.ex#L114-L120

```
  defp get_default_variant do
    case Application.get_env(:explorer, :chain_type) do
      :rsk -> "rsk"
      :filecoin -> "filecoin"
      _ -> "geth"
    end
  end
```

{% hint style="info" %}
BlockScout currently requires a full archive node in order to import every state change for every address on the target network.
{% endhint %}


## Configs

| Application | Environment | Config path                                                                                                                                                                                                                          |
| ----------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Explorer    | Dev         | [https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/explorer/config/dev](https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/explorer/config/dev)   |
|             | Prod        | [https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/explorer/config/prod](https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/explorer/config/prod) |
| Indexer     | Dev         | [https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/indexer/config/dev](https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/indexer/config/dev)     |
|             | Prod        | [https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/indexer/config/prod](https://github.com/blockscout/blockscout/tree/a2625803c831fb86e38ffe0e28d94bfd697914ce/apps/indexer/config/prod)   |

## Variables to connect to JSON RPC client

| Name                    | Environment Variable         | Default Value                                  | Description                                                                                                                                      |
| ----------------------- | ---------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **HTTP Endpoint**       | `ETHEREUM_JSONRPC_HTTP_URL`  | http://localhost:8545 | The HTTP Endpoint is used to fetch `blocks`, `transactions`, `receipts`, `coin/token balances`.                                                  |
| **Fallback HTTP Endpoint** | `ETHEREUM_JSONRPC_FALLBACK_HTTP_URL`                    | (empty) |Fallback JSON RPC HTTP url. |
| **Tracing Endpoint**    | `ETHEREUM_JSONRPC_TRACE_URL` | http://localhost:8545 | The Tracing endpoint is used to fetch `internal transactions` and `block traces`. In most cases this endpoint is identical to the HTTP Endpoint. |
| **Fallback Tracing Endpoint** | `ETHEREUM_JSONRPC_FALLBACK_TRACE_URL`                    | (empty) |Fallback JSON RPC tracing url. |
| **Eth_call Requests Endpoint**    | `ETHEREUM_JSONRPC_ETH_CALL_URL` | (empty) | JSON RPC url for `eth_call` method requests. |
| **Fallback Eth_call Requests Endpoint**    | `ETHEREUM_JSONRPC_FALLBACK_ETH_CALL_URL` | (empty) | Fallback JSON RPC `eth_call` url. |
| **WebSockets Endpoint** | `ETHEREUM_JSONRPC_WS_URL`    | ws://localhost:8546                            | The WebSockets endpoint subscribes to `newHeads` which alerts the indexer to fetch the new block from the subscription.                          |

## Geth

More information on Geth JSON-RPC [is available here](https://geth.ethereum.org/docs/interacting-with-geth/rpc).

```
sudo /usr/bin/geth --http --http.addr 0.0.0.0 --port 30303 --http.port 8545 --http.api debug,net,eth,shh,web3,txpool --ws.api "eth,net,web3,network,debug,txpool" --ws --ws.addr 0.0.0.0 --ws.port 8546 --ws.origins "*" --sepolia --datadir=/rinkeby --syncmode "full" --gcmode "archive" --http.vhosts "*"
```

_Tracing and pruning: By default, state for the last 128 blocks kept in memory. Most states are garbage collected. If you are running a block explorer or other service relying on transaction tracing without an archive node (--gcmode=archive), you need to trace within this window! Alternatively, specify the "reexec" tracer option to allow regenerating historical state; and ideally switch to chain tracing which amortizes overhead across all traced blocks._

## Erigon

More information on Erigon configuration [is available here](https://erigon.gitbook.io/erigon/advanced-usage/configure-erigon).

## Nethermind

More information on Nethermind configuration [is available here](https://docs.nethermind.io/fundamentals/configuration/).

## Reth

More information on Reth configuration [is available here](https://reth.rs/run/config.html).

## RSKj

More information on RSKj configuration [is available here](https://dev.rootstock.io/rsk/node/configure/reference/).

## Besu

More information on Besu configuration [is available here](https://besu.hyperledger.org/stable/public-networks/how-to/configuration-file).

## Lotus

More information on Lotus configuration [is available here](https://lotus.filecoin.io/lotus/configure/defaults/).

## OpenEthereum

```
--jsonrpc-interface all --jsonrpc-apis web3,eth,net,parity,pubsub,traces --ws-interface all --fat-db=on --pruning=archive --ws-apis all --ws-origins all --ws-hosts all
```