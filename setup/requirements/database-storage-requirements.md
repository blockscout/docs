# Database Storage Requirements

The configuration variable `db_storage` can be used to define the amount of storage allocated to your RDS instance. The chart below shows an estimated amount of storage that is required to index individual chains. Note these numbers are estimates and are constantly increasing.

&#x20;The `db_storage` can only be adjusted 1 time in a 24 hour period on AWS.

| Chain                | Storage (GiB) |
| -------------------- | ------------- |
| Ethereum Mainnet     | 21000         |
| Ethereum Sepolia     | 5200          |
| Gnosis Chain         | 21000         |
| Gnosis Chiado        | 470           |
| Ethereum Classic     | 555           |

_Note_: as of 23.12.2024

