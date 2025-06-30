# Cosmos-based chains

With the [SHUTTLE proxy server developed by Fair Math](https://github.com/fairmath/shuttle/), Blockscout can be used as an out-of-the-box explorer for Cosmos-based chains. [Visit the open-source Fair Math repo for instructions on running SHUTTLE](https://github.com/fairmath/shuttle/).

SHUTTLE works as a proxy on websocket connection and HTTP requests. Incoming JSON RPC requests are translated to corresponding Cosmos HTTP requests and as a result transmitted in the Ethereum format.

{% hint style="info" %}
The project is currently under development with new features and methods in progress. Community involvement is also encouraged to help build out full compatibility.
{% endhint %}

The following methods are currently supported, meaning core processes like indexing blocks,  transactions, internal transactions, and coin balances are functional.

```
eth_blockNumber
eth_getBalance
eth_getBlockByHash
eth_getBlockByNumber
eth_getTransactionByHash
eth_getTransactionByBlockHashAndIndex
eth_getTransactionByBlockNumberAndIndex
eth_getTransactionReceipt
```

These methods are not yet implemented:

```
eth_call
eth_getCode
eth_getUncleByBlockHashAndIndex
eth_getLogs
```

As a result, the following functionality is limited:

* The explorer doesn't detect smart contracts, meaning all addresses are displayed as EoAs. Smart contract verification and interaction doesn't yet work and tokens and their balances are not detected.&#x20;
* Transaction revert reasons, token metadata, and NFT instance metadata are not yet available.
