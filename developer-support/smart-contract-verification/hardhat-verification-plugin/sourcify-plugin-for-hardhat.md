# Sourcify Plugin for Hardhat

Similar to the  [hardhat verification plugin, ](./)this plugin submits the contract source and other info of all deployed contracts to Sourcify.

### Verify

Similar to the verification approach described in the [hardhat verification plugin,](./) you can verify the contract source code in the Sourcify as well by setting the following in the hardhat config file:

```typescript
// ...
const config: HardhatUserConfig = {
  // ...
  sourcify: {
    enabled: true
  },
  // ...
};

export default config;
```

```
npx hardhat verify --network <network> DEPLOYED_CONTRACT_ADDRESS "Constructor argument 1"
```

Optimism Sepolia example:

```
> npx hardhat verify --network optimism-sepolia 0xCD562a6426b474390A9E7e554b9B4f9f62Ea38Ba 1234
Successfully submitted source code for contract
contracts/Lock.sol:Lock at 0xCD562a6426b474390A9E7e554b9B4f9f62Ea38Ba
for verification on the block explorer. Waiting for verification result...

Successfully verified contract Lock on the block explorer.
https://optimism-sepolia.blockscout.com/address/0xCD562a6426b474390A9E7e554b9B4f9f62Ea38Ba#code

Successfully verified contract Lock on Sourcify.
https://repo.sourcify.dev/contracts/full_match/11155420/0xCD562a6426b474390A9E7e554b9B4f9f62Ea38Ba/
```

## Confirm Verification on BlockScout

Go to your BlockScout instance and paste the contract address into the search bar.

<figure><img src="../../../.gitbook/assets/paste-contract-address-1.png" alt=""><figcaption></figcaption></figure>

Scroll down to see verified status. A green checkmark ✅ means the contract is verified.

<figure><img src="../../../.gitbook/assets/verify-contract-2.png" alt=""><figcaption></figcaption></figure>

If your screen size is limited, you may need to click the 3 dots to view and click through to the contract.

<figure><img src="../../../.gitbook/assets/verify-contract-3.png" alt=""><figcaption></figcaption></figure>

Scroll down to see and interact with the contract code.

<figure><img src="../../../.gitbook/assets/verify-contracts-4.png" alt=""><figcaption></figcaption></figure>

