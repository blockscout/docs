---
description: '?module=transaction'
---

# Transaction

### &#x20;`https://instance_base_url/api?module=transaction`

## Get transaction info

`gettxinfo`

Information related to a specified transaction. Includes:

* blockNumber
* confirmations
* from
* gasLimit (in wei)
* gasPrice (in wei)
* gasUsed
* hash
* input
* logs (array)
* revert reason
* success
* timeStamp
* to
* value (in wei)&#x20;

**Example**

```
https://instance_base_url/api
   ?module=transaction
   &action=gettxinfo
   &txhash={transactionHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter | Description                                                                                                                      |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| txhash    | `string` containing the transaction hash                                                                                         |
| index     | <mark style="background-color:yellow;">optional</mark>  nonnegative `integer` that represents the log index used for pagination. |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "result": {
    "revertReason": "No credit of that type",
    "blockNumber": "3",
    "confirmations": "0",
    "from": "0x000000000000000000000000000000000000000c",
    "gasLimit": "91966",
    "gasPrice": "100000",
    "gasUsed": "95123",
    "hash": "0x0000000000000000000000000000000000000000000000000000000000000004",
    "input": "0x04",
    "logs": [
      {
        "address": "0x000000000000000000000000000000000000000e",
        "data": "0x00",
        "topics": [
          "First Topic",
          "Second Topic",
          "Third Topic",
          "Fourth Topic"
        ]
      }
    ],
    "success": true,
    "timeStamp": "1541018182",
    "to": "0x000000000000000000000000000000000000000d",
    "value": "67612"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get transaction receipt status

`gettxreceiptstatus`&#x20;

Also available through a GraphQL 'transaction' query. `Status` field return:

* `0` = failed transaction
* `1` = successful transaction

**Example**

```
https://instance_base_url/api
   ?module=transaction
   &action=gettxreceiptstatus
   &txhash={transactionHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter | Description                              |
| --------- | ---------------------------------------- |
| txhash    | `string` containing the transaction hash |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": {
    "status": "1"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get error status and message

`getstatus`&#x20;

Also available through a GraphQL 'transaction' query. Includes the following:

* errDescription: string with error message
* isError
  * 0 = pass, no error
  * 1 = error

**Example**

```
https://instance_base_url/api
   ?module=transaction
   &action=getstatus
   &txhash={transactionHash}
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter | Description                              |
| --------- | ---------------------------------------- |
| txhash    | `string` containing the transaction hash |
{% endtab %}

{% tab title="Example Result" %}
```
{
  "message": "OK",
  "result": {
    "errDescription": "Out of gas",
    "isError": "1"
  },
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

\
