---
description: '?module=token'
---

# Token

### &#x20;`https://instance_base_url/api?module=token`

{% swagger method="get" path=" " baseUrl=" &action=getToken" summary="Get ERC-20 or ERC-721 token by contract address" %}
{% swagger-description %}
Info on name, symbol, supply and type for a token contract address.

Example

`https://instance_base_url/api?module=token&action=getToken&contractaddress=0xabcd...abcd`
{% endswagger-description %}

{% swagger-parameter in="query" name="contractaddress" type="160-bit code" required="true" %}
Contract address hash of the ERC-20/ERC-721 token
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="successful operation" %}
{% tabs %}
{% tab title="Response Model" %}
| Output             | Type                                              | Example                                      |
| ------------------ | ------------------------------------------------- | -------------------------------------------- |
| message            | string                                            | ok                                           |
| result             | token object                                      | \<see following>                             |
|    catalogued      | boolean                                           | "true"                                       |
|    contractAddress | address hash                                      | "0x95426f2bc716022fcf1def006dbc4bb81f5b5164" |
|    decimals        | integer (# of decimals token can be divided into) | "18"                                         |
|    name            | string                                            | "Some Token Name"                            |
|    symbol          | string (trading symbol)                           | "STN"                                        |
|    totalSupply     | integer                                           | "1000000000"                                 |
|    type            | enum                                              | <p>"ERC-20"<br>"ERC-721"</p>                 |
| status             | enum (0,1)                                        | <p>0 = error<br>1 = ok</p>                   |
{% endtab %}

{% tab title="Example Response" %}
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
{% endswagger-response %}

{% swagger-response status="200: OK" description="error" %}
```javascript
{
  "message": "Invalid contract address hash",
  "result": null,
  "status": "0"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path=" " baseUrl=" &action=getTokenHolders" summary="Get token holders by contract address" %}
{% swagger-description %}
Return token holder's accounts and amounts held for a specified token contract address.

**Example**

`https://instance_base_url/api?module=token&action=getTokenHolders&contractaddress=0x...abcd&page=2&offset=2`
{% endswagger-description %}

{% swagger-parameter in="query" name="contractaddress" type="160-bit code" required="true" %}
Contract address hash of the ERC-20/ERC-721 token
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" type="Integer" %}
Nonnegative integer representing the page number used for pagination. 'offset' must also be provided.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="offset" type="Integer" %}
Nonnegative integer representing the max number of records to return when paginating. 'page' must also be provided.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="successful operation" %}
{% tabs %}
{% tab title="Response Model" %}
| Output                        | Type             | Example                                      |
| ----------------------------- | ---------------- | -------------------------------------------- |
| message                       | string           | "OK"                                         |
| result                        | array            | <p>Token Holder Detail array</p><p></p>      |
|    address (holder's address) | address hash     | "0x95426f2bc716022fcf1def006dbc4bb81f5b5164" |
|    value (token value held)   | integer (in wei) | "1000000000000000000"                        |
| status                        | enum (0,1)       | <p>0 = error<br>1 = ok</p>                   |
{% endtab %}

{% tab title="Example Response" %}
```
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
{% endswagger-response %}

{% swagger-response status="200: OK" description="error" %}
```javascript
{
  "message": "Invalid contract address format",
  "result": null,
  "status": "0"
}
```
{% endswagger-response %}
{% endswagger %}
