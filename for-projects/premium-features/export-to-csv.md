---
description: Export of blockchain entities related to address into CSV file
---

# Export to CSV

_Side note:_ simplified export to CSV\*  __contained in Blockscout releases up to 3.5.1. From 3.5.2 enhanced CSV export is available as a premium feature.

\*export of transactions and tokens transfers is supported only, and there is no way to indicate a period of unloading.

Export to CSV is available under several tabs of address page: transactions, internal transactions, tokens, logs.

![](../../.gitbook/assets/screenshot-2021-02-01-at-09.54.38.png)

You will find _Download CSV_ button under the list of entities related to the tab.

![](../../.gitbook/assets/screenshot-2021-02-01-at-09.59.12.png)

_Note:_ under the _Tokens_ tab, the list of token transfers will be exported.

After clicking to the button you will be moved to _/csv-export_ page for a given address and given type of export \(transactions, internal-transactions, token-transfers, logs\).

![](../../.gitbook/assets/screenshot-2021-01-28-at-20.46.23%20%281%29.png)

It is possible to specify an arbitrary period for the data to be exported. By default, the current period is the last month. After challenging reCaptcha the  data for chosen period should be exported.

![](../../.gitbook/assets/screenshot-2021-02-01-at-10.11.08.png)

_Tip_: In order to prevent hitting 30 secs loading timeout, choose a period as smaller as possible.

