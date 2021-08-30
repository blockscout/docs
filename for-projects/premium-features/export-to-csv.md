---
description: Export of blockchain entities related to address into a CSV file
---

# Export to CSV

Export to CSV is a premium feature providing users a way to easily download and analyze blockchain data. It is available for tabs on the address page including transactions, internal transactions, tokens, and logs.

{% hint style="info" %}
Note: simplified CSV exports \(transactions and transfers only, with no ability to define time periods\) __exist in Blockscout releases up to 3.5.1. From v3.5.2+ enhanced CSV export is available as a premium feature.
{% endhint %}

![](../../.gitbook/assets/screenshot-2021-02-01-at-09.54.38.png)

You will find the _Download CSV_ button under the list of entities related to the tab.

![](../../.gitbook/assets/screenshot-2021-02-01-at-09.59.12.png)

_Note:_ under the _Tokens_ tab, the list of token transfers will be exported.

After clicking the button you will be forwarded to a  _/csv-export_ page for a given address and given type of export \(transactions, internal-transactions, token-transfers, logs\).

![](../../.gitbook/assets/screenshot-2021-01-28-at-20.46.23%20%281%29%20%281%29%20%281%29%20%281%29.png)

It is possible to specify an arbitrary period for the data export. By default, the current period is the previous month. After completing the reCaptcha, the data for the chosen period should be exported.

![](../../.gitbook/assets/screenshot-2021-02-01-at-10.11.08.png)

{% hint style="info" %}
_Tip_: In order to prevent hitting a 30 secs loading timeout, choose the smallest period possible for your data needs. 
{% endhint %}

