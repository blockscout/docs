# Separate Indexer, Web App, and API

Blockscout supports several modes which run in a single all-in-one application by default.

**Modes**

* [Indexer](separate-indexer-web-app-and-api.md#indexer-mode)
* [Web UI](separate-indexer-web-app-and-api.md#web-application-mode)
* [API](separate-indexer-web-app-and-api.md#api-mode)
* All-in-one (default)

It is possible to run modes separately or in different combinations. For example, you may want to run the `indexer mode + API` to create an indexed db with programmatic access and no UI, or `indexer mode + UI` to leverage Blockscout as a read-only explorer.

Note that the application is limited to 1 running indexer per 1 Blockscout instance.  However, the indexer automatically reruns child processes within the Elixir architecture, making it quite fault-tolerant.&#x20;

To run these modes separately, adjust ENV variables as follows:

{% hint style="info" %}
After extending the set of environment variables for the instance, recompile the application (or rebuilt the docker image, if this is Docker version) to enable mode settings.
{% endhint %}

## Indexer mode

To run Blockscout in indexer mode, disable the web application and API:

```javascript
export DISABLE_WEBAPP=true
export API_V1_READ_METHODS_DISABLED=true
export API_V1_WRITE_METHODS_DISABLED=true
```

## Web application mode

To run Blockscout in web application mode only, disable the indexer and API read methods (API write functionality is not disabled to support smart contracts verification in the UI).

```javascript
export DISABLE_INDEXER=true
export API_V1_READ_METHODS_DISABLED=true
```

{% hint style="info" %}
If you have a separate web application and indexer and they are connected to the same database (via DATABASE\_URL), you will see new incoming items on the web UI like in the all-in-one mode. This configuration allows you to scale the web UI separately from indexer.
{% endhint %}

## API mode

To run in API mode, disable the indexer and webapp.

```jsx
export DISABLE_INDEXER=true
export DISABLE_WEBAPP=true
```

{% hint style="info" %}
In API mode the web UI will show the API docs page at the default path (/). In the default all-in-one mode, it is located on the /api-docs page.
{% endhint %}

## Web UI + API mode

```
export DISABLE_INDEXER=true
```
