# ENVs

The app instance can be customized by passing the following variables to the Node.js environment at runtime. Some of these variables have been deprecated, and their full list can be found in the [file](DEPRECATED_ENVS.md).

## Read before you run the app

### Variables compulsoriness

Please note that in the tables below, the "Compulsoriness" column indicates whether the variable is required for starting up the application, except for the "App Features" section. All features are optional by definition; therefore, the "Compulsoriness" column indicates whether a certain variable is required or optional only within the context of that feature, not for the entire application.

### Disclaimer about using variables

Please be aware that all environment variables prefixed with `NEXT_PUBLIC_` will be exposed to the browser. So any user can obtain its values. Make sure that for all 3rd-party services keys (e.g., Auth0, WalletConnect, etc.) in the services administration panel you have created a whitelist of allowed origins and have added your app domain into it. That will help you prevent using your key by unauthorized app, if someone gets its value.

### Note about escaping variables values

All json-like values should be single-quoted. If it contains a hash (`#`) or a dollar-sign (`$`) the whole value should be wrapped in single quotes as well (see `dotenv` [readme](https://github.com/bkeepers/dotenv#variable-substitution) for the reference)

&#x20;

## Table of contents

* [App configuration](envs.md#app-configuration)
* [Blockchain parameters](envs.md#blockchain-parameters)
* [API configuration](envs.md#api-configuration)
* [UI configuration](envs.md#ui-configuration)
  * [Homepage](envs.md#homepage)
  * [Navigation](envs.md#navigation)
  * [Footer](envs.md#footer)
  * [Favicon](envs.md#favicon)
  * [Meta](envs.md#meta)
  * [Views](envs.md#views)
    * [Block](envs.md#block-views)
    * [Address](envs.md#address-views)
    * [Transaction](envs.md#transaction-views)
    * [NFT](envs.md#nft-views)
  * [Misc](envs.md#misc)
* [App features](envs.md#app-features)
  * [My account](envs.md#my-account)
  * [Gas tracker](envs.md#gas-tracker)
  * [Advanced filter](envs.md#advanced-filter)
  * [Address verification](envs.md#address-verification-in-my-account) in "My account"
  * [Blockchain interaction](envs.md#blockchain-interaction-writing-to-contract-etc) (writing to contract, etc.)
  * [Banner ads](envs.md#banner-ads)
  * [Text ads](envs.md#text-ads)
  * [Beacon chain](envs.md#beacon-chain)
  * [User operations](envs.md#user-operations-erc-4337)
  * [Rollup chain](envs.md#rollup-chain)
  * [Export data to CSV file](envs.md#export-data-to-csv-file)
  * [Google analytics](envs.md#google-analytics)
  * [Mixpanel analytics](envs.md#mixpanel-analytics)
  * [GrowthBook feature flagging and A/B testing](envs.md#growthbook-feature-flagging-and-ab-testing)
  * [GraphQL API documentation](envs.md#graphql-api-documentation)
  * [REST API documentation](envs.md#rest-api-documentation)
  * [Marketplace](envs.md#marketplace)
  * [Solidity to UML diagrams](envs.md#solidity-to-uml-diagrams)
  * [Blockchain statistics](envs.md#blockchain-statistics)
  * [Web3 wallet integration](envs.md#web3-wallet-integration-add-token-or-network-to-the-wallet) (add token or network to the wallet)
  * [Transaction interpretation](envs.md#transaction-interpretation)
  * [Verified tokens info](envs.md#verified-tokens-info)
  * [Name service integration](envs.md#name-service-integration)
  * [Metadata service integration](envs.md#metadata-service-integration)
  * [Public tag submission](envs.md#public-tag-submission)
  * [Data availability](envs.md#data-availability)
  * [Bridged tokens](envs.md#bridged-tokens)
  * [Safe{Core} address tags](envs.md#safecore-address-tags)
  * [Address profile API](envs.md#address-profile-api)
  * [Address XStar XHS score](envs.md#address-xstar-xhs-score)
  * [SUAVE chain](envs.md#suave-chain)
  * [Celo chain](envs.md#celo-chain)
  * [Ton Application Chain (TAC)](envs.md#ton-application-chain-tac)
  * [MetaSuites extension](envs.md#metasuites-extension)
  * [Validators list](envs.md#validators-list)
  * [Sentry error monitoring](envs.md#sentry-error-monitoring)
  * [Rollbar error monitoring](envs.md#rollbar-error-monitoring)
  * [OpenTelemetry](envs.md#opentelemetry)
  * [DeFi dropdown](envs.md#defi-dropdown)
  * [Multichain balance button](envs.md#multichain-balance-button)
  * [Get gas button](envs.md#get-gas-button)
  * [Save on gas with GasHawk](envs.md#save-on-gas-with-gashawk)
  * [Rewards service API](envs.md#rewards-service-api)
  * [DEX pools](envs.md#dex-pools)
* [3rd party services configuration](envs.md#external-services-configuration)

&#x20;

## App configuration

| Variable                           | Type            | Description                                                                                                                                                                                      | Compulsoriness | Default value | Example value      | Version |
| ---------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | ------------- | ------------------ | ------- |
| NEXT\_PUBLIC\_APP\_PROTOCOL        | `http \| https` | App url schema                                                                                                                                                                                   | -              | `https`       | `http`             | v1.0.x+ |
| NEXT\_PUBLIC\_APP\_HOST            | `string`        | App host                                                                                                                                                                                         | Required       | -             | `blockscout.com`   | v1.0.x+ |
| NEXT\_PUBLIC\_APP\_PORT            | `number`        | Port where app is running                                                                                                                                                                        | -              | `3000`        | `3001`             | v1.0.x+ |
| NEXT\_PUBLIC\_APP\_ENV             | `string`        | App env (e.g development, staging, production, etc.).                                                                                                                                            | -              | `production`  | `staging`          | v1.0.x+ |
| NEXT\_PUBLIC\_APP\_INSTANCE        | `string`        | Name of app instance. Used for app monitoring purposes. If not provided, it will be constructed from `NEXT_PUBLIC_APP_HOST`                                                                      | -              | -             | `wonderful_kepler` | v1.0.x+ |
| NEXT\_PUBLIC\_USE\_NEXT\_JS\_PROXY | `boolean`       | Tells the app to proxy all APIs request through the NextJS app. **We strongly advise not to use it in the production environment**, since it can lead to performance issues of the NodeJS server | -              | `false`       | `true`             | v1.8.0+ |

&#x20;

## Blockchain parameters

_Note!_ The `NEXT_PUBLIC_NETWORK_CURRENCY` variables represent the blockchain's native token used for paying transaction fees. `NEXT_PUBLIC_NETWORK_SECONDARY_COIN` variables refer to tokens like protocol-specific tokens (e.g., OP token on Optimism chain) or governance tokens (e.g., GNO on Gnosis chain).

| Variable                                         | Type                      | Description                                                                                                                                                | Compulsoriness | Default value | Example value              | Version  |
| ------------------------------------------------ | ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | -------------------------- | -------- |
| NEXT\_PUBLIC\_NETWORK\_NAME                      | `string`                  | Displayed name of the network                                                                                                                              | Required       | -             | `Gnosis Chain`             | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_SHORT\_NAME               | `string`                  | Used for SEO attributes (e.g, page description)                                                                                                            | -              | -             | `OoG`                      | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_ID                        | `number`                  | Chain id, see [https://chainlist.org](https://chainlist.org) for the reference                                                                             | Required       | -             | `99`                       | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_RPC\_URL                  | `string \| Array<string>` | Chain public RPC server url, see [https://chainlist.org](https://chainlist.org) for the reference. Can contain a single string value, or an array of urls. | -              | -             | `https://core.poa.network` | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_NAME            | `string`                  | Network currency name                                                                                                                                      | -              | -             | `Ether`                    | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_WEI\_NAME       | `string`                  | Name of network currency subdenomination                                                                                                                   | -              | `wei`         | `duck`                     | v1.23.0+ |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_SYMBOL          | `string`                  | Network currency symbol                                                                                                                                    | -              | -             | `ETH`                      | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_DECIMALS        | `string`                  | Network currency decimals                                                                                                                                  | -              | `18`          | `6`                        | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_SECONDARY\_COIN\_SYMBOL   | `string`                  | Network secondary coin symbol.                                                                                                                             | -              | -             | `GNO`                      | v1.29.0+ |
| NEXT\_PUBLIC\_NETWORK\_MULTIPLE\_GAS\_CURRENCIES | `boolean`                 | Set to `true` for networks where users can pay transaction fees in either the native coin or ERC-20 tokens.                                                | -              | `false`       | `true`                     | v1.33.0+ |
| NEXT\_PUBLIC\_NETWORK\_VERIFICATION\_TYPE        | `validation` \| `mining`  | Verification type in the network. Irrelevant for Arbitrum (verification type is always `posting`) and ZkEvm (verification type is always `sequencing`) L2s | -              | `mining`      | `validation`               | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_TOKEN\_STANDARD\_NAME     | `string`                  | Name of the standard for creating tokens                                                                                                                   | -              | `ERC`         | `BEP`                      | v1.31.0+ |
| NEXT\_PUBLIC\_IS\_TESTNET                        | `boolean`                 | Set to true if network is testnet                                                                                                                          | -              | `false`       | `true`                     | v1.0.x+  |

&#x20;

## API configuration

| Variable                               | Type            | Description                           | Compulsoriness | Default value | Example value    | Version |
| -------------------------------------- | --------------- | ------------------------------------- | -------------- | ------------- | ---------------- | ------- |
| NEXT\_PUBLIC\_API\_PROTOCOL            | `http \| https` | Main API protocol                     | -              | `https`       | `http`           | v1.0.x+ |
| NEXT\_PUBLIC\_API\_HOST                | `string`        | Main API host                         | Required       | -             | `blockscout.com` | v1.0.x+ |
| NEXT\_PUBLIC\_API\_PORT                | `number`        | Port where API is running on the host | -              | -             | `3001`           | v1.0.x+ |
| NEXT\_PUBLIC\_API\_BASE\_PATH          | `string`        | Base path for Main API endpoint url   | -              | -             | `/poa/core`      | v1.0.x+ |
| NEXT\_PUBLIC\_API\_WEBSOCKET\_PROTOCOL | `ws \| wss`     | Main API websocket protocol           | -              | `wss`         | `ws`             | v1.0.x+ |

&#x20;

## UI configuration

### Homepage

| Variable                                     | Type                                                                                                                                                                                                             | Description                                                                                                                                                                                          | Compulsoriness | Default value                                                                                                                                                                                                                       | Example value                                                                                                                                      | Version  |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_HOMEPAGE\_CHARTS               | `Array<'daily_txs' \| 'daily_operational_txs' \| 'coin_price' \| 'secondary_coin_price' \| 'market_cap' \| 'tvl'>`                                                                                               | List of charts displayed on the home page                                                                                                                                                            | -              | -                                                                                                                                                                                                                                   | `['daily_txs','coin_price','market_cap']`                                                                                                          | v1.0.x+  |
| NEXT\_PUBLIC\_HOMEPAGE\_STATS                | `Array<'latest_batch' \| 'total_blocks' \| 'average_block_time' \| 'total_txs' \| 'total_operational_txs' \| 'latest_l1_state_batch' \| 'wallet_addresses' \| 'gas_tracker' \| 'btc_locked' \| 'current_epoch'>` | List of stats widgets displayed on the home page                                                                                                                                                     | -              | For zkSync, zkEvm and Arbitrum rollups: `['latest_batch','average_block_time','total_txs','wallet_addresses','gas_tracker']`, for other cases: `['total_blocks','average_block_time','total_txs','wallet_addresses','gas_tracker']` | `['total_blocks','total_txs','wallet_addresses']`                                                                                                  | v1.35.x+ |
| NEXT\_PUBLIC\_HOMEPAGE\_PLATE\_TEXT\_COLOR   | `string`                                                                                                                                                                                                         | Text color of the hero plate on the homepage (escape "#" symbol if you use HEX color codes or use rgba-value instead). **DEPRECATED** _Use `NEXT_PUBLIC_HOMEPAGE_HERO_BANNER_CONFIG` instead_        | -              | `white`                                                                                                                                                                                                                             | `\#DCFE76`                                                                                                                                         | v1.0.x+  |
| NEXT\_PUBLIC\_HOMEPAGE\_PLATE\_BACKGROUND    | `string`                                                                                                                                                                                                         | Background css value for hero plate on the homepage (escape "#" symbol if you use HEX color codes or use rgba-value instead). **DEPRECATED** _Use `NEXT_PUBLIC_HOMEPAGE_HERO_BANNER_CONFIG` instead_ | -              | `radial-gradient(103.03% 103.03% at 0% 0%, rgba(183, 148, 244, 0.8) 0%, rgba(0, 163, 196, 0.8) 100%), var(--chakra-colors-blue-400)`                                                                                                | `radial-gradient(at 15% 86%, hsla(350,65%,70%,1) 0px, transparent 50%)` \| `no-repeat bottom 20% right 0px/100% url(https://placekitten/1400/200)` | v1.1.0+  |
| NEXT\_PUBLIC\_HOMEPAGE\_HERO\_BANNER\_CONFIG | `HeroBannerConfig`, see details [below](envs.md#hero-banner-configuration-properties)                                                                                                                            | Configuration of hero banner appearance.                                                                                                                                                             | -              | -                                                                                                                                                                                                                                   | See [below](envs.md#hero-banner-configuration-properties)                                                                                          | v1.35.0+ |

#### Hero banner configuration properties

_Note_ Here, all values are arrays of up to two strings. The first string represents the value for the light color mode, and the second string represents the value for the dark color mode. If the array contains only one string, it will be used for both color modes.

| Variable    | Type                                                                                                                        | Description                                                                                                                                                                                       | Compulsoriness | Default value                                                                                                                            | Example value                                                                           |
| ----------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| background  | `[string, string]`                                                                                                          | Banner background (could be a solid color, gradient or picture). The string should be a valid `background` CSS property value.                                                                    | -              | `['radial-gradient(103.03% 103.03% at 0% 0%, rgba(183, 148, 244, 0.8) 0%, rgba(0, 163, 196, 0.8) 100%), var(--chakra-colors-blue-400)']` | `['lightpink','no-repeat bottom 20% right 0px/100% url(https://placekitten/1400/200)']` |
| text\_color | `[string, string]`                                                                                                          | Banner text background. The string should be a valid `color` CSS property value.                                                                                                                  | -              | `['white']`                                                                                                                              | `['lightpink','#DCFE76']`                                                               |
| border      | `[string, string]`                                                                                                          | Banner border. The string should be a valid `border` CSS property value.                                                                                                                          | -              | -                                                                                                                                        | `['1px solid yellow','4px dashed #DCFE76']`                                             |
| button      | `Partial<Record<'_default' \| '_hover' \| '_selected', {'background'?: [string, string]; 'text_color?:[string, string]'}>>` | The button on the banner. It has three possible states: `_default`, `_hover`, and `_selected`. The `_selected` state reflects when the user is logged in or their wallet is connected to the app. | -              | -                                                                                                                                        | `{'_default':{'background':['deeppink'],'text_color':['white']}}`                       |

&#x20;

### Navigation

| Variable                                      | Type                                 | Description                                                                                                                                                                                                                                                                             | Compulsoriness | Default value | Example value                                                                                                                                                                     | Version  |
| --------------------------------------------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_NETWORK\_LOGO                   | `string`                             | Network logo; if not provided, placeholder will be shown; _Note_ the logo height should be 24px and width less than 120px                                                                                                                                                               | -              | -             | `https://placekitten.com/240/40`                                                                                                                                                  | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_LOGO\_DARK             | `string`                             | Network logo for dark color mode; if not provided, **inverted** regular logo will be used instead                                                                                                                                                                                       | -              | -             | `https://placekitten.com/240/40`                                                                                                                                                  | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_ICON                   | `string`                             | Network icon; used as a replacement for regular network logo when nav bar is collapsed; if not provided, placeholder will be shown; _Note_ the icon size should be at least 60px by 60px                                                                                                | -              | -             | `https://placekitten.com/60/60`                                                                                                                                                   | v1.0.x+  |
| NEXT\_PUBLIC\_NETWORK\_ICON\_DARK             | `string`                             | Network icon for dark color mode; if not provided, **inverted** regular icon will be used instead                                                                                                                                                                                       | -              | -             | `https://placekitten.com/60/60`                                                                                                                                                   | v1.0.x+  |
| NEXT\_PUBLIC\_FEATURED\_NETWORKS              | `string`                             | URL of configuration file (`.json` format only) or file content string representation. It contains list of featured networks that will be shown in the network menu. See [below](envs.md#featured-network-configuration-properties) list of available properties for particular network | -              | -             | `https://example.com/featured_networks_config.json` \| `[{'title':'Astar(EVM)','url':'https://astar.blockscout.com/','group':'Mainnets','icon':'https://example.com/astar.svg'}]` | v1.0.x+  |
| NEXT\_PUBLIC\_OTHER\_LINKS                    | `Array<{url: string; text: string}>` | List of links for the "Other" navigation menu                                                                                                                                                                                                                                           | -              | -             | `[{'url':'https://blockscout.com','text':'Blockscout'}]`                                                                                                                          | v1.0.x+  |
| NEXT\_PUBLIC\_NAVIGATION\_HIDDEN\_LINKS       | `Array<LinkId>`                      | List of external links hidden in the navigation. Supported ids are `eth_rpc_api`, `rpc_api`                                                                                                                                                                                             | -              | -             | `['eth_rpc_api']`                                                                                                                                                                 | v1.16.0+ |
| NEXT\_PUBLIC\_NAVIGATION\_HIGHLIGHTED\_ROUTES | `Array<string>`                      | List of menu item routes that should have a lightning label                                                                                                                                                                                                                             | -              | -             | `['/accounts']`                                                                                                                                                                   | v1.31.0+ |
| NEXT\_PUBLIC\_NAVIGATION\_LAYOUT              | `vertical \| horizontal`             | Navigation menu layout type                                                                                                                                                                                                                                                             | -              | `vertical`    | `horizontal`                                                                                                                                                                      | v1.32.0+ |

#### Featured network configuration properties

| Variable             | Type                            | Description                                                                                                                | Compulsoriness | Default value | Example value                         |
| -------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------- |
| title                | `string`                        | Displayed name of the network                                                                                              | Required       | -             | `Gnosis Chain`                        |
| url                  | `string`                        | Network explorer main page url                                                                                             | Required       | -             | `https://blockscout.com/xdai/mainnet` |
| group                | `Mainnets \| Testnets \| Other` | Indicates in which tab network appears in the menu                                                                         | Required       | -             | `Mainnets`                            |
| icon                 | `string`                        | Network icon; if not provided, the common placeholder will be shown; _Note_ that icon size should be at least 60px by 60px | -              | -             | `https://placekitten.com/60/60`       |
| isActive             | `boolean`                       | Pass `true` if item should be shown as active in the menu                                                                  | -              | -             | `true`                                |
| invertIconInDarkMode | `boolean`                       | Pass `true` if icon colors should be inverted in dark mode                                                                 | -              | -             | `true`                                |

&#x20;

### Footer

| Variable                    | Type     | Description                                                                                                                                                                                                                                                        | Compulsoriness | Default value | Example value                                                                                                                                                                                    | Version |
| --------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| NEXT\_PUBLIC\_FOOTER\_LINKS | `string` | URL of configuration file (`.json` format only) or file content string representation. It contains list of link groups to be displayed in the footer. See [below](envs.md#footer-links-configuration-properties) list of available properties for particular group | -              | -             | `https://example.com/footer_links_config.json` \| `[{'title':'My chain','links':[{'text':'About','url':'https://example.com/about'},{'text':'Contacts','url':'https://example.com/contacts'}]}]` | v1.1.1+ |

The app version shown in the footer is derived from build-time ENV variables `NEXT_PUBLIC_GIT_TAG` and `NEXT_PUBLIC_GIT_COMMIT_SHA` and cannot be overwritten at run-time.

#### Footer links configuration properties

| Variable | Type                                   | Description         | Compulsoriness | Default value | Example value                                              |
| -------- | -------------------------------------- | ------------------- | -------------- | ------------- | ---------------------------------------------------------- |
| title    | `string`                               | Title of link group | Required       | -             | `Company`                                                  |
| links    | `Array<{'text':string;'url':string;}>` | list of links       | Required       | -             | `[{'text':'Homepage','url':'https://www.blockscout.com'}]` |

&#x20;

### Favicon

By default, the app has generic favicon. You can override this behavior by providing the following variable. Hence, the favicon assets bundle will be generated at the container start time and will be used instead of default one.

| Variable             | Type     | Description | Compulsoriness | Default value              | Example value                     | Version  |
| -------------------- | -------- | ----------- | -------------- | -------------------------- | --------------------------------- | -------- |
| FAVICON\_MASTER\_URL | `string` | -           | -              | `NEXT_PUBLIC_NETWORK_ICON` | `https://placekitten.com/180/180` | v1.11.0+ |

&#x20;

### Meta

Settings for meta tags, OG tags and SEO

| Variable                                     | Type      | Description                                                                                                                                                                               | Compulsoriness | Default value               | Example value                                                                                                                                                                                              | Version  |
| -------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_PROMOTE\_BLOCKSCOUT\_IN\_TITLE | `boolean` | Set to `true` to promote Blockscout in meta and OG titles                                                                                                                                 | -              | `true`                      | `true`                                                                                                                                                                                                     | v1.12.0+ |
| NEXT\_PUBLIC\_OG\_DESCRIPTION                | `string`  | Custom OG description                                                                                                                                                                     | -              | -                           | `Open-source block explorer by Blockscout. Search transactions, verify smart contracts, analyze addresses, and track network activity. Complete blockchain data and APIs for the %network_title% network.` | v1.12.0+ |
| NEXT\_PUBLIC\_OG\_IMAGE\_URL                 | `string`  | OG image url. Minimum image size is 200 x 20 pixels (recommended: 1200 x 600); maximum supported file size is 8 MB; 2:1 aspect ratio; supported formats: image/jpeg, image/gif, image/png | -              | `static/og_placeholder.png` | `https://placekitten.com/1200/600`                                                                                                                                                                         | v1.12.0+ |
| NEXT\_PUBLIC\_OG\_ENHANCED\_DATA\_ENABLED    | `boolean` | Set to `true` to populate OG tags (title, description) with API data for social preview robot requests                                                                                    | -              | `false`                     | `true`                                                                                                                                                                                                     | v1.29.0+ |
| NEXT\_PUBLIC\_SEO\_ENHANCED\_DATA\_ENABLED   | `boolean` | Set to `true` to pre-render page titles (e.g Token page) on the server side and inject page h1-tag to the markup before it is sent to the browser.                                        | -              | `false`                     | `true`                                                                                                                                                                                                     | v1.30.0+ |

&#x20;

### Views

#### Block views

| Variable                                   | Type                  | Description                                                                                        | Compulsoriness | Default value | Example value                     | Version  |
| ------------------------------------------ | --------------------- | -------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------- | -------- |
| NEXT\_PUBLIC\_VIEWS\_BLOCK\_HIDDEN\_FIELDS | `Array<BlockFieldId>` | Array of the block fields ids that should be hidden. See below the list of the possible id values. | -              | -             | `'["burnt_fees","total_reward"]'` | v1.10.0+ |

**Block fields list**

| Id             | Description                                                                |
| -------------- | -------------------------------------------------------------------------- |
| `base_fee`     | Base fee                                                                   |
| `burnt_fees`   | Burnt fees                                                                 |
| `total_reward` | Total block reward                                                         |
| `nonce`        | Block nonce                                                                |
| `miner`        | Address of block's miner or validator                                      |
| `L1_status`    | Short interpretation of the batch lifecycle (applicable for Rollup chains) |
| `batch`        | Batch index (applicable for Rollup chains)                                 |

&#x20;

#### Address views

| Variable                                                    | Type                                                                  | Description                                                                                                                                                                                                                                                                                                                                             | Compulsoriness                                                          | Default value                | Example value                         | Version  |
| ----------------------------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | ---------------------------- | ------------------------------------- | -------- |
| NEXT\_PUBLIC\_VIEWS\_ADDRESS\_IDENTICON\_TYPE               | `"github" \| "jazzicon" \| "gradient_avatar" \| "blockie" \| "nouns"` | Default style of address identicon appearance. Choose between [GitHub](https://github.blog/2013-08-14-identicons/), [Metamask Jazzicon](https://metamask.github.io/jazzicon/), [Gradient Avatar](https://github.com/varld/gradient-avatar), [Ethereum Blocky](https://mycryptohq.github.io/ethereum-blockies-base64/) and [Nouns](https://nouns.wtf)    | -                                                                       | `jazzicon`                   | `gradient_avatar`                     | v1.12.0+ |
| NEXT\_PUBLIC\_VIEWS\_ADDRESS\_FORMAT                        | `Array<"base16" \| "bech32">`                                         | Displayed address format, could be either `base16` standard or [`bech32`](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki#bech32) standard. If the array contains multiple values, the address format toggle will appear in the UI, allowing the user to switch between formats. The first item in the array will be the default format. | -                                                                       | `'["base16"]'`               | `'["bech32", "base16"]'`              | v1.36.0+ |
| NEXT\_PUBLIC\_VIEWS\_ADDRESS\_BECH\_32\_PREFIX              | `string`                                                              | Human-readable prefix of `bech32` address format.                                                                                                                                                                                                                                                                                                       | Required, if `NEXT_PUBLIC_VIEWS_ADDRESS_FORMAT` contains "bech32" value | -                            | `duck`                                | v1.36.0+ |
| NEXT\_PUBLIC\_VIEWS\_ADDRESS\_HIDDEN\_VIEWS                 | `Array<AddressViewId>`                                                | Address views that should not be displayed. See below the list of the possible id values.                                                                                                                                                                                                                                                               | -                                                                       | -                            | `'["top_accounts"]'`                  | v1.15.0+ |
| NEXT\_PUBLIC\_VIEWS\_CONTRACT\_SOLIDITYSCAN\_ENABLED        | `boolean`                                                             | Set to `true` if SolidityScan reports are supported                                                                                                                                                                                                                                                                                                     | -                                                                       | -                            | `true`                                | v1.19.0+ |
| NEXT\_PUBLIC\_VIEWS\_CONTRACT\_EXTRA\_VERIFICATION\_METHODS | `Array<'solidity-hardhat' \| 'solidity-foundry'>`                     | Pass an array of additional methods from which users can choose while verifying a smart contract. Both methods are available by default, pass `'none'` string to disable them all.                                                                                                                                                                      | -                                                                       | -                            | `['solidity-hardhat']`                | v1.33.0+ |
| NEXT\_PUBLIC\_VIEWS\_CONTRACT\_LANGUAGE\_FILTERS            | `Array<'solidity' \| 'vyper' \| 'yul' \| 'scilla'>`                   | Pass an array of contract languages that will be displayed as options in the filter on the verified contract page.                                                                                                                                                                                                                                      | -                                                                       | `['solidity','vyper','yul']` | `['solidity','vyper','yul','scilla']` | v1.37.0+ |

**Address views list**

| Id             | Description  |
| -------------- | ------------ |
| `top_accounts` | Top accounts |

&#x20;

#### Transaction views

| Variable                                    | Type                          | Description                                                                                                                       | Compulsoriness | Default value | Example value          | Version  |
| ------------------------------------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ---------------------- | -------- |
| NEXT\_PUBLIC\_VIEWS\_TX\_HIDDEN\_FIELDS     | `Array<TxFieldsId>`           | Array of the transaction fields ids that should be hidden. See below the list of the possible id values.                          | -              | -             | `'["value","tx_fee"]'` | v1.15.0+ |
| NEXT\_PUBLIC\_VIEWS\_TX\_ADDITIONAL\_FIELDS | `Array<TxAdditionalFieldsId>` | Array of the additional fields ids that should be added to the transaction details. See below the list of the possible id values. | -              | -             | `'["fee_per_gas"]'`    | v1.15.0+ |

**Transaction fields list**

| Id             | Description                                                                |
| -------------- | -------------------------------------------------------------------------- |
| `value`        | Sent value                                                                 |
| `fee_currency` | Fee currency                                                               |
| `gas_price`    | Price per unit of gas                                                      |
| `tx_fee`       | Total transaction fee                                                      |
| `gas_fees`     | Gas fees breakdown                                                         |
| `burnt_fees`   | Amount of native coin burnt for transaction                                |
| `L1_status`    | Short interpretation of the batch lifecycle (applicable for Rollup chains) |
| `batch`        | Batch index (applicable for Rollup chains)                                 |

**Transaction additional fields list**

| Id            | Description                                                            |
| ------------- | ---------------------------------------------------------------------- |
| `fee_per_gas` | Amount of total fee divided by total amount of gas used by transaction |

&#x20;

#### Token views

| Variable                                          | Type      | Description                                                                                                                                                   | Compulsoriness | Default value | Example value | Version  |
| ------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_VIEWS\_TOKEN\_SCAM\_TOGGLE\_ENABLED | `boolean` | Show the "Hide scam tokens" toggle in the site settings dropdown. This option controls the visibility of tokens with a poor reputation in the search results. | -              | `false`       | `true`        | v1.38.0+ |

&#x20;

#### NFT views

| Variable                                      | Type                                                                                                               | Description                                                                                                                                                                                                                                                      | Compulsoriness | Default value | Example value                                                                                                                                                                                                            | Version  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| NEXT\_PUBLIC\_VIEWS\_NFT\_MARKETPLACES        | `Array<NftMarketplace>` where `NftMarketplace` can have following [properties](envs.md#nft-marketplace-properties) | Used to build up links to NFT collections and NFT instances in external marketplaces.                                                                                                                                                                            | -              | -             | `[{'name':'OpenSea','collection_url':'https://opensea.io/assets/ethereum/{hash}','instance_url':'https://opensea.io/assets/ethereum/{hash}/{id}','logo_url':'https://opensea.io/static/images/logos/opensea-logo.svg'}]` | v1.15.0+ |
| NEXT\_PUBLIC\_HELIA\_VERIFIED\_FETCH\_ENABLED | `boolean`                                                                                                          | Indicates that the [Helia verified fetch](https://github.com/ipfs/helia-verified-fetch/tree/main/packages/verified-fetch) should be used for retrieving content of NFT assets (currently limited to images) directly from IPFS network using trustless gateways. | -              | `true`        | `false`                                                                                                                                                                                                                  | v1.37.0+ |

**NFT marketplace properties**

| Variable        | Type     | Description                       | Compulsoriness | Default value | Example value                                             |
| --------------- | -------- | --------------------------------- | -------------- | ------------- | --------------------------------------------------------- |
| name            | `string` | Displayed name of the marketplace | Required       | -             | `OpenSea`                                                 |
| collection\_url | `string` | URL template for NFT collection   | Required       | -             | `https://opensea.io/assets/ethereum/{hash}`               |
| instance\_url   | `string` | URL template for NFT instance     | Required       | -             | `https://opensea.io/assets/ethereum/{hash}/{id}`          |
| logo\_url       | `string` | URL of marketplace logo           | Required       | -             | `https://opensea.io/static/images/logos/opensea-logo.svg` |

_Note_ URL templates should contain placeholders of NFT hash (`{hash}`) and NFT id (`{id}`). This placeholders will be substituted with particular values for every collection or instance.

&#x20;

### Misc

| Variable                                      | Type                                                                                                                                 | Description                                                                                                             | Compulsoriness | Default value | Example value                                                                                                                                | Version  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_NETWORK\_EXPLORERS              | `Array<NetworkExplorer>` where `NetworkExplorer` can have following [properties](envs.md#network-explorer-configuration-properties)  | Used to build up links to transactions, blocks, addresses in other chain explorers.                                     | -              | -             | `[{'title':'Anyblock','baseUrl':'https://explorer.anyblock.tools','paths':{'tx':'/ethereum/poa/core/tx'}}]`                                  | v1.0.x+  |
| NEXT\_PUBLIC\_CONTRACT\_CODE\_IDES            | `Array<ContractCodeIde>` where `ContractCodeIde` can have following [properties](envs.md#contract-code-ide-configuration-properties) | Used to build up links to IDEs with contract source code.                                                               | -              | -             | `[{'title':'Remix IDE','url':'https://remix.blockscout.com/?address={hash}&blockscout={domain}','icon_url':'https://example.com/icon.svg'}]` | v1.23.0+ |
| NEXT\_PUBLIC\_HAS\_CONTRACT\_AUDIT\_REPORTS   | `boolean`                                                                                                                            | Set to `true` to enable Submit Audit form on the contract page                                                          | -              | `false`       | `true`                                                                                                                                       | v1.25.0+ |
| NEXT\_PUBLIC\_HIDE\_INDEXING\_ALERT\_BLOCKS   | `boolean`                                                                                                                            | Set to `true` to hide indexing alert in the page header about indexing chain's blocks                                   | -              | `false`       | `true`                                                                                                                                       | v1.17.0+ |
| NEXT\_PUBLIC\_HIDE\_INDEXING\_ALERT\_INT\_TXS | `boolean`                                                                                                                            | Set to `true` to hide indexing alert in the page footer about indexing block's internal transactions                    | -              | `false`       | `true`                                                                                                                                       | v1.17.0+ |
| NEXT\_PUBLIC\_MAINTENANCE\_ALERT\_MESSAGE     | `string`                                                                                                                             | Used for displaying custom announcements or alerts in the header of the site. Could be a regular string or a HTML code. | -              | -             | `Hello world! 🤪`                                                                                                                            | v1.13.0+ |
| NEXT\_PUBLIC\_COLOR\_THEME\_DEFAULT           | `'light' \| 'dim' \| 'midnight' \| 'dark'`                                                                                           | Preferred color theme of the app                                                                                        | -              | -             | `midnight`                                                                                                                                   | v1.30.0+ |
| NEXT\_PUBLIC\_FONT\_FAMILY\_HEADING           | `FontFamily`, see full description [below](envs.md#font-family-configuration-properties)                                             | Special typeface to use in page headings (`<h1>`, `<h2>`, etc.)                                                         | -              | -             | `{'name':'Montserrat','url':'https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap'}`                        | v1.35.0+ |
| NEXT\_PUBLIC\_FONT\_FAMILY\_BODY              | `FontFamily`, see full description [below](envs.md#font-family-configuration-properties)                                             | Main typeface to use in page content elements.                                                                          | -              | -             | `{'name':'Raleway','url':'https://fonts.googleapis.com/css2?family=Raleway:wght@400;500;600;700&display=swap'}`                              | v1.35.0+ |
| NEXT\_PUBLIC\_MAX\_CONTENT\_WIDTH\_ENABLED    | `boolean`                                                                                                                            | Set to `true` to restrict the page content width on extra-large screens.                                                | -              | `true`        | `false`                                                                                                                                      | v1.34.1+ |

#### Network explorer configuration properties

| Variable | Type                                                      | Description                                                                                                                        | Compulsoriness | Default value | Example value                     |
| -------- | --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------- |
| logo     | `string`                                                  | URL to explorer logo file. Should be at least 40x40.                                                                               | -              | -             | `'https://foo.app/icon.png'`      |
| title    | `string`                                                  | Displayed name of the explorer                                                                                                     | Required       | -             | `Anyblock`                        |
| baseUrl  | `string`                                                  | Base url of the explorer                                                                                                           | Required       | -             | `https://explorer.anyblock.tools` |
| paths    | `Record<'tx' \| 'block' \| 'address' \| 'token', string>` | Map of explorer entities and their paths. Path can be a template with `:id` or `:id_lowercase` param, or a string (see note below) | Required       | -             | `{'tx':'/ethereum/poa/core/tx'}`  |

_Note_ If a path template contains `:id` or `:id_lowercase`, it will be replaced with the entity-id in its original case or lowercased respectively. If neither parameter is present, the entity-id will be appended to the end of the path in lowercase. For example, with baseUrl `https://explorer.anyblock.tools`:

* Path `{'tx':'/ethereum/poa/core/tx/:id/details'}` and entity-id `0x123...AbC` results in `https://explorer.anyblock.tools/ethereum/poa/core/tx/0x123...AbC/details`
* Path `{'tx':'/ethereum/poa/core/tx/:id_lowercase/details'}` and entity-id `0x123...AbC` results in `https://explorer.anyblock.tools/ethereum/poa/core/tx/0x123...abc/details`
* Path `{'tx':'/ethereum/poa/core/tx'}` and entity-id `0x123...AbC` results in `https://explorer.anyblock.tools/ethereum/poa/core/tx/0x123...abc`

#### Contract code IDE configuration properties

| Variable  | Type     | Description                                                                                   | Compulsoriness | Default value | Example value                                                      |
| --------- | -------- | --------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------------------------------ |
| title     | `string` | Displayed name of the IDE                                                                     | Required       | -             | `Remix IDE`                                                        |
| url       | `string` | URL of the IDE with placeholders for contract hash (`{hash}`) and current domain (`{domain}`) | Required       | -             | `https://remix.blockscout.com/?address={hash}&blockscout={domain}` |
| icon\_url | `string` | URL of the IDE icon                                                                           | Required       | -             | `https://example.com/icon.svg`                                     |

#### Font family configuration properties

| Variable | Type     | Description                                                                                    | Compulsoriness | Default value | Example value                                                                           |
| -------- | -------- | ---------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------------------------------------------------------------- |
| name     | `string` | Font family name; used to define the `font-family` CSS property.                               | Required       | -             | `Montserrat`                                                                            |
| url      | `string` | URL for external font. Ensure the font supports the following weights: 400, 500, 600, and 700. | Required       | -             | `https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap` |

&#x20;

## App features

_Note_ The variables which are marked as required should be passed as described in order to enable the particular feature, but they are not required in the entire app context.

### My account

| Variable                                  | Type      | Description                                                                                                                                                                                                                             | Compulsoriness | Default value | Example value                                  | Version |
| ----------------------------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ---------------------------------------------- | ------- |
| NEXT\_PUBLIC\_IS\_ACCOUNT\_SUPPORTED      | `boolean` | Set to true if network has account feature                                                                                                                                                                                              | Required       | -             | `true`                                         | v1.0.x+ |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_APP\_SITE\_KEY | `boolean` | See [below](envs.md#google-recaptcha)                                                                                                                                                                                                   | Required       | -             | `<your-secret>`                                | v1.0.x+ |
| NEXT\_PUBLIC\_AUTH0\_CLIENT\_ID           | `string`  | **DEPRECATED** Client id for [Auth0](https://auth0.com/) provider                                                                                                                                                                       | -              | -             | `<your-secret>`                                | v1.0.x+ |
| NEXT\_PUBLIC\_AUTH\_URL                   | `string`  | **DEPRECATED** Account auth base url; it is used for building login URL (`${ NEXT_PUBLIC_AUTH_URL }/auth/auth0`) and logout return URL (`${ NEXT_PUBLIC_AUTH_URL }/auth/logout`); if not provided the base app URL will be used instead | -              | -             | `https://blockscout.com`                       | v1.0.x+ |
| NEXT\_PUBLIC\_LOGOUT\_URL                 | `string`  | **DEPRECATED** Account logout url. Required if account is supported for the app instance.                                                                                                                                               | -              | -             | `https://blockscoutcom.us.auth0.com/v2/logout` | v1.0.x+ |

&#x20;

### Gas tracker

This feature is **enabled by default**. To switch it off pass `NEXT_PUBLIC_GAS_TRACKER_ENABLED=false`.

| Variable                            | Type                   | Description                                                                                                                                                                                                                                                                                             | Compulsoriness | Default value       | Example value | Version  |
| ----------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------------- | ------------- | -------- |
| NEXT\_PUBLIC\_GAS\_TRACKER\_ENABLED | `boolean`              | Set to true to enable "Gas tracker" in the app                                                                                                                                                                                                                                                          | Required       | `true`              | `false`       | v1.25.0+ |
| NEXT\_PUBLIC\_GAS\_TRACKER\_UNITS   | Array<`usd` \| `gwei`> | Array of units for displaying gas prices on the Gas Tracker page, in the stats snippet on the Home page, and in the top bar. The first value in the array will take priority over the second one in all mentioned views. If only one value is provided, gas prices will be displayed only in that unit. | -              | `[ 'usd', 'gwei' ]` | `[ 'gwei' ]`  | v1.25.0+ |

&#x20;

### Advanced filter

This feature is **enabled by default**. To switch it off pass `NEXT_PUBLIC_ADVANCED_FILTER_ENABLED=false`.

| Variable                                | Type      | Description                                             | Compulsoriness | Default value | Example value | Version  |
| --------------------------------------- | --------- | ------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_ADVANCED\_FILTER\_ENABLED | `boolean` | Set to true to enable "Advanced filter" page in the app | Required       | `true`        | `false`       | v1.37.0+ |

&#x20;

### Address verification in "My account"

_Note_ all ENV variables required for [My account](envs.md#my-account) feature should be passed alongside the following ones:

| Variable                                | Type     | Description                    | Compulsoriness | Default value | Example value                                    | Version |
| --------------------------------------- | -------- | ------------------------------ | -------------- | ------------- | ------------------------------------------------ | ------- |
| NEXT\_PUBLIC\_CONTRACT\_INFO\_API\_HOST | `string` | Contract Info API endpoint url | Required       | -             | `https://contracts-info.services.blockscout.com` | v1.1.0+ |
| NEXT\_PUBLIC\_ADMIN\_SERVICE\_API\_HOST | `string` | Admin Service API endpoint url | Required       | -             | `https://admin-rs.services.blockscout.com`       | v1.1.0+ |

&#x20;

### Blockchain interaction (writing to contract, etc.)

| Variable                                   | Type     | Description                                                                  | Compulsoriness | Default value | Example value              | Version |
| ------------------------------------------ | -------- | ---------------------------------------------------------------------------- | -------------- | ------------- | -------------------------- | ------- |
| NEXT\_PUBLIC\_WALLET\_CONNECT\_PROJECT\_ID | `string` | Project id for [WalletConnect](https://cloud.walletconnect.com/) integration | Required       | -             | `<your-secret>`            | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_RPC\_URL            | `string` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | Required       | -             | `https://core.poa.network` | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_NAME                | `string` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | Required       | -             | `Gnosis Chain`             | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_ID                  | `number` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | Required       | -             | `99`                       | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_NAME      | `string` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | Required       | -             | `Ether`                    | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_SYMBOL    | `string` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | Required       | -             | `ETH`                      | v1.0.x+ |
| NEXT\_PUBLIC\_NETWORK\_CURRENCY\_DECIMALS  | `string` | See in [Blockchain parameters](envs.md#blockchain-parameters) section        | -              | `18`          | `6`                        | v1.0.x+ |

&#x20;

### Banner ads

This feature is **enabled by default** with the `slise` ads provider. To switch it off pass `NEXT_PUBLIC_AD_BANNER_PROVIDER=none`.

| Variable                                       | Type                                                     | Description                                      | Compulsoriness | Default value | Example value                                  | Version  |
| ---------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------ | -------------- | ------------- | ---------------------------------------------- | -------- |
| NEXT\_PUBLIC\_AD\_BANNER\_PROVIDER             | `slise` \| `adbutler` \| `coinzilla` \| `hype` \| `none` | Ads provider                                     | -              | `slise`       | `coinzilla`                                    | v1.0.x+  |
| NEXT\_PUBLIC\_AD\_BANNER\_ADDITIONAL\_PROVIDER | `adbutler`                                               | Additional ads provider to mix with the main one | -              | -             | `adbutler`                                     | v1.28.0+ |
| NEXT\_PUBLIC\_AD\_ADBUTLER\_CONFIG\_DESKTOP    | `{ id: string; width: string; height: string }`          | Placement config for desktop Adbutler banner     | -              | -             | `{'id':'123456','width':'728','height':'90'}`  | v1.3.0+  |
| NEXT\_PUBLIC\_AD\_ADBUTLER\_CONFIG\_MOBILE     | `{ id: string; width: number; height: number }`          | Placement config for mobile Adbutler banner      | -              | -             | `{'id':'654321','width':'300','height':'100'}` | v1.3.0+  |

&#x20;

### Text ads

This feature is **enabled by default** with the `coinzilla` ads provider. To switch it off pass `NEXT_PUBLIC_AD_TEXT_PROVIDER=none`.

| Variable                         | Type                  | Description  | Compulsoriness | Default value | Example value | Version |
| -------------------------------- | --------------------- | ------------ | -------------- | ------------- | ------------- | ------- |
| NEXT\_PUBLIC\_AD\_TEXT\_PROVIDER | `coinzilla` \| `none` | Ads provider | -              | `coinzilla`   | `none`        | v1.0.x+ |

&#x20;

### Beacon chain

| Variable                                      | Type      | Description                                    | Compulsoriness | Default value                         | Example value | Version |
| --------------------------------------------- | --------- | ---------------------------------------------- | -------------- | ------------------------------------- | ------------- | ------- |
| NEXT\_PUBLIC\_HAS\_BEACON\_CHAIN              | `boolean` | Set to true for networks with the beacon chain | Required       | -                                     | `true`        | v1.0.x+ |
| NEXT\_PUBLIC\_BEACON\_CHAIN\_CURRENCY\_SYMBOL | `string`  | Beacon network currency symbol                 | -              | `NEXT_PUBLIC_NETWORK_CURRENCY_SYMBOL` | `ETH`         | v1.0.x+ |

&#x20;

### User operations (ERC-4337)

| Variable                     | Type      | Description                                                | Compulsoriness | Default value | Example value | Version  |
| ---------------------------- | --------- | ---------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_HAS\_USER\_OPS | `boolean` | Set to true to show user operations related data and pages | -              | -             | `true`        | v1.23.0+ |

&#x20;

### Rollup chain

| Variable                                             | Type                                                                              | Description                                                                                                                                                                                                                                                                                                  | Compulsoriness                    | Default value | Example value                                                  | Version  |
| ---------------------------------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------- | ------------- | -------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_ROLLUP\_TYPE                           | `'optimistic' \| 'arbitrum' \| 'shibarium' \| 'zkEvm' \| 'zkSync' \| 'scroll'`    | Rollup chain type                                                                                                                                                                                                                                                                                            | Required                          | -             | `'optimistic'`                                                 | v1.24.0+ |
| NEXT\_PUBLIC\_ROLLUP\_L1\_BASE\_URL                  | `string`                                                                          | Blockscout base URL for L1 network. **DEPRECATED** _Use `NEXT_PUBLIC_ROLLUP_PARENT_CHAIN` instead_                                                                                                                                                                                                           | Required                          | -             | `'http://eth-goerli.blockscout.com'`                           | v1.24.0+ |
| NEXT\_PUBLIC\_ROLLUP\_L2\_WITHDRAWAL\_URL            | `string`                                                                          | URL for L2 -> L1 withdrawals (Optimistic stack only)                                                                                                                                                                                                                                                         | Required for `optimistic` rollups | -             | `https://app.optimism.io/bridge/withdraw`                      | v1.24.0+ |
| NEXT\_PUBLIC\_ROLLUP\_STAGE\_INDEX                   | `1 \| 2`                                                                          | Reflects the maturity and decentralization level of the chain based on [L2BEAT's framework](https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe). The label will be added to the sidebar according to the provided stage index. Not applicable for testnets.  | -                                 | -             | `1`                                                            | v2.1.0+  |
| NEXT\_PUBLIC\_FAULT\_PROOF\_ENABLED                  | `boolean`                                                                         | Set to `true` for chains with fault proof system enabled (Optimistic stack only)                                                                                                                                                                                                                             | -                                 | -             | `true`                                                         | v1.31.0+ |
| NEXT\_PUBLIC\_HAS\_MUD\_FRAMEWORK                    | `boolean`                                                                         | Set to `true` for instances that use MUD framework (Optimistic stack only)                                                                                                                                                                                                                                   | -                                 | -             | `true`                                                         | v1.33.0+ |
| NEXT\_PUBLIC\_INTEROP\_ENABLED                       | `boolean`                                                                         | Enables "Interop messages" page (Optimistic stack only)                                                                                                                                                                                                                                                      | -                                 | `false`       | `true`                                                         | v1.39.0+ |
| NEXT\_PUBLIC\_ROLLUP\_HOMEPAGE\_SHOW\_LATEST\_BLOCKS | `boolean`                                                                         | Set to `true` to display "Latest blocks" widget instead of "Latest batches" on the home page                                                                                                                                                                                                                 | -                                 | -             | `true`                                                         | v1.36.0+ |
| NEXT\_PUBLIC\_ROLLUP\_OUTPUT\_ROOTS\_ENABLED         | `boolean`                                                                         | Enables "Output roots" page (Optimistic stack only)                                                                                                                                                                                                                                                          | -                                 | `false`       | `true`                                                         | v1.37.0+ |
| NEXT\_PUBLIC\_ROLLUP\_PARENT\_CHAIN\_NAME            | `string`                                                                          | Set to customize L1 transaction status labels in the UI (e.g., "Sent to "). This setting is applicable only for Arbitrum-based chains. **DEPRECATED** _Use `NEXT_PUBLIC_ROLLUP_PARENT_CHAIN` instead_                                                                                                        | -                                 | -             | `DuckChain`                                                    | v1.37.0+ |
| NEXT\_PUBLIC\_ROLLUP\_PARENT\_CHAIN                  | `ParentChain`, see details [below](envs.md#parent-chain-configuration-properties) | Configuration parameters for the parent chain.                                                                                                                                                                                                                                                               | -                                 | -             | `{'baseUrl':'https://explorer.duckchain.io'}`                  | v1.38.0+ |
| NEXT\_PUBLIC\_ROLLUP\_DA\_CELESTIA\_NAMESPACE        | `string`                                                                          | Hex-string for creating a link to the transaction batch on the Seleneium explorer. "0x"-format and 60 symbol length. Available only for Arbitrum roll-ups.                                                                                                                                                   | -                                 | -             | `0x00000000000000000000000000000000000000ca1de12a9905be97beaf` | v1.38.0+ |
| NEXT\_PUBLIC\_ROLLUP\_DA\_CELESTIA\_CELENIUM\_URL    | `string`                                                                          | URL for the Selenium explorer. It is used to create links to the Data Availability Blobs page. The URL should contain the full path without any search parameters related to the blob, as these will be constructed at runtime for each blob separately. Available only for Optimistic or Arbitrum roll-ups. | -                                 | -             | `https://mocha.celenium.io/blob`                               | v2.0.2+  |

#### Parent chain configuration properties

| Variable  | Type                                                  | Description                                                                                                                                                                    | Compulsoriness | Default value | Example value                                |
| --------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | ------------- | -------------------------------------------- |
| id        | `number`                                              | Chain id, see [https://chainlist.org](https://chainlist.org) for the reference.                                                                                                | -              | -             | `42`                                         |
| name      | `string`                                              | Displayed name of the chain. Set to customize L1 transaction status labels in the UI (e.g., "Sent to "). Currently, this setting is applicable only for Arbitrum-based chains. | -              | -             | `DuckChain`                                  |
| baseUrl   | `string`                                              | Base url of the chain explorer.                                                                                                                                                | Required       | -             | `https://explorer.duckchain.io`              |
| rpcUrls   | `Array<string>`                                       | Chain public RPC server urls, see [https://chainlist.org](https://chainlist.org) for the reference.                                                                            | -              | -             | `['https://rpc.duckchain.io']`               |
| currency  | `{ name: string; symbol: string; decimals: number; }` | Chain currency config.                                                                                                                                                         | -              | -             | `{ name: Quack, symbol: QUA, decimals: 18 }` |
| isTestnet | `boolean`                                             | Set to true if network is testnet.                                                                                                                                             | -              | -             | `true`                                       |

&#x20;

### Export data to CSV file

| Variable                                  | Type     | Description                           | Compulsoriness | Default value | Example value   | Version |
| ----------------------------------------- | -------- | ------------------------------------- | -------------- | ------------- | --------------- | ------- |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_APP\_SITE\_KEY | `string` | See [below](envs.md#google-recaptcha) | true           | -             | `<your-secret>` | v1.0.x+ |

&#x20;

### Google analytics

| Variable                                      | Type     | Description                                                               | Compulsoriness | Default value | Example value | Version |
| --------------------------------------------- | -------- | ------------------------------------------------------------------------- | -------------- | ------------- | ------------- | ------- |
| NEXT\_PUBLIC\_GOOGLE\_ANALYTICS\_PROPERTY\_ID | `string` | Property ID for [Google Analytics](https://analytics.google.com/) service | true           | -             | `UA-XXXXXX-X` | v1.0.x+ |

&#x20;

### Mixpanel analytics

| Variable                               | Type     | Description                                                           | Compulsoriness | Default value | Example value   | Version |
| -------------------------------------- | -------- | --------------------------------------------------------------------- | -------------- | ------------- | --------------- | ------- |
| NEXT\_PUBLIC\_MIXPANEL\_PROJECT\_TOKEN | `string` | Project token for [Mixpanel](https://mixpanel.com/) analytics service | true           | -             | `<your-secret>` | v1.1.0+ |

&#x20;

### GrowthBook feature flagging and A/B testing

| Variable                                | Type     | Description                                                         | Compulsoriness | Default value | Example value   | Version  |
| --------------------------------------- | -------- | ------------------------------------------------------------------- | -------------- | ------------- | --------------- | -------- |
| NEXT\_PUBLIC\_GROWTH\_BOOK\_CLIENT\_KEY | `string` | Client SDK key for [GrowthBook](https://www.growthbook.io/) service | true           | -             | `<your-secret>` | v1.22.0+ |

&#x20;

### GraphQL API documentation

This feature is **always enabled**, but you can disable it by passing `none` value to `NEXT_PUBLIC_GRAPHIQL_TRANSACTION` variable.

| Variable                            | Type     | Description                                                                                | Compulsoriness | Default value | Example value                                                        | Version |
| ----------------------------------- | -------- | ------------------------------------------------------------------------------------------ | -------------- | ------------- | -------------------------------------------------------------------- | ------- |
| NEXT\_PUBLIC\_GRAPHIQL\_TRANSACTION | `string` | Txn hash for default query at GraphQl playground page. Pass `none` to disable the feature. | -              | -             | `0x4a0ed8ddf751a7cb5297f827699117b0f6d21a0b2907594d300dc9fed75c7e62` | v1.0.x+ |

&#x20;

### REST API documentation

This feature is **always enabled**, but you can disable it by passing `none` value to `NEXT_PUBLIC_API_SPEC_URL` variable.

| Variable                     | Type     | Description                                                                   | Compulsoriness | Default value                                                                              | Example value                                                                              | Version |
| ---------------------------- | -------- | ----------------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------- |
| NEXT\_PUBLIC\_API\_SPEC\_URL | `string` | Spec to be displayed on `/api-docs` page. Pass `none` to disable the feature. | -              | `https://raw.githubusercontent.com/blockscout/blockscout-api-v2-swagger/main/swagger.yaml` | `https://raw.githubusercontent.com/blockscout/blockscout-api-v2-swagger/main/swagger.yaml` | v1.0.x+ |

&#x20;

### Marketplace

| Variable                                              | Type      | Description                                                                                                                                                                                                                                                                                               | Compulsoriness | Default value | Example value                                                   | Version  |
| ----------------------------------------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_MARKETPLACE\_ENABLED                    | `boolean` | `true` means that the marketplace page will be enabled                                                                                                                                                                                                                                                    | Required       | -             | `true`                                                          | v1.24.1+ |
| NEXT\_PUBLIC\_MARKETPLACE\_CONFIG\_URL                | `string`  | URL of configuration file (`.json` format only) which contains list of apps that will be shown on the marketplace page. See [below](envs.md#marketplace-app-configuration-properties) list of available properties for an app. Can be replaced with NEXT\_PUBLIC\_ADMIN\_SERVICE\_API\_HOST               | Required       | -             | `https://example.com/marketplace_config.json`                   | v1.0.x+  |
| NEXT\_PUBLIC\_ADMIN\_SERVICE\_API\_HOST               | `string`  | Admin Service API endpoint url. Can be used instead of NEXT\_PUBLIC\_MARKETPLACE\_CONFIG\_URL                                                                                                                                                                                                             | -              | -             | `https://admin-rs.services.blockscout.com`                      | v1.1.0+  |
| NEXT\_PUBLIC\_MARKETPLACE\_SUBMIT\_FORM               | `string`  | Link to form where authors can submit their dapps to the marketplace                                                                                                                                                                                                                                      | Required       | -             | `https://airtable.com/shrqUAcjgGJ4jU88C`                        | v1.0.x+  |
| NEXT\_PUBLIC\_MARKETPLACE\_SUGGEST\_IDEAS\_FORM       | `string`  | Link to form where users can suggest ideas for the marketplace                                                                                                                                                                                                                                            | -              | -             | `https://airtable.com/appiy5yijZpMMSKjT/pag3t82DUCyhGRZZO/form` | v1.24.0+ |
| NEXT\_PUBLIC\_NETWORK\_RPC\_URL                       | `string`  | See in [Blockchain parameters](envs.md#blockchain-parameters) section                                                                                                                                                                                                                                     | Required       | -             | `https://core.poa.network`                                      | v1.0.x+  |
| NEXT\_PUBLIC\_MARKETPLACE\_CATEGORIES\_URL            | `string`  | URL of configuration file (`.json` format only) which contains the list of categories to be displayed on the marketplace page in the specified order. If no URL is provided, then the list of categories will be compiled based on the `categories` fields from the marketplace (apps) configuration file | -              | -             | `https://example.com/marketplace_categories.json`               | v1.23.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_SECURITY\_REPORTS\_URL     | `string`  | URL of configuration file (`.json` format only) which contains app security reports for displaying security scores on the Marketplace page                                                                                                                                                                | -              | -             | `https://example.com/marketplace_security_reports.json`         | v1.28.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_FEATURED\_APP              | `string`  | ID of the featured application to be displayed on the banner on the Marketplace page                                                                                                                                                                                                                      | -              | -             | `uniswap`                                                       | v1.29.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_BANNER\_CONTENT\_URL       | `string`  | URL of the banner HTML content                                                                                                                                                                                                                                                                            | -              | -             | `https://example.com/banner`                                    | v1.29.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_BANNER\_LINK\_URL          | `string`  | URL of the page the banner leads to                                                                                                                                                                                                                                                                       | -              | -             | `https://example.com`                                           | v1.29.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_RATING\_AIRTABLE\_API\_KEY | `string`  | Airtable API key                                                                                                                                                                                                                                                                                          | -              | -             | -                                                               | v1.33.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_RATING\_AIRTABLE\_BASE\_ID | `string`  | Airtable base ID with dapp ratings                                                                                                                                                                                                                                                                        | -              | -             | -                                                               | v1.33.0+ |
| NEXT\_PUBLIC\_MARKETPLACE\_GRAPH\_LINKS\_URL          | `string`  | URL of the file (`.json` format only) which contains the list of The Graph links to be displayed on the Marketplace page                                                                                                                                                                                  | -              | -             | `https://example.com/graph_links.json`                          | v1.36.0+ |

#### Marketplace app configuration properties

| Property         | Type            | Description                                                                                  | Compulsoriness | Example value                         |
| ---------------- | --------------- | -------------------------------------------------------------------------------------------- | -------------- | ------------------------------------- |
| id               | `string`        | Used as slug for the app. Must be unique in the app list.                                    | Required       | `'app'`                               |
| external         | `boolean`       | `true` means that the application opens in a new window, but not in an iframe.               | -              | `true`                                |
| title            | `string`        | Displayed title of the app.                                                                  | Required       | `'The App'`                           |
| logo             | `string`        | URL to logo file. Should be at least 288x288.                                                | Required       | `'https://foo.app/icon.png'`          |
| shortDescription | `string`        | Displayed only in the app list.                                                              | Required       | `'Awesome app'`                       |
| categories       | `Array<string>` | Displayed category.                                                                          | Required       | `['Security', 'Tools']`               |
| author           | `string`        | Displayed author of the app                                                                  | Required       | `'Bob'`                               |
| url              | `string`        | URL of the app which will be launched in the iframe.                                         | Required       | `'https://foo.app/launch'`            |
| description      | `string`        | Displayed only in the modal dialog with additional info about the app.                       | Required       | `'The best app'`                      |
| site             | `string`        | Displayed site link                                                                          | -              | `'https://blockscout.com'`            |
| twitter          | `string`        | Displayed twitter link                                                                       | -              | `'https://twitter.com/blockscoutcom'` |
| telegram         | `string`        | Displayed telegram link                                                                      | -              | `'https://t.me/poa_network'`          |
| github           | `string`        | Displayed github link                                                                        | -              | `'https://github.com/blockscout'`     |
| internalWallet   | `boolean`       | `true` means that the application can automatically connect to the Blockscout wallet.        | -              | `true`                                |
| priority         | `number`        | The higher the priority, the higher the app will appear in the list on the Marketplace page. | -              | `7`                                   |

&#x20;

### Solidity to UML diagrams

| Variable                                 | Type     | Description                              | Compulsoriness | Default value | Example value                                | Version  |
| ---------------------------------------- | -------- | ---------------------------------------- | -------------- | ------------- | -------------------------------------------- | -------- |
| NEXT\_PUBLIC\_VISUALIZE\_API\_HOST       | `string` | Visualize API endpoint url               | Required       | -             | `https://visualizer.services.blockscout.com` | v1.0.x+  |
| NEXT\_PUBLIC\_VISUALIZE\_API\_BASE\_PATH | `string` | Base path for Visualize API endpoint url | -              | -             | `/poa/core`                                  | v1.29.0+ |

&#x20;

### Blockchain statistics

| Variable                             | Type     | Description                          | Compulsoriness | Default value | Example value                           | Version  |
| ------------------------------------ | -------- | ------------------------------------ | -------------- | ------------- | --------------------------------------- | -------- |
| NEXT\_PUBLIC\_STATS\_API\_HOST       | `string` | Stats API endpoint url               | Required       | -             | `https://stats.services.blockscout.com` | v1.0.x+  |
| NEXT\_PUBLIC\_STATS\_API\_BASE\_PATH | `string` | Base path for Stats API endpoint url | -              | -             | `/poa/core`                             | v1.29.0+ |

&#x20;

### Web3 wallet integration (add token or network to the wallet)

This feature is **enabled by default** with the `['metamask']` value. To switch it off pass `NEXT_PUBLIC_WEB3_WALLETS=none`.

| Variable                                            | Type                                                | Description                                                                                                                            | Compulsoriness | Default value    | Example value    | Version  |
| --------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ---------------- | ---------------- | -------- |
| NEXT\_PUBLIC\_WEB3\_WALLETS                         | `Array<'metamask' \| 'coinbase' \| 'token_pocket'>` | Array of Web3 wallets which will be used to add tokens or chain to. The first wallet which is enabled in user's browser will be shown. | -              | `[ 'metamask' ]` | `[ 'coinbase' ]` | v1.10.0+ |
| NEXT\_PUBLIC\_WEB3\_DISABLE\_ADD\_TOKEN\_TO\_WALLET | `boolean`                                           | Set to `true` to hide icon "Add to your wallet" next to token addresses                                                                | -              | -                | `true`           | v1.0.x+  |

&#x20;

### Transaction interpretation

| Variable                                            | Type                              | Description                                                                              | Compulsoriness | Default value | Example value | Version  |
| --------------------------------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_TRANSACTION\_INTERPRETATION\_PROVIDER | `blockscout` \| `noves` \| `none` | Transaction interpretation provider that displays human readable transaction description | -              | `none`        | `blockscout`  | v1.21.0+ |

&#x20;

### External transactions

| Variable                                         | Type                                                                             | Description                                                                                       | Compulsoriness | Default value | Example value                                                                                                                         | Version  |
| ------------------------------------------------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_TX\_EXTERNAL\_TRANSACTIONS\_CONFIG | `{ chain_name: string; chain_logo_url: string; explorer_url_template: string; }` | Configuration of the external transactions links that should be added to the transaction details. | -              | -             | `{ chain_name: 'ethereum', chain_logo_url: 'https://example.com/logo.png', explorer_url_template: 'https://explorer.com/tx/{hash}' }` | v1.38.0+ |

&#x20;

### Verified tokens info

| Variable                                | Type     | Description                    | Compulsoriness | Default value | Example value                                    | Version |
| --------------------------------------- | -------- | ------------------------------ | -------------- | ------------- | ------------------------------------------------ | ------- |
| NEXT\_PUBLIC\_CONTRACT\_INFO\_API\_HOST | `string` | Contract Info API endpoint url | Required       | -             | `https://contracts-info.services.blockscout.com` | v1.0.x+ |

&#x20;

### Name service integration

This feature allows resolving blockchain addresses using human-readable domain names.

| Variable                               | Type     | Description                   | Compulsoriness | Default value | Example value                          | Version  |
| -------------------------------------- | -------- | ----------------------------- | -------------- | ------------- | -------------------------------------- | -------- |
| NEXT\_PUBLIC\_NAME\_SERVICE\_API\_HOST | `string` | Name Service API endpoint url | Required       | -             | `https://bens.services.blockscout.com` | v1.22.0+ |

&#x20;

### Metadata service integration

This feature allows name tags and other public tags for addresses.

| Variable                                   | Type     | Description                       | Compulsoriness | Default value | Example value                              | Version  |
| ------------------------------------------ | -------- | --------------------------------- | -------------- | ------------- | ------------------------------------------ | -------- |
| NEXT\_PUBLIC\_METADATA\_SERVICE\_API\_HOST | `string` | Metadata Service API endpoint url | Required       | -             | `https://metadata.services.blockscout.com` | v1.30.0+ |

&#x20;

### Public tag submission

This feature allows you to submit an application with a public address tag.

| Variable                                   | Type     | Description                           | Compulsoriness | Default value | Example value                              | Version  |
| ------------------------------------------ | -------- | ------------------------------------- | -------------- | ------------- | ------------------------------------------ | -------- |
| NEXT\_PUBLIC\_METADATA\_SERVICE\_API\_HOST | `string` | Metadata Service API endpoint url     | Required       | -             | `https://metadata.services.blockscout.com` | v1.30.0+ |
| NEXT\_PUBLIC\_ADMIN\_SERVICE\_API\_HOST    | `string` | Admin Service API endpoint url        | Required       | -             | `https://admin-rs.services.blockscout.com` | v1.1.0+  |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_APP\_SITE\_KEY  | `string` | See [below](envs.md#google-recaptcha) | true           | -             | `<your-secret>`                            | v1.0.x+  |

&#x20;

### Data Availability

This feature enables views related to blob transactions (EIP-4844), such as the Blob Txns tab on the Transactions page and the Blob details page.

| Variable                                  | Type      | Description                                    | Compulsoriness | Default value | Example value | Version  |
| ----------------------------------------- | --------- | ---------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_DATA\_AVAILABILITY\_ENABLED | `boolean` | Set to true to enable blob transactions views. | Required       | -             | `true`        | v1.28.0+ |

&#x20;

### Bridged tokens

This feature allows users to view tokens that have been bridged from other EVM chains. Additional tab "Bridged" will be added to the tokens page and the link to original token will be displayed on the token page.

| Variable                               | Type                                                                                                                                       | Description                                                                                                                                  | Compulsoriness | Default value | Example value                                                                                       | Version  |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_BRIDGED\_TOKENS\_CHAINS  | `Array<BridgedTokenChain>` where `BridgedTokenChain` can have following [properties](envs.md#bridged-token-chain-configuration-properties) | Used for displaying filter by the chain from which token where bridged. Also, used for creating links to original tokens in other explorers. | Required       | -             | `[{'id':'1','title':'Ethereum','short_title':'ETH','base_url':'https://eth.blockscout.com/token'}]` | v1.14.0+ |
| NEXT\_PUBLIC\_BRIDGED\_TOKENS\_BRIDGES | `Array<TokenBridge>` where `TokenBridge` can have following [properties](envs.md#token-bridge-configuration-properties)                    | Used for displaying text about bridges types on the tokens page.                                                                             | Required       | -             | `[{'type':'omni','title':'OmniBridge','short_title':'OMNI'}]`                                       | v1.14.0+ |

#### Bridged token chain configuration properties

| Variable     | Type     | Description                                                                         | Compulsoriness | Default value | Example value                      |
| ------------ | -------- | ----------------------------------------------------------------------------------- | -------------- | ------------- | ---------------------------------- |
| id           | `string` | Base chain id, see [https://chainlist.org](https://chainlist.org) for the reference | Required       | -             | `1`                                |
| title        | `string` | Displayed name of the chain                                                         | Required       | -             | `Ethereum`                         |
| short\_title | `string` | Used for displaying chain name in the list view as tag                              | Required       | -             | `ETH`                              |
| base\_url    | `string` | Base url to original token in base chain explorer                                   | Required       | -             | `https://eth.blockscout.com/token` |

_Note_ The url to original token will be constructed as `<base_url>/<token_hash>`, e.g `https://eth.blockscout.com/token/<token_hash>`

#### Token bridge configuration properties

| Variable     | Type     | Description                                                           | Compulsoriness | Default value | Example value |
| ------------ | -------- | --------------------------------------------------------------------- | -------------- | ------------- | ------------- |
| type         | `string` | Bridge type; should be matched to `bridge_type` field in API response | Required       | -             | `omni`        |
| title        | `string` | Bridge title                                                          | Required       | -             | `OmniBridge`  |
| short\_title | `string` | Bridge short title for displaying in the tags                         | Required       | -             | `OMNI`        |

&#x20;

### Safe{Core} address tags

For the smart contract addresses which are [Safe{Core} accounts](https://safe.global/) public tag "Multisig: Safe" will be displayed in the address page header alongside to Safe logo.

| Variable                             | Type     | Description                                                                                                                    | Compulsoriness | Default value | Example value | Version  |
| ------------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------ | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_SAFE\_TX\_SERVICE\_URL | `string` | The Safe transaction service URL. See full list of supported networks [here](https://docs.safe.global/api-supported-networks). | -              | -             | `uniswap`     | v1.26.0+ |

&#x20;

### Address profile API

This feature allows the integration of an external API to fetch user info for addresses or contracts. When configured, if the API returns a username, a public tag with a custom link will be displayed in the address page header.

| Variable                             | Type                                                                                                           | Description                                                                                                       | Compulsoriness | Default value | Example value | Version  |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_ADDRESS\_USERNAME\_TAG | `{api_url: string; tag_link_template: string; tag_icon: string; tag_bg_color: string; tag_text_color: string}` | Address profile API tag configuration properties. See [below](envs.md#user-profile-api-configuration-properties). | -              | -             | `uniswap`     | v1.35.0+ |

&#x20;

#### Address profile API configuration properties

| Variable            | Type     | Description                                                                                          | Compulsoriness | Default value | Example value                       |
| ------------------- | -------- | ---------------------------------------------------------------------------------------------------- | -------------- | ------------- | ----------------------------------- |
| api\_url\_template  | `string` | User profile API URL. Should be a template with `{address}` variable                                 | Required       | -             | `https://example-api.com/{address}` |
| tag\_link\_template | `string` | External link to the profile. Should be a template with `{username}` variable                        | -              | -             | `https://example.com/{address}`     |
| tag\_icon           | `string` | Public tag icon (.svg) url                                                                           | -              | -             | `https://example.com/icon.svg`      |
| tag\_bg\_color      | `string` | Public tag background color (escape "#" symbol if you use HEX color codes or use rgba-value instead) | -              | -             | `\#000000`                          |
| tag\_text\_color    | `string` | Public tag text color (escape "#" symbol if you use HEX color codes or use rgba-value instead)       | -              | -             | `\#FFFFFF`                          |

&#x20;

### Address XStar XHS score

This feature allows the integration of an XStar API to fetch XHS score for addresses. When configured, if the API returns a score, a public tag with that score will be displayed in the address page header.

| Variable                        | Type     | Description                                                                             | Compulsoriness | Default value | Example value                                                                                        | Version  |
| ------------------------------- | -------- | --------------------------------------------------------------------------------------- | -------------- | ------------- | ---------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_XSTAR\_SCORE\_URL | `string` | XStar XHS score documentation URL for the address tag. Enables the XStar score feature. | -              | -             | `https://docs.xname.app/the-solution-adaptive-proof-of-humanity-on-blockchain/xhs-scoring-algorithm` | v1.36.0+ |

&#x20;

### SUAVE chain

For blockchains that implement SUAVE architecture additional fields will be shown on the transaction page ("Allowed peekers", "Kettle"). Users also will be able to see the list of all transactions for a particular Kettle in the separate view.

| Variable                       | Type      | Description                                                                                                          | Compulsoriness | Default value | Example value | Version  |
| ------------------------------ | --------- | -------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_IS\_SUAVE\_CHAIN | `boolean` | Set to true for blockchains with [SUAVE architecture](https://writings.flashbots.net/mevm-suave-centauri-and-beyond) | Required       | -             | `true`        | v1.14.0+ |

&#x20;

### Celo chain

For blockchains that use the Celo platform. _Note_, that once the Celo mainnet becomes an L2 chain, these variables will be migrated to the Rollup configuration section.

| Variable                               | Type      | Description                                                                                                                                              | Compulsoriness | Default value | Example value | Version  |
| -------------------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_CELO\_ENABLED            | `boolean` | Indicates that it is a Celo-based chain.                                                                                                                 | -              | -             | `true`        | v1.37.0+ |
| NEXT\_PUBLIC\_CELO\_L2\_UPGRADE\_BLOCK | `number`  | Indicates the block number when the Celo-type chain transitioned to L2. This is used to display links to the Epoch block page from a regular block page. | -              | -             | `26369280`    | v1.37.0+ |

&#x20;

### Ton Application Chain (TAC)

For Ton Application Chains, this feature enables additional views, such as a list of cross-chain operations and a detailed page for a specific cross-chain operation, as well as extra fields on the transaction page.

| Variable                                           | Type     | Description                                                                                                | Compulsoriness | Default value | Example value                                    | Version |
| -------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------------ | ------- |
| NEXT\_PUBLIC\_TAC\_OPERATION\_LIFECYCLE\_API\_HOST | `string` | URL for the TAC Operation Lifecycle service.                                                               | Required       | -             | `https://tac-operation-lifecycle.blockscout.com` | v2.1.0+ |
| NEXT\_PUBLIC\_TAC\_TON\_EXPLORER\_URL              | `string` | URL of the Ton chain explorer. This is used to build links to transactions and addresses on the Ton chain. | Required       | -             | `https://tonscan.org`                            | v2.1.0+ |

&#x20;

### MetaSuites extension

Enables [MetaSuites browser extension](https://github.com/blocksecteam/metasuites) to integrate with the app views.

| Variable                          | Type      | Description                       | Compulsoriness | Default value | Example value | Version  |
| --------------------------------- | --------- | --------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_METASUITES\_ENABLED | `boolean` | Set to true to enable integration | Required       | -             | `true`        | v1.26.0+ |

&#x20;

### Validators list

The feature enables the Validators page which provides detailed information about the validators of the PoS chains.

| Variable                              | Type                                      | Description | Compulsoriness | Default value | Example value | Version  |
| ------------------------------------- | ----------------------------------------- | ----------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_VALIDATORS\_CHAIN\_TYPE | `'stability' \| 'blackfort' \| 'zilliqa'` | Chain type  | Required       | -             | `'stability'` | v1.25.0+ |

&#x20;

### Sentry error monitoring

_Note_ This feature is **deprecated**. All ENV variables will be removed in the future releases.

| Variable                              | Type      | Description                                             | Compulsoriness | Default value | Example value   | Version  |
| ------------------------------------- | --------- | ------------------------------------------------------- | -------------- | ------------- | --------------- | -------- |
| NEXT\_PUBLIC\_SENTRY\_DSN             | `string`  | Client key for your Sentry.io app                       | Required       | -             | `<your-secret>` | v1.0.x+  |
| SENTRY\_CSP\_REPORT\_URI              | `string`  | URL for sending CSP-reports to your Sentry.io app       | -              | -             | `<your-secret>` | v1.0.x+  |
| NEXT\_PUBLIC\_SENTRY\_ENABLE\_TRACING | `boolean` | Enables tracing and performance monitoring in Sentry.io | -              | `false`       | `true`          | v1.17.0+ |

&#x20;

### Rollbar error monitoring

| Variable                             | Type     | Description                           | Compulsoriness | Default value | Example value   | Version  |
| ------------------------------------ | -------- | ------------------------------------- | -------------- | ------------- | --------------- | -------- |
| NEXT\_PUBLIC\_ROLLBAR\_CLIENT\_TOKEN | `string` | Client token for your Rollbar project | Required       | -             | `<your-secret>` | v1.37.x+ |

&#x20;

### OpenTelemetry

OpenTelemetry SDK for Node.js app could be enabled by passing `OTEL_SDK_ENABLED=true` variable. Configure the OpenTelemetry Protocol Exporter by using the generic environment variables described in the [OT docs](https://opentelemetry.io/docs/specs/otel/protocol/exporter/#configuration-options). Note that this Next.js feature is currently experimental. The Docker image should be built with the `NEXT_OPEN_TELEMETRY_ENABLED=true` argument to enable it.

| Variable           | Type      | Description                         | Compulsoriness | Default value | Example value | Version  |
| ------------------ | --------- | ----------------------------------- | -------------- | ------------- | ------------- | -------- |
| OTEL\_SDK\_ENABLED | `boolean` | Run-time flag to enable the feature | Required       | `false`       | `true`        | v1.18.0+ |

&#x20;

### DeFi dropdown

If the feature is enabled, a single button or a dropdown (if more than 1 item is provided) will be displayed at the top of the explorer page, which will take a user to the specified application in the marketplace or to an external site.

| Variable                            | Type                                                              | Description                                                                                                 | Compulsoriness | Default value | Example value                                                                                                                 | Version  |
| ----------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | -------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_DEFI\_DROPDOWN\_ITEMS | `[{ text: string; icon: string; dappId?: string, url?: string }]` | An array of dropdown items containing the button text, icon name and dappId in DAppscout or an external url | -              | -             | `[{'text':'Swap','icon':'swap','dappId':'uniswap'},{'text':'Payment link','icon':'payment_link','dappId':'peanut-protocol'}]` | v1.31.0+ |

&#x20;

### Multichain balance button

If the feature is enabled, a Multichain balance button will be displayed on the address page, which will take you to the portfolio application in the marketplace or to an external site.

| Variable                                            | Type                                                                       | Description                                                                                             | Compulsoriness | Default value | Example value                                                                                                         | Version  |
| --------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------- | ------------- | --------------------------------------------------------------------------------------------------------------------- | -------- |
| NEXT\_PUBLIC\_MULTICHAIN\_BALANCE\_PROVIDER\_CONFIG | `[{ name: string; url_template: string; dapp_id?: string; logo: string }]` | Multichain portfolio application config See [below](envs.md#multichain-button-configuration-properties) | -              | -             | `[{ name: 'zerion', url_template: 'https://app.zerion.io/{address}/overview', logo: 'https://example.com/icon.svg'}]` | v1.31.0+ |

&#x20;

#### Multichain button configuration properties

| Variable      | Type     | Description                                                                                 | Compulsoriness | Default value | Example value                              |
| ------------- | -------- | ------------------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------ |
| name          | `string` | Multichain portfolio application name                                                       | Required       | -             | `zerion`                                   |
| url\_template | `string` | Url template to the portfolio. Should be a template with `{address}` variable               | Required       | -             | `https://app.zerion.io/{address}/overview` |
| dapp\_id      | `string` | Set for open a Blockscout dapp page with the portfolio instead of opening external app page | -              | -             | `zerion`                                   |
| logo          | `string` | Multichain portfolio application logo (.svg) url                                            | -              | -             | `https://example.com/icon.svg`             |

&#x20;

### Get gas button

If the feature is enabled, a Get gas button will be displayed in the top bar, which will take you to the gas refuel application in the marketplace or to an external site.

| Variable                                    | Type                                                                      | Description                                                                         | Compulsoriness | Default value | Example value                                                                                                                                          | Version  |
| ------------------------------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | -------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| NEXT\_PUBLIC\_GAS\_REFUEL\_PROVIDER\_CONFIG | `{ name: string; url_template: string; dapp_id?: string; logo?: string }` | Get gas button config. See [below](envs.md#get-gas-button-configuration-properties) | -              | -             | `{ name: 'Need gas?', dapp_id: 'smol-refuel', url_template: 'https://smolrefuel.com/?outboundChain={chainId}', logo: 'https://example.com/icon.png' }` | v1.33.0+ |

&#x20;

#### Get gas button configuration properties

| Variable      | Type     | Description                                                              | Compulsoriness | Default value | Example value                                     |
| ------------- | -------- | ------------------------------------------------------------------------ | -------------- | ------------- | ------------------------------------------------- |
| name          | `string` | Text on the button                                                       | Required       | -             | `Need gas?`                                       |
| url\_template | `string` | Url template, may contain `{chainId}` variable                           | Required       | -             | `https://smolrefuel.com/?outboundChain={chainId}` |
| dapp\_id      | `string` | Set for open a Blockscout dapp page instead of opening external app page | -              | -             | `smol-refuel`                                     |
| logo          | `string` | Gas refuel application logo url                                          | -              | -             | `https://example.com/icon.png`                    |

&#x20;

### Save on gas with GasHawk

The feature enables a "Save with GasHawk" button next to the "Gas used" value on the address page.

| Variable                             | Type      | Description                         | Compulsoriness | Default value | Example value | Version  |
| ------------------------------------ | --------- | ----------------------------------- | -------------- | ------------- | ------------- | -------- |
| NEXT\_PUBLIC\_SAVE\_ON\_GAS\_ENABLED | `boolean` | Set to "true" to enable the feature | -              | -             | `true`        | v1.35.0+ |

&#x20;

### Rewards service API

This feature enables Blockscout Merits program. It requires that the [My account](envs.md#my-account) and [Blockchain interaction](envs.md#blockchain-interaction-writing-to-contract-etc) features are also enabled.

| Variable                                  | Type     | Description | Compulsoriness | Default value | Example value         | Version  |
| ----------------------------------------- | -------- | ----------- | -------------- | ------------- | --------------------- | -------- |
| NEXT\_PUBLIC\_REWARDS\_SERVICE\_API\_HOST | `string` | API URL     | -              | -             | `https://example.com` | v1.36.0+ |

&#x20;

### DEX pools

| Variable                                | Type      | Description                       | Compulsoriness | Default value | Example value                                    | Version  |
| --------------------------------------- | --------- | --------------------------------- | -------------- | ------------- | ------------------------------------------------ | -------- |
| NEXT\_PUBLIC\_DEX\_POOLS\_ENABLED       | `boolean` | Set to true to enable the feature | Required       | -             | `true`                                           | v1.37.0+ |
| NEXT\_PUBLIC\_CONTRACT\_INFO\_API\_HOST | `string`  | Contract Info API endpoint url    | Required       | -             | `https://contracts-info.services.blockscout.com` | v1.0.x+  |

&#x20;

### Badge claim link

| Variable                               | Type     | Description                                    | Compulsoriness | Default value | Example value         | Version  |
| -------------------------------------- | -------- | ---------------------------------------------- | -------------- | ------------- | --------------------- | -------- |
| NEXT\_PUBLIC\_GAME\_BADGE\_CLAIM\_LINK | `string` | Provide to enable the easter egg badge feature | -              | -             | `https://example.com` | v1.37.0+ |

&#x20;

## External services configuration

### Google ReCaptcha

To obtain the variable values, please refer to the [reCAPTCHA documentation](https://developers.google.com/recaptcha) and check the [Blockscout reCAPTCHA config docs](https://docs.blockscout.com/setup/configuration-options/recaptcha). Please note that we currently support only **reCAPTCHA v2 in invisible mode**, read more [here](https://developers.google.com/recaptcha/docs/versions#recaptcha_v2_invisible_recaptcha_badge).

| Variable                                      | Type     | Description                                 | Compulsoriness | Default value | Example value     | Version |
| --------------------------------------------- | -------- | ------------------------------------------- | -------------- | ------------- | ----------------- | ------- |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_V3\_APP\_SITE\_KEY | `string` | **DEPRECATED** Google reCAPTCHA v3 site key | -              | -             | `<your-secret>`   | v1.36.x |
| NEXT\_PUBLIC\_RE\_CAPTCHA\_APP\_SITE\_KEY     | `string` | Google reCAPTCHA v2 site key                | -              | -             | `<your-site-key>` | v1.0.x+ |
