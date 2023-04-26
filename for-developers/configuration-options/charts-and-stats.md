---
description: New Blockscout stats service
---

# Charts and Stats

The new version of Blockscout includes a charts and stats service where chain statistics can be setup.&#x20;

<figure><img src="../../.gitbook/assets/stats (1).png" alt=""><figcaption><p>Stats page example</p></figcaption></figure>

## Basic Setup

* The stats service can be run with the following docker compose file, which runs a separate postgres database for the service. [https://github.com/blockscout/blockscout/blob/master/docker-compose/services/docker-compose-stats.yml](https://github.com/blockscout/blockscout/blob/master/docker-compose/services/docker-compose-stats.yml)
* ENV variables related to the stats service: [ https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-stats.env](https://github.com/blockscout/blockscout/blob/master/docker-compose/envs/common-stats.env)
  * Most variables can remain the same on installation. If you did not use Docker compose to setup Blockscout, you may need to assign `STATS__BLOCKSCOUT_DB_URL` to your DB url.
* Finally, point the `NEXT_PUBLIC_STATS_API_HOST` ENV variable ([https://github.com/blockscout/frontend/blob/main/configs/envs/.env.common#L16](https://github.com/blockscout/frontend/blob/main/configs/envs/.env.common#L16)) to the stats service.
