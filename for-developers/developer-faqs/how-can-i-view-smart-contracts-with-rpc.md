# How can I view smart contracts with RPC?

Use the JSON RPC `listcontracts` endpoint. For example, to view verified contracts, use the following query. Pagination is available

```shell
curl -X GET "
https://blockscout.com/xdai/mainnet/api?module=contract&action=listcontracts&page=1&offset=50&filter=verified
" -H "accept: application/json"
```

