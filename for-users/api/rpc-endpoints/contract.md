---
description: '?module=contract'
---

# Contract

{% hint style="info" %}
Page is under construction. For a list of RPC endpoints, visit [https://blockscout.com/eth/mainnet/api-docs](https://blockscout.com/eth/mainnet/api-docs)
{% endhint %}

### &#x20;`https://instance_base_url/api?module=contract`

## Get a list of contracts

List sorted in ascending order based on the time a contact was first indexed by the explorer. With filters \`not\_decompiled\`(\`4\`) or \`not\_verified(4)\` the results will not be sorted for performance reasons.

**Example:**

```
https://instance_base_url/api
   ?module=contract
   &action=listcontracts
```

{% tabs %}
{% tab title="Request Params" %}
| Parameter                      | Description                                                                                                                                                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| page                           | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the page number used for pagination. 'offset' must also be provided.                                                           |
| offset                         | <mark style="background-color:yellow;">optional</mark> nonnegative `integer` representing the max number of records to return when paginating. 'page' must also be provided.                                             |
| filter                         | <mark style="background-color:yellow;">optional</mark>  string `verified`\|`decompiled`\|`unverified`\|`not_decompiled`\|`empty`, or `1`\|`2`\|`3`\|`4`\|`5` respectively. Returns  contracts with the requested status. |
| not\_decompiled\_with\_version | <mark style="background-color:yellow;">optional</mark> `string` ensures none of the returned contracts were decompiled with the provided version. Ignored unless filtering for `decompiled` contracts.                   |
| verified\_at\_start\_timestamp | <mark style="background-color:yellow;">optional</mark>  `unix timestamp` Represents the starting timestamp for verified contracts. Only used with `verified` filter.                                                     |
| verified\_at\_end\_timestamp   | <mark style="background-color:yellow;">optional</mark> `unix timestamp` Represents the ending timestamp for verified contracts. Only used with `verified` filter.                                                        |
{% endtab %}

{% tab title="Example Result" %}
```json
{
  "message": "OK",
  "result": [
    {
      "ABI": "[{\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event\"\n}, {\n\"type\":\"event\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\",\"indexed\":true},{\"name\":\"b\",\"type\":\"bytes32\",\"indexed\":false}],\n\"name\":\"Event2\"\n}, {\n\"type\":\"function\",\n\"inputs\": [{\"name\":\"a\",\"type\":\"uint256\"}],\n\"name\":\"foo\",\n\"outputs\": []\n}]\n",
      "CompilerVersion": "v0.2.1-2016-01-30-91a6b35",
      "ContractName": "Test",
      "OptimizationUsed": "1",
      "SourceCode": "pragma solidity >0.4.24;\n\ncontract Test {\nconstructor() public { b = hex\"12345678901234567890123456789012\"; }\nevent Event(uint indexed a, bytes32 b);\nevent Event2(uint indexed a, bytes32 b);\nfunction foo(uint a) public { emit Event(a, b); }\nbytes32 b;\n}\n"
    }
  ],
  "status": "1"
}
```
{% endtab %}
{% endtabs %}

## Get transaction receipt status

Also available through a GraphQL 'transaction' query.

