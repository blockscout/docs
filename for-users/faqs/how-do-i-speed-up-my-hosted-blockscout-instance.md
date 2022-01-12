# How do I speed up my hosted BlockScout instance?

BlockScout can be resource intensive. If your instance is running slowly:

* clear the cache - the application cache is cleared on restart by running:\
  `sudo systemctl restart explorer.service`
* increase the memory limit for indexers [https://github.com/poanetwork/blockscout/blob/b48305ece284e00084e2bb47ff1ad501bf24f115/apps/indexer/config/config.exs#L36 8](https://github.com/poanetwork/blockscout/blob/b48305ece284e00084e2bb47ff1ad501bf24f115/apps/indexer/config/config.exs#L36) if indexing is slow.
* increase the number of CPUs if CPU is running at 100% on the web app server
* increase the memory if memory consumption is high on the web app server
* increase the number of CPUs or/and increase the memory on the database server if consumption is high.

Instructions for accessing and upgrading CPUs/memory will differ based on your setup. If you are running BlockScout on AWS, these settings can be accessed through your AWS services portal.

{% hint style="success" %}
Content moved from: [https://forum.poa.network/t/faq-hosted-blockscout-instance-is-running-slowly/2473](https://forum.poa.network/t/faq-hosted-blockscout-instance-is-running-slowly/2473)
{% endhint %}
