---
description: Migrate to the new frontend using Docker
---

# All-In-One Container

{% hint style="info" %}
You will use the [**`docker-compose.yml`**](https://github.com/blockscout/blockscout/blob/master/docker-compose/docker-compose.yml) file.
{% endhint %}

## Prerequisites

* Docker v20.10+
* Docker-compose 2.x.x+
* Running Ethereum JSON RPC client

Please see [https://github.com/blockscout/blockscout/tree/master/docker-compose](https://github.com/blockscout/blockscout/tree/master/docker-compose) for additional information

## Migration

### 1) Pull changes from the master branch

We assume Blockscout is already deployed in your environment.

```
git pull origin master
```

### 2) Navigate to the docker compose folder

```
cd docker-compose
```

### 3) Adjust backend envs for your instance

Replace the example environment variables in the `environment:` list of the `docker-compose.yml` file.

<pre><code><strong>cat docker-compose.yml
</strong></code></pre>

By default, standard test setup ENV variables (ganache) are set in the `environment:` list. Replace these with env vars from your existing backend. The only one you **NEED to keep** is **`API_V2_ENABLED='true'`** . Any values added here will override existing variables when starting the docker container.

<pre data-full-width="true"><code><strong>environment:
</strong>        ETHEREUM_JSONRPC_VARIANT: 'ganache'
        ETHEREUM_JSONRPC_HTTP_URL: http://host.docker.internal:8545/
        ETHEREUM_JSONRPC_WS_URL: ws://host.docker.internal:8545/
        INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER: 'true'
        INDEXER_DISABLE_PENDING_TRANSACTIONS_FETCHER: 'true'
        DATABASE_URL: postgresql://postgres:@host.docker.internal:7432/blockscout?ssl=false
        ECTO_USE_SSL: 'false'
        SECRET_KEY_BASE: '56NtB48ear7+wMSf0IQuWDAAazhpb31qyc7GiyspBP2vh7t5zlCsF5QDv76chXeN'
        CHAIN_ID: '1337'
        API_V2_ENABLED: 'true'
        MIX_ENV: 'prod'
</code></pre>

### 4) Run docker compose

Run all containers (up) and run processes in the background (-d).

```
docker-compose up -d
```

Check progress and view containers:

```
Docker ps
```

### 5) Check the proxy configuration

```
cd proxy
Cat default.conf.template
```

Unless you overrode the default configs, you will see the default port for the backend is 4000, and 3000 for the frontend. However, these are not exposed because they are running within the container. **This means localhost:3000 will not work.**

Since the proxy is in place (listen 80) the whole application should default to port 80 (which is just localhost). So your instance with the new frontend should now be served on localhost. [More details about the recommended proxy setup](proxy-setup.md).

{% hint style="info" %}
It may take several minutes for the frontend to propagate during this process.
{% endhint %}

### 6) Adjust frontend ENVs if needed

There are several required ENVs for the frontend. If required variables are missing or invalid the frontend will show in error message and will not run the app.

* The common list of [frontend ENVs and descriptions](../../information-and-settings/env-variables/frontend-common-envs.md).
* A detailed list with all available ENVs is in the [frontend repo folder.](https://github.com/blockscout/frontend/blob/main/docs/ENVS.md)

To adjust, stop the frontend container, update the env file (or pass variables directly), and restart the container.

### 7) Check Microservice ENVs

Typically the default values will provide what you need for the [`common-visualizer.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-visualizer.env), [`common-stats.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-stats.env), and [`common-smart-contract-verifier.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-smart-contract-verifier.env) files.

Note that in the `smart-contract-verifier.envs` the `SMART_CONTRACT_VERIFIER__SOLIDITY__FETCHER__LIST__LIST_URL` variable is different depending on your OS. The default is Linux, if you are running macOS or Windows be sure to comment out the appropriate variables.
