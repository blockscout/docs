# API

## BlockScout Internal Documentation

To view Modules and API Reference documentation:

1. Generate documentation.

   `mix docs`

2. View the generated docs.

   `open doc/index.html`

## BlockScout API Usage

Api calls can be accessed from the BlockScout footer \(or top menu depending on the BlockScout instance\). BlockScout supports several methods:

1. [Graphiql](https://github.com/graphql/graphiql): An IDE for exploring GraphQL
2. RPC: API provided for developers transitioning their applications from Etherscan to BlockScout. Supports GET and POST requests.
3. Eth RPC: Supports the most popular [JSON RPC methods](https://github.com/ethereum/wiki/wiki/JSON-RPC).

## GraphQL

Send Queries to quickly get information. Use the **Docs button** to quickly find arguments accepted by the schema. More information is available in our [BlockScout GraphQL tutorial](https://forum.poa.network/t/graphql-in-blockscout/1971).

![Docs button for GraphQL](../../.gitbook/assets/screen-shot-2019-10-08-at-10.48.07-am.png)

## ETH RPC

We support the following methods. Requests and return data are identical to the documentation.

* [eth\_getBalance](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_getbalance)
* [eth\_getLogs](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_getlogs)
* [eth\_blockNumber](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_blocknumber)



