# Why are Market Cap/Token Price stats wrong?

One reason may be related to the CoinGecko API refusing Blockscout requests without an API key.&#x20;

If impacted, apply this pull request to your instance:&#x20;

[https://github.com/blockscout/blockscout/pull/5613](https://github.com/blockscout/blockscout/pull/5613)

It implements CoinGecko API key management and alternative CoinMarketCap exchange rates.
