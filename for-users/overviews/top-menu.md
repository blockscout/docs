# Top Menu

The top menu contains navigational items for exploration. The menu is customizable, and different instances can have different menus depending on the needs of the chain.&#x20;

<figure><img src="../../.gitbook/assets/top1.png" alt=""><figcaption><p>Ethereum Mainnet Menu</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Top-menu-items.png" alt=""><figcaption><p>Expanded Items</p></figcaption></figure>

## Blocks

* **Blocks:** Access high-level data for blocks, beginning with the most recent.\
  <img src="../../.gitbook/assets/blocks-1 (1).png" alt="" data-size="original">
* **Uncles:** Not valid for PoS consensus (but available for PoW consensus chains such as Ethereum Classic), uncles are created when 2 blocks are mined at the same time. Only 1 block can be added to the chain, and Uncles are the blocks that are not added, but miners still receive rewards for these blocks.
* **Forked Blocks (Reorgs):** Blocks which are not included in the primary chain due to chain reorganizations.

## Transactions

* **Mined**: Transactions which have been added to the chain, either by validators or miners depending on the chain type.
* **Pending**: Transactions still in the mempool which are waiting to be mined. These transactions may be mined or excluded depending on gas fees or network congestion.

## Tokens

Token menu is often configured differently depending on the instance.&#x20;

* **All:**  A list of ERC-20 tokens deployed to the chain.&#x20;
* **Native** (ie **ETH** on mainnet): Displays native token holders, ordered by balance.
* **Bridged**: If a chain includes bridged tokens (ie [Gnosis Chain](https://blockscout.com/xdai/mainnet)) these can be catalogued here.

## APIs

* **GraphQL**: Explore API calls using GraphQL and the in-browser IDE. Learn more about the [GraphQL Blockscout integration here](../api/graphql.md).
* **RPC**: API supporting GET and POST requests for many different API calls.
* **Eth RPC**: Supports the most popular [JSON RPC methods.](https://ethereum.github.io/execution-apis/api-documentation/)

## Apps

Customizable menu that can link to different ecosystem applications, utilities and statistics. [Gnosis Chain](https://blockscout.com/xdai/mainnet) currently has the most robust example of the Apps menu.

<figure><img src="../../.gitbook/assets/Apps.png" alt=""><figcaption></figcaption></figure>

## Networks

The current network name along with a dropdown displaying available instances.  Self-hosted chains may choose to only show their Mainnet and testnets. Hosted instances typically include links to other Hosted instances including Ethereum, Ethereum Classic, and Gnosis Chain.

## Night Mode

Switch to a dark background using the night-mode toggle.

<figure><img src="../../.gitbook/assets/night-mode.png" alt=""><figcaption></figcaption></figure>

## Search Bar

The comprehensive search bar allows for search by address, token name, token symbol, transaction hash, block number, tag or project name. It is typically the easiest way to find data quickly, and populates with inline results as you type.

## Custom Project Logo

Also included in the top menu is the Project logo. Projects can add and change custom logo using ENV variables during deployment. [More info here](../../for-developers/configuration-options/branding-configs.md).

<figure><img src="../../.gitbook/assets/customizable-logo.png" alt=""><figcaption></figcaption></figure>

