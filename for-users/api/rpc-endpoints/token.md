---
description: '?module=token'
---

# Token

### &#x20;`https://instance_base_url/api?module=token`

## Get ERC-20 or ERC-721 token by contract address

Info on name, symbol, supply and type for a token contract address.

**Example**

```
https://instance_base_url/api
   ?module=token
   &action=getToken
   &contractaddress={contractaddressHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter       | Description                                                                                    |
| --------------- | ---------------------------------------------------------------------------------------------- |
| contractaddress | `string` containing the contract address hash - a 160-bit code used for identifying contracts. |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": {
    "cataloged": true,
    "contractAddress": "0x0000000000000000000000000000000000000000",
    "decimals": "18",
    "name": "Example Token",
    "symbol": "ET",
    "totalSupply": "1000000000",
    "type": "ERC-20"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get token holders by contract address

Returns an array of token holder's accounts and amounts held for a specified token contract address.

Example

```
https://instance_base_url/api
   ?module=token
   &action=getTokenHolders
   &contractaddress={contractaddressHash}
   &page={integer}
   &offset={integer}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter       | Description                                                                                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contractaddress | `string`  containing the contract address hash of the ERC-20/ERC-721 token                                                                                                   |
| page            | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the page number used for pagination. 'offset' must also be provided.               |
| offset          | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the max number of records to return when paginating. 'page' must also be provided. |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": [
    {
      "address": "0x3887e82dbdbe8ec6db44e6298a2d48af572a3b78",
      "value": "153737849289497644937838"
    },
    {
      "address": "0xc894c5de34cb2a3615c737d1276876e44e9700a3",
      "value": "77247336418828547887499"
    }
  ],
  "status": "1"
}
```
{% endtab %}
{% endtabs %}
