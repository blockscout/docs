# Integrate Merits

### What are Blockscout Merits?

Merits are digital rewards collected by interacting with Blockscout and Blockscout-related apps and by participating in various activities (like contests, X participation, telegram participation, app participation and more).  Merits are chain agnostic and can be incorporated into any application. For more details see the [Merits section of the docs](../using-blockscout/merits/).

### Using Merits as an activity incentive

Merits are used to incentivize different activities within the Blockscout universe. For example:

* **Blockscout explorer basics:** You earn Merits by signing up for the program. Once you are signed up, you can earn additional Merits by completing a daily claim. You can also share your referral code and earn Merits when new users sign up with that code.&#x20;
* **Blockscout activity pass:** The activity pass allows you to earn Merits for additional Blockscout activities like verifying and interacting with contracts.
* **Telegram mini app.** The telegram Blockscout Merits Bot allows for direct communication with subscribers. Users who download the bot receive extra Merits -> [https://t.me/blockscout\_merits\_bot](https://t.me/blockscout_merits_bot)
* **Swapscout swapping app**. Merits are incorporated in the app so that users can view their balance and earn Merits for their swaps. [https://swap.blockscout.com/](https://swap.blockscout.com/)
* **Blockscout campaigns**. Participants in time-gated campaigns such as rating Dapps or Twitter(X) contests receive additional Merits.
* **Partner campaigns**. Merits are allocated to users of other protocols as an additional incentive for use.

### Integrating Merits into your application

Merits can be integrated in different ways into your application.  Ideas may be to include Merits as a reward for user interactions with your app or a general reward for any activity.  Merits can be distributed to users via the API.

Users can have the ability to sign up for Merits through your app and/or login to their Merits account. You can also display individual Merits balances and leaderboard balances within your application.&#x20;

You can retrieve basic data without an API key, but for interactivity purposes you will need to request one via our Discord channel.&#x20;

### Getting Started

1. Request your API key at:&#x20;
2. API hostname (and test merits dashboard): [https://merits-staging.blockscout.com](https://merits-staging.blockscout.com)

### Get Basic Merit Info for Users

{% openapi-operation spec="poa-api" path="/api/v1/auth/user/{address}" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

{% openapi-operation spec="poa-api" path="/api/v1/leaderboard/users/{address}" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

### Partner distribution information

Balances can be added for entities (partners) who can then distribute Merits to their users. \
&#xNAN;_\* Requires API Key - Add the assigned API KEY in the Authorization header to see your information._

{% openapi-operation spec="poa-api" path="/partner/api/v1/balance" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

### Distribute Merits

_\* Requires API Key - Add the assigned API KEY in the Authorization header to add your distribution information._

_Notes:_

* `id` must be unique per each API KEY, so it’s recommended to include date or time period describing the distribution period.
* `distributions`
  * Max `1000` wallets per distribution.
  * Amounts less than `0.01` per address are not allowed.
  * Amounts can be in decimals, max 2 decimal digits precision is recommended.
* create\_missing\_accounts
  * `true`: allows distributions to not yet registered Merits accounts.&#x20;
  * `false`: only allow distributions to users that are already registered.

{% openapi-operation spec="poa-api" path="/partner/api/v1/distribute" method="post" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

### Login and Registration Flow - Get User Token

_Use the following flow to get a User Token_

1. Get Nonce from Backend

{% openapi-operation spec="poa-api" path="/api/v1/auth/nonce" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

2. Ask for a signature from a user with a predefined message

```
// Formatted message example


merits.blockscout.com wants you to sign in with your Ethereum account:
0x813399e5b08Bb50b038AA7dF6347b6AF2D163328

Sign-In for the Blockscout Merits program.

URI: 
https://merits-staging.blockscout.com
Version: 1
Chain ID: 1
Nonce: 4MCWIDlddqsmJAZOZ
Issued At: 2025-03-18T12:23:51.549Z
Expiration Time: 2026-03-18T12:23:51.549Z
```

3. Send data to get a user token

{% openapi-operation spec="poa-api" path="/api/v1/auth/login" method="post" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

### Calls Requiring a User Token

_\*Requires User Token: put the user token in the Authorization header_

{% openapi-operation spec="poa-api" path="/api/v1/user/balances" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

{% openapi-operation spec="poa-api" path="/api/v1/user/logs" method="get" %}
[Broken link](broken-reference)
{% endopenapi-operation %}







