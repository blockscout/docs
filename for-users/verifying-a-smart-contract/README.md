---
description: Verifying your deployed contract
---

# Verifying a Smart Contract

Once verified, a smart contract or token contract's source code becomes publicly available and verifiable, creating transparency and trust.&#x20;

Verification is available for both Solidity and Vyper contracts. Currently, there are 7 methods for verification using the Blockscout UI.

{% hint style="success" %}
To learn more about the smart contract verification Rust microservice and verification algorithm [see this page for developers](../../for-developers/information-and-settings/smart-contract-verification.md).
{% endhint %}

{% hint style="info" %}
👷🏻‍♂️ If preferred you can verify directly from your Hardhat dev environment.&#x20;

* [Hardhat Verification Plugin](hardhat-verification-plugin.md)
* [Sourcify Plugin for Hardhat](sourcify-plugin-for-hardhat.md)
{% endhint %}

## Smart Contract Verification with Blockscout

1\) Go to the Verify contract page _(Other -> Verify contract)_

<figure><img src="../../.gitbook/assets/sourcify-blockscout-1.png" alt=""><figcaption></figcaption></figure>

2\) Enter in the contract address you received during deployment. The dropdown will show you several available verification options. Select the one you would like to use and continue.

<figure><img src="../../.gitbook/assets/verify-and-publish-2.png" alt=""><figcaption></figcaption></figure>

* Solidity ([Flattened source code)](./#via-flattened-source-code)
* Solidity ([Standard JSON input](./#via-standard-json-input))
* Solidity ([Sourcify](contracts-verification-via-sourcify.md))
* Solidity (Multi-part files)
* [Vyper (Contract](./#vyper-contract))
* Vyper (Multi-part files)
* Vyper (Standard JSON input)

## Solidity (Flattened source code)

<figure><img src="../../.gitbook/assets/flattened-source-code.png" alt=""><figcaption></figcaption></figure>

1. **Contract Address:** The `0x` address supplied on contract creation (added above)
2. **Is Yul contract:** Select if the contract is coded in Yul for efficiency.
3. **Include Nightly Builds**: Select if you want to show nightly builds.
4. **Compiler:** derived from the first line in the contract `pragma solidity X.X.X`. Use the corresponding compiler version rather than the nightly build.
5. **EVM Version:** Select the correct[ EVM version ](../../for-developers/evm-version-information.md)if known, otherwise use default.
6. **Optimization Enabled:** If you enabled optimization during compilation, select and enter the run value. 200 is the Solidity Compiler default value. Only change if you changed this value while compiling.
7. &#x20;**Enter the Solidity Contract Code:** You may need to flatten your solidity code if it utilizes a library or inherits dependencies from another contract. We recommend [hardhat ](https://hardhat.org/hardhat-runner/docs/advanced/flattening)or the [POA solidity flattener](https://github.com/poanetwork/solidity-flattener).
8. **Add Contract Libraries:** Enter the name and 0x address for any required libraries called in the .sol file. You can add multiple contracts with the "+" button.
9. Click the `Verify and Publish` button.
10. If all goes well, you will see a checkmark :white\_check\_mark: next to Code in the code tab, and an additional tab called `Read Contract`. The contract name will now appear in BlockScout with any transactions related to your contract.

## Solidity (Standard JSON input)

{% hint style="warning" %}
Instructions for the new Blockscout UI are in process. The steps are similar, but these instructions currently use the old UI.
{% endhint %}

![](../../.gitbook/assets/standard-json.png)

1. **Contract Name**. There are several options:
   1. Leave blank.
   2. Enter contract name: `MyContract`.
   3. Enter path to the contract and it's name: `path/to/file.sol:MyContract` (path should match what is written in your JSON file).
2. **Include nightly builds**. You can choose **Yes** or **No** depending on your compiler.
3. **Compiler.** Choose the compiler version used to compile your smart contract.
4. **Standard Input JSON.** Attach your Standard Input JSON file. File should follows solidity [format](https://docs.soliditylang.org/en/latest/using-the-compiler.html#input-description) and all the sources must be in Liternal Content format, not an URL.
5. **Try to fetch constructor arguments automatically.** Select No if you want to provide ABI-encoded Constructor Arguments or the contract does not have any.
6. **ABI-encoded Constructor Arguments.** Fill it with ABI-encoded Constructor Arguments or leave blank.

After filling the form click the **Verify & publish** button and wait for the response.

## Via Sourcify: Sources and metadata JSON file

See the [Contract Verification via Sourcify](contracts-verification-via-sourcify.md) page for details.

## Vyper Contract

{% hint style="warning" %}
Instructions for the new Blockscout UI are in process. The steps are similar, but these instructions currently use the old UI.
{% endhint %}

![](../../.gitbook/assets/vyper.png)

1. **Contract Address:** The `0x` address supplied on contract creation. Should autopopulate
2. **Contract Name:** Should autopopulate
3. **Compiler**: Select the compiler version used in the source code.
4. **Enter the Vyper Contract Code:** Copy and paste the contract code
5. **ABI-encoded Constructor Arguments (if required):**  [See this page for more info](../abi-encoded-constructor-arguments.md).
6. Click the `Verify and Publish` button.
7. If all goes well, you will see a checkmark :white\_check\_mark: next to Code in the code tab, and an additional tab called `Read Contract`. The contract name will now appear in BlockScout with any transactions related to your contract.

## Troubleshooting

If you receive the dreaded `There was an error compiling your contract` message this means the bytecode doesn't match the supplied sourcecode. Unfortunately, there are many reasons this may be the case. Here are a few things to try:

1\) Double check the compiler version is correct.

{% hint style="info" %}
Check all version digits - for example 0.5.1 is different from 0.5.10
{% endhint %}

2\) Check that an extra space has not been added to the end of the contract. When pasting in, an extra space may be added. Delete this and attempt to recompile.

3\) Copy, paste and verify your source code in Remix. You may find some exceptions here.

### Verification in a dev environment

The [Hardhat verification plugin](hardhat-verification-plugin.md) supports BlockScout. You can also choose to use the [Sourcify plugin](sourcify-plugin-for-hardhat.md) to verify with Sourcify from your hardhat environment.
