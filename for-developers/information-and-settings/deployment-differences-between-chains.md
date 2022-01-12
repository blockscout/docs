# Deployment Differences Between Chains

## All chains must define the following ENV variables:

| Environment Variable          | Default                                   |
| ----------------------------- | ----------------------------------------- |
| BLOCKSCOUT\_VERSION           | `unknown`                                 |
| COIN                          | `POA`                                     |
| DB\_HOST                      | -                                         |
| DB\_PASSWORD                  | -                                         |
| DB\_PORT                      | -                                         |
| DB\_USERNAME                  | -                                         |
| ETHEREUM\_JSONRPC\_HTTP\_URL  | `http://localhost:8545`                   |
| ETHEREUM\_JSONRPC\_TRACE\_URL | `http://localhost:8545`                   |
| ETHEREUM\_JSONRPC\_WS\_URL    | `ws://localhost:8546`                     |
| ETHEREUM\_JSONRPC\_VARIANT    | `parity`                                  |
| HEART\_BEAT\_TIMEOUT          | `30`                                      |
| HEART\_COMMAND                | `sudo systemctl restart explorer.service` |
| LOGO                          | `/images/blockscout_logo.svg`             |
| NETWORK                       | `POA Network`                             |
| SUBNETWORK                    | `Sokol Testnet`                           |
| NETWORK\_ICON                 | `_test_network_icon.html`                 |
| LINK\_TO\_OTHER\_EXPLORERS    | `true`                                    |

## Changes not configurable with ENV variables:

**Update `Validated/Validator` to `Mined/Miner` or `Signed/Signer` ** [https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/priv/gettext/default.pot](https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/priv/gettext/default.pot)

**Update Memory Usage:** [https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/indexer/config/config.exs#L36](https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/indexer/config/config.exs#L36)

**Update Theme:** [https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/assets/css/theme/\_variables.scss#L1](https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/assets/css/theme/\_variables.scss#L1)

**Update Coin Name:** [https://github.com/poanetwork/blockscout/blob/5b5a0b3cfe47fcbb3631b82e58aeb2c7c9c48504/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po#L398](https://github.com/poanetwork/blockscout/blob/5b5a0b3cfe47fcbb3631b82e58aeb2c7c9c48504/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po#L398)

**Update other explorers (if-applicable)** [https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/config/config.exs#L22-L26](https://github.com/poanetwork/blockscout/blob/12aa15671142af00b35ff05aeac107c2c686c4c8/apps/block\_scout\_web/config/config.exs#L22-L26)

### POA Core

| Environment Variable       | Value                                        |
| -------------------------- | -------------------------------------------- |
| METADATA\_CONTRACT         | `0xE3FfFD154931EB80b2aCE096EC32D6df23661203` |
| VALIDATORS\_CONTRACT       | `0xa105Db0e6671C7B5f4f350ff1Af6460E6C696e71` |
| LINK\_TO\_OTHER\_EXPLORERS | `false`                                      |

### POA Sokol

| Environment Variable       | Value                                        |
| -------------------------- | -------------------------------------------- |
| METADATA\_CONTRACT         | `0x81c47A798226e1b90A1b4C9dBDd844033B528D06` |
| VALIDATORS\_CONTRACT       | `0x4c6a159659CCcb033F4b2e2Be0C16ACC62b89DDB` |
| LINK\_TO\_OTHER\_EXPLORERS | `false`                                      |

### xDAI

| Environment Variable       | Value                                        |
| -------------------------- | -------------------------------------------- |
| SUPPLY\_MODULE             | `TokenBridge`                                |
| SOURCE\_MODULE             | `TransactionAndLog`                          |
| METADATA\_CONTRACT         | `0x61e561dc17597b15e0195a201b539ee7b9add3ff` |
| VALIDATORS\_CONTRACT       | `0x22e1229a2c5b95a60983b5577f745a603284f535` |
| LINK\_TO\_OTHER\_EXPLORERS | `false`                                      |

### Rinkeby, Goerli (non-hosted)

| Environment Variable | Value    |
| -------------------- | -------- |
| BLOCK\_TRANSFORMER   | `clique` |

{% hint style="success" %}
Content moved from [https://forum.poa.network/t/deployment-differences-between-each-blockscout-chain/1950](https://forum.poa.network/t/deployment-differences-between-each-blockscout-chain/1950)
{% endhint %}



###

###
