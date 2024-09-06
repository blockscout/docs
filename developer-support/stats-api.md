# Stats API

{% hint style="info" %}
More Info coming soon
{% endhint %}

The [stats microservice](https://github.com/blockscout/blockscout-rs/tree/main/stats) collects data from a Blockscout instance and calculates statistics based on predefined values. The calculated data is available through a REST API, providing access to this statistical information. There are 3 primary endpoints=

{% swagger src="../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json" path="/api/v2/stats" method="get" %}
[ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json](<../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json>)
{% endswagger %}

{% swagger src="../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json" path="/api/v2/stats/charts/transactions" method="get" %}
[ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json](<../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json>)
{% endswagger %}

{% swagger src="../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json" path="/api/v2/stats/charts/market" method="get" %}
[ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json](<../.gitbook/assets/ANDREWGROSS_1-Stats-1.0.0-resolved (1) (1).json>)
{% endswagger %}

