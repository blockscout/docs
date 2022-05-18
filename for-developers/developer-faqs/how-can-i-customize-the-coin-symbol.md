# How can I customize the coin symbol / name?

### Coin Name

* Specify coin name with the `COIN` and `COIN_NAME` [ENV variables ](../information-and-settings/env-variables.md)

BlockScout utilizes the `COIN` environment variable which pulls the associated market data from the Coinmarketcap.com API or CoinGecko API to provide pricing data throughout the application.

{% hint style="info" %}
Variable can be set manually here:\
[https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/explorer/config/config.exs#L11](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/explorer/config/config.exs#L11)\
\
po file (see below for more details re:po files)\
[https://github.com/blockscout/blockscout/blob/master/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po#L1121](https://github.com/blockscout/blockscout/blob/master/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po#L1121)
{% endhint %}

### Displayed Coin Symbol

BlockScout uses `gettext` to create the displayed coin symbols throughout the application. Gettext documentation is [available here](https://hexdocs.pm/gettext/Gettext.html). In BlockScout there are `po` and `pot` files in the `BlockScoutWeb` Umbrella application.

The default text will be listed as ([Example Instance](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po#L405)):

* msgid "ETH"
* msgstr "POA"

To edit the POA symbol throughout the application, replace the `msgstr` value with your target value in the following files:

**Po File:** [https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po)

**Pot File:** [https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/default.pot](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/default.pot)

{% hint style="success" %}
Content moved from: [https://forum.poa.network/t/faq-how-can-i-customize-coin-symbol/1875](https://forum.poa.network/t/faq-how-can-i-customize-coin-symbol/1875)
{% endhint %}

