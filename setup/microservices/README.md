# Microservices

Blockscout microservices are individual components written in Rust designed to provide full functionality to the explorer. This architecture allows for better scalability, easier maintenance, and more flexible deployment options.

Information about Blockscout microservices and how to run them is available here:

{% embed url="https://github.com/blockscout/blockscout-rs" %}

Services Include:

1. [blockscout-ens](https://github.com/blockscout/blockscout-rs/blob/main/blockscout-ens) - indexed data of domain name service for blockscout instances.
2. [da-indexer](https://github.com/blockscout/blockscout-rs/blob/main/da-indexer) - collects blobs from different DA solutions (e.g, Celestia)
3. [eth-bytecode-db](https://github.com/blockscout/blockscout-rs/blob/main/eth-bytecode-db) - Ethereum Bytecode Database. Cross-chain smart-contracts database used for automatic contracts verification
4. [proxy-verifier](https://github.com/blockscout/blockscout-rs/blob/main/proxy-verifier) - backend for the standalone multi-chain verification service
5. [sig-provider](https://github.com/blockscout/blockscout-rs/blob/main/sig-provider) - aggregator of ethereum signatures for transactions and events
6. [smart-contract-verifier](https://github.com/blockscout/blockscout-rs/blob/main/smart-contract-verifier) - smart-contracts verification
7. [stats](https://github.com/blockscout/blockscout-rs/blob/main/stats) - service designed to calculate and present statistical information from a Blockscout instance
8. [user-ops-indexer](https://github.com/blockscout/blockscout-rs/blob/main/user-ops-indexer) - service designed to index, decode and serve user operations as per the ERC-4337 standard
9. [visualizer](https://github.com/blockscout/blockscout-rs/blob/main/visualizer) - service for evm visualization such as:
   1. Solidity contract visualization using [sol2uml](https://www.npmjs.com/package/sol2uml)
