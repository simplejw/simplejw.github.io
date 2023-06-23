---
layout: post
title:  Database
date:   2022-04-07 12:00:00 +0800
categories: docker command
parent: Docker
nav_order: 3
---


# Docker 部署 Mysql Mongo
--------

- docker-compose.yml 文件

```yml
# Use root/example as user/password credentials
version: '3.1'

services:

  web_mysql:
    image: mysql:8
    command: 
      --default-authentication-plugin=mysql_native_password
      --character-set-server=utf8mb4
      --collation-server=utf8mb4_general_ci
      --sql_mode=""
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
      TZ: Asia/Shanghai
    # command: mysqld --sql_mode=""
    ports:
      - 3306:3306
    volumes:
      - ./mysql/etc:/etc/mysql
      - ./mysql/conf.d:/etc/mysql/conf.d
      - ./mysql/data:/var/lib/mysql 
      - ./mysql/log:/var/log/mysql
      # - ./mysql-files:/var/lib/mysql-files
    networks:
        - net-database


  web_mongo:
    image: mongo:latest
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    ports:
      - 27017:27017
    volumes:
      - ./mongo/db:/data/db
      - ./mongo/log:/var/log/mongodb
      - ./mongo/etc:/etc/mongo
    networks:
        - net-database

networks:
  # net-mysql:
  # net-mongo:
  net-database:
```