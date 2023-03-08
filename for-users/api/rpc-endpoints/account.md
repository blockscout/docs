# Account

{% hint style="info" %}
Page is under construction. For a list of RPC endpoints, visit [https://blockscout.com/eth/mainnet/api-docs](https://blockscout.com/eth/mainnet/api-docs)
{% endhint %}

### &#x20;`?module=account`

## Get the native token balance for an address

Many chains use their own native tokens. On Ethereum, this will return the result in "Ether", on Gnosis it will be "xDai", etc. Results are returned in wei.

Example:

```
https://instance_base_url/api
   ?module=account
   &action=balance
   &address=0x...abcd
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter |                                       |
| --------- | ------------------------------------- |
| address   | `string` containing the address hash. |
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
