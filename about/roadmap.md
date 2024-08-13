---
description: Upcoming enhancements and updates to BlockScout
---

# Roadmap

{% hint style="info" %}
The Blockscout roadmap is a high-level strategic plan designed to guide research and development. **Target dates and details are reviewed by the team and subject to move, adjust and change as the project evolves**. Note that only completed items ( :white\_check\_mark: Status: Complete) are considered achieved project milestones.

_Last update: May 29, 2024 |_ [_Changelog_](roadmap.md#change-log)
{% endhint %}

## 🟦 Q1-2 2024

Items currently in progress. Some are planned for Q1 completion while others will extend to Q2 2024.

### 🟦  New Microservices

In addition to the Admin dashboard, other microservices in development include:

* DeFiLlama tags support providing additional information about wallet addresses.
* Token pricing extension providing real-time market data for various tokens.
* :white\_check\_mark: Visualizer service offering various visualization schemes, such as Sol2UML and transaction graphs for complex blockchain data analysis.
* Multi-chain search extension for ecosystems where many chains co-exist within a similar environment (ie Optimism, Astar etc.)
* EOA analytics service for advanced analytics per address including:
  * Tx type distributions
  * Tx frequency and popular contract usage
  * Average values/fees/types
  * Governance and voting participation

### 🟦  ENS Support

Support for the Ethereum Name Service (ENS) and its popular forks by:

* :white\_check\_mark: Resolving ENS names for addresses and listing names for the address
* :white\_check\_mark:  Enabling search by ENS name
* Providing advanced name lookup features
* Resolve ENS name for addresses, list names for the address
* :white\_check\_mark: Search by ENS name
* Advanced Name lookup

### 🟦  POS and Rollup Feature Expansion

* POS consensus support including deposits, withdrawals and other pertinent details such as finalization status, proposed slot and epoch, fee recipient and consensus info. This includes tracking and monitoring of deposits on the Ethereum 2.0 Beacon Chain, providing insights into the progress of Ethereum's transition to Proof of Stake (PoS).
* L2 support including additional features for popular L2 scaling solutions by providing insights into L2 network performance, transactions, and smart contracts

### 🟦  Blockscout Swap Native Dapp

A native swap application will be integrated into the Dapp marketplace so that users can trade tokens easily and securely from one convenient location.

### 🟦  Smart Search

Research incorporating AI functionality to introduce smart search capabilities:

* Natural language queries
* Boolean search
* Instant analytics

### 🟦 Governance Views & Interactivity

Governance platforms and voting mechanism integrations, allowing users to monitor and participate in on-chain governance activities directly from Blockscout.

### 🟦 CEX/DEX Views

Provide insights into trading activities and liquidity on both centralized and decentralized exchanges, allowing users to compare and analyze exchange data.

### 🟦  RPC API Expansion&#x20;

Add additional routes and endpoints for users, explore most-requested and most-used endpoints to optimize API.

### 🟦 Personal Asset Management

My Account functionality will be extended to enable portfolio views and management of assets across protocols and chains.

### 🟦  NFT Module Exploration

Explore a dedicated NFT explorer module to include:

* Top NFTs
* Latest Trades, Transfers and Mints
* NFT Marketplace & Platform Integrations

### 🟦   Ongoing Interface Improvements

Add improvements as informed by usage trends. May include "Popular Apps" views for the marketplace module, "Top Statistic" views relevant to most used applications and contracts, and detailed statistics related to node performance.

### 🟦  Ongoing Tooling Improvements

Continue to research and improve tooling for developers including requested tools such as:

* Transaction decoder: decodes raw tx data
* Balance checker
* Similar contracts search
* Unit converter
* Advanced debugger

## :white\_check\_mark: Completed

### :white\_check\_mark:  Gas Tracker

Users can monitor gas prices and trends to help them make informed decisions about transaction fees and timing.

### :white\_check\_mark: Human Readable Transactions v1

Display complex transactions in an easily understandable format for non-technical users. This includes the ability to automatically decode transaction data, including tokens, contracts, and events.

### &#x20;:white\_check\_mark: Universal Smart Contract front-end

Improve and simplify the Smart Contract deployment & verification process. Integrate React components to abstract away common on-chain operations.

### :white\_check\_mark: Improved Indexer Performance

**Target Date:** Q2 2023\
**Status**: :white\_check\_mark: Completed

Load speed, database optimization & caching, data parsing features to maintain optimal performance. These efforts will continue as additional features are added to BlockScout.

### :white\_check\_mark: Advanced Filter and Sort

**Target Date:** Q2 2023\
**Status**: :white\_check\_mark: Completed

Enhance filter and sort options so users can view transaction data in various formats including transaction types, assets & time ranges. Explore ability to save and share custom filter configurations.

### :white\_check\_mark: My Account Improvements

**Target Date:** Q2 2023\
**Status**: :white\_check\_mark: Completed

My Account beta is active and will be rolled out on a case-by-base basis, with hosted instances receiving priority. Includes adding the following features:

* Watchlists: Users can create watchlists for specific addresses or contracts, and view all transactions from the watchlists on the main page.
* Enhanced CSV export features
* Smart contract ownership verification
* Airdrop eligibility tool

### :white\_check\_mark: Admin Dashboard

**Target Date:** Q2 2023\
**Status**: :white\_check\_mark: Completed

Rust microservice which will provide a comprehensive dashboard for blockchain administrators. Available for hosted versions first.

* Token info
* Public tags
* Real-time network monitoring, chain statistics, user analytics

### :white\_check\_mark: Landing Page

**Target Date:** Q3 2022\
**Status**: :white\_check\_mark: Completed

A new landing page is in development for Blockscout to assist new users and developers understand the Blockscout feature set and find information quickly.

### :white\_check\_mark: UI Redesign

**Target Date:** Q3-Q4 2022\
**Status**: :white\_check\_mark: v1 Completed see [https://eth-goerli.blockscout.com/](https://eth-goerli.blockscout.com/)

A new UI interface is under development to improve data exploration, optimize views, and provide overall better UX for Blockscout users. The UI is being built from the ground up. It will overhaul all aspects of Blockscout engagement, creating a complete all-in-one interface for chain exploration. In addition to a modern design, the upgrade will also improvements to features such as:

* **Search**:  Prominent search, mobile upgrades, improved dropdown, full-page results, search control
* **Data Sort/Filtering**: Ability to sort data (ascending & descending by column). Improved pagination and filtering abilities.
* **My Account**: See below for features related to My Account functionality.

### :white\_check\_mark: DApp Marketplace v1

**Target Date:** Q4 2022\
**Status**:  :white\_check\_mark: v1 Completed

Chain users will be able to access applications and modules directly from Blockscout, vastly improving the overall chain experience. Interoperability, swaps, transactions, and 3rd party project-based apps will be accessible and integrated with the modular interface.

Blockscout will also develop native applications for this marketplace. Several are in active development.

* **Blockscout Swap**: Swap feature using an aggregator under the hood for simple swaps without leaving Blockscout.
* **Blockscout Revoke**: Find contracts/apps you have granted allowances to (the ability to spend tokens on your behalf) and revoke these permissions.
* More TBD

### :white\_check\_mark: My Account Functionality v1

**Target Date:** Q3 2022\
**Status**:  :white\_check\_mark:  Instance deployed on Gnosis Chain. Undergoing improvements.

We will explore adding account features for users looking for explorer personalizations, including alerts and notifications, the ability to watch specific addresses, name and customize data within the dashboard, and other advanced features.

### :white\_check\_mark: Blockscout Rust Microservices v1

**Target Date:** Q3 2022\
**Status**:  :white\_check\_mark:  v1 completed - Smart Contract Verification microservice

New Rust-developed microservices will be enabled on Blockscout to extend functionality and modularity. We are revamping smart contract verification to use a Rust module and working on a smart contract uml visualization module to start.

### :white\_check\_mark: Deployment Improvements

**Target Date:** Q3 2022\
**Status**: :white\_check\_mark: Completed, Documentation in progress

BlockScout deployment can be complicated for new users. Deployment improvements within a Docker environment will enable a fast path for easy setup and deployment.

### :white\_check\_mark: Ethereum Mainnet BlockScout Instance

**Target Date:** Q2 2022\
**Status**: :white\_check\_mark: Instance deployed, optimizations ongoing.

BlockScout offered prior support for the Ethereum mainnet. This instance was discontinued;  however a new instance is now planned to further increase explorer diversity on Ethereum and provide additional transparency for Ethereum users.

### :white\_check\_mark: ERC721 Metadata

**Target Date:** Q4 2019\
**Status:** :white\_check\_mark: Complete, ERC721 Metadata storage and display ([Release 2.1.0](https://forum.poa.network/t/blockscout-2-1-0-release/3128)) and verification checks ([Release 2.1.1](https://forum.poa.network/t/blockscout-2-1-1-release/3172)) are implemented.

[ERC-721](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) non-fungible tokens represent ownership of digital or physical assets. Each token is unique, and may include images and other data which identifies the asset and provides additional information. This might include registration information (for example land, property or art registration), identifying numbers or other data unique to that token. As ERC-721 tokens continue to proliferate, it is important to display the relevant information related to each owned token.&#x20;

### :white\_check\_mark: Staking DApp Integration

**Target Date:** Q3 2020\
**Status:** :white\_check\_mark: Complete Q4 2020

BlockScout will support the new POSDAO staking consensus mechanism through an on-board UI. The initial implementation will support the [xDai Stable Chain](https://xdaichain.com). This will allow users to place stake directly from the interface, monitor validator activity, and participate in consensus on the xDai Chain.

### :white\_check\_mark: Smart Contract Write Functionality

**Target Date:** Q2 - Q3 2020\
**Status**: :white\_check\_mark: Complete, Write contract/ write proxy functionalities are implemented ([Release 3.3.0](https://forum.poa.network/t/blockscout-v3-3-0-beta/3558)).

Users can currently verify and read contracts on BlockScout. The next smart contract development phase will allow users to interact with contracts directly through the interface.  Verified contract methods will be accessible and users can connect through a web3 wallet (such as MetaMask) to access and execute contract functions.

### :white\_check\_mark: ERC1155 Support

**Target Date:** Q2 2021\
**Status**: :white\_check\_mark: Basic Functionality added for xDai chain, additional support in process.

ERC-1155 tokens are increasing in popularity as a way to manage multiple-token types including fungible and non-fungible tokens within a single instance. This feature provides parsing and display of tokens contained within an ERC-1155. Additional functionality such as metadata display is in process.

### :white\_check\_mark: Rollup Support

**Target Date:** Q4 2021\
**Status**: :white\_check\_mark: Instances for Optimism and Arbitrum on Gnosis Chain

BlockScout availability and support is available for Optimism and Arbitrum on the Gnosis Chain. Includes tracking for gas price on L1 and the L2 implementations. Currently Optimism is the favored deployment.

* Optimism: [https://blockscout.com/xdai/optimism](https://blockscout.com/xdai/optimism)
* Arbitrum: [https://blockscout.com/xdai/aox/](https://blockscout.com/xdai/aox/)

### :white\_check\_mark: EIP-1559 Support

**Target Date:** Q3-Q4 2021\
**Status**: :white\_check\_mark: Complete

The Gnosis Chain explorer supports EIP-1559 functionality with a stated transaction type (2 for EIP-1559) and includes data reporting of Max Fee per Gas, Max Priority Fee per Gas and Priority Fee / Tip paid for a transaction.

### :white\_check\_mark: Multi-file Contract Source Code Verification

**Target Date:** Q4 2021\
**Status:**  :white\_check\_mark: Complete

BlockScout supports verification for contracts via multiple methods including Hardhat and the Hardhat and Sourcify plugins. [More information is available here](../using-blockscout/verifying-a-smart-contract/).

## Change Log

| Update       | Items                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 29.05.2024   | <p>Minor update: Will be adding a major overhaul in June for Q3-Q4 and will reconfigure, add new items and remove others.<br></p><p>Completed:</p><ul><li>Gas Tracker</li><li>Basic ENS support</li></ul><p>Removed <span data-gb-custom-inline data-tag="emoji" data-code="1f389">🎉</span></p><ul><li>AWS template</li><li>Multisender native dapp</li></ul>                                   |
| _03.01.2024_ | <p>Update milestones for Q1 2024. </p><p>Completed:</p><ul><li>Universal smart contract front-end</li><li>Human readable transactions v1</li></ul>                                                                                                                                                                                                                                               |
| _07.11.2023_ | Updated milestones to reflect current quarterly work. A more extensive update with many reworked milestones will be added for 2024.                                                                                                                                                                                                                                                              |
| _10.08.2023_ | <p>Updated Q3 milestones to account for completed items.</p><p></p><p>Completed:</p><ul><li>Improved indexer performance</li><li>Advanced filter and search</li><li>My Account improvements</li><li>Admin Account </li></ul>                                                                                                                                                                     |
| _17.04.2023_ | <ul><li>Revamp roadmap for 2023 milestones by Q.</li><li>Moved all In-research items to appropriate Q.</li><li><p>Added:</p><ul><li>Q2,Q3,Q4 2023 items</li></ul></li><li><p>Completed:</p><ul><li>Landing Page</li><li>React UI v1</li><li>Rust Microservices v1</li><li>DApp Marketplace v1</li><li>My Account v1</li></ul></li></ul>                                                          |
| 27.07.2022   | <ul><li>Updated marketplace to include Blockscout native DApps</li><li>Added Blockscout Microservices</li><li>Added Multi-chain search</li><li>Added personal asset management features</li><li>Added Blockscout ID</li><li>Combined several elements into UI category</li><li>Deployment improvements (Docker image) moved to completed.</li><li>Update Research Phase items to 2023.</li></ul> |
| 06.07.2022   | <p>Added:</p><ul><li>Analytics Dashboards</li><li>UI Overhaul</li><li>Modular Plug-and-Play Library</li></ul><p>Completed:</p><ul><li>Ethereum Mainnet Instance<br></li></ul>                                                                                                                                                                                                                    |
| 11.04.2022   | <ul><li>Rearranged into Completed and Ongoing Categories. </li><li>Updated Ongoing Item dates</li><li>Added UI enhancements</li><li><p>Marked as Completed</p><ul><li>EIP-1559 Support &#x3C;Completed></li><li>Rollup Support &#x3C;Completed></li><li>Multi-file Contract Source Code Verification &#x3C;Completed></li></ul></li></ul>                                                        |
| _04.08.2021_ | <p></p><ul><li><p>Added multiple new items to Q4 Roadmap including:</p><ul><li>EIP-1559 Support</li><li>Ethereum Mainnet Instance</li><li>My Account Functionality</li><li>Rollup Support</li><li>Deployment Improvements</li><li>Multi-file Contract Source Code Verification</li><li>Block/Address Detail Page Improvements</li><li>Data Sorting/Filtering</li></ul></li></ul>                 |
|              |                                                                                                                                                                                                                                                                                                                                                                                                  |
