# Customized Backend

{% hint style="info" %}
You will use the [**`external-backend.yml`**](https://github.com/blockscout/blockscout/blob/master/docker-compose/external-backend.yml)file.
{% endhint %}

## Prerequisites

* Docker v20.10+
* Docker-compose 2.x.x+
* Running Ethereum JSON RPC client

Please see [https://github.com/blockscout/blockscout/tree/master/docker-compose](https://github.com/blockscout/blockscout/tree/master/docker-compose) for additional information

### 1) Pull changes from the Blockscout master branch

We assume Blockscout is already deployed in your environment.

```
git pull origin master
```

### 2) Navigate to the docker compose folder

```
cd docker-compose
```

### 3) Run docker compose with BACK\_PROXY\_PASS variable.

You will pass in the backend proxy url when running docker compose. The standard configuration for the backend is `http//host.docker.internal:4000` but if you've made any changes pass in your url.

Run all containers (up) and run processes in the background (-d).

```
BACK_PROXY_PASS=http//host.docker.internal:4000 docker compose -f external-backend.yml up -d
```

View progress and check containers

```
Docker ps
```

### 4) Check the proxy configuration

```
cd proxy
Cat default.conf.template
```

Unless you overrode the default configs (or did not provide the `FRONT_PROXY_PASS` variable) , you will see the default port for the backend is `4000`, and `3000` for the frontend.

However, with the proxy setup the whole application will default to port `80` (which is just localhost). Your frontend instance should now be served on localhost. [More details about the recommended proxy setup](proxy-setup.md).

{% hint style="info" %}
It may take several minutes for the frontend to propagate during this process.
{% endhint %}

### 5) Adjust frontend ENVs if needed

There are several required ENVs for the frontend. If required variables are missing or invalid the frontend will show in error message and will not run the app.

* The common list of [frontend ENVs and descriptions](../../information-and-settings/env-variables/frontend-common-envs/).
* A detailed list with all available ENVs is in the [frontend repo folder.](https://github.com/blockscout/frontend/blob/main/docs/ENVS.md)

To adjust, stop the frontend container, update the env file (or pass variables directly), and restart the container.

### 6) Check Microservice ENVs

Typically the default values will provide what you need for the [`common-visualizer.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-visualizer.env), [`common-stats.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-stats.env), and [`common-smart-contract-verifier.env`](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-smart-contract-verifier.env) files.

Note that in the `smart-contract-verifier.envs` the `SMART_CONTRACT_VERIFIER__SOLIDITY__FETCHER__LIST__LIST_URL` variable is different depending on your OS. The default is Linux, if you are running macOS or Windows be sure to comment out the appropriate variables.
