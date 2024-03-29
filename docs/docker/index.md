---
layout: post
title:  Docker
date:   2021-10-31 20:31:00 +0800
categories: docker command
has_children: true
nav_order: 1
---



# Docker 常用命令
--------

1. 进入容器
	```bash
	docker-compose exec {service_name} bash

	docker container exec -it {container_id} bash
	```


2. 执行PHP脚本
	```bash
	docker run -it --rm --name my-running-script -d -v "$PWD":/usr/share/nginx/html/default -w /usr/share/nginx/html/default dnp_web_php72_fpm(images name) php ./yii queue/listen
	# Supervisord 去除 -it -d 参数
	```


3. 容器服务连接宿主机 connect from a container to a service on the host

	> You can also reach the gateway using [`gateway.docker.internal`](https://docs.docker.com/desktop/networking/)

	> Linux `172.17.0.1:3306` 


4. 构建Docker Hub镜像仓库
	```shell
	# 登录
	docker login

	# 镜像打标签
	# docker tag dnp_web_nginx:latest simplejw/dnp_web_nginx:latest
	docker tag <本地镜像名称>:<本地镜像版本号> <远程空间名称>/<远程镜像名称>:<远程镜像版本号>

	# 推送镜像至Docker Hub镜像仓库
	# docker push simplejw/dnp_web_nginx:latest
	docker push <远程空间名称>/<远程镜像名称>:<远程镜像版本号>

	# 拉取镜像
	# docker pull simplejw/dnp_web_nginx:latest
	docker pull <远程空间名称>/<远程镜像名称>:<远程镜像版本号>

	# 删除本地镜像
	# docker image rm simplejw/dnp_web_nginx:latest
	docker image rm <本地镜像名称>:<本地镜像版本号>
	```

5. 构建阿里云个人镜像仓库
	```shell
	# 登录镜像仓库
	docker login --username=<镜像仓库登录名> registry.cn-<个人版实例所在的地域>.aliyuncs.com

	# 镜像打标签
	docker tag <镜像ID> registry.cn-<个人版实例所在地域>.aliyuncs.com/<命名空间名称>/<镜像仓库名称>：<镜像版本号>

	# 推送镜像至个人版实例
	docker push registry.cn-<个人版实例所在地域>.aliyuncs.com/<命名空间名称>/<镜像仓库名称>：<镜像版本号>

	# 拉取镜像
	docker pull registry.cn-<个人版实例所在地域>.aliyuncs.com/<命名空间名称>/<镜像仓库名称>：<镜像版本号>

	# 执行docker images，在返回结果中可以看到拉取的镜像，说明拉取镜像成功。
	# docker compose 文件要指定image: 镜像名:tag
	```
