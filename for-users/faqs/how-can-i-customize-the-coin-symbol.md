# How can I customize the coin symbol?

BlockScout utilizes the `COIN` environment variable which pulls the associated market data from the Coinmarketcap.com API or CoinGecko API to provide pricing data throughout the application.

{% hint style="info" %}
This variable can be set manually here:  
[https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/explorer/config/config.exs\#L11](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/explorer/config/config.exs#L11)
{% endhint %}

### Displayed Coin Symbol

BlockScout uses `gettext` to create the displayed coin symbols throughout the application. Gettext documentation is [available here](https://hexdocs.pm/gettext/Gettext.html). In BlockScout there are `po` and `pot` files in the `BlockScoutWeb` Umbrella application.

The default text will be listed as \([Example Instance](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block_scout_web/priv/gettext/en/LC_MESSAGES/default.po#L405)\):

* msgid "ETH"
* msgstr "POA"

To edit the POA symbol throughout the application, replace the `msgstr` value with your target value in the following files:

**Po File:** [https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/en/LC\_MESSAGES/default.po](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block_scout_web/priv/gettext/en/LC_MESSAGES/default.po)

**Pot File:** [https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block\_scout\_web/priv/gettext/default.pot](https://github.com/poanetwork/blockscout/blob/03061be2f710a1fc84c6ce555f676e8bb9dfa54d/apps/block_scout_web/priv/gettext/default.pot)

{% hint style="success" %}
Content moved from: [https://forum.poa.network/t/faq-how-can-i-customize-coin-symbol/1875](https://forum.poa.network/t/faq-how-can-i-customize-coin-symbol/1875)
{% endhint %}





