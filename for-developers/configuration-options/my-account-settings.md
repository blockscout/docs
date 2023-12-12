# My Account Settings

[My Account](../../for-users/my-account/) is now available for chains that would like to incorporate personalization into their explorer. You will need to configure several 3rd party accounts to fully interact with the My Account feature. These include:

* [Uberauth](https://hexdocs.pm/ueberauth/readme.html): User authentication & login
* [Sendgrid](https://sendgrid.com/): Watchlist notifications
* [Airtable](https://www.airtable.com/): Public Tag requests via API

Once these are setup, [update your Blockscout instance](../deployment/manual-old-ui/) and add the [My Account ENV variables](../information-and-settings/env-variables/#account-related-env-variables). Below are examples from the [Gnosis Chain instance](https://blockscout.com/xdai/mainnet) with some private info redacted.

```
ACCOUNT_ENABLED=true
ACCOUNT_AUTH0_DOMAIN=login.blockscout.com
ACCOUNT_AUTH0_CLIENT_ID=...
ACCOUNT_AUTH0_CLIENT_SECRET=...
ACCOUNT_SENDGRID_API_KEY=...
ACCOUNT_SENDGRID_SENDER=noreply@blockscout.com
ACCOUNT_SENDGRID_TEMPLATE=d-...
ACCOUNT_PUBLIC_TAGS_AIRTABLE_URL=https://api.airtable.com/v0/.../Public%20Tags
ACCOUNT_PUBLIC_TAGS_AIRTABLE_API_KEY=key...
ACCOUNT_CLOAK_KEY=...
ACCOUNT_REDIS_URL=redis://redis_db:6379
ACCOUNT_DATABASE_URL=postgresql://user:pass@host:port/db
```

## Airtable Schema

Add `request_type` and `request_id` variables to the airtable when configuring for your My Account settings.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

## List of required variables

The following variables are needed for your airtable.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
