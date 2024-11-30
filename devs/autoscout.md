---
description: Deploy a production-ready instance on the cloud in 5 minutes
---

# Autoscout cloud deployment

## Autoscout Beta

{% hint style="info" %}
Autoscout is currently in Beta. It is available for general testing at \
[https://deploy.blockscout.com/](https://deploy.blockscout.com/), however some features may not yet be functional.
{% endhint %}

### Get Started with Autoscout

1. **Create an account:** To get started, go to [https://deploy.blockscout.com/](https://deploy.blockscout.com/), create an account, and login to get started.
2. **Request credits:** You will need credits to launch your explorer. Please use Discord to let us know that you have created an instance. Go to the [Blockscout Discord](https://discord.gg/blockscout) `#autoscout` channel and share your email, and we will top off your account for testing.&#x20;
3. **Add a new instance:** You can start adding an instance before credits are added to your account. Click the Add instance button to get started.
4. **Add your network info**:  See below for info on configuration and parameters.
5. **Deploy your explorer:** Click save and deploy to start the deployment process. In 5-10 minutes your explorer will be live and indexing your chain. Once deployed you can access your explorer link.

## Create Instance

There are several tabs to fill out to start your instance; Info, Branding, and Rollup config (if needed). You can also add plugins (currently the only live plugin is stats) once your instance is indexed. You can come back and edit parameters later, but this may require relaunching the instance.

### Info

<figure><img src="../.gitbook/assets/create-instance.png" alt=""><figcaption></figcaption></figure>

The following parameters are in the Info section. \* parameters are required.

* **Instance size\***: Select based on the number of transactions anticipated for the instance. The costs are currently placeholders, but your credits will be impacted according to chain usage.
* **Chain name**: The chain name will be shown in the top explorer banner.
* **Instance name\***:  A label for your instance, it is reflected in the url of the instance ie https://instance-name.cloud.blockscout.com/
* **Chain ID**: If you don't know the chain ID you can get with the `eth_chainId` JSON-RPC method.
* **Node type:** Choose from the list of clients for the archive node:
  * Besu, Erigon, Ganache, Geth, Parity
* **Gas token symbol**: Will show in the interface, for example ETH if your chain uses Ether for gas.
* **Mainnet or Testnet**: Select the type of chain, if Testnet a label will be added to the instance.
* **This chain is a Rollup**: If selected, another field will appear to select **Arbitrum** or **Optimism**. These are the 2 currently supported rollup types. You will then fill out additional information in the Rollup Config tab.
* **RPC URL\***: The archive node url (https://your-rpc-url)
* **WS URL**: The websocket url (wss://ws.your-websocket-url)
* **Custom Domain**: You can use a custom domain for your instance but must configure your DNS and add a DNS `CNAME` record pointing to `autoscout.cname.blockscout.com`
* **Public RPC URL**: Enables 'add to Metamask button'. Can be the same as the RPC URL if this is a public node.
* **WalletConnect project ID:** Enables the ability for Read and Write functionality with smart contracts. [Learn more about setting one up here](../setup/configuration-options/walletconnect-project-id-for-contract-read-write.md).

### Branding

<figure><img src="../.gitbook/assets/customize-layout.png" alt=""><figcaption></figcaption></figure>

* **Default color theme**: Choose between a light theme and 3 variations of a darker theme.
* **Default address identicon:** Select from 4 different options for default identicons in your instance.
* **Vertical or Horizontal menu**: Select vertica for a side menu or horizontal for a top menu.
* **Full logo URL**:  Add a url link to your full logo image in horizontal format. Supported formats: image/jpeg, image/gif, image/png. Add one for light mode and one for dark mode if desired (users can switch modes manually).
* **Logo sign (square) URL**: Add a url link to your square logo image in horizontal format. Supported formats: image/jpeg, image/gif, image/png. Add one for light mode and one for dark mode if desired (users can switch modes manually).
* **Header background gradient and text color**: Choose your desired background color gradients with the selector and choose your preferred text color. You will see a preview in the interface.&#x20;
* **Favicon and OG image URL**: Add your favicon and [OG image](https://ogp.me/). OG image specs: Minimum image size is 200×20pixels (recommended: 1200×600); maximum supported file size is 8 MB; 2:1 aspect ratio; supported formats: image/jpeg, image/gif, image/png
* **Footer links**: Add up to 3 columns along with titles and urls for the links you want added to each column.&#x20;

### Rollup Config

If your chain is a rollup (Arbitrum and Optimism rollups are currently supported) you will select in the info screen and then fillout the Rollup config info.  \


{% hint style="info" %}
* Read the [Rollup deployment and config details](https://docs.blockscout.com/setup/deployment/rollup-deployment#arbitrum)
  * [Arbitrum](../setup/env-variables/backend-envs-chain-specific.md#arbitrum-management) ENV variables
  * [Optimism](../setup/env-variables/backend-envs-chain-specific.md#optimism-rollup-management) ENV variables
{% endhint %}

<figure><img src="../.gitbook/assets/rollup-params.png" alt=""><figcaption></figcaption></figure>

