---
description: '?module=account'
---

# Account

{% hint style="info" %}
Page is under construction. For a full description of RPC endpoints, visit [https://blockscout.com/xdai/mainnet/api-docs](https://blockscout.com/xdai/mainnet/api-docs)
{% endhint %}

### `https://instance_base_url/api?module=account`

## Return balance from a provided block

`eth_get_balance`

Mimics Ethereum JSON RPC's eth\_getBalance

**Example:**

```
https://instance_base_url/api
   ?module=account
   &action=eth_get_balance
   &address={addressHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter   |  Description                                                                                                                                                                                                                                                                                                                                                            |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **address** | `string` containing the address hash.                                                                                                                                                                                                                                                                                                                                   |
| **block**   | <p><mark style="background-color:yellow;">optional</mark>. Block number as a string, or <code>latest</code>, <code>earliest</code> or <code>pending</code> <br><br>Latest is the latest balance in a <em>consensus</em> block. Earliest is the first recorded balance for the address. Pending is the latest balance in a consensus <em>or</em> nonconsensus block.</p> |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x0234c8a3397aab58"
}
```
{% endtab %}
{% endtabs %}

## Get the native token balance for an address

`balance`

Many chains use their own native tokens. On Ethereum, this will return the result in "Ether", on Gnosis it will be "xDai", etc. Results are returned in wei.

**Example:**

```
https://instance_base_url/api
   ?module=account
   &action=balance
   &address={addressHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter   |  Description                          |
| ----------- | ------------------------------------- |
| **address** | `string` containing the address hash. |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": "663046792267785498951364",
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Also available through a GraphQL `address` query.
{% endhint %}

{% hint style="info" %}
If the balance hasn't been updated recently, the node is double-checked to fetch the absolute latest balance. This will not be reflected in the current request, but once it is updated, subsequent requests will show the updated balance. If you want to know if there is a check for another balance, use the `balancemult`i action. That contains a property called `stale` that will let you know to recheck that balance in the near future.
{% endhint %}

## Get balance for multiple addresses

`balancemulti`

## Get pending transactions by address

`pendingtxlist`

## Get transactions by address

`txlist`

## Get internal transactions by transaction or address hash

`txlistinternal`

## Get token transfer events by address

`tokentx`

## Get token account balance for token contract address

`tokenbalance`

## Get list of tokens owned by address

`tokenlist`

## Get list of blocks mined by address

`getminedblocks`

## Get a list of accounts and their balances

`listaccounts`
