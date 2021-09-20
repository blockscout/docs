# ENV Variables

{% hint style="info" %}
This table is horizontally scrollable, version information is located in the last column.
{% endhint %}

{% hint style="info" %}
Additional information related to certain variables is available on the [ansible deployment](../ansible-deployment/) page.
{% endhint %}

{% hint style="info" %}
You will find deprecated ENV vars in [Deprecated ENV Variables](https://docs.blockscout.com/for-developers/information-and-settings/deprecated-env-variables) chapter
{% endhint %}

* To set variables using the CLI, use the export command. For example:

  ```bash
  $ export ETHEREUM_JSONRPC_VARIANT=parity
  $ export COIN=POA
  $ export NETWORK=POA
  ```

{% file src="../../.gitbook/assets/blockscout-env.csv" caption="ENV Variables CSV \(7.21.2021\)" %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Required</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Default</th>
      <th style="text-align:left">Version</th>
      <th style="text-align:left">Need recompile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>NETWORK</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Environment variable for the main EVM network such as Ethereum or POA</td>
      <td
      style="text-align:left">POA</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SUBNETWORK</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Environment variable for the subnetwork such as Core or Sokol Network.
        This will be displayed as selected in the chains list dropdown.</td>
      <td
      style="text-align:left">POA Sokol</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>LOGO</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Environment variable for the header logo image location. The logo files
        names for different chains can be found <a href="https://github.com/poanetwork/blockscout/tree/master/apps/block_scout_web/assets/static/images">here</a>
      </td>
      <td style="text-align:left">/images/blockscout_logo.svg</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>LOGO_FOOTER</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Environment variable for the footer logo image location. The logo files
        names for different chains can be found <a href="https://github.com/poanetwork/blockscout/tree/master/apps/block_scout_web/assets/static/images">here</a>
      </td>
      <td style="text-align:left">/images/blockscout_logo.svg</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETHEREUM_JSONRPC_VARIANT</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Tells the application which RPC Client the node is using (i.e. <code>geth</code>, <code>parity</code>, <code>besu</code>,
        or <code>ganache</code>) (<a href="client-settings-parity-geth-ganache.md">See Client Settings for more info</a>)</td>
      <td
      style="text-align:left">parity</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETHEREUM_JSONRPC_HTTP_URL</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">The RPC endpoint used to fetch blocks, transactions, receipts, tokens.</td>
      <td
      style="text-align:left">localhost:8545</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETHEREUM_JSONRPC_TRACE_URL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The RPC endpoint specifically for the Geth/Parity/Besu client used by
        trace_block and trace_replayTransaction. This can be used to designate
        a tracing node.</td>
      <td style="text-align:left">localhost:8545</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETHEREUM_JSONRPC_WS_URL</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">The WebSockets RPC endpoint used to subscribe to the <code>newHeads</code> subscription
        alerting the indexer to fetch new blocks.</td>
      <td style="text-align:left">ws://localhost:8546</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETHEREUM_JSONRPC_TRANSPORT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Specifies the transport for Blockscout to connect to the Ethereum Node.
        Available transports are <code>http</code> and <code>ipc</code>. If <code>ipc</code> is
        selected, also set <code>IPC_PATH</code> variable</td>
      <td style="text-align:left">http</td>
      <td style="text-align:left">v3.1.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>IPC_PATH</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Path to the IPC file of the running node if IPC transport is chosen</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v2.1.1+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>NETWORK_PATH</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Used to set a network path other than what is displayed in the root directory.
        An example would be to add <code>/eth/mainnet/</code> to the root directory.</td>
      <td
      style="text-align:left">/</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>API_PATH</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">PATH in API endpoint URL at API docs page</td>
      <td style="text-align:left">/</td>
      <td style="text-align:left">v3.1.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SOCKET_ROOT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Custom websocket path</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.0.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BLOCKSCOUT_HOST</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Host for API endpoint examples</td>
      <td style="text-align:left">localhost</td>
      <td style="text-align:left">v2.1.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BLOCKSCOUT_PROTOCOL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Url scheme for blockscout</td>
      <td style="text-align:left">in prod env <code>https</code> is used, in dev env <code>http</code> is used</td>
      <td
      style="text-align:left">v2.1.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SECRET_KEY_BASE</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Use mix phx.gen.secret to generate a new Secret Key Base string to protect
        production assets.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHECK_ORIGIN</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Used to check the origin of requests when the origin header is present.
        It defaults to <code>false</code>. In case of true, it will check against
        the host value.</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>PORT</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Default port the application runs on is 4000</td>
      <td style="text-align:left">4000</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>COIN</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">The coin here is checked via the CoinGecko API to obtain USD prices on
        graphs and other areas of the UI</td>
      <td style="text-align:left">POA</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>COINGECKO_COIN_ID</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Explicitly set CoinGecko coin ID</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>METADATA_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This environment variable is specifically used by POA Network to obtain
        Validators information to display in the UI.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>VALIDATORS_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This environment variable is specifically used by POA Network to obtain
        the list of current validators.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>KEYS_MANAGER_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This environment variable is specifically used by POA Network to set KeysManager
        proxy contract in order to obtain payout key by mining key. This needs
        to identify distributed reward to the validator.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>REWARDS_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Emission rewards contract address. This env var is used only if <code>EMISSION_FORMAT</code> is
        set to <code>POA</code>
      </td>
      <td style="text-align:left"><code>0xeca443e8e1ab29971a45a9c57a6a9875701698a5</code>
      </td>
      <td style="text-align:left">v2.0.4+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN_BRIDGE_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Token bridge proxy contract. For `TokenBridge` supply module.</td>
      <td
      style="text-align:left"><code>0x7301CFA0e1756B71869E93d4e4Dca5c7d0eb0AA6</code>
        </td>
        <td style="text-align:left">v1.3.2+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>EMISSION_FORMAT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Should be set to <code>POA</code> if you have block emission identical to
        POA Network. This env var is used only if <code>CHAIN_SPEC_PATH</code> is
        set</td>
      <td style="text-align:left"><code>DEFAULT</code>
      </td>
      <td style="text-align:left">v2.0.4+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHAIN_SPEC_PATH</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Chain specification path (absolute file system path or URL) to import
        block emission reward ranges and genesis account balances from. Geth- and
        OpenEthereum-style specs are supported.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v2.0.4+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SUPPLY_MODULE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This environment variable is used by the xDai Chain/RSK in order to tell
        the application how to calculate the total supply of the chain. Available
        values are <code>TokenBridge</code>, <code>RSK</code>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SOURCE_MODULE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">This environment variable is used to calculate the exchange rate and is
        specifically used by the xDai Chain. Available value is <code>TokenBridge</code>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DATABASE_URL</code>
      </td>
      <td style="text-align:left">&#x2705;</td>
      <td style="text-align:left">Variable to define the Database endpoint.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>POOL_SIZE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Production environment variable to define the number of database connections
        allowed.</td>
      <td style="text-align:left">20</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ECTO_USE_SSL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Production environment variable to use SSL on Ecto queries.</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DATADOG_HOST</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Host configuration setting for <a href="https://docs.datadoghq.com/integrations/">Datadog integration</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DATADOG_PORT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Port configuration setting for <a href="https://docs.datadoghq.com/integrations/">Datadog integration</a>.</td>
      <td
      style="text-align:left">(empty}</td>
        <td style="text-align:left">all</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SPANDEX_BATCH_SIZE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/spandex-project/spandex">Spandex</a> and Datadog
        configuration setting.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SPANDEX_SYNC_THRESHOLD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/spandex-project/spandex">Spandex</a> and Datadog
        configuration setting.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>HEART_BEAT_TIMEOUT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Production environment variable to restart the application in the event
        of a crash.</td>
      <td style="text-align:left">30</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>HEART_COMMAND</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Production environment variable to restart the application in the event
        of a crash.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BLOCKSCOUT_VERSION</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Added to the footer to signify the current BlockScout version.</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v1.3.4+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RELEASE_LINK</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The link to Blockscout release notes in the footer.</td>
      <td style="text-align:left">https: //github.com/poanetwork/ blockscout/releases/ tag/${BLOCKSCOUT_VERSION}</td>
      <td
      style="text-align:left">v1.3.5+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ELIXIR_VERSION</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Elixir version to install on the node before Blockscout deploy. It is
        used in bash script in Terraform / Ansible deployment script</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">all</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BLOCK_TRANSFORMER</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Transformer for blocks: base or clique.</td>
      <td style="text-align:left">base</td>
      <td style="text-align:left">v1.3.4+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>GRAPHIQL_TRANSACTION</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Default transaction hash in a sample query to GraphiQL.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v1.2.0+</td>
      <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FIRST_BLOCK</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The block number, where indexing begins from.</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">v1.3.8+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>LAST_BLOCK</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The block number, where indexing stops.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v2.0.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>LINK_TO_OTHER_EXPLORERS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">true/false. If true, links to other explorers are added in the footer</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v1.3.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>OTHER_EXPLORERS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The list of alternative explorers. This env var was introduced in PR
        <a
        href="https://github.com/poanetwork/blockscout/pull/3414">#3414</a>.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SUPPORTED_CHAINS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An array of supported chains that display in the footer and in the chains
        dropdown. This var was introduced in this PR <a href="https://github.com/poanetwork/blockscout/pull/1900">#1900</a> and
        looks like an array of JSON objects.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v2.0.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BLOCK_COUNT_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">time to live of blocks with consensus count cache in seconds. This var
        was introduced in <a href="https://github.com/poanetwork/blockscout/pull/1876">#1876</a>
      </td>
      <td style="text-align:left">2 hours</td>
      <td style="text-align:left">v2.0.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TXS_COUNT_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates the total txs
        count.</td>
      <td style="text-align:left">2 hours</td>
      <td style="text-align:left">v1.3.9+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_COUNT_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">time to live of cache in seconds. This var was introduced in <a href="https://github.com/poanetwork/blockscout/pull/2822">#2822</a>
      </td>
      <td style="text-align:left">2 hours</td>
      <td style="text-align:left">v2.1.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_SUM_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">time to live of addresses sum (except burn address) cache in seconds.
        This var was introduced in <a href="https://github.com/poanetwork/blockscout/pull/2862">#2862</a>
      </td>
      <td style="text-align:left">1 hour</td>
      <td style="text-align:left">v2.1.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOTAL_GAS_USAGE_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates the total gas
        usage.</td>
      <td style="text-align:left">2 hours</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_TRANSACTIONS_GAS_USAGE_COUNTER_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates gas usage at
        the address.</td>
      <td style="text-align:left">30 minutes</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN_HOLDERS_COUNTER_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates holders count
        of the token.</td>
      <td style="text-align:left">1 hour</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN_TRANSFERS_COUNTER_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates transfers count
        of the token.</td>
      <td style="text-align:left">1 hour</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_WITH_BALANCES_UPDATE_INTERVAL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task, which calculates addresses with
        balances.</td>
      <td style="text-align:left">30 minutes</td>
      <td style="text-align:left">v1.3.9+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN_METADATA_UPDATE_INTERVAL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in seconds to restart the task which updates token metadata</td>
      <td
      style="text-align:left">60 * 60 * 24 <em>*</em> 2</td>
        <td style="text-align:left">v2.0.1+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>AVERAGE_BLOCK_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Update of average block period cache, in seconds</td>
      <td style="text-align:left">30 minutes</td>
      <td style="text-align:left">v2.0.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MARKET_HISTORY_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Update of market history cache, in seconds</td>
      <td style="text-align:left">6 hours</td>
      <td style="text-align:left">v2.0.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ALLOWED_EVM_VERSIONS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">the comma-separated list of allowed EVM versions for contract verification.
        This var was introduced in <a href="https://github.com/poanetwork/blockscout/pull/1964">#1964</a>
      </td>
      <td style="text-align:left">&quot;homestead, tangerineWhistle, spuriousDragon, byzantium, constantinople,
        petersburg&quot;</td>
      <td style="text-align:left">v2.0.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>UNCLES_IN_AVERAGE_BLOCK_TIME</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Include or exclude non-consensus blocks in avg block time calculation.
        Exclude if <code>false</code>.</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v2.0.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_WEBAPP</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If <code>true</code>, endpoints to webapp are hidden (compile-time). Also,
        enabling it makes notifications go through <code>db_notify</code>
      </td>
      <td style="text-align:left"><code>false</code>
      </td>
      <td style="text-align:left">v2.0.3+</td>
      <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_READ_API</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If <code>true</code>, read-only endpoints to API are hidden (compile-time)</td>
      <td
      style="text-align:left"><code>false</code>
        </td>
        <td style="text-align:left">v2.0.3+</td>
        <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_WRITE_API</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If <code>true</code>, write endpoints to API are hidden (compile-time)</td>
      <td
      style="text-align:left"><code>false</code>
        </td>
        <td style="text-align:left">v2.0.3+</td>
        <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_INDEXER</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If <code>true</code>, indexer application doesn&apos;t run</td>
      <td style="text-align:left"><code>false</code>
      </td>
      <td style="text-align:left">v2.0.3+</td>
      <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>WEBAPP_URL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Link to web application instance, e.g. <code>protocol://host/path</code>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v2.0.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>API_URL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Link to API instance, e.g. <code>protocol://host/path</code>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v2.0.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>WOBSERVER_ENABLED</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If <code>true</code> enables wobserver interface</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.2+</td>
      <td style="text-align:left">&#x2705;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_ADDRESS_MARKETCAP_PERCENTAGE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Configures market cap percentage column on the top accounts page</td>
      <td
      style="text-align:left"><code>true</code>
        </td>
        <td style="text-align:left">v2.1.1+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHECKSUM_ADDRESS_HASHES</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">If set to <code>true</code>, redirects to checksummed version of address
        hashes</td>
      <td style="text-align:left">true</td>
      <td style="text-align:left">v3.1.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHECKSUM_FUNCTION</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Defines checksum address function. 2 available values: <code>rsk</code>, <code>eth</code>
      </td>
      <td style="text-align:left">eth</td>
      <td style="text-align:left">v2.0.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_EXCHANGE_RATES</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables or enables fetching of coin price from Coingecko API</td>
      <td
      style="text-align:left">false</td>
        <td style="text-align:left">v3.1.2+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_KNOWN_TOKENS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables or enables token symbol for known contract</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ENABLE_TXS_STATS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables or enables txs per day stats gathering</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_PRICE_CHART</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables or enables price and market cap of coin charts on the main page</td>
      <td
      style="text-align:left">false</td>
        <td style="text-align:left">v3.1.2+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_TXS_CHART</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables or enables txs count per day chart on the main page</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>HISTORY_FETCH_INTERVAL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Interval in minutes how often to request count of txs per current day
        in order to display txs count per day chart on the main page</td>
      <td style="text-align:left">60</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TXS_HISTORIAN_INIT_LAG</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The initial delay in minutes in txs count history fetching in order to
        display txs count per day history chart on the main page</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">v3.1.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TXS_STATS_DAYS_TO_COMPILE_AT_INIT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Number of days for fetching of history of txs count per day in order to
        display it in txs count per day history chart on the main page</td>
      <td
      style="text-align:left">365</td>
        <td style="text-align:left">v3.1.2+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>COIN_BALANCE_HISTORY_DAYS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Number of days to consider at coin balance history chart</td>
      <td style="text-align:left">10</td>
      <td style="text-align:left">v3.1.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>APPS_MENU</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">true/false. If true, the Apps navigation menu item appears</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.3.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>EXTERNAL_APPS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An array of external apps to display in Apps menu item. This var was introduced
        in this PR <a href="https://github.com/poanetwork/blockscout/pull/3184">#3184</a> and
        looks like an array of JSON objects.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ETH_OMNI_BRIDGE_MEDIATOR</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An address of home OmniBridge mediator to bridge multiple tokens from
        Ethereum. Providing this address enables bridged tokens functionality:
        bridged status and link to the original token in the foreign chain.</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v3.6.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BSC_OMNI_BRIDGE_MEDIATOR</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">An address of home OmniBridge mediator to bridge multiple tokens from
        Binance Smart Chain. Providing this address enables bridged tokens functionality:
        bridged status and link to the original token in the foreign chain.</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v3.6.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>AMB_BRIDGE_MEDIATORS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A comma-separated list of AMB extensions&apos; mediators&apos; addresses&apos;
        hashes to fetch bridged tokens through those mediators.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>GAS_PRICE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Gas price in Gwei. If the variable is present, gas price displays on the
        main page</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.2+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FOREIGN_JSON_RPC</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">JSON RPC endpoint to the foreign chain in order to get metadata of bridged
        through Omni-bridge token. It was introduced in this PR <a href="https://github.com/poanetwork/blockscout/pull/3282">#3282</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BRIDGE_MARKET_CAP_UPDATE_INTERVAL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Market cap update interval for `TokenBridge` supply module as for TokenBridge
        and for OmniBridge as well, in seconds. It was introduced in this PR
        <a
        href="https://github.com/poanetwork/blockscout/pull/3293">#3293</a>
      </td>
      <td style="text-align:left">30 minutes</td>
      <td style="text-align:left">v3.3.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RESTRICTED_LIST</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A comma-separated list of addresses to enable restricted access to them</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v3.3.3+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>RESTRICTED_LIST_KEY</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">A key to access addresses listed in<code>RESTRICTED_LIST</code> variable.
        Can be passed via query param to the page&apos;s URL: <code>?key=...</code>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_TRANSACTIONS_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">time to live of address&apos; transactions counter in seconds. This var
        was introduced in <a href="https://github.com/poanetwork/blockscout/pull/3330">#3330</a>
      </td>
      <td style="text-align:left">1 hour</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISABLE_BRIDGE_MARKET_CAP_UPDATER</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables recurring consolidation of TokenBridge market cap from TokenBridge,
        OmniBridge and AMB extensions</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.3.3+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>POS_STAKING_CONTRACT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The address of POSDAO staking contract. When provided, enables staking
        DApp. ValidatorSet and BlockReward contract addresses are fetched using
        corresponding getters.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.4.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ENABLE_POS_STAKING_IN_MENU</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Enables Staking dapp in the menu</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TOKEN_EXCHANGE_RATE_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Managing cache invalidation for token&apos;s exchange rate.</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.5.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ADDRESS_TOKENS_USD_SUM_CACHE_PERIOD</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Managing of cache invalidation period for the sum of USD value of tokens
        per tokens&apos; holder address</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.5.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_MAINTENANCE_ALERT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables/enables announcement at the top of the explorer</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAINTENANCE_ALERT_MESSAGE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Message text of the announcement at the top of the explorer</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_STAKING_WARNING</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Disables/enables announcement inside staking dapp</td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>STAKING_WARNING_MESSAGE</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Message text of the announcement inside staking dapp</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CUSTOM_CONTRACT_ADDRESSES_TEST_TOKEN</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">List of test tokens addresses: test label will be applied and those tokens
        will be excluded from omni bridge market cap calculation</td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">v3.6.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ENABLE_SOURCIFY_INTEGRATION</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Enables or disables verification of contracts through Sourcify</td>
      <td
      style="text-align:left">false</td>
        <td style="text-align:left">v3.7.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SOURCIFY_SERVER_URL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">URL to Sourcify backend</td>
      <td style="text-align:left"><a href="https://sourcify.dev/server">https://sourcify.dev/server</a>
      </td>
      <td style="text-align:left">v3.7.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SOURCIFY_REPO_URL</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">URL to Sourcify repository with fully verified contracts</td>
      <td style="text-align:left">
        <p><a href="https://repo.sourcify.dev/contracts/">https://repo.sourcify.dev/contracts/</a>*</p>
        <p></p>
        <p>*before 3.7.1 <a href="https://repo.sourcify.dev/contracts/full_match/">https://repo.sourcify.dev/contracts/full_match/</a>
        </p>
      </td>
      <td style="text-align:left">v3.7.0+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>CHAIN_ID</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Chain ID of the network. For instance, 100 in the case of xDai chain.</td>
      <td
      style="text-align:left">(empty)</td>
        <td style="text-align:left">v3.7.0+</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>MAX_SIZE_UNLESS_HIDE_ARRAY</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Hide long arrays in smart-contracts. To get more details: <a href="https://github.com/blockscout/blockscout/pull/4218">#4218</a>
      </td>
      <td style="text-align:left">50</td>
      <td style="text-align:left">v3.7.1+</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ENABLE_1559_SUPPORT</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Enables store and display of additional fields on block and transaction
        according to <a href="https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1559.md">EIP-1559</a>
      </td>
      <td style="text-align:left">false</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>HIDE_BLOCK_MINER</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Hides miner/validator/sequencer on block page and tiles if the value is
        `true` Implemented in <a href="https://github.com/blockscout/blockscout/pull/4611">#4611</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>DISPLAY_TOKEN_ICONS</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Displays token icons from TrustWallet assets repository if <code>true</code>.
        Implemented in <a href="https://github.com/blockscout/blockscout/pull/4596">#4596</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>SHOW_TENDERLY_LINK</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">if <code>true</code>, &quot;Open in Tenderly&quot; button is displayed
        on the transaction page. Implemented in <a href="https://github.com/blockscout/blockscout/pull/4656">#4656</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>TENDERLY_CHAIN_PATH</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Chain path to the transaction in Tenderly. For instance, for transactions
        in xDai, Tenderly link looks like this https://dashboard.tenderly.co/tx/xdai/0x...,
        then <code>TENDERLY_CHAIN_PATH =/xdai. </code>Implemented in <a href="https://github.com/blockscout/blockscout/pull/4656">#4656</a>
      </td>
      <td style="text-align:left">(empty)</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
	 <tr>
      <td style="text-align:left"><code>MAX_STRING_LENGTH_WITHOUT_TRIMMING</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Hide long contract method data. For more details: <a href="https://github.com/blockscout/blockscout/pull/4667">#4667</a>
      </td>
      <td style="text-align:left">2040</td>
      <td style="text-align:left">master</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>



