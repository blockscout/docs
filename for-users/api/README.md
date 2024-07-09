# API

## Blockscout Internal Documentation

To view Modules and API Reference documentation:

1.  Generate documentation.

    `mix docs`
2.  View the generated docs.

    `open doc/index.html`

## Blockscout API Usage

API calls can be accessed from the Blockscout main menu, footer or header depending on the instance.

Blockscout supports several methods:

1. **REST API**: API that serves the UI for **new instances** of Blockscout.   -> [More info](rest-api-endpoints.md)
2. **RPC API**: provided for developers transitioning their applications from Etherscan to Blockscout. Supports GET and POST requests.\
   \-> [More info](rpc-endpoints/)
3. **Eth RPC API**: Supports the most popular [JSON RPC methods](https://ethereum.github.io/execution-apis/api-documentation/). \
   \-> [More info](eth-rpc.md)
4. [**Graphiql**](https://github.com/graphql/graphiql): An IDE for exploring GraphQL.

<figure><img src="../../.gitbook/assets/API-menu.png" alt=""><figcaption><p>API access in new instance</p></figcaption></figure>

![APIs in header menu of old UI](../../.gitbook/assets/header.png)

![API links in the footer](../../.gitbook/assets/APIs.png)

## GraphQL

Send Queries to quickly get information. Use the **Docs button** to quickly find arguments accepted by the schema. More information is available in our [Blockscout GraphQL tutorial](https://forum.poa.network/t/graphql-in-blockscout/1971).

![Docs button for GraphQL](<../../.gitbook/assets/Screen Shot 2019-10-08 at 10.48.07 AM.png>)

## ETH RPC

Blockscout supports the following methods. Requests and return data are identical to the [Ethereum documentation](https://eth.wiki/json-rpc/API).

* eth\_blockNumber
* eth\_getBalance
* eth\_getLogs
* eth\_gasPrice
* eth\_getTransactionByHash
* eth\_getTransactionReceipt
* eth\_chainId
* eth\_maxPriorityFeePerGas
* eth\_getTransactionCount
* eth\_getCode
* eth\_getStorageAt
* eth\_estimateGas
* eth\_getBlockByNumber
* eth\_getBlockByHash
* eth\_sendRawTransaction
* eth\_call

More details on [ETH RPC for Blockscout](eth-rpc.md) are available here.

## API Keys

If My Account is enabled, users can add up to 3 API keys to ensure 10 request/second limits. When API Keys are not used, the global default is 50 requests/second.

* More info on [My Account and adding API Keys](../my-account/api-keys.md)
* More info on [API Requests and Limits](requests-and-limits.md)
