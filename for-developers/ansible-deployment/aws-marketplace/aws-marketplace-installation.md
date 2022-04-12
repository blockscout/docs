---
description: Prerequisites and installation parameters
---

# Prerequisites & Install Parameters

## Installation Prerequisites:

#### Required:

1. **Valid email address:** You will receive a temporary password used to access your instance.
2. **Amazon EC2 Public Key (InstanceKey)**. You must create or upload a key pair to your AWS account. [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
3. **ARNCertificate:** You must create or import an ssl certificate to the AWS Certificate Manager service. **This requires a registered domain name** you can access.
   * How to create a certificate: [https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html)
   * How to import an existing certificate: [https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html)
4. **Access to a full archive node running a blockchain with an EVM client**. The node will be connected during installation using the EthereumJsonRPC parameters. BlockScout currently supports [Geth](https://ethereum.gitbooks.io/frontier-guide/getting\_a\_client.html), [Parity](https://wiki.parity.io/Setup), [RSK](https://github.com/rsksmart/rskj/wiki/Install-RskJ-and-join-the-RSK-Wasabi-Mainnet) and [Ganache](https://www.trufflesuite.com/docs/ganache/quickstart).
   * [Example Instructions on creating a local node are available here.](aws-ec2-archive-node-setup.md)

#### Optional: Route traffic following deployment:

If you leave the `CognitoCallbackDomain` parameter blank during installation and want to use your own domain later, you will need to route traffic to the LoadBalancer and change the Cognito App client settings.

A) Re-route your DNS

* Example instruction to route traffic using Route 53: [https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html)

B) Configure Cognito settings

* Change the callback URL(s) in client settings. [https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-settings.html](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-settings.html)

## AWS Installation:

See [Install from AWS Marketplace](install-from-aws-marketplace.md) for an installation walkthrough.

## Installation Parameters:

Most parameters can be left as default during installation. For a full list of variables see the [ENV variables list](../../information-and-settings/env-variables.md).

{% hint style="info" %}
During configuration, the first item to input is **Stack Name.** This is an identifier that helps you find a particular stack from a list of stacks. It must start with an alphabetic character and can't be longer than 128 characters.
{% endhint %}

The following parameters require a user-input value.

| Parameter               | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ARNCertificate          | <p>SSL certificate from point 3 above. More information on certificates is available here: <a href="https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html">https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html</a><br><br>Example: <code>arn:aws:acm:us-east-1:123456789012:certificate/1156aa0c-daa3-4cb1-af6d-6f16202ebf2c</code></p>                                                                                            |
| CognitoCallbackDomain   | <p>Add the domain(s) where you will access BlockScout and append “/oauth2/idpresponse" to the end. <strong>If you do not have a domain, leave this field blank</strong>. It will be populated with the LoadBalancerDNS created at the end of the process.<br><br>Example: <code>https://your.domain/oauth2/idpresponse</code></p>                                                                                                                              |
| CognitoUserEmail        | <p>Enter any valid email. You will receive a temporary password here after deployment. <br><br> Example: <code>youremail@email.com</code></p>                                                                                                                                                                                                                                                                                                                  |
| DBPassword              | Add a secure password here for database access. Must contain only letters and numbers, and be 8 characters or more. **Record this password for later access**.                                                                                                                                                                                                                                                                                                 |
| EthereumJsonRPCHttpURL  | <p>This is the node url used to fetch blocks, transactions, receipts &#x26; tokens. See the instructions on setting up a node on AWS for more information. If setup through AWS, you can find the address in EC2 Dashboard -> Instances -> click to corresponding archive node instance.<br><br>You will retrieve the ip address and add the port number afterwards. The port for Parity is 8545.<br><br>Example: <code>http://node.ip.address:8545</code></p> |
| EthereumJsonRPCTraceURL | <p>Input the same value as above. This is used to fetch internal transactions and block traces.<br><br>Example: <code>http://node.ip.address:8545</code></p>                                                                                                                                                                                                                                                                                                   |
| EthereumJsonRPCWsURL    | <p>The Network RPC endpoint in websocket mode. The default parity port is 8546.<br><br>Example: <code>ws://localhost:8546</code></p>                                                                                                                                                                                                                                                                                                                           |
| GraphiQLTransaction     | <p>Any transaction from the chain can be used. This hash provides a sample query in the GraphIQL Playground and always begins with “0x…”<br><br>Example: <code>0x9415741aa80cacb3e2a9f48506010a3f31fddc7e7a00421381b4e4679d5eba20</code></p>                                                                                                                                                                                                                   |
| IngressIPRangeLB        | IP address range for access to your LoadBalancer instance. Recommend using `0.0.0.0/0` for access from all IPs, or specify your local IP with `your.ip/32`. You can find your ip here: [https://support.google.com/websearch/answer/1696588](https://support.google.com/websearch/answer/1696588)                                                                                                                                                              |
| InstanceKey             | From step 2 above. The instance key name is located at EC2 Dashboard -> Network & Security -> Key Pairs. It should be available as a dropdown in the template.                                                                                                                                                                                                                                                                                                 |
| SecretKeybase           | <p>Secret key for production assets protection in base64. You can generate this on the command line of your local machine using the following command: "openssl rand -base64 16" <br><br>Example: <code>d29vbmcyY2hhaUNvaG5nCg==</code></p>                                                                                                                                                                                                                    |

{% hint style="success" %}
This instruction was moved from [https://forum.poa.network/t/aws-marketplace-installation/3076](https://forum.poa.network/t/aws-marketplace-installation/3076)
{% endhint %}
