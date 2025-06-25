---
description: Merits for incentives testing
---

# Integrate Merits

***

{% hint style="warning" %}
This guide features APIs for integrating test Merits into your application.&#x20;
{% endhint %}

### What are Blockscout Merits?

Merits are digital rewards collected by interacting with Blockscout and Blockscout-related apps and by participating in various activities (like contests, X participation, telegram participation, app participation and more).  Merits are chain agnostic and can be incorporated into any application. For more details see the [Merits section of the docs](../using-blockscout/merits/).

### Using Merits as an activity incentive

Merits are used to incentivize different activities within the Blockscout universe. For example:

* **Blockscout explorer basics:** Earn Merits by signing up for the program. Once you are signed up, you can earn additional Merits by completing a daily claim. You can also share your referral code and earn Merits when new users sign up with that code.&#x20;
* **Telegram mini app.** The telegram Blockscout Merits Bot allows for direct communication with subscribers. Users who download the bot receive extra Merits -> [https://t.me/blockscout\_merits\_bot](https://t.me/blockscout_merits_bot)
* **Swapscout swapping app**. Merits are incorporated in the app so that users can view their balance and earn Merits for their swaps. [https://swap.blockscout.com/](https://swap.blockscout.com/). **This is a good example of an external app that incorporates Merits.**
* **Revokescout app.** Merits are used to incentivize users but there is no sign in or interface. We simply check addresses that use the application and distribute Merits to those addresses.
* **Blockscout campaigns**. Participants in time-gated campaigns such as rating Dapps or Twitter(X) contests receive additional Merits. We collect the Ethereum addresses of winners and distribute Merits manually.
* **Partner campaigns**. Merits are allocated to users of other protocols as an additional incentive for use. Partners provide us with a list of addresses and tasks they completed and we distribute accordingly.

### Integrating Test Merits into your application

Merits can be integrated in different ways into your application.  Ideas may be to include Merits as a reward for user interactions with your app or a general reward for any activity.  Merits can be distributed to users via the API.

Users can have the ability to sign up for Merits through your app and/or login to their Merits account. You can also display individual Merits balances and leaderboard balances within your application. However, these are optional integrations.

To qualify for the bounty, you simply need to provide Merit incentives for certain activities, and then distribute those merits appropriately. As long as you have the participant's Ethereum address you can distribute Merits.

{% hint style="warning" %}
Note: You can retrieve basic data without an API key, but **for interactivity purposes you will need to request one via our Discord channe**l. See below.
{% endhint %}

### Getting started

1. Request your API key at: [https://ethglobal.com/discord](https://ethglobal.com/discord) in the #partner-blockscout channel
2. API hostname (and test merits dashboard): [https://merits-staging.blockscout.com](https://merits-staging.blockscout.com)

{% hint style="info" %}
A full list of endpoints is available on our swagger page here: [https://blockscout.github.io/swaggers/services/merits/main/index.html](https://blockscout.github.io/swaggers/services/merits/main/index.html)
{% endhint %}

### Get basic Merit info for a user

{% openapi-operation spec="poa-api" path="/api/v1/auth/user/{address}" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Get leaderboard ranking for a user

{% openapi-operation spec="poa-api" path="/api/v1/leaderboard/users/{address}" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Partner balance and distribution information

When you request an API key you become a partner! You will receive a balance of test Merits which can then be distributed to your users. \
&#xNAN;_\* Requires API Key - Add the assigned API KEY in the Authorization header to see your information._

{% openapi-operation spec="poa-api" path="/partner/api/v1/balance" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
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
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Login and Registration Flow - Get User Token

_Use the following flow to get a User Token_

1. Get Nonce from Backend

{% openapi-operation spec="poa-api" path="/api/v1/auth/nonce" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
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
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### API Calls Requiring a User Token

_\*Requires User Token: put the user token in the Authorization header_

{% openapi-operation spec="poa-api" path="/api/v1/user/balances" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="poa-api" path="/api/v1/user/logs" method="get" %}
[OpenAPI poa-api](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/7b4077d6c925bfd621e560fb5cea9377bb825408c6b6bdac5d281dfac0b98a5d.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250625%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250625T154753Z&X-Amz-Expires=172800&X-Amz-Signature=f399ab6024a24686b773d9f0f8f193b8a8d134797a59f12af9b25c58c86da660&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}







