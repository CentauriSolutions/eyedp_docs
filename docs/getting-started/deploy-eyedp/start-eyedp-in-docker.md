---
layout: default
title: Start EyeDP in Docker
nav_order: 1
parent: Deploy EyeDP
grand_parent: Getting Started
---

The easiest way to get started hosting EyeDP on your own infrastructure
is to use Docker Compose. The following can be customized to your needs and
should be places behind a load-balancer, such as Traefik or Nginx.

```yaml
version: '3'
services:
  db:
    image: postgres
    volumes:
      - 'postgres:/var/lib/postgresql/data'
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=super-secure-password
  redis:
    image: redis
    volumes:
      - 'redis:/data'
  web:
    image: centaurisolutions/eyedp
    volumes:
      - ./log:/eyedp/log
    ports:
      - "3000:3000"
    depends_on:
      - db
      - redis
    links:
      - db
      - redis
    environment:
      - RAILS_ENV=production
      - DATABASE_URL=postgres://postgres:super-secure-password@db:5432/eyedp
      - SECRET_KEY_BASE=o8w64gurfvwtiu64wlyregfvcw74iu6eryfV
      - DISABLE_SSL=true
      - RAILS_SERVE_STATIC_FILES=true
      - SSO_DOMAIN=.example.com
      - TOTP_ENCRYPTION_KEY=something-really-awesome-that's-at-least-32-bytes
  sidekiq:
    image: centaurisolutions/eyedp
    command: bundle exec sidekiq
    volumes:
      - ./log:/eyedp/log
    depends_on:
      - db
      - redis
    links:
      - db
      - redis
    environment:
      DATABASE_URL: postgres://postgres:super-secure-password@db:5432/myapp_development
      TOTP_ENCRYPTION_KEY: something-really-awesome-that's-at-least-32-bytes
      REDIS_URL: redis://redis:6379
      RAILS_ENV: development
volumes:
  postgres:
  redis:
```

After configuring this how you want it, you can initialize the database and
first admin user with `docker-compose run web bin/setup` and then you can start
the application with `docker-compose up -d`.

When you're ready to put a load balancer in front of EyeDP, it is recommended
to configure it to  aggressively cache resources that come from the `/assets`
path, as these include hashes to ensure that they are highly cachable as well
as updatable by the application. An example configuration for Nginx follows:

```
proxy_cache_path /var/cache/nginx/eyedp levels=1:2
                   keys_zone=eyedp:10m max_size=1g inactive=60m;

upstream app {
    server localhost:3000 fail_timeout=0;
}

server {
    listen 80;
    server_name localhost;

    proxy_cache_key $scheme$request_method$host$request_uri;
    
    location /assets/ {
        proxy_redirect off;
        proxy_pass_header Cookie;
        proxy_ignore_headers Set-Cookie;
        proxy_hide_header Set-Cookie;

        proxy_cache eyedp;
        proxy_cache_valid 200 302  120m;
        proxy_cache_valid 404      1m;

        proxy_pass http://app;
    }


    location / {
        proxy_pass http://app;
        # This assumes that you actually are using https
        proxy_set_header X-Forwarded-Proto https;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }

    error_page 500 502 503 504 /500.html;
    client_max_body_size 4G;
    keepalive_timeout 10;
}
```

To use the above configuration with the caching bits, you'll need to ensure
that the cache directory exists: `mkdir -p /var/cache/nginx/eyedp`.