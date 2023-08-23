---
description: NGINX default tempalte
---

# Proxy Setup

## Proxy setup

It is recommended to run a web proxy behind the frontend and backend for optimized installation.

Currently all urls **except the following** should be routed to the backend:

```
= /
/_next
/node-api
/apps
/account
/accounts
/static
/auth/profile
/auth/unverified-email
/txs
/tx
/blocks
/block
/login
/address
/stats
/search-results
/token
/tokens
/visualize
/api-docs
/csv-export
/verified-contracts
/graphiql
/withdrawals
/l2-output-roots
/l2-txn-batches
/l2-withdrawals
/l2-deposits
```

{% hint style="info" %}
_**NOTE:**_ only exact path to `/` should be followed to the frontend
{% endhint %}

## Example Config File

This is an example configuration for NGINX. It is also located in the Blockscout repo at [`docker-compose/proxy/default.conf.template`](https://github.com/blockscout/blockscout/blob/master/docker-compose/proxy/default.conf.template)

In this example the frontend and backend are forwarded to port 80, meaning the new frontend will be available on localhost without needing to specify a port number.

```
map $http_upgrade $connection_upgrade {

  default upgrade;
  ''      close;
}

server {
    listen       80;
    server_name  localhost;
    proxy_http_version 1.1;

    location / {
        proxy_pass            http://backend:4000;
        proxy_http_version    1.1;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
    }
    location = / {
        proxy_pass            http://frontend:3000;
        proxy_http_version    1.1;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
    }
    location ~ ^/(_next|node-api|apps|account|accounts|static|auth/profile|auth/unverified-email|txs|tx|blocks|block|login|address|stats|search-results|token|tokens|visualize|api-docs|csv-export|verified-contracts|graphiql|withdrawals) {
        proxy_pass            http://frontend:3000;
        proxy_http_version    1.1;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
    }
}
server {
    listen       8080;
    server_name  localhost;
    proxy_http_version 1.1;
    proxy_hide_header Access-Control-Allow-Origin;
    proxy_hide_header Access-Control-Allow-Methods;
    add_header 'Access-Control-Allow-Origin' 'http://localhost' always;
    add_header 'Access-Control-Allow-Credentials' 'true' always;
    add_header 'Access-Control-Allow-Methods' 'PUT, GET, POST, OPTIONS, DELETE, PATCH' always;

    location / {
        proxy_pass            http://stats:8050;
        proxy_http_version    1.1;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
    }
}
```

{% hint style="info" %}
_**NOTE:**_ For production usage you should add at a minimum the correct hostname and TLS configuration.
{% endhint %}

{% hint style="info" %}
_**NOTE:**_ Here the _stats_ service also uses separate port on nginx, but for production usage we recommend a separate hostname for stats. CORS policy for stats should allow the frontend domain.
{% endhint %}
