---
description: Basic support available now for ERC-1155s
---

# ERC-1155 Support

[ERC-1155](https://eips.ethereum.org/EIPS/eip-1155) contracts are designed to support multiple token types within a single contract. This standard is being adopted rapidly for efficiency and optimization, and is being used to bundle multi-token transactions and approvals while supporting both fungible and non-fungible tokens.

ERC-1155s contain additional information which is not typically handled by the default BlockScout instance. This includes recognition and labelling for ERC-1155 contracts, indexing instance balances for both fts and nfts, parsing single and batched transactions, and monitoring and displaying minting events. 

Basic support is now available for projects as a premium add-on, with additional visual improvements and support for ERC-1155s coming soon.

## xDai Chain Example

ERC-1155s are supported for the xDai Chain and any new ERC-1155 instances are recognized on deployment. For ERC-1155 contracts created prior to the enhanced support, a new single or batched transfer, mint, or token instance creation triggers contract recognition.  
  
[https://blockscout.com/xdai/mainnet/tokens/0x93d0c9a35c43f6BC999416A06aaDF21E68B29EBA/token-transfers](https://blockscout.com/xdai/mainnet/tokens/0x93d0c9a35c43f6BC999416A06aaDF21E68B29EBA/token-transfers)

![](../../.gitbook/assets/erc1155-example.png)

