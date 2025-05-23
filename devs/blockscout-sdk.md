# Blockscout SDK

{% hint style="info" %}
Attention EthGlobal Hackathon Participants. \
\
We have a $3000 Bounty available for best SDK Usage (1 $2000 prize and 1 $1000 prize).  Add the Blockscout SDK into your app to provide interactivity and instant explorer feedback to your users.



Note: The Blockscout SDK is currently in beta release. Please report any issues on the [Blockscout Discord](https://discord.gg/blockscout).
{% endhint %}

## Overview

The Blockscout App SDK is a React toolkit designed to integrate Blockscout transaction notifications and transaction history into your decentralized applications (dApps). It provides an easy-to-use interface for displaying transaction status updates and viewing transaction history with real-time updates and mobile-responsive design.

{% hint style="success" %}
* Repo: [https://github.com/blockscout/app-sdk](https://github.com/blockscout/app-sdk)
* NPM Package [https://www.npmjs.com/package/@blockscout/app-sdk ](https://www.npmjs.com/package/@blockscout/app-sdk)
{% endhint %}

### Key Features

* **Transaction Toast Notifications** - Real-time transaction status updates with pending, success, and error states
* **Transaction History Popup** - View recent transactions for specific addresses or entire chains
* **Transaction Interpretation** - Detailed transaction summaries and interpretations
* **Multi-chain Support** - Compatible with any blockchain that has a Blockscout explorer instance
* **Mobile-responsive Design** - Optimized for both desktop and mobile experiences

### Installation

Install the SDK using npm or yarn:

```bash
npm install @blockscout/app-sdk
# or
yarn add @blockscout/app-sdk
```

### Transaction Toast Notifications

The transaction toast feature provides real-time notifications for transaction status updates, showing pending, success, and error states with detailed transaction information.

#### Setup

Wrap your application with the `NotificationProvider`:

```jsx
import { NotificationProvider } from "@blockscout/app-sdk";

function App() {
  return (
    <NotificationProvider>
      <YourApp />
    </NotificationProvider>
  );
}
```

#### Usage

Use the `useNotification` hook to display transaction toasts:

```jsx
import { useNotification } from "@blockscout/app-sdk";

function YourComponent() {
  const { openTxToast } = useNotification();

  const handleTransaction = async (txHash) => {
    try {
      // Your transaction logic here
      await sendTransaction();
      
      // Show transaction toast
      openTxToast("1", txHash); // '1' is the chain ID for Ethereum mainnet
    } catch (error) {
      console.error("Transaction failed:", error);
    }
  };

  return (
    <button onClick={() => handleTransaction("0x123...")}>
      Send Transaction
    </button>
  );
}
```

#### Toast Features

* Real-time status updates (pending, success, error)
* Transaction interpretation and summaries
* Links to block explorer
* Automatic status polling
* Error handling with revert reasons

### Transaction History Popup

The transaction history popup allows users to view recent transactions for a specific address or all transactions on a chain.

#### Setup

Wrap your application with the `TransactionPopupProvider`:

```jsx
import { TransactionPopupProvider } from "@blockscout/app-sdk";

function App() {
  return (
    <TransactionPopupProvider>
      <YourApp />
    </TransactionPopupProvider>
  );
}
```

#### Usage

Use the `useTransactionPopup` hook to open transaction history:

```jsx
import { useTransactionPopup } from "@blockscout/app-sdk";

function YourComponent() {
  const { openPopup } = useTransactionPopup();

  // Show transactions for a specific address
  const showAddressTransactions = () => {
    openPopup({
      chainId: "1", // Ethereum mainnet
      address: "0x123...", // Optional: specific address
    });
  };

  // Show all transactions for a chain
  const showAllTransactions = () => {
    openPopup({
      chainId: "1", // Ethereum mainnet
    });
  };

  return (
    <div>
      <button onClick={showAddressTransactions}>
        View Address Transactions
      </button>
      <button onClick={showAllTransactions}>
        View All Transactions
      </button>
    </div>
  );
}
```

#### Popup Features

* View recent transactions
* Filter by address
* Transaction status indicators
* Transaction interpretation
* Links to block explorer
* Mobile-responsive design
* Loading states and error handling

### Supported Chains

The SDK is compatible with any blockchain that has a Blockscout explorer instance with API v2 support.&#x20;

* Chains are listed in [Chainscout](https://chains.blockscout.com/).&#x20;
* Chain IDs can be retrieved from [https://github.com/blockscout/chainscout/blob/main/data/chains.json](https://github.com/blockscout/chainscout/blob/main/data/chains.json)
* To verify if your target chain ID is supported, visit the [compatibility checker](https://sdk-compatibility.blockscout.com/).

#### Common Supported Chain IDs

* `1` - Ethereum Mainnet
* `137` - Polygon Mainnet
* `42161` - Arbitrum One
* `10` - Optimism

### API Reference

#### useNotification Hook

```typescript
const { openTxToast } = useNotification();

// Open a transaction toast
openTxToast(chainId: string, hash: string): Promise<void>
```

#### useTransactionPopup Hook

```typescript
const { openPopup } = useTransactionPopup();

// Open transaction popup
openPopup(options: {
  chainId: string;
  address?: string;
}): void
```

### Complete Integration Example

Here's a complete example showing how to integrate both features:

```jsx
import React from 'react';
import { 
  NotificationProvider, 
  TransactionPopupProvider,
  useNotification,
  useTransactionPopup 
} from "@blockscout/app-sdk";

function TransactionComponent() {
  const { openTxToast } = useNotification();
  const { openPopup } = useTransactionPopup();

  const sendTransaction = async () => {
    const txHash = "0x123..."; // Your transaction hash
    await openTxToast("1", txHash);
  };

  const viewHistory = () => {
    openPopup({
      chainId: "1",
      address: "0x456..." // Optional
    });
  };

  return (
    <div>
      <button onClick={sendTransaction}>Send Transaction</button>
      <button onClick={viewHistory}>View Transaction History</button>
    </div>
  );
}

function App() {
  return (
    <NotificationProvider>
      <TransactionPopupProvider>
        <TransactionComponent />
      </TransactionPopupProvider>
    </NotificationProvider>
  );
}

export default App;
```

### Contributing

This project is currently in beta closed for external contributions.

