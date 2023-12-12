# Hardware & Hosting Requirements

Resource requirements may vary based on chain size and other parameters. This mainly impacts [database storage](../for-developers/information-and-settings/database-storage-requirements.md) requirements. Basic [prerequisites ](../for-developers/information-and-settings/requirements.md)and settings can be found throughout the [Information and Settings](../for-developers/information-and-settings/) section for developers.

BlockScout requires a full archive node to import every state change for every address on the target network.

## Recommended Base Hardware

EVM chains can differ in size and requirements, these are the recommendations for optimal performance.

| CPU | 16 core, 32 thread |
| --- | ------------------ |
| RAM | 128GB              |

## Hosting Requirements

Minimums are listed for an AWS Cloud instance and can be inferred to other hosting providers.

|                               |                                                                                                                                                                                                                                                                                                                 |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application                   | <ul><li>1x EC2 m5a.xlarge instance running Linux</li><li>8GB of EBS General Purpose SSD (NVMe)</li></ul>                                                                                                                                                                                                        |
| Database                      | <ul><li>1x RDS Database running on db.t3.large using PostgreSQL v12+</li><li>500GB of General Purpose SSD (depending on chain size)</li><li>See <a href="../for-developers/information-and-settings/database-storage-requirements.md">Database Storage Requirements</a> for chain-relevant baselines.</li></ul> |
| Amazon Elastic Load Balancing | <ul><li>Average 100 new connections/sec per Elastic Load Balancer</li></ul>                                                                                                                                                                                                                                     |

{% hint style="info" %}
Requirements will vary based on chain. For example, these are the recommended requirements for a Harmony Explorer Node:

**Setup**: AWS i3en.12xlarge or equivalent, with local disk storage\
**Storage**: \~24TB (4x NVMe SSD) is recommended for Archival Explorer Nodes on Shard 0\
**OS**: Latest Ubuntu Linux (LTS Version)\
**Network**: 100M+ bandwidth
{% endhint %}

{% hint style="success" %}
For additional information, see:

* [General Requirements:](../for-developers/information-and-settings/requirements.md) Software required for deployment
* [Database Storage Requirements](../for-developers/information-and-settings/database-storage-requirements.md): Storage required for common chains to give a sense of needed storage
* [Node Tracing Requirements](../for-developers/information-and-settings/node-tracing-json-rpc-requirements.md): JSON RPC methods
* [Client Setting Requirements](../for-developers/information-and-settings/client-settings.md): Settings related to client implementations (ie Geth, OpenEthereum, etc)
{% endhint %}
