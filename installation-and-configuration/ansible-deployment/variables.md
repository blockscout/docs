---
description: ENV variables must be configured per chain
---

# Variables

## Configuration

The single point of configuration in this script is a `group_vars/all.yml` file. 

First, copy it from `group_vars/all.yml.example` template by executing the `cp group_vars/all.yml.example group_vars/all.yml` command. Then modify it via any text editor you want \(vim example - `vim group_vars/all.yml`\). 

The subsections below describe the variables you may want to adjust. 

* [Common Variables](variables.md#common-variables)
* [Infrastructure Variables](variables.md#infrastructure-variables)
* [BlockScout Detail Variables](variables.md#blockscout-detail-variables)

## Common Variables

* `aws_access_key` and `aws_secret_key` is a credentials pair that provides access to AWS for the deployer.
* `backend` variable defines whether deployer should keep state files remote or locally. Set `backend` variable to `true` if you want to save state file to the remote S3 bucket.
* `upload_config_to_s3` - set to `true` if you want to upload config `all.yml` file to the S3 bucket automatically after the deployment. Will not work if `backend` is set to false.
* `upload_debug_info_to_s3` - set to `true` if you want to upload full log output to the S3 bucket automatically after the deployment. Will not work if `backend` is set to false.

{% hint style="danger" %}
Locally logs are stored at `log.txt` which is not cleaned automatically. Do not forget to clean manually or use the `clean.yml` playbook
{% endhint %}

* `bucket` represents a globally unique name of the bucket where your configs and state will be stored. It will be created automatically during the deployment.
* `prefix` - is a unique tag to use for provisioned resources \(5 alphanumeric chars or less\).
* `chains` - maps chains to the URLs of HTTP RPC endpoints, an ordinary blockchain node can be used.
* The `region` should be left at `us-east-1` as some of the other regions fail for different reasons.

{% hint style="warning" %}
a chain name SHOULD NOT be more than 5 characters. Otherwise, it will throw an error because the aws load balancer name should not be greater than 32 characters.
{% endhint %}

## Infrastructure Variables

* `dynamodb_table` represents the name of table that will be used for Terraform state lock management.
* If `ec2_ssh_key_content` variable is not empty, Terraform will try to create EC2 SSH key with the `ec2_ssh_key_name` name. Otherwise, the existing key with `ec2_ssh_key_name` name will be used.
* `instance_type` defines a size of the Blockscout instance that will be launched during the deployment process.
* `vpc_cidr`, `public_subnet_cidr`, `db_subnet_cidr` represent the network configuration for the deployment. Usually you will leave as is. However, if you want to modify, understand that `db_subnet_cidr` represents not a single network, but a group of networks that start with a defined CIDR block increased by 8 bits.

{% hint style="info" %}
Number of networks: 2   
 `db_subnet_cidr`: "10.0.1.0/16"  
 Real networks: 10.0.1.0/24 and 10.0.2.0/24
{% endhint %}

* An internal DNS zone with`dns_zone_name` name will be created to take care of BlockScout internal communications.
* The name of a IAM key pair to use for EC2 instances, if you provide a name which already exists it will be used, otherwise it will be generated for you.
* If `use_ssl` is set to `false`, SSL will be forced on Blockscout. To configure SSL, use `alb_ssl_policy` and `alb_certificate_arn` variables.
* The `root_block_size` is the amount of storage on your EC2 instance. This value can be adjusted by how frequently logs are rotated. Logs are located in `/opt/app/logs` of your EC2 instance.
* The `pool_size` defines the number of connections allowed by the RDS instance;
* `secret_key_base` is a random password used for BlockScout internally. It is highly recommended to gernerate your own `secret_key_base` before the deployment. For instance, you can do it via `openssl rand -base64 64 | tr -d '\n'` command.
* `new_relic_app_name` and `new_relic_license_key` should usually stay empty unless you want and know how to configure New Relic integration.
* `elixir_version` - is an Elixir version used in BlockScout release.
* `chain_trace_endpoint` - maps chains to the URLs of HTTP RPC endpoints, which represents a node where state pruning is disabled \(archive node\) and tracing is enabled. If you don't have a trace endpoint, you can simply copy values from `chains` variable.
* `chain_ws_endpoint` - maps chains to the URLs of HTTP RPCs that supports websockets. This is required to get the real-time updates. Can be the same as `chains` if websocket is enabled there \(but make sure to use`ws(s)` instead of `htpp(s)` protocol\).
* `chain_jsonrpc_variant` - a client used to connect to the network. Can be `parity`, `geth`, etc.
* `chain_logo` - maps chains to the it logos. Place your own logo at `apps/block_scout_web/assets/static` and specify a relative path at `chain_logo` variable.
* `chain_coin` - a name of the coin used in each particular chain.
* `chain_network` - usually, a name of the organization keeping group of networks, but can represent a name of any logical network grouping you want.
* `chain_subnetwork` - a name of the network to be shown at BlockScout.
* `chain_network_path` - a relative URL path which will be used as an endpoint for defined chain. For example, if we will have our BlockScout at `blockscout.com` domain and place `core` network at `/poa/core`, then the resulting endpoint will be `blockscout.com/poa/core` for this network.
* `chain_network_icon` - maps the chain name to the network navigation icon at apps/block\_scout\_web/lib/block\_scout\_web/templates/icons without .eex extension.
* `chain_graphiql_transaction` - is a variable that maps chain to a random transaction hash on that chain. This hash will be used to provide a sample query in the GraphIQL Playground.
* `chain_block_transformer` - will be `clique` for clique networks like Rinkeby and Goerli, and `base` for the rest.
* `chain_heart_beat_timeout`, `chain_heart_command` - configs for the integrated heartbeat. First describes a timeout after the command described at the second variable will be executed.
* Each of the `chain_db_*` variables configures the database for each chain. Each chain will have the separate RDS instance.
* `chain_blockscout_version` - is a text at the footer of BlockScout instance. Usually represents the current BlockScout version.

## BlockScout Detail Variables

* `blockscout_repo` - a direct link to the Blockscout repo.
* `chain_branch` - maps branch at `blockscout_repo` to each chain.
* Specify the `chain_merge_commit` variable if you want to merge any of the specified `chains` with the commit in the other branch. Usually may be used to update production branches with the releases from master branch.
* `skip_fetch` - if this variable is set to `true` , BlockScout repo will not be cloned and the process will start from building the dependencies. Use this variable to prevent playbooks from overriding manual changes in cloned repo.
* `ps_*` variables represents a connection details to the test Postgres database. This one will not be installed automatically, so make sure `ps_*` credentials are valid before starting the deployment.
* `chain_custom_environment` - is a map of variables that should be overrided when deploying the new version of Blockscout. Can be omitted.

{% hint style="warning" %}
`chain_custom_environment` variables **will not be** propagated to the Parameter Store at production servers and need to be set there manually.
{% endhint %}

