---
description: NGINX default template
---

# Proxy Setup

## Proxy setup

It is recommended to run a web proxy behind the frontend and backend for optimized installation.

These urls should be routed to the backend:
```
/api
/socket
/sitemap.xml
/auth/auth0
/auth/auth0/callback
/auth/logout
```

All other urls should be routed to the frontend.

## Example Config File

This is an example configuration for NGINX. It is also located in the Blockscout repo at [`docker-compose/proxy/default.conf.template`](https://github.com/blockscout/blockscout/blob/master/docker-compose/proxy/default.conf.template)

In this example the frontend and backend are forwarded to port `80`, meaning the new frontend will be available on localhost without needing to specify a port number.

```
map $http_upgrade $connection_upgrade {

  default upgrade;
  ''      close;
}

server {
    listen       80;
    server_name  localhost;
    proxy_http_version 1.1;

    location ~ ^/(api|socket|sitemap.xml|auth/auth0|auth/auth0/callback|auth/logout) {
        proxy_pass            ${BACK_PROXY_PASS};
        proxy_http_version    1.1;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
    }
    location / {
        proxy_pass            ${FRONT_PROXY_PASS};
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
        proxy_pass            http://stats:8050/;
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
    listen       8081;
    server_name  localhost;
    proxy_http_version 1.1;
    proxy_hide_header Access-Control-Allow-Origin;
    proxy_hide_header Access-Control-Allow-Methods;
    add_header 'Access-Control-Allow-Origin' 'http://localhost' always;
    add_header 'Access-Control-Allow-Credentials' 'true' always;
    add_header 'Access-Control-Allow-Methods' 'PUT, GET, POST, OPTIONS, DELETE, PATCH' always;
    add_header 'Access-Control-Allow-Headers' 'DNT,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range,Authorization,x-csrf-token' always;

    location / {
        proxy_pass            http://visualizer:8050/;
        proxy_http_version    1.1;
        proxy_buffering       off;
        proxy_set_header      Host "$host";
        proxy_set_header      X-Real-IP "$remote_addr";
        proxy_connect_timeout 30m;
        proxy_read_timeout    30m;
        proxy_send_timeout    30m;
        proxy_set_header      X-Forwarded-For "$proxy_add_x_forwarded_for";
        proxy_set_header      X-Forwarded-Proto "$scheme";
        proxy_set_header      Upgrade "$http_upgrade";
        proxy_set_header      Connection $connection_upgrade;
        proxy_cache_bypass    $http_upgrade;
        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' 'http://localhost' always;
            add_header 'Access-Control-Allow-Credentials' 'true' always;
            add_header 'Access-Control-Allow-Methods' 'PUT, GET, POST, OPTIONS, DELETE, PATCH' always;
            add_header 'Access-Control-Allow-Headers' 'DNT,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range,Authorization,x-csrf-token' always;
            add_header 'Access-Control-Max-Age' 1728000;
            add_header 'Content-Type' 'text/plain charset=UTF-8';
            add_header 'Content-Length' 0;
            return 204;
        }
    }
}
```

{% hint style="info" %}
_**NOTE:**_ For production usage you should add at a minimum the correct `server_name` (ie [eth.blockscout.com](http://eth.blockscout.com/)) and TLS info (`ssl_certificate`, `ssl_certificate_key`, `other required variables?`) at a minimum.
{% endhint %}

{% hint style="info" %}
_**NOTE:**_ Here the _stats_ service also uses separate port on nginx, but for production usage we recommend a separate hostname for stats. CORS policy for stats should allow the frontend domain.
{% endhint %}
