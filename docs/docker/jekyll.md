---
layout: post
title:  Jekyll
date:   2022-04-07 12:00:00 +0800
categories: docker command
parent: Docker
nav_order: 3
---


# Docker 部署 Jekyll
--------

- docker-compose.yml 文件


```
version: '3'

services:

  myblog:
    command: jekyll serve --livereload
    image: jekyll/jekyll
    volumes:
      - ./www:/srv/jekyll
      - ./vendor/bundle:/usr/local/bundle
    ports:
      - 4000:4000
      - 35729:35729

```

**Note:** 
- YML格式
- remote_theme 和 theme
- ruby > 3.0 ? Gemfile 添加 `gem "webrick"`

