# API keys

API Keys are available to enhance request availability. Keys give users the ability to query the API up to 10 requests/sec.

{% hint style="info" %}
The value of requests per API key is managed via `API_RATE_LIMIT_BY_KEY`. The default value is _50_.
{% endhint %}

A maximum of 3 keys can be created for each account.

## Create API key

**1) Login to My Account in Blockscout** <[_login instructions_](./)> to get started. Once logged in:

1. Go to API keys in the user menu.
2. Press Add API key.

<figure><img src="../../.gitbook/assets/blockscout-api-1.png" alt=""><figcaption></figcaption></figure>

**2)** **Fill in the Name field**. Add a Name for your API key. This is for your information only and to differentiate between different keys. Press **Generate API key.**

<figure><img src="../../.gitbook/assets/blockscout-api-key-2.png" alt=""><figcaption></figcaption></figure>

**3) API key generated.** The API Key is now added to your API dashboard. You can copy the key or edit the name/delete the key at any time. In addition you can add 2 additional keys (up to 3 per account).

<figure><img src="../../.gitbook/assets/blockscout-api-key-3.png" alt=""><figcaption></figcaption></figure>

## Use API key

Add the following to the end of a query to use your API key:\
`&apikey=your-api-key`

For example, a query to get more info on USDT on Optimism with the API key `fdbfa288-1695-454e-a369-4501253a120`would be formatted as follows:

`https://optimism.blockscout.com/api?module=token&action=getToken&contractaddress=0x94b008aA00579c1307B0EF2c499aD98a8ce58e58&apikey=fdbfa288-1695-454e-a369-4501253a120`

{% hint style="info" %}
For more info on RPC calls see the [RPC API Endpoints documentation](../../devs/apis/rpc/).
{% endhint %}
