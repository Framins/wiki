# Server

* [Basic](basic.md)
* [Firewall](firewall.md)
* [SSH](ssh/README.md)
* [Apache](apache.md)
* [Nginx](nginx.md)
* [GitLab](gitlab/README.md)
* [Redmine](redmine/README.md)
* [Message Queue](mq/message-queue.md)

Sentry
------

參考 `docker-compose.yml` 檔

```yml
sentry:
  ports:
    - 8080:9000
  image: slafs/sentry:7.7
  links:
    - redis
    - postgres
  environment:
    SECRET_KEY: random_value
    SENTRY_ADMIN_USERNAME: admin
    SENTRY_ADMIN_PASSWORD: password
    SENTRY_URL_PREFIX: http://sentry.example.com
    SENTRY_REDIS_HOST: redis
    DATABASE_URL: postgres://postgres:@postgres/postgres

redis:
  image: redis:3.2-alpine

postgres:
  image: postgres:9.5
  environment:
    POSTGRES_PASSWORD: password
```

Reference
---------

[httpd 比較](http://jetfar.com/apache-nginx-lighttpd-future-compared/)
