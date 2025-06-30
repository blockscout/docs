# Kubernetes Deployment

{% hint style="success" %}
&#x20;🚗  [Autoscout is now available](../../using-blockscout/autoscout.md), providing a simple one-click explorer deployment with Blockscout's optimized hosting infrastructure. Use it for early testing, modifications, and launching a full production-grade explorer. [Get Started Now](../../using-blockscout/autoscout.md) and have **your explorer up-and-running in minutes.**
{% endhint %}

We've released a Helm chart to deploy Blockscout stack ([backend](https://github.com/blockscout/blockscout), [frontend](https://github.com/blockscout/frontend) and [stats](https://github.com/blockscout/blockscout-rs/tree/main/stats)) to a kubernetes cluster.&#x20;

Baseline instructions are available at [https://github.com/blockscout/helm-charts/tree/main/charts/blockscout-stack](https://github.com/blockscout/helm-charts/tree/main/charts/blockscout-stack).

### Troubleshooting

1. Check your values are correct, for example if you don't have Prometheus installed [disable it here](https://github.com/blockscout/helm-charts/blob/7fe62850a9d0ab220041598722569ab13fa54540/charts/blockscout-stack/values.yaml#L33)
2. Ingress is disabled by default as is common practice, you will likely want to enable ingress and configure hostnames accordingly.
3. Check your .yaml files for any unneeded whitespaces, this can impact functionality.
4. Make sure env variables are declared correctly ie DATABASE\_URL: “X”
5. Frontend values should exist in their own root section, at the same level as blockscout values (and not nested within the blockscout root).

For example:

````yaml
```yaml
blockscout:
  env:
    DATABASE_URL: "X"
    ETHEREUM_JSONRPC_VARIANT: geth
    ETHEREUM_JSONRPC_HTTP_URL: "X"
    ETHEREUM_JSONRPC_TRACE_URL: "X"
  ingress:
    enabled: true
    hostname: host-name.com
frontend:
  image:
    tag: latest
  ingress:
    enabled: true
```
````
