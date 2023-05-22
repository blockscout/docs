---
description: '?module=token'
---

# Token

### &#x20;`https://instance_base_url/api?module=token`

## Get ERC-20 or ERC-721 token by contract address

`getToken`

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

`getTokenHolders`

Returns an array of token holder's accounts and amounts held for a specified token contract address.

**Example**

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

## Get bridged tokens list

`bridgedTokenList`

Returns an array of bridged token information (uses native bridge application and only returns when applicable - depends on implementation).

**Example**

```
https://instance_base_url/api
   ?module=token
   &action=bridgedTokenList
   &chainid={chainid}
   &page={integer}
   &offset={integer}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter | Description                                                                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| chainID   | nonnegative `integer` that represents the chain id where the original token exists.                                                                                          |
| page      | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the page number used for pagination. 'offset' must also be provided.               |
| offset    | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the max number of records to return when paginating. 'page' must also be provided. |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": [
    {
      "foreignChainId": "1",
      "foreignTokenContractAddressHash": "0x0ae055097c6d159879521c384f1d2123d1f195e6",
      "homeContractAddressHash": "0xb7d311e2eb55f2f68a9440da38e7989210b9a05e",
      "homeDecimals": "18",
      "homeHolderCount": 393,
      "homeName": "STAKE on xDai",
      "homeSymbol": "STAKE",
      "homeTotalSupply": "1484374.775044204093387391",
      "homeUsdValue": "18807028.39981006586321824397"
    },
    {
      "foreignChainId": "1",
      "foreignTokenContractAddressHash": "0xf5581dfefd8fb0e4aec526be659cfab1f8c781da",
      "homeContractAddressHash": "0xd057604a14982fe8d88c5fc25aac3267ea142a08",
      "homeDecimals": "18",
      "homeHolderCount": 73,
      "homeName": "HOPR Token on xDai",
      "homeSymbol": "HOPR",
      "homeTotalSupply": "26600449.86076749062791602",
      "homeUsdValue": "6638727.472651464170990256943"
    }
  ],
  "status": "1"
}
```
{% endtab %}
{% endtabs %}
