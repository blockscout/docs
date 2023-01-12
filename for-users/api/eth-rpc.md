# ETH RPC

The Blockscout ETH RPC API supports 3 methods in the exact format specified for Ethereum nodes, see the [Ethereum JSON-RPC Specification](https://ethereum.github.io/execution-apis/api-documentation/) for more details. These methods are provided for your convenience. In general, custom RPC methods are recommended.&#x20;

The following 3 methods are supported:

* eth\_blockNumber
* eth\_getBalance
* eth\_getLogs

In the following examples we use the Ethereum mainnet with the base instance url  `https://blockscout.com/eth/mainnet`. When sending a request add `/api/eth-rpc` to the end of the base url.

## eth\_blockNumber

Returns the latest block number in the chain in hexidecimal format.\
Type: <mark style="background-color:green;">POST</mark>

**Example**

{% code overflow="wrap" %}
```json
// Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_blockNumber","params":[]}' https://blockscout.com/eth/mainnet/api/eth-rpc
// Response
{
  "jsonrpc": "2.0",
  "result": "0xfa0b0e",
  "id": 0
}
```
{% endcode %}

## eth\_getBalance&#x20;

Returns the balance of a given address in wei. Note the `earliest` parameter does not work as expected because genesis block balances are not currently imported.

**Required Parameters**

|                          |                                                                               |
| ------------------------ | ----------------------------------------------------------------------------- |
| Type                     | <mark style="background-color:green;">POST</mark>                             |
| Data (string)            | 20 Byte address to check balance                                              |
| Quantity or Tag (string) | Integer value of a block number, or a tag "latest" for the most recent block. |

**Example**&#x20;

{% code overflow="wrap" %}
```json
// Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getBalance","params":["0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045","latest"]}' https://blockscout.com/eth/mainnet/api/eth-rpc
// Response
{
  "jsonrpc": "2.0",
  "result": "0x1d863bf76508104fb", //34039260923474019579
  "id": 0
}

```
{% endcode %}

## eth\_getLogs

Will never return more than 1000 log entries. For this reason, you can use pagination options to request the next page. Pagination options params: {"logIndex": "3D", "blockNumber": "6423AC"} which include parameters from the last log received from the previous request. These three parameters are required for pagination.

**Example**

{% code overflow="wrap" %}
```json
//Request
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getLogs","params":[{"address":"0xc78Be425090Dbd437532594D12267C5934Cc6c6f","paging_options":{"logIndex":"3D","blockNumber":"6423AC"},"fromBlock":"earliest","toBlock":"latest","topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef"]}]}' https://blockscout.com/eth/mainnet/api/eth-rpc
```
{% endcode %}
