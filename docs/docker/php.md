---
layout: post
title:  PHP
date:   2022-04-07 12:00:00 +0800
categories: docker command
parent: Docker
nav_order: 2
---


# Docker 部署 PHP Nginx Radis
--------

- 目录结构

```
dnp
├── nginx
│   └── certs/
│   └── conf/
│   └── log/
│   └── certs/
│ 
│ 
├── php-fpm
│   └── tmp/
│   └── php.ini
│   └── www.conf
│   └── Dockerfile
│ 
│ 
├── redis
│   └── redis.conf
│ 
│ 
├── www/
│ 
│ 
└── docker-compose.yml
```

- docker-compose.yml 文件

```yml
version: '3'
services:
  web_nginx:
    # build: ./nginx
    image: nginx:1.24
    ports:
      - "80:80"
      - "443:443"
    volumes:
      # source
      - ./www/:/usr/share/nginx/html/
      - ./nginx/log/:/var/log/nginx/:rw
      - ./nginx/certs/:/etc/ssl/certs/:ro
      - ./nginx/conf/:/etc/nginx/conf.d/:ro
    networks:
        - frontend

  web_php_fpm:
    build: ./php-fpm
    # image: dnp_web_php_fpm:latest
    expose:
      - "9000"
      # - "9003"
    volumes:
      - ./php-fpm/php.ini:/usr/local/etc/php/php.ini:ro
      - ./php-fpm/www.conf:/usr/local/etc/php-fpm.d/www.conf:ro
      - ./php-fpm/tmp/:/tmp/
      - ./www/:/usr/share/nginx/html/
    networks:
        - frontend
        - backend
        - database_net-database

  web_redis:
    # build: ./redis
    image: redis:7.0
    ports:
      - "6379:6379"
    volumes:
      # source
      - ./redis/redis.conf:/usr/local/etc/redis/redis.conf:ro
    networks:
        - backend

  elasticsearch:
    image: elasticsearch:7.8.1
    container_name: elasticsearch_781
    environment:
      - node.name=es-node
      - cluster.name=es-cluster
      - discovery.type=single-node
    volumes:
      - ./elasticsearch/esdata:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
      - 9300:9300
    networks:
      - frontend

  kibana:
    image: kibana:7.8.1
    container_name: kibana_781
    ports:
      - 5601:5601
    networks:
      - frontend

networks:
  frontend:
  backend:
  database_net-database:
    external: true
```


