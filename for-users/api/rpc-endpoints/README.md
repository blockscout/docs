---
description: API designed for ease of use
---

# RPC Endpoints

This API is provided for developers transitioning applications from Etherscan to BlockScout and applications requiring general API and data support. It supports GET and POST requests.

{% hint style="info" %}
Base URLs vary by instance, but all follow the same pattern. Simply add `/ap`i to the end of the url. For example with the Goerli instance.

* Base url: [https://eth-goerli.blockscout.com](https://eth-goerli.blockscout.com/)
* API url: [https://eth-goerli.blockscout.com/api](https://eth-goerli.blockscout.com/api)

An example query includes a module and action(s)/parameters. For example: \
[https://eth-goerli.blockscout.com/api?module=**account**\&action=**listaccounts**\&page=2\&offset=5](https://eth-goerli.blockscout.com/api?module=account\&action=listaccounts\&page=2\&offset=5)
{% endhint %}

The following modules are supported. Click through to see specific endpoints and parameters.

| [Account](account.md)         | `?module=account`     |
| ----------------------------- | --------------------- |
| [Logs](logs.md)               | `?module=logs`        |
| [Token](token.md)             | `?module=token`       |
| [Stats](stats.md)             | `?module=stats`       |
| [Block](block.md)             | `?module=block`       |
| [Contract](contract.md)       | `?module=contract`    |
| [Transaction](transaction.md) | `?module=transaction` |

