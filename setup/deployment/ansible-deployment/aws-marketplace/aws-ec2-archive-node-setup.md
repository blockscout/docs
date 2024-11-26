---
description: >-
  The following provides an example node setup. Performance related parameters
  will vary per chain.
---

# AWS EC2 archive node setup with OpenEthereum (formerly Parity)

{% hint style="warning" %}
See the [OpenEthereum Documentation](https://openethereum.github.io/wiki/) for complete instructions for any chain setup
{% endhint %}

{% hint style="info" %}
Any chain requires an amount of storage capable of storing all archive data. For best performance choose the best available storage device (ie NVMe SSD).
{% endhint %}

1.  Setup an EC2 instance and choose the best available storage  (ie NVMe SSD).&#x20;

    [https://aws.amazon.com/ec2/getting-started/](https://aws.amazon.com/ec2/getting-started/)

    * During setup you will [configure Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html). For security purposes, you should limit the inbound traffic to RPC and WebSocket interfaces (default ports are `8545` and `8546`). Limit connection to these ports to the BlockScout application server's IP address if setting up BlockScout (find in the details section of your created instance) or to your local network.  You can also set limit port connections later through the EC2 -> Security Groups panel.\

2.  [Connect to your instance using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html) Specify the private key ( `.pem` ) file, the user name for your AMI, and the public DNS name for your instance. For example, if you used Amazon Linux 2 or the Amazon Linux AMI, the user name is `ec2-user`. If ubuntu, the user name is `ubuntu`. \
    [Find info about your instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-get-info-about-instance)

    \
    **Example:** `ssh -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com`\

3. Install OpenEthereum from [GitHub releases page](https://github.com/openethereum/openethereum/releases) for the corresponding platform\

4. Create a config file called node.toml (**see below for config file specs including** [**xDai archive node specs**](aws-ec2-archive-node-setup.md#xdai-archive-node-configuration)) and edit accordingly `vim node.toml`\

5. Connect and Sync an archive node using the config file. `parity --config node.toml`\

6.  Find your EC2 url to connect with BlockScout: Go to **EC2 Dashboard -> Instances ->&#x20;**_**corresponding archive node instance**_ and record the ip address. When configuring BlockScout you will use this address along with port 8545 to connect via the EthereumJsonRPCHttpURL parameter.

    For example: `192.0.2.1:8545`

**Additional Resources**

* [AWS Marketplace Instructions](aws-marketplace-installation.md)
* [See the xDai Docs for instructions on installing a local instance of xDai using OpenEthereum or Nethermind](https://www.xdaichain.com/for-developers/install-xdai-client).

#### Node.toml file general instructions

Below we provide a general example file as well as the settings we use for our xDai node config. In general:

* Parity should run in "fatdb+archive+traces" mode with `pruning="archive"`, `fatdb="on"`, `tracing="on"`.
* Both RPC and WebSockets interfaces should be opened and allow calls to `"web3","eth","net","parity","pubsub","traces"` APIs.
* A full list of configuration options is available at: [https://wiki.parity.io/Configuring-Parity-Ethereum](https://openethereum.github.io/wiki/Configuring-Parity-Ethereum)

## Configuration file example

The following example file outlines general parameters - Performance-related parameters like `processing_threads`, `server_threads` or `cache_size_db` will vary based on the chain size, available hardware, parity version, general traffic load etc. Often these are adjusted through a trial-and-error process. [See below for xDai Archive Node Specs.](aws-ec2-archive-node-setup.md#xdai-archive-node-configuration)

### General Specs

```
[parity]
chain = "CHAIN NAME or PATH TO SPEC.JSON"

[network]
nat="ext:<PUBLIC IP>"
warp = false

[rpc]
apis = ["web3","eth","net","parity","traces"]
processing_threads = 8
server_threads = 16
interface = "0.0.0.0"
cors=["all"]

[websockets]
port = 8546
interface = "0.0.0.0"
max_connections = 1000
apis = ["web3","eth","net","parity","pubsub","traces"]
origins = ["all"]
hosts = ["all"]

[ui]
disable = true

[snapshots]
disable_periodic = true

[footprint]
tracing = "on"
pruning = "archive"
fat_db = "on"
cache_size_db = 12000
```

### xDai archive node configuration

These are the settings we use to run the xDai archive node.

```
[parity]
chain = "xdai"

[network]
nat="ext:<PUBLIC IP>"

[rpc]
apis = ["web3","eth","net", "parity", "traces"]
processing_threads = 50
server_threads = 100
interface = "0.0.0.0"
cors=["all"]

[footprint]
tracing = "on"
pruning = "archive"
fat_db = "on"

[websockets]
max_connections = 1000
interface = "0.0.0.0"
apis = ["web3","eth","net","parity", "pubsub", "traces"]
origins = ["all"]
hosts = ["all"]

[ui]
disable = true

[snapshots]
disable_periodic = true

[mining]
min_gas_price = 1000000000
```

{% hint style="success" %}
This instruction was moved from: [https://forum.poa.network/t/example-archive-node-setup-with-parity-on-an-aws-ec2-instance/3077](https://forum.poa.network/t/example-archive-node-setup-with-parity-on-an-aws-ec2-instance/3077)
{% endhint %}
