---
Title: Verifying Contracts via Remix
description: Learn how to verify smart contracts using the Remix IDE and Blockscout Plugin.
---

# 🔍 Verifying Smart Contracts Using Remix IDE with Blockscout

Blockscout provides a **Remix plugin** that allows developers to verify their smart contracts directly from the [Remix IDE](https://remix.ethereum.org ), streamlining the verification process without leaving your development environment.

This guide explains how to use the **Blockscout Remix Plugin** to verify your contract on EVM-compatible chains like Polygon, Optimism, Gnosis Chain, etc.

---

## ✅ Prerequisites

Before verifying your smart contract:

1. Your contract must already be **deployed on-chain**.
2. You should have:
   - The **contract address**
   - The **source code**
   - Compiler version and optimization settings used during deployment
3. Make sure the network you deployed to uses **Blockscout** as its explorer.

---

## 🛠️ Step-by-Step Verification Guide

### 1. Open Remix IDE
Go to: [https://remix.ethereum.org ](https://remix.ethereum.org )  
Open the **Solidity file** of the contract you want to verify.

### 2. Go to the "Plugins" Section
On the left sidebar, click the **Plugins icon** (a puzzle piece).

### 3. Activate the Blockscout Plugin
- In the plugins manager:
  - Search for **"Blockscout"**
  - Click **"Activate"**

> If the plugin doesn't appear, ensure it's installed or check the official repository: [Blockscout Remix Plugin](https://github.com/blockscout/blockscout-remix-plugin )

### 4. Launch the Blockscout Plugin
Once activated, find the plugin under the **"Deploy & Run Transactions"** section or re-launch the plugin panel.

Click on the **Blockscout Plugin** to open it.

### 5. Enter Contract Information
You'll typically need to enter:
- **Contract Address**: Address where the contract was deployed
- **Network**: Select the chain from a dropdown (e.g., Gnosis Chain, Polygon zkEVM)
- **API Endpoint** *(if applicable)*: Some networks may require an Etherscan-like API key or endpoint

### 6. Compile and Submit for Verification
- Remix will compile your contract using the same settings used during deployment.
- It will generate metadata for verification.
- Click **"Verify on Blockscout"**.
- Confirm details and submit.

### 7. Check Verification Status
After submission:
- Wait for confirmation from the explorer.
- Visit the **Blockscout explorer** for your network.
- Navigate to your contract address and confirm the source code is now verified.

---

## 🛑 Troubleshooting Tips

| Issue | Solution |
|------|----------|
| `Compiler version mismatch` | Ensure the Solidity version in Remix matches exactly the one used for deployment |
| `Metadata hash mismatch` | Make sure constructor arguments are correctly encoded |
| `Plugin not found` | Search GitHub for `blockscout remix plugin` and install manually |
| `Contract not verified` | Double-check optimization runs, constructor args, and source code |

---

## 📚 Additional Resources

- [Blockscout Remix Plugin GitHub](https://github.com/blockscout/blockscout-remix-plugin )
- [Remix Plugin Documentation](https://remix-ide.readthedocs.io/en/latest/ )
- [Blockscout Explorer](https://blockscout.com )
