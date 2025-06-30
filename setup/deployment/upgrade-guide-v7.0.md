# Upgrade Guide (v7.0 & v8.0)

{% hint style="success" %}
&#x20;🚗  [Autoscout is now available](../../using-blockscout/autoscout.md), providing a simple one-click explorer deployment with Blockscout's optimized hosting infrastructure. Use it for early testing, modifications, and launching a full production-grade explorer. [Get Started Now](../../using-blockscout/autoscout.md) and have **your explorer up-and-running in minutes.**
{% endhint %}

{% hint style="info" %}
We continue to add new features and functionality to Blockscout and recommend updating your instance with each new release. You can check compatibility between your current backend and frontend versions in the [Compatibility Matrix](../requirements/back-front-compatibility-matrix.md).
{% endhint %}

{% hint style="warning" %}
If it has been a while since your last upgrade, we recommend performing incremental upgrades to ensure proper performance. For example if you are running backend v6.9.0, first upgrade to v6.10.0 prior to upgrading to the [latest 7.0 version](https://github.com/blockscout/blockscout/releases). This reduces downtime and ensures all breaking changes are handled.\
\
Please update to v7.0 before updating to v8.0. Follow the same process below replacing v7 with the latest front and backend repositories.
{% endhint %}

## Getting Started

{% hint style="success" %}
This guide walks through the process of updating Blockscout to backend v7.0.2 and frontend v1.38.0 (March, 2025) from v6.10.X. If you have questions about a different upgrade, [contact us in Discord](https://discord.gg/blockscout).\
\
Breaking changes follow the instructions.
{% endhint %}

### 1) Update backend ENV variables

{% hint style="warning" %}
Backend variable renaming only applies to the 6.10.X -> 7.0.X update. If you are performing a more extensive update, please check renaming & deprecations from the release notes of every minor release (6.8.0, 6.9.0 etc) within your update range.&#x20;
{% endhint %}

Newly renamed variables include the `MIGRATION`prefix.  If a variable contained `MIGRATION` in the name previously, it has been moved to the beginning of the variable. Expand below to see all variables you need to rename.

<details>

<summary>Backend Renamed Variables</summary>



| Old name                                                       | New name                                                        |
| -------------------------------------------------------------- | --------------------------------------------------------------- |
| TOKEN\_ID\_MIGRATION\_FIRST\_BLOCK                             | MIGRATION\_TOKEN\_ID\_FIRST\_BLOCK                              |
| TOKEN\_ID\_MIGRATION\_CONCURRENCY                              | MIGRATION\_TOKEN\_ID\_CONCURRENCY                               |
| TOKEN\_ID\_MIGRATION\_BATCH\_SIZE                              | MIGRATION\_TOKEN\_ID\_BATCH\_SIZE                               |
| SHRINK\_INTERNAL\_TRANSACTIONS\_BATCH\_SIZE                    | MIGRATION\_SHRINK\_INTERNAL\_TRANSACTIONS\_BATCH\_SIZE          |
| SHRINK\_INTERNAL\_TRANSACTIONS\_CONCURRENCY                    | MIGRATION\_SHRINK\_INTERNAL\_TRANSACTIONS\_CONCURRENCY          |
| TOKEN\_INSTANCE\_OWNER\_MIGRATION\_CONCURRENCY                 | MIGRATION\_TOKEN\_INSTANCE\_OWNER\_CONCURRENCY                  |
| TOKEN\_INSTANCE\_OWNER\_MIGRATION\_BATCH\_SIZE                 | MIGRATION\_TOKEN\_INSTANCE\_OWNER\_BATCH\_SIZE                  |
| TOKEN\_INSTANCE\_OWNER\_MIGRATION\_ENABLED                     | MIGRATION\_TOKEN\_INSTANCE\_OWNER\_ENABLED                      |
| DENORMALIZATION\_MIGRATION\_BATCH\_SIZE                        | MIGRATION\_DENORMALIZATION\_BATCH\_SIZE                         |
| DENORMALIZATION\_MIGRATION\_CONCURRENCY                        | MIGRATION\_DENORMALIZATION\_CONCURRENCY                         |
| TOKEN\_TRANSFER\_TOKEN\_TYPE\_MIGRATION\_BATCH\_SIZE           | MIGRATION\_TOKEN\_TRANSFER\_TOKEN\_TYPE\_BATCH\_SIZE            |
| TOKEN\_TRANSFER\_TOKEN\_TYPE\_MIGRATION\_CONCURRENCY           | MIGRATION\_TOKEN\_TRANSFER\_TOKEN\_TYPE\_CONCURRENCY            |
| SANITIZE\_INCORRECT\_NFT\_BATCH\_SIZE                          | MIGRATION\_SANITIZE\_INCORRECT\_NFT\_BATCH\_SIZE                |
| SANITIZE\_INCORRECT\_NFT\_CONCURRENCY                          | MIGRATION\_SANITIZE\_INCORRECT\_NFT\_CONCURRENCY                |
| SANITIZE\_INCORRECT\_NFT\_TIMEOUT                              | MIGRATION\_SANITIZE\_INCORRECT\_NFT\_TIMEOUT                    |
| SANITIZE\_INCORRECT\_WETH\_BATCH\_SIZE                         | MIGRATION\_SANITIZE\_INCORRECT\_WETH\_BATCH\_SIZE               |
| SANITIZE\_INCORRECT\_WETH\_CONCURRENCY                         | MIGRATION\_SANITIZE\_INCORRECT\_WETH\_CONCURRENCY               |
| SANITIZE\_INCORRECT\_WETH\_TIMEOUT                             | MIGRATION\_SANITIZE\_INCORRECT\_WETH\_TIMEOUT                   |
| REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_BATCH\_SIZE           | MIGRATION\_REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_BATCH\_SIZE |
| REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_CONCURRENCY           | MIGRATION\_REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_CONCURRENCY |
| REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_TIMEOUT               | MIGRATION\_REINDEX\_INTERNAL\_TRANSACTIONS\_STATUS\_TIMEOUT     |
| FILECOIN\_PENDING\_ADDRESS\_OPERATIONS\_MIGRATION\_BATCH\_SIZE | MIGRATION\_FILECOIN\_PENDING\_ADDRESS\_OPERATIONS\_BATCH\_SIZE  |
| FILECOIN\_PENDING\_ADDRESS\_OPERATIONS\_MIGRATION\_CONCURRENCY | MIGRATION\_FILECOIN\_PENDING\_ADDRESS\_OPERATIONS\_CONCURRENCY  |
| ARBITRUM\_DA\_RECORDS\_NORMALIZATION\_MIGRATION\_BATCH\_SIZE   | MIGRATION\_ARBITRUM\_DA\_RECORDS\_NORMALIZATION\_BATCH\_SIZE    |
| ARBITRUM\_DA\_RECORDS\_NORMALIZATION\_MIGRATION\_CONCURRENCY   | MIGRATION\_ARBITRUM\_DA\_RECORDS\_NORMALIZATION\_CONCURRENCY    |

</details>

### 2) Install backend

-> [blockscout/blockscout:7.0.2](https://hub.docker.com/layers/blockscout/blockscout/7.0.2/images/sha256-b846205631b5bf525022c7d15d076fe0fcbf627e00e03b8285aeccffed3ad145)

### 3) Install frontend

-> [ghcr.io/blockscout/frontend:v1.38.0](https://github.com/blockscout/frontend/pkgs/container/frontend/365117431?tag=v1.38.0)

<details>

<summary>Frontend Variable Updates</summary>

| From                                                                                          | To                                             | Example                                                                                                                                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>NEXT_PUBLIC_ROLLUP_L1_BASE_URL<br><br>NEXT_PUBLIC_ROLLUP_PARENT_CHAIN_NAME<br></p>         | <p>NEXT_PUBLIC_ROLLUP_PARENT_CHAIN<br><br></p> | <p>current values<br><code>NEXT_PUBLIC_ROLLUP_L1_BASE_URL =&#x3C;L1-url></code><br><br><code>NEXT_PUBLIC_ROLLUP_PARENT_CHAIN_NAME =&#x3C;chain-name></code><br></p><p>new values<br><code>NEXT_PUBLIC_ROLLUP_PARENT_CHAIN={'name':'&#x3C;chain-name>','baseUrl':'&#x3C;L1-url>'}</code></p>                                             |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_V3\_APP\_SITE\_KEY                                                 | NEXT\_PUBLIC\_RE\_CAPTCHA\_APP\_SITE\_KEY      |                                                                                                                                                                                                                                                                                                                                         |
| <p>NEXT_PUBLIC_HOMEPAGE_PLATE_TEXT_COLOR<br><br>NEXT_PUBLIC_HOMEPAGE_PLATE_BACKGROUND<br></p> | NEXT\_PUBLIC\_HOMEPAGE\_HERO\_BANNER\_CONFIG   | <p>current values<br><code>NEXT_PUBLIC_HOMEPAGE_PLATE_BACKGROUND=&#x3C;my-background></code><br><br><code>NEXT_PUBLIC_HOMEPAGE_PLATE_TEXT_COLOR=&#x3C;my-text-color></code><br><br>new values<br><code>NEXT_PUBLIC_HOMEPAGE_HERO_BANNER_CONFIG={'background':['&#x3C;my-background>'],'text_color':['&#x3C;my-text-color>']}</code></p> |

**Deprecated Frontend Variables**

| Deprecated                            |
| ------------------------------------- |
| NEXT\_PUBLIC\_AUTH0\_CLIENT\_ID       |
| NEXT\_PUBLIC\_AUTH\_URL               |
| NEXT\_PUBLIC\_LOGOUT\_URL             |
| FAVICON\_GENERATOR\_API\_KEY          |
| NEXT\_PUBLIC\_SENTRY\_DSN             |
| SENTRY\_CSP\_REPORT\_URI              |
| NEXT\_PUBLIC\_SENTRY\_ENABLE\_TRACING |

</details>

### 4) Install microservices

-> Stats microservice [ghcr.io/blockscout/stats:v2.5.0](https://github.com/blockscout/blockscout-rs/pkgs/container/stats/353347284?tag=v2.5.0).

-> Use the `latest` tag to install any other microservices used with your instance\
[https://github.com/blockscout/blockscout-rs](https://github.com/blockscout/blockscout-rs)

## Breaking Changes

{% hint style="danger" %}
`/api/v1/health`, `/api/v1/health/liveness`, `/api/v1/health/readiness` have been removed in favor of `/api/health/**` endpoints.&#x20;
{% endhint %}

{% hint style="danger" %}
`/api/v2/addresses/:address_hash` returns 200 instead 404 for valid hashes which are not in the DB.
{% endhint %}

{% hint style="danger" %}
`/api/v2/tokens/:token_hash/instances` owner’s ens\_domain\_name property now preloads the ens domain name.
{% endhint %}

{% hint style="danger" %}
transaction hash and address hash are no longer mandatory in the `txlistinternal` API v1 endpoint
{% endhint %}

{% hint style="danger" %}
`/metrics` endpoint available on indexer pod (previously existed only on API pod)
{% endhint %}
