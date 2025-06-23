# Celestia Node / Indexer

{% hint style="info" %}
More info on the Blockscout + Celestia integration is available in this blog post: [https://www.blog.blockscout.com/celestia-superhighway-supporting-high-data-availability-on-blockscout/](https://www.blog.blockscout.com/celestia-superhighway-supporting-high-data-availability-on-blockscout/)
{% endhint %}

## How to run a Celestia light node with a Celestia blobs indexer

We'll use Docker Compose to run everything we need: Celestia Light node, Blobs indexer, and Postgres DB for it.

### Setup

The `docker-compose.yml` contains the following:

```yml
services:
  celestia-light-node:
    image: ghcr.io/celestiaorg/celestia-node:v0.21.8-mocha
    container_name: celestia-light-node
    restart: always
    env_file:
      - node.env
    command: ["celestia", "light", "start", "--core.ip", "${RPC_URL}", "--core.port", "9090", "--p2p.network", "${P2P_NETWORK}", "--rpc.addr", "0.0.0.0", "--rpc.skip-auth", "--gateway", "--gateway.addr", "0.0.0.0"]
    ports:
      - 26658:26658
      - 9090:9090
    volumes:
      - /data/celestia:/home/celestia

  database:
    image: postgres:15
    container_name: 'da-indexer-postgres'
    restart: always
    environment:
      POSTGRES_PASSWORD: 'our_password'
      POSTGRES_USER: 'postgres'
      POSTGRES_HOST_AUTH_METHOD: 'trust'
    ports:
      - 5432:5432
    volumes:
      - /data/postgres:/var/lib/postgresql/data

  da-indexer:
    image: ghcr.io/blockscout/da-indexer:v1.1.0
    container_name: 'da-indexer'
    restart: always
    depends_on:
      - database
    ports:
      - "8050:8050"
      - "8051:8051"
    env_file:
      - indexer.env
```

Make sure to replace `our_password` for the DB with your password.

This yml requires having two env files in the same directory:

**1)** `node.env` for configuring the light node:

```
P2P_NETWORK=mocha
RPC_URL=celestia-mocha-archive-rpc.mzonder.com
# P2P_NETWORK=celestia
# RPC_URL=celestia-rpc.brightlystake.com
```

Uncomment and use the last two lines when you need Celestia Mainnet instead of Celestia Mocha. \
\
The lists of Celestia RPC nodes can be found at:

* &#x20;[https://docs.celestia.org/how-to-guides/mocha-testnet#production-rpc-endpoints](https://docs.celestia.org/how-to-guides/mocha-testnet#production-rpc-endpoints)
* &#x20;[https://docs.celestia.org/how-to-guides/mainnet#production-rpc-endpoints](https://docs.celestia.org/how-to-guides/mainnet#production-rpc-endpoints)

**2)** `indexer.env` for configuring the blobs indexer:

```
DA_INDEXER__INDEXER__DA__CELESTIA__RPC__URL="http://celestia-light-node:26658"
DA_INDEXER__INDEXER__DA__CELESTIA__SAVE_BATCH_SIZE=1000
DA_INDEXER__INDEXER__CONCURRENCY=15
DA_INDEXER__DATABASE__CONNECT__URL=postgres://postgres:our_password@database:5432/blockscout
DA_INDEXER__DATABASE__CREATE_DATABASE="true"
DA_INDEXER__DATABASE__RUN_MIGRATIONS="true"
```

Here you only need to replace `our_password` with the DB password defined in the `docker-compose.yml`.

### Usage

* To start the services, run `docker compose up -d`.
* To see the last indexer logs, run `docker logs -n 100 da-indexer`.
* To see the last node logs, run `docker logs -n 100 celestia-light-node`.

After services are started, the indexer API is available here: http://example.com:8050/api/v1/celestia/blob

Please note, the node needs some time to sync with other Celestia nodes and download data.

* Examples and descriptions for the API are available in project's readme: [https://github.com/blockscout/blockscout-rs/tree/main/da-indexer#readme](https://github.com/blockscout/blockscout-rs/tree/main/da-indexer#readme)
* More detailed tutorials: [https://docs.celestia.org/](https://docs.celestia.org/)

{% hint style="info" %}
More info on the Blockscout + Celestia integration is available in this blog post: [https://www.blog.blockscout.com/celestia-superhighway-supporting-high-data-availability-on-blockscout/](https://www.blog.blockscout.com/celestia-superhighway-supporting-high-data-availability-on-blockscout/)
{% endhint %}
