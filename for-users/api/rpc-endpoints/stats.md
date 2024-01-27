---
description: '?module=stats'
---

# Stats

{% hint style="info" %}
Page is under construction. For a full description of RPC endpoints, visit [https://gnosis.blockscout.com/api-docs](https://gnosis.blockscout.com/api-docs)
{% endhint %}

### &#x20; `https://instance_base_url/api?module=stats`

## Get [ERC-20](https://github.com/ethereum/EIPs/issues/20) or [ERC-721](https://github.com/ethereum/EIPs/issues/721) token total supply by contract address

`tokensupply`

**Example**

```
https://instance_base_url/api
   ?module=stats
   &action=tokensupply
   &contractaddress={contractAddressHash}
```

{% tabs %}
{% tab title="Request Param" %}
| Parameter       | Description                                                                                    |
| --------------- | ---------------------------------------------------------------------------------------------- |
| contractaddress | `string` containing the contract address hash - a 160-bit code used for identifying contracts. |
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

## Get total supply in Wei from exchange

`ethsupplyexchange`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

## Get total supply in Wei from DB

`ethsupply`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

## Get total coin supply from DB minus burnt number

`coinsupply`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

## Get latest price of native coin in USD and BTC

`ethprice`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

## Get latest price of native coin in USD and BTC in more general format

`coinprice`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

## Get total transaction fees in Wei paid by users to validators per day

`totalfees`

**Example:**

```
// Some code
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |  Description |
| --------- | ------------ |
| param     | description  |
{% endtab %}

{% tab title="Example Result" %}
```
// Some code
```
{% endtab %}
{% endtabs %}

##
