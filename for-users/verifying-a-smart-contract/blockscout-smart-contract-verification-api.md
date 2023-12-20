---
description: Blockscout also offers a contract verification API.
---

# Blockscout smart-contract verification API

Use the appropriate Blockscout instance endpoint to verify if the smart contract microservice is enabled.&#x20;

In the following examples we use https://eth.blockscout.com to query Ethereum.

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/verification/config" method="get" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

{% hint style="warning" %}
`0x` contract addresses in POST example urls below should be replaced with your contract hash supplied on contract creation. Variables in the body are examples and should be replaced with your contract details.
{% endhint %}

## Flattened contract

For more information on parameters to pass, see the [flattened source code information on the Verifying a smart contract page](./#via-flattened-source-code).&#x20;

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0xb12cad649a56e67188bbaa56583c18dc7d2812ed/verification/via/flattened-code" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Via Standard JSON input

For more information on parameters to pass, see the [flattened source code information on the Verifying a smart contract page](./#via-flattened-source-code). `0x` contract in POST example should be replaced with your contract hash.

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0x9c1c619176b4f8521a0ab166945d785b92aef453/verification/via/standard-input" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Via Sourcify Files

For more information on parameters to pass, see the [Contract Verification via Sourcify](contracts-verification-via-sourcify.md). `0x` contract in POST example url should be replaced with your contract hash, as should your relevant variables.

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0x030f7c7dbd472864220bcf9e37ede1b8a3125970/verification/via/sourcify" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Multi-part Solidity files

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0x030f7c7dbd472864220bcf9e37ede1b8a3125970/verification/via/multi-part" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Vyper Contracts

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0xd73249995040f04cb891bdf0f997579ee3a6676c/verification/via/vyper-code" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Vyper Multi-part files

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0xc3fd3c09d5481f4d6c85e70775804de4c93fe630/verification/via/vyper-multi-part" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}

## Vyper Standard JSON input

{% swagger src="../../.gitbook/assets/openapi (2).json" path="/api/v2/smart-contracts/0xc3fd3c09d5481f4d6c85e70775804de4c93fe630/verification/via/vyper-standard-input" method="post" %}
[openapi (2).json](<../../.gitbook/assets/openapi (2).json>)
{% endswagger %}





