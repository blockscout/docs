# ☑️ ENV Variables

Blockscout uses ENVs for setting hundreds of different parameters. Please see the various sections for ENV names, descriptions, default values and versioning.

See below for info on setting ENV variables, time formatting and other info.

{% hint style="success" %}
* [Backend ENVs: Common](env-variables/backend-env-variables.md)
* [Backend ENVs: Chain Specific](env-variables/backend-envs-chain-specific.md)
* [Backend ENVs: Integrations](env-variables/backend-envs-integrations.md)
* [Frontend ENVs: Common](env-variables/frontend-common-envs.md)
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

## Example ENV Variables Set

The following variables are set for the [Gnosis Chain Blockscout Instance](https://gnosis.blockscout.com/). _Note that some variables are not included as they contain private information which should not be exposed._

{% file src="../../.gitbook/assets/Gnosis-Chain-Variables.txt" %}

## Backend ENV spreadsheet

[Link to a google sheet with active ENVs](https://docs.google.com/spreadsheets/d/17-mbKNyi\_lqZOYfjDCZnEbjA9OldVL1BvLoWP8MsTaM/edit?usp=sharing)

## Time format

Can be set in format `1h` for 1 hour, `1m` for 1 minute, `1s` or `1` for 1 second, `1ms` for 1 millisecond

{% hint style="warning" %}
_Note_: **Before release 5.1.2, all environment variables of time format supported only integers in seconds (without dimensions) as values.**
{% endhint %}

