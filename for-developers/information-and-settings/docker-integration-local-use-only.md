# Docker Integration \(Local Use Only\)

{% hint style="warning" %}
This integration is not production ready - use locally for now.
{% endhint %}

## Usage

Blockscout requires `PostgreSQL` server. This is provided by starting the script \(new docker image will be created named `postgres`\)

**Start command** `make start` - Sets everything up and starts BlockScout in a docker container. To connect it to your local environment, configure using the [ENV variables](docker-integration-local-use-only.md#env-variables) described below.

**Example connecting to local `ganache` instance running on port `2000` on Mac/Windows:**

```text
COIN=DAI \
ETHEREUM_JSONRPC_VARIANT=ganache \ 
ETHEREUM_JSONRPC_HTTP_URL=http://host.docker.internal:2000 \
ETHEREUM_JSONRPC_WS_URL=ws://host.docker.internal:2000 \
make start
```

Blockscout will be available on `localhost:4000`

{% hint style="info" %}
**mac/Windows**: Docker provides a special URL - `host.docker.internal` - that is available in the container and routed to your local machine.

**Linux:** Docker is starting using `--network=host` and all services are available on `localhost`
{% endhint %}

#### Migrations

By default, `Makefile` completes migrations on `PostgreSQL` creation.

You can also run migrations manually using the `make migrate` command.

{% hint style="danger" %}
Migrations will clean up your local database
{% endhint %}

## Env variables

BlockScout supports 3 different JSON RPC Variants. Variant can be configured using `ETHEREUM_JSONRPC_VARIANT` environment variable.

**Example:**

```text
ETHEREUM_JSONRPC_VARIANT=ganache make start
```

{% hint style="warning" %}
Do not use `sudo with make start` command since

> Basically, whenever one uses `sudo` with the Makefile/Docker, it causes this error of not being able to communicate with the node.

[https://github.com/poanetwork/blockscout/issues/2795\#issuecomment-546076853](https://github.com/poanetwork/blockscout/issues/2795#issuecomment-546076853)

otherwise, application inside the container cannot read environment variables including archive node's RPC/WebSockets endpoints
{% endhint %}

**Available options are:**

* `parity` - Parity JSON RPC \(works for OpenEthereum & Nethermind client as well\) \(**Default**\)
* `geth` - Geth JSON RPC
* `besu` - Hyperledger Besu RPC
* `ganache` - Ganache JSON RPC

| Variable | Description | Default value |
| :--- | :--- | :--- |
| `ETHEREUM_JSONRPC_VARIANT` | Variant of your JSON RPC service: `parity`, `geth`, `besu` or `ganache` | `parity` |
| `ETHEREUM_JSONRPC_HTTP_URL` | HTTP JSON RPC URL Only for `geth` or `ganache` variant | See below - based on JSONRPC variant |
| `ETHEREUM_JSONRPC_WS_URL` | WS JSON RPC url | See below - based on JSONRPC variant |
| `ETHEREUM_JSONRPC_TRACE_URL` | Trace URL **Only for `parity` variant** | `http://localhost:8545` |
| `COIN` | Default Coin | `POA` |
| `LOGO` | Coin logo | Empty |
| `NETWORK` | Network | Empty |
| `SUBNETWORK` | Subnetwork | Empty |
| `NETWORK_ICON` | Network icon | Empty |
| `NETWORK_PATH` | Network path | `/` |

### Default Values for JSONRPC Variants

`ETHEREUM_JSONRPC_HTTP_URL` default values:

* For `parity` - `http://localhost:8545`
* For `geth` - `https://mainnet.infura.io/8lTvJTKmHPCHazkneJsY`
* For `besu` - `http://localhost:8545`
* For `ganache` - `http://localhost:7545`

`ETHEREUM_JSONRPC_WS_URL` default values:

* For `parity` - `ws://localhost:8546`
* For `geth` - `wss://mainnet.infura.io/8lTvJTKmHPCHazkneJsY/ws`
* For `besu` - `ws://localhost:8546`
* For `ganache` - `ws://localhost:7545`


## Known issues

### Windows Makefile error

C:\Program Files\Docker\Docker\resources\bin\docker.exe: Error response from daemon: OCI runtime create failed: container_linux.go:349: starting container process caused "exec: "C:/Program Files/Git/usr/bin/sh": stat C:/Program Files/Git/usr/bin/sh: no such file or directory": unknown.
make: *** [Makefile:265: start] Error 127


On receiving this error you can change the Makefile and make the following adjustments to `docker\Makefile`:

* From: `$(DOCKER_IMAGE) /bin/sh -c "echo $$MIX_ENV && mix do ecto.create, ecto.migrate"`
* To: `$(DOCKER_IMAGE) //bin/sh -c "echo $$MIX_ENV && mix do ecto.create, ecto.migrate"`

* From: `$(DOCKER_IMAGE) /bin/sh -c "mix phx.server"`
* To: `$(DOCKER_IMAGE) //bin/sh -c "mix phx.server"`
