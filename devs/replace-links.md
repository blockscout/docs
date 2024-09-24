# Replace Links

{% hint style="warning" %}
Under Construction
{% endhint %}

{% hint style="info" %}
This page will detail how to replace links from other explorers to Blockscout. In most cases simply replacing the front end of the url is needed.

For example, replace [https://etherscan.com/](https://etherscan.com/) with [https://eth.blockscout.com/](https://eth.blockscout.com/) and the corresponding links to blocks, transactions, etc will be mapped to the Blockscout explorer rather than Etherscan.\
\
Blockscout linking architecture follows [EIP-3091 ](https://eips.ethereum.org/EIPS/eip-3091)standardization for the following:

* Blocks \
  `<BLOCK_EXPLORER_URL>/block/<BLOCK_HASH_OR_HEIGHT>`
* Transactions\
  `<BLOCK_EXPLORER_URL>/tx/<TX_HASH>`
* Accounts\
  `<BLOCK_EXPLORER_URL>/address/<ACCOUNT_ADDRESS>`
* Tokens\
  `<BLOCK_EXPLORER_URL>/token/<TOKEN_ADDRESS>`


{% endhint %}

