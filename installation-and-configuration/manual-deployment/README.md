# Manual Deployment

For automated deployment, see [Ansible deployment](../ansible-deployment/).

BlockScout requires a **full archive node** in order to import every state change for every address on the target network. For client specific settings related to a node running parity or geth, please see [Client Settings](../client-settings-parity-geth-ganache.md).

## Deployment Steps

1\) `git clone https://github.com/poanetwork/blockscout`

2\) `cd blockscout`

3\) Setup default configurations:  
 `cp apps/explorer/config/dev.secret.exs.example apps/explorer/config/dev.secret.exs`

`cp apps/block_scout_web/config/dev.secret.exs.example apps/block_scout_web/config/dev.secret.exs`

4\) Update `apps/explorer/config/dev.secret.exs`

* **Linux:** Update the database username and password configuration
* **Mac:** Remove the `username` and `password` fields
* **Optional:** Set up a default configuration for testing. `cp apps/explorer/config/test.secret.exs.example apps/explorer/config/test.secret.exs` 

{% hint style="info" %}
_Example usage:_ Changing the default Postgres port from localhost:15432 if [Boxen](https://github.com/boxen/boxen) is installed.
{% endhint %}

5\) If you have deployed previously, delete the `apps/block_scout_web/priv/static` folder. This removes static assets from the previous build.

6\) Install dependencies. `mix do deps.get, local.rebar --force, deps.compile, compile`

7\) If not already running, start postgres: `pg_ctl -D /usr/local/var/postgres start`

{% hint style="success" %}
To check [postgres status](https://www.postgresql.org/docs/9.6/app-pg-isready.html): `pg_isready`
{% endhint %}

8\) Create and migrate database `mix do ecto.create, ecto.migrate`

{% hint style="info" %}
If you have run previously, drop the previous database `mix do ecto.drop, ecto.create, ecto.migrate`
{% endhint %}

9\) Install Node.js dependencies

* `cd apps/block_scout_web/assets; npm install && node_modules/webpack/bin/webpack.js --mode production; cd -`
* `cd apps/explorer && npm install; cd -`

10\) Enable HTTPS in development. The Phoenix server only runs with HTTPS.

* `cd apps/block_scout_web`
* `mix phx.gen.cert blockscout blockscout.local; cd -`
* Add blockscout and blockscout.local to your `/etc/hosts`

```text
   127.0.0.1       localhost blockscout blockscout.local

   255.255.255.255 broadcasthost

   ::1             localhost blockscout blockscout.local
```

{% hint style="info" %}
If using Chrome, Enable `chrome://flags/#allow-insecure-localhost`
{% endhint %}

11\) Set your environment variables as needed.

CLI Example:

```text
export COIN=DAI
export NETWORK_ICON=_network_icon.html
export ... 
```

{% hint style="info" %}
The `ETHEREUM_JSONRPC_VARIANT` will vary depending on your client \(parity, geth etc\). [See this forum post](https://forum.poa.network/t/faq-what-settings-are-required-on-a-parity-or-geth-client/1805) for more information on client settings.
{% endhint %}

12\) Return to the root directory and start the Phoenix Server. `mix phx.server`

13\) [Check your instance](check-your-manual-deployment-instance.md)

## 

