---
description: '?module=stats'
---

# Stats

{% hint style="info" %}
Page is under construction. For a list of RPC endpoints, visit [https://blockscout.com/eth/mainnet/api-docs](https://blockscout.com/eth/mainnet/api-docs)
{% endhint %}

### &#x20; `https://instance_base_url/api?module=stats`

## Get [ERC-20](https://github.com/ethereum/EIPs/issues/20) or [ERC-721](https://github.com/ethereum/EIPs/issues/721) token total supply by contract address

**Example**

```
https://instance_base_url/api
   ?module=stats
   &action=tokensupply
   &contractaddress={contractAddressHash}
```

{% tabs %}
{% tab title="Request Param" %}
| Parameter       | Description                                                                           |
| --------------- | ------------------------------------------------------------------------------------- |
| contractaddress | `string` containing the address hash - A 160-bit code used for identifying contracts. |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": "21265524714464",
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

##
