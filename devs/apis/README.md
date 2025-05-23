# Blockscout APIs

## Blockscout API Usage

API information can be accessed from the Blockscout main menu, footer or header depending on the instance.

Blockscout supports several methods:

1. [**REST API**](rest/): API that serves the UI for Blockscout.
2. [**RPC API**](rpc/): provided for developers transitioning applications from Etherscan to Blockscout. Supports GET and POST requests, simply replace Etherscan url with Blockscout url to use the RPC.
3. [**Eth RPC API**](rpc/eth-rpc.md): Supports the most popular [JSON RPC methods](https://ethereum.github.io/execution-apis/api-documentation/).
4. [**Graphiql**](https://github.com/graphql/graphiql): An IDE for exploring GraphQL.

<figure><img src="../../.gitbook/assets/API-menu.png" alt=""><figcaption><p>API access in new instance</p></figcaption></figure>

## API Keys

API Keys are not needed by default. Blockscout instances have a standard global request setting of 10/requests per second. However, My Account users can add up to 3 API keys to ensure 10 request/second limits per account.

* More info on [My Account and adding API Keys](../../using-blockscout/my-account/api-keys.md)
* More info on [API Requests and Limits](requests-and-limits.md)

## Blockscout Internal Documentation

To view Modules and API Reference documentation:

1.  Generate documentation.

    `mix docs`
2.  View the generated docs.

    `open doc/index.html`

