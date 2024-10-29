# ☑️ ENV Variables

Blockscout uses ENVs for setting hundreds of different parameters. Please see the various sections for ENV names, descriptions, default values and versioning.

{% hint style="success" %}
* [Backend ENVs: Common](backend-env-variables.md)
* [Backend ENVs: Chain Specific](backend-envs-chain-specific.md)
* [Backend ENVs: Integrations](backend-envs-integrations.md)
* [Frontend ENVs: Common](frontend-common-envs.md)
{% endhint %}

{% hint style="info" %}
You will find deprecated ENV vars on the [Deprecated ENV Variables](https://docs.blockscout.com/for-developers/information-and-settings/deprecated-env-variables) page.
{% endhint %}

## Set ENV Variables with CLI

Use the export command to set variables. For example:

```bash
$ export ETHEREUM_JSONRPC_VARIANT=nethermind
$ export COIN=POA
$ export NETWORK=POA
```

## Required ENV variables

Please see the [Backend ENVs page](backend-env-variables.md) for details. Required variables are located in the General Management section and marked with a ✅

## Example ENV Variables Set

The following variables are set for the [Gnosis Chain Blockscout Instance](https://gnosis.blockscout.com/). _Note that some variables are not included as they contain private information which should not be exposed._

{% file src="../../.gitbook/assets/Gnosis-Chain-Variables.txt" %}

## Time format

Can be set in format `1h` for 1 hour, `1m` for 1 minute, `1s` or `1` for 1 second, `1ms` for 1 millisecond

{% hint style="warning" %}
_Note_: **Before release 5.1.2, all environment variables of time format supported only integers in seconds (without dimensions) as values.**
{% endhint %}

