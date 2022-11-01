---
description: For local builds
---

# Docker Integration

{% hint style="success" %}
Please see [https://github.com/blockscout/blockscout/tree/master/docker-compose](https://github.com/blockscout/blockscout/tree/master/docker-compose) for all required information.
{% endhint %}

### Configs for different Ethereum clients

The repo above contains built-in configs for different clients without needing to build the image.

{% hint style="warning" %}
**Note for Linux users**: Linux users who run Blockscout in docker with a local node need to run the node on [http://0.0.0.0/](http://0.0.0.0/) rather than [http://127.0.0.1/](http://127.0.0.1/)
{% endhint %}

* Erigon: `docker-compose -f docker-compose-no-build-erigon.yml up -d`
* Geth: `docker-compose -f docker-compose-no-build-geth.yml up -d`
* Nethermind, OpenEthereum: `docker-compose -f docker-compose-no-build-nethermind up -d`
* Ganache: `docker-compose -f docker-compose-no-build-ganache.yml up -d`
* HardHat network: `docker-compose -f docker-compose-no-build-hardhat-network.yml up -d`
* Running only explorer without DB: `docker-compose -f docker-compose-no-build-no-db-container.yml up -d`. In this case, one container is created - for the explorer itself. And it assumes that the DB credentials are provided through `DATABASE_URL` environment variable.

All of the configs assume the Ethereum JSON RPC is running at [http://localhost:8545](http://localhost:8545/).

