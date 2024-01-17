---
description: Basic support for ERC-1155s
---

# ERC-1155 Support

[ERC-1155](https://eips.ethereum.org/EIPS/eip-1155) contracts are designed to support multiple token types within a single contract. This standard is being adopted rapidly for efficiency and optimization, and is being used to bundle multi-token transactions and approvals while supporting both fungible and non-fungible tokens.

Recognition and labelling for ERC-1155 contracts, indexing instance balances for both fts and nfts, parsing single and batched transactions, and monitoring and displaying minting events are included.

## GnosisChain Example

ERC-1155s are supported for the Gnosis Chain and any new ERC-1155 instances are recognized on deployment. For ERC-1155 contracts created prior to the enhanced support, a new single or batched transfer, mint, or token instance creation triggers contract recognition.\
\
[https://gnosis.blockscout.com/token/0x93d0c9a35c43f6BC999416A06aaDF21E68B29EBA?tab=token_transfers](https://gnosis.blockscout.com/token/0x93d0c9a35c43f6BC999416A06aaDF21E68B29EBA?tab=token_transfers)

![](../../.gitbook/assets/erc1155-example.png)
