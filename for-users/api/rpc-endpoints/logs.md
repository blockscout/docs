# Logs

### &#x20;`https://instance_base_url/api?module=logs`

## Get Event Logs by Address and/or Topic(s)

Event logs for an address and topic. Use **and/or** with the topic operator to specify topic retrieval options when adding multiple topics. Up to a maximum of 1,000 event logs.

**Example:**

```
https://instance_base_url/api
   ?module=logs
   &action=getLogs
   &fromBlock=1379224
   &toBlock=13792288
   &address=0x33990122638b9132ca29c723bdf037f1a891a70c
   &topic0=0xf63780e752c6a54a94fc52715dbc5518a3b4c3c2833d301a204226548a2a8545
   &topic1=0x72657075746174696f6e00000000000000000000000000000000000000000000
   &topic0_1_opr=or
```

_\*=required field_

{% tabs %}
{% tab title="Request Params" %}
| Parameter      | Description                                                                                                                                                                                     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fromBlock\*    | `integer` block number to start searching for logs. `latest` is also supported                                                                                                                  |
| toBlock\*      | <p><code>integer</code> block number to stop searching for logs. <code>latest</code> is also supported.<br><br><em>Note can be same as fromBlock if looking at logs for a single block</em></p> |
| address\*      | `string` 160-bit code used for identifying contracts. An address and/or topic is required.                                                                                                      |
| topic0\*       | `string` for first required topic.                                                                                                                                                              |
| topic1         | `string` for 2nd optional topic.                                                                                                                                                                |
| topic2         | `string` for 3rd optional topic.                                                                                                                                                                |
| topic3         | `string` for 4th optional topic.                                                                                                                                                                |
| topic0\_1\_opr | operator when topic 0 and 1 are used. Either `and` or `or`                                                                                                                                      |
| topic0\_2\_opr | operator for topic 0 and topic 2. Either `and` or `or`                                                                                                                                          |
| topic0\_3\_opr | operator for topic 0 and topic 3. Either `and` or `or`                                                                                                                                          |
| topic1\_2\_opr | operator for topic 1 and topic 2. Either `and` or `or`                                                                                                                                          |
| topic1\_3\_opr | the topic operator for topic 1 and topic 3. Either `and` or `or`                                                                                                                                |
| topic2\_3\_opr | the topic operator for topic 2 and topic 3. Either `and` or `or`                                                                                                                                |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": [
    {
      "address": "0x33990122638b9132ca29c723bdf037f1a891a70c",
      "blockNumber": "0x5c958",
      "data": "0x",
      "gasPrice": "0xba43b7400",
      "gasUsed": "0x10682",
      "logIndex": "0x",
      "timeStamp": "0x561d688c",
      "topics": [
        "0xf63780e752c6a54a94fc52715dbc5518a3b4c3c2833d301a204226548a2a8545",
        "0x72657075746174696f6e00000000000000000000000000000000000000000000",
        "0x000000000000000000000000d9b2f59f3b5c7b3c67047d2f03c3e8052470be92"
      ],
      "transactionHash": "0x0b03498648ae2da924f961dda00dc6bb0a8df15519262b7e012b7d67f4bb7e83",
      "transactionIndex": "0x"
    }
  ],
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

