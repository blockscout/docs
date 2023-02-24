# Requests & Limits

The default rate limit for requests is [50 requests/sec](https://github.com/blockscout/blockscout-account/blob/726c806e0ad517eac8f3d5b8ceff31cbf256415b/config/runtime.exs#L121) set via the `default_api_rate_limit` variable. This applies to global requests which do not originate from a whitelisted address or do not use an API key.

* **Individual API key**: An API key can be created by the user in the My Account section (currently available on select instances). Requests made using an individual API key are limited to 50 req/sec but are not shared by other users.
* **Static API key**:  A per instance API key (_note this functionality was created prior to individual API keys and may have limited utility_) can be managed via the `API_RATE_LIMIT_STATIC_API_KEY` variable.
* **IP Whitelist**:  A default limit can be applied to whitelisted IPs via the `API_RATE_LIMIT_WHITELISTED_IPS` variable. This can be used to assign custom limits to prioritized applications.



