# How can I customize the coin symbol / name?

### Exchange Rates Coin Name

* Specify coin name for exchange rates fetcher with the `COIN` [ENV variables ](../information-and-settings/env-variables.md)

BlockScout utilizes the `COIN` environment variable which pulls the associated market data from the Coinmarketcap.com API or CoinGecko API to provide pricing data throughout the application.


### Displayed Coin Symbol

In order to set displayed coin symbol, instance maintainer should set `COIN_NAME` runtime environment variable:

```text
export COIN_NAME=
```

For instance, in case of POA instance of Blockscout:

```text
export COIN_NAME=POA
```
