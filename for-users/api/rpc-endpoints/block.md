---
description: '?module=block'
---

# Block

{% hint style="info" %}
Page is under construction. For a list of RPC endpoints, visit [https://blockscout.com/eth/mainnet/api-docs](https://blockscout.com/eth/mainnet/api-docs)
{% endhint %}

### `https://instance_base_url/api?module=block`

## Get block reward by block number

Returns the block reward and 'uncle' block rewards when applicable.

**Example:**

```
https://api.etherscan.io/api
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

