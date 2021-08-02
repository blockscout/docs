---
description: Upcoming enhancements and updates to BlockScout
---

# Roadmap

## ERC721 Metadata

**Target Date:** Q4 2019  
**Status:** ✅ Complete, ERC721 Metadata storage and display \([Release 2.1.0](https://forum.poa.network/t/blockscout-2-1-0-release/3128)\) and verification checks \([Release 2.1.1](https://forum.poa.network/t/blockscout-2-1-1-release/3172)\) are implemented.

[ERC-721](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) non-fungible tokens represent ownership of digital or physical assets. Each token is unique, and may include images and other data which identifies the asset and provides additional information. This might include registration information \(for example land, property or art registration\), identifying numbers or other data unique to that token. As ERC-721 tokens continue to proliferate, it is important to display the relevant information related to each owned token. 

## Staking DApp Integration

**Target Date:** Q3 2020  
**Status:** ✅ Complete Q4 2020

BlockScout will support the new POSDAO staking consensus mechanism through an on-board UI. The initial implementation will support the [xDai Stable Chain](https://xdaichain.com). This will allow users to place stake directly from the interface, monitor validator activity, and participate in consensus on the xDai Chain.

## Smart Contract Write Functionality

**Target Date:** Q2 - Q3 2020  
**Status**: ✅ Complete, Write contract/ write proxy functionalities are implemented \([Release 3.3.0](https://forum.poa.network/t/blockscout-v3-3-0-beta/3558)\).

Users can currently verify and read contracts on BlockScout. The next smart contract development phase will allow users to interact with contracts directly through the interface.  Verified contract methods will be accessible and users can connect through a web3 wallet \(such as MetaMask\) to access and execute contract functions.

## ERC1155 Support

**Target Date:** Q2 2021  
**Status**: ✅ Basic Functionality added for xDai chain, additional support in process.

ERC-1155 tokens are increasing in popularity as a way to manage multiple-token types including fungible and non-fungible tokens within a single instance. This feature provides parsing and display of tokens contained within an ERC-1155. Additional functionality such as metadata display is in process.

## Search Enhancements

**Target Date:** Q4 2021  
**Status**:  ☑ Ongoing

Most users access an explorer through the search function. Search should be robust, optimized for mobile and include additional information about contracts, tokens etc. We will continue to optimize the search functionality to provide users with robust search data on BlockScout. Some items of focus include:

* Prominent search bar
* Mobile upgrades
* Improved dropdown
* Full-page results
* Search control functionality

## EIP-1559 Support

**Target Date:** Q3-Q4 2021  
**Status**:  ☑ Ongoing

The London upgrade will create additional data points for exploration, including burn fees, priority fees, current gas target and more. These items will be incorporated into the explorer for chains after the London upgrade is completed.

## Ethereum Mainnet BlockScout Instance

**Target Date:** Q4 2021  
**Status**: In Development

BlockScout offered prior support for the Ethereum mainnet. This instance was discontinued;  however a new instance is now planned to further increase explorer diversity on Etheum and provide additional transparency for Ethereum users.

## My Account Functionality

**Target Date:** Q4 2021  
**Status**: R&D

We will explore adding account features for users looking for explorer personalizations, including alerts and notifications, the ability to watch specific addresses, name and customize data within the dashboard, and other advanced features.

## Rollup Support

**Target Date:** Q4 2021  
**Status**: R&D

BlockScout availability and support for both optimistic and zkRollups in operation on chains supported by BlockScout.

## Deployment Improvements

**Target Date:** Q4 2021  
**Status**: In Development

BlockScout deployment can be complicated for new users. Deployment improvements within a Docker environment will enable a fast path for easy setup and deployment.

## NFT View Interface

**Target Date:** Q4 2021  
**Status**: Ideation phase

As NFTs become more important to the ecosystem, the explorer will be updated and redesigned to display images, attributes and other data in a user-friendly interface.

## Block/Address Detail Page Improvements

**Target Date:** Q4 2021  
**Status**: Ideation phase

Improve data views, add additional fields, and update display and organization so users can clearly and quickly find and explore blockchain data on detail pages.

## Data Sorting/Filtering

**Target Date:** Q4 2021  
**Status**:  Ideation phase

Data in a tabular format should be easily sortable \(ascending, descending by column\). Improved pagination and filtering will give users access to view and filter data directly within the BlockScout interface.

## Data Storage Optimization

**Target Date:** Ongoing

Updating and optimizing the indexing scheme for storable data. We are working to decrease the BlockScout database size while preserving the same level of functionality.

## Performance Enhancements

**Target Date:** Ongoing - [80% covered in release 3.0.0](https://forum.poa.network/t/blockscout-v3-0-0-beta-block-hash-indexing-approach/3250)

As chain data grows exponentially, load speed, database optimization & caching, data parsing and front-end improvements are all required to maintain optimal performance. These efforts will continue as additional features are added to BlockScout.

## 

