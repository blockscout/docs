# How to fix Unknown Private Network error?

In a self-hosted or locally deployed instance, when attempting to do a **write transaction** on a verified contract, the following errors may appear:

{% hint style="warning" %}
**Unauthorized**\
****"You connected to Unknown Private Network chain in the wallet, but the current instance of Blockscout is for Unknown Private Network chain"
{% endhint %}

{% hint style="danger" %}
"No "from" address specified in neither the give options, nor the default options."
{% endhint %}

### To **T**roubleshoot:&#x20;

* Check that you set the correct `CHAIN_ID` env variable
* Check correct variable for `NETWORK_ID`
* Check that Metamask (or other web3 wallets) is connected to correct network.
* [Read more about this issue here](https://github.com/blockscout/blockscout/issues/5803).



