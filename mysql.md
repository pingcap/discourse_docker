## Install MySQL 5.7 Server

* apt-get install mysql-server

## Create User

```
sudo cat /etc/mysql/debian.cnf
# Login MySQL with root;

CREATE USER 'discourse'@'localhost' IDENTIFIED BY 'password123ABC&';

# Login MySQL with discourse

CREATE DATABASE IF NOT EXISTS discourse;
```

## Config utf8mb4

vim /etc/mysql/my.cnf

```
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
```

## Config Bind IP

vim /etc/mysql/mysql.conf.d/mysqld.cnf

firewall setting requred.

```
bind-address            = 0.0.0.0
```

## Discourse Deploy With Docker

* https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md

## Config Discourse With MySQL

detail: https://meta.discourse.org/t/running-discourse-with-a-separate-postgresql-server/46375

vim containers/app.yml

rm `templates/postgres.template.yml` line

set env in containers/app.yml

```
 DISCOURSE_DB_USERNAME: discourse
 DISCOURSE_DB_PASSWORD: s3kr1t
 DISCOURSE_DB_HOST: <IP or hostname>
 DISCOURSE_DB_NAME: discourse
 ```

 get `DISCOURSE_DB_HOST` ip: `ip -4 addr show docker0 | grep -Po 'inet \K[\d.]+'`

 ## Launch Discourse

 * `./launcher rebuild app`




