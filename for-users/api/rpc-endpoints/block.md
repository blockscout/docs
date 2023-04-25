---
description: '?module=block'
---

# Block

### `https://instance_base_url/api?module=block`

## Get block reward by block number

`getblockreward`

Returns the block reward and 'uncle' block rewards when applicable.

**Example:**

```
https://instance_base_url/api
   ?module=block
   &action=getblockreward
   &blockno={blockNumber}
```

{% tabs %}
{% tab title="Request Param" %}
| Parameter | Description                                                     |
| --------- | --------------------------------------------------------------- |
| blockno   | `integer` block number to check block rewards for eg. `2165403` |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": {
    "blockMiner": "0x13a06d3dfe21e0db5c016c03ea7d2509f7f8d1e3",
    "blockNumber": "2165403",
    "blockReward": "5314181600000000000",
    "timeStamp": "1472533979",
    "uncleInclusionReward": null,
    "uncles": null
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get block number by time stamp

`getblocknobytime`

Returns the block number created closest to a provided timestamp.

**Example:**

```
https://instance_base_url/api
   ?module=block
   &action=getblocknobytime
   &timestamp={blockTimestamp}
   &closest={before/after}
```

{% tabs %}
{% tab title="Request Param" %}


| Parameter | Description                                                          |
| --------- | -------------------------------------------------------------------- |
| timestamp | `integer` representing the Unix timestamp in seconds.                |
| closest   | closest block to the provided timestamp, either `before` or `after`. |

Note: [How to convert date/time to a Unix timestamp](https://www.unixtimestamp.com/).
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": {
    "blockNumber": "2165403"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get the latest block number

`eth_block_number`

Mimics Ethereum JSON RPC's eth\_blockNumber.

**Example:**

```
https://instance_base_url/api
   ?module=block
   &action=eth_block_number
```

{% tabs %}
{% tab title="Request Param" %}
| Parameter | Description                                                                                                          |
| --------- | -------------------------------------------------------------------------------------------------------------------- |
| id        | <mark style="background-color:yellow;">optional</mark> nonnegative integer that represents the json rpc request id.  |

More on [json rpc request id](https://www.jsonrpc.org/specification).
{% endtab %}

{% tab title="Example Result" %}
```
{
  "jsonrpc": "2.0",
  "result": "0x103538a",
  "id": 1
}
```
{% endtab %}
{% endtabs %}
