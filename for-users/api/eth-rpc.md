# ETH RPC

In addition to the custom [RPC endpoints documented here](rpc-endpoints/), the Blockscout ETH RPC API supports 3 methods in the exact format specified for Ethereum nodes, see the [Ethereum JSON-RPC Specification](https://ethereum.github.io/execution-apis/api-documentation/) for more details.&#x20;

These methods are provided for your convenience. In general, custom RPC methods are recommended.&#x20;

The following 3 methods are supported:

* eth\_blockNumber
* eth\_getBalance
* eth\_getLogs

In the following examples we use the Ethereum mainnet with the base instance url  `https://eth.blockscout.com`. When sending a request add `/api/eth-rpc` to the end of the base url.

## eth\_blockNumber

Returns the latest block number in the chain in hexidecimal format. No params are needed.\
Type: <mark style="background-color:green;">POST</mark>

**Example**

{% code overflow="wrap" %}
```json
// Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_blockNumber","params":[]}' https://eth.blockscout.com/api/eth-rpc
// Response
{
  "jsonrpc": "2.0",
  "result": "0xfa0b0e",
  "id": 0
}
```
{% endcode %}

## eth\_getBalance&#x20;

Returns the balance of a given address in wei. Note the `earliest` parameter does not work as expected because genesis block balances are not currently imported. Parameters are required.

**Required Parameters**

<table><thead><tr><th width="130.5"></th><th></th></tr></thead><tbody><tr><td>Type</td><td><mark style="background-color:green;">POST</mark></td></tr><tr><td>Data (string)</td><td>20 Byte address to check balance</td></tr><tr><td>Quantity or Tag (string)</td><td>Integer value of a block number, or a tag "latest" for the most recent block.</td></tr></tbody></table>

**Example**&#x20;

{% code overflow="wrap" %}
```json
// Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getBalance","params":["0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045","latest"]}' https://eth.blockscout.com/api/eth-rpc
// Response
{
  "jsonrpc": "2.0",
  "result": "0x1d863bf76508104fb", //34039260923474019579
  "id": 0
}

```
{% endcode %}

## eth\_getLogs

Returns an array of logs matching a specified filter object.  Params are optional based on data you want to receive. From more information, see this [post on eth\_getLogs](https://medium.com/alchemy-api/deep-dive-into-eth-getlogs-5faf6a66fd81).

Note: Never returns more than 1000 log entries. You can use pagination options to request the next page. Pagination options params: {"logIndex": "3D", "blockNumber": "6423AC"} which include parameters from the last log received from the previous request. These three parameters are required for pagination.

**Parameters**

<table><thead><tr><th width="181.5"></th><th></th></tr></thead><tbody><tr><td>Type</td><td><mark style="background-color:green;">POST</mark></td></tr><tr><td><code>address</code><br>(string, array)</td><td>20Byte contract address or list of addresses to collect logs from.</td></tr><tr><td><code>fromBlock</code> <br>(Quantity/Tag)</td><td>Integer block number, <code>"latest"</code> (default) for the last mined block  or <code>"pending"</code>, <code>"earliest"</code> for not yet mined transactions.</td></tr><tr><td><code>toBlock</code><br>(Quantity/Tag)</td><td> Integer block number, <code>"latest"</code> (default) for the last mined block  or <code>"pending"</code>, <code>"earliest"</code> for not yet mined transactions.</td></tr><tr><td><code>topics</code> <br>(string, array)</td><td>Array of 32 Byte <code>DATA</code> topics. Topics are order-dependent. Each topic can also be an array of DATA with "or" options</td></tr><tr><td><code>paging_options</code></td><td><code>logIndex</code> and <code>blockNumber</code> explained above.</td></tr></tbody></table>



**Example Query**

{% code overflow="wrap" %}
```json
//Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getLogs","params":[{"address":"0xc78Be425090Dbd437532594D12267C5934Cc6c6f","paging_options":{"logIndex":"3D","blockNumber":"6423AC"},"fromBlock":"earliest","toBlock":"latest","topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef"]}]}' https://eth.blockscout.com/api/eth-rpc
```
{% endcode %}

{% code overflow="wrap" %}
```json
//Response (end)
{"address":"0xc78be425090dbd437532594d12267c5934cc6c6f","blockHash":"0x574755e06bf0cec6d59a8cc7db183d4545a90242d03d5bc3806681277356cf4b","blockNumber":"0x79D4CF","data":"0x000000000000000000000000000000000000000000000c81c6f8fe7064224e6e","logIndex":"0x42","removed":false,"topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef","0x0000000000000000000000000000000000000000000000000000000000000000","0x00000000000000000000000078c04412a6eb2f524ccf50b5f3d863a82e2f8d6f"],"transactionHash":"0xd35fe29c81484258f38b4848a4d44f54f3dc0b9b3d10ad094b8cd5f3a4815e64","transactionIndex":"0x6D","type":"mined"},{"address":"0xc78be425090dbd437532594d12267c5934cc6c6f","blockHash":"0xcb58a082f58bea43dfb6be8addf97c915190175b9f0f0abc1e05bfd02573f010","blockNumber":"0x7BA949","data":"0x000000000000000000000000000000000000000000000c81c6272987dea5867a","logIndex":"0x38","removed":false,"topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef","0x0000000000000000000000000000000000000000000000000000000000000000","0x0000000000000000000000001082e1c4a9c9f946ba102667a14f206c0f81e147"],"transactionHash":"0xd12770e7a1dfa759f6a645981e4bd1d75d2ed131b52565e436bce90b5b39f137","transactionIndex":"0x89","type":"mined"}],"id":0}
```
{% endcode %}
