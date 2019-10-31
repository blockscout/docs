---
description: Prerequisites and installation parameters
---

# AWS Marketplace Installation

## Installation Prerequisites:

#### Required:

1. **Valid email address:** You will receive a temporary password used to access your instance.
2. **Amazon EC2 Public Key \(InstanceKey\)**. You must create or upload a key pair to your AWS account. [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
3. **ARNCertificate:** You must create or import an ssl certificate to the AWS Certificate Manager service. **This requires a registered domain name** you can access.
   * How to create a certificate: [https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html)
   * How to import an existing certificate: [https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html](https://docs.aws.amazon.com/acm/latest/userguide/import-certificate.html)
4. **Access to a full archive node running a blockchain with an EVM client**. The node will be connected during installation using the EthereumJsonRPC parameters. BlockScout currently supports [Geth](https://ethereum.gitbooks.io/frontier-guide/getting_a_client.html), [Parity](https://wiki.parity.io/Setup), [RSK](https://github.com/rsksmart/rskj/wiki/Install-RskJ-and-join-the-RSK-Wasabi-Mainnet) and [Ganache](https://www.trufflesuite.com/docs/ganache/quickstart).
   * [Example Instructions on creating a local node are available here](https://forum.poa.network/t/example-archive-node-setup-with-parity-on-an-aws-ec2-instance/3077).

#### Optional: Route traffic following deployment:

If you leave the `CognitoCallbackDomain` parameter blank during installation and want to use your own domain later, you will need to route traffic to the LoadBalancer and change the Cognito App client settings.

A\) Re-route your DNS

* Example instruction to route traffic using Route 53: [https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-elb-load-balancer.html)

B\) Configure Cognito settings

* Change the callback URL\(s\) in client settings. [https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-settings.html](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-app-settings.html)

## Installation Parameters:

Most parameters can be left as default during installation. For a full list of variables see the ENV variables list.

The following parameters require a user-input value.

| Parameter | Value |
| :--- | :--- |
| ARNCertificate | SSL certificate from point 3 above. More information on certificates is available here: [https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)  Example: `arn:aws:acm:us-east-1:123456789012:certificate/1156aa0c-daa3-4cb1-af6d-6f16202ebf2c` |
| CognitoCallbackDomain | Add the domain\(s\) where you will access BlockScout and append “/oauth2/idpresponse" to the end. If you do not have a domain, leave this field blank. It will be populated with the LoadBalancerDNS created at the end of the process.  Example: `https://your.domain/oauth2/idpresponse` |
| CognitoUserEmail | Enter any valid email. You will receive a temporary password here after deployment.    Example: `youremail@email.com` |
| DBPassword | Add a secure password here for database access. Record this password for later access. |
| EthereumJsonRPCHttpURL | This is the node url used to fetch blocks, transactions, receipts & tokens. See the instructions on setting up a node on AWS for more information. If setup through AWS, you can find the address in EC2 Dashboard -&gt; Instances -&gt; click to corresponding archive node instance.  You will retrieve the ip address and add the port number afterwards. The port for Parity is 8545.  Example: `http://node.ip.address:8545` |
| EthereumJsonRPCTraceURL | Input the same value as above. This is used to fetch internal transactions and block traces.  Example: `http://node.ip.address:8545` |
| EthereumJsonRPCWsURL | The Network RPC endpoint in websocket mode. The default parity port is 8546.  Example: `ws://localhost:8546` |
| GraphiQLTransaction | Any transaction from the chain can be used. This hash provides a sample query in the GraphIQL Playground and always begins with “0x…”  Example: `0x9415741aa80cacb3e2a9f48506010a3f31fddc7e7a00421381b4e4679d5eba20` |
| IngressIPRangeLB | IP address range for access to your LoadBalancer instance. Recommend using `0.0.0.0/0` for access from all IPs, or specify your local IP with `your.ip/32`. You can find your ip here: [https://support.google.com/websearch/answer/1696588](https://support.google.com/websearch/answer/1696588) |
| InstanceKey | From step 2 above. The instance key is located at EC2 Dashboard -&gt; Network & Security -&gt; Key Pairs. It should be available as a dropdown. |
| SecretKeybase | Secret key for production assets protection in base64. You can generate this on the command line of your,local machine using the following command: "openssl rand -base64 16"   Example: `d29vbmcyY2hhaUNvaG5nCg==` |

{% hint style="success" %}
This instruction was moved from [https://forum.poa.network/t/aws-marketplace-installation/3076](https://forum.poa.network/t/aws-marketplace-installation/3076)
{% endhint %}

