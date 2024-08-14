---
description: Export of blockchain entities related to address into a CSV file
---

# CSV Exports

Export to CSV gives users a way to easily download and analyze blockchain data. It is available for tabs on the address page including transactions, internal transactions, tokens, and logs.

{% hint style="info" %}
Note: simplified CSV exports (transactions and transfers only, with no ability to define time periods) exist in Blockscout releases up to 3.5.1.  Enhanced CSV export is available from v3.5.2+
{% endhint %}

![](<../.gitbook/assets/Screenshot 2021-02-01 at 09.54.38.png>)

You will find the _Download CSV_ button under the list of entities related to the tab.

![](<../.gitbook/assets/Screenshot 2021-02-01 at 09.59.12.png>)

{% hint style="info" %}
_Note:_ under the _Tokens_ tab, the list of token transfers will be exported.
{% endhint %}

After clicking the button you will be forwarded to a _/csv-export_ page for a given address and given type of export (transactions, internal-transactions, token-transfers, logs).

![](<../.gitbook/assets/screenshot-2021-01-28-at-20.46.23 (1) (1) (1) (1) (1).png>)

It is possible to specify an arbitrary period for the data export. By default, the current period is the previous month. After completing the reCaptcha, the data for the chosen period should be exported.

![](<../.gitbook/assets/Screenshot 2021-02-01 at 10.11.08.png>)

{% hint style="info" %}
_Tip_: In order to prevent hitting a 30 secs loading timeout, choose the smallest time period possible for your data needs.
{% endhint %}
