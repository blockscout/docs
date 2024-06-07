---
description: API designed for ease of use
---

# RPC API Endpoints

This API is provided for developers transitioning applications from Etherscan to BlockScout and applications requiring general API and data support. It supports GET and POST requests.&#x20;

{% hint style="info" %}
URLs vary by instance. With typical installations, access the API by adding `/api` to the end of the url. For example with the Goerli instance.

* URL: [https://eth-goerli.blockscout.com](https://eth-goerli.blockscout.com/)
* API URL: [https://eth-goerli.blockscout.com/api](https://eth-goerli.blockscout.com/api)

An example query includes a module and action(s)/parameters. For example: \
[https://eth-goerli.blockscout.com/api?module=**account**\&action=**listaccounts**\&page=2\&offset=5](https://eth-goerli.blockscout.com/api?module=account\&action=listaccounts\&page=2\&offset=5)
{% endhint %}

The following modules are supported. Click through to see specific endpoints and parameters.

<table data-header-hidden><thead><tr><th width="158"></th><th></th></tr></thead><tbody><tr><td><a href="account.md">Account</a></td><td><code>?module=account</code></td></tr><tr><td><a href="logs.md">Logs</a></td><td><code>?module=logs</code></td></tr><tr><td><a href="token.md">Token</a></td><td><code>?module=token</code></td></tr><tr><td><a href="stats.md">Stats</a></td><td><code>?module=stats</code></td></tr><tr><td><a href="block.md">Block</a></td><td><code>?module=block</code></td></tr><tr><td><a href="contract.md">Contract</a></td><td><code>?module=contract</code></td></tr><tr><td><a href="transaction.md">Transaction</a></td><td><code>?module=transaction</code></td></tr></tbody></table>

