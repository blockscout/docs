# My Account Settings

[My Account](../../for-users/my-account/) is now available for chains that would like to incorporate personalization into their explorer. You will need to configure several 3rd party accounts to fully interact with the My Account feature. These include:

* [Uberauth](https://hexdocs.pm/ueberauth/readme.html): User authentication & login
* [Sendgrid](https://sendgrid.com/): Watchlist notifications
* [Airtable](https://www.airtable.com/):  Public Tag requests via API

Once these are setup, [update your Blockscout instance](../manual-deployment/) and add the [My Account ENV variables](../information-and-settings/env-variables.md#account-related-env-variables). Below are examples from the [Gnosis Chain instance](https://blockscout.com/xdai/mainnet) with some private info redacted.&#x20;

```
ACCOUNT_ENABLED=true
ACCOUNT_AUTH0_DOMAIN=login.blockscout.com
ACCOUNT_AUTH0_CLIENT_ID=...
ACCOUNT_AUTH0_CLIENT_SECRET=...
ACCOUNT_AUTH0_CALLBACK_URL=https://blockscout.com/xdai/mainnet/auth/auth0/callback
ACCOUNT_AUTH0_LOGOUT_URL=https://....us.auth0.com/v2/logout
ACCOUNT_AUTH0_LOGOUT_RETURN_URL=https://blockscout.com/xdai/mainnet/auth/logout
ACCOUNT_SENDGRID_API_KEY=...
ACCOUNT_SENDGRID_SENDER=noreply@blockscout.com
ACCOUNT_SENDGRID_TEMPLATE=d-...
ACCOUNT_PUBLIC_TAGS_AIRTABLE_URL=https://api.airtable.com/v0/.../Public%20Tags
ACCOUNT_PUBLIC_TAGS_AIRTABLE_API_KEY=key...
ACCOUNT_CLOAK_KEY=...
ACCOUNT_REDIS_URL=redis://redis_db:6379
ACCOUNT_DATABASE_URL=postgresql://user:pass@host:port/db
```
