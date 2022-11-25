---
layout: post
title:  Git
date:   2021-10-31 20:31:00 +0800
categories: git command
has_children: true
nav_order: 1
---

# Git 代码库


1. 初始化空库
	```shell
	cd /opt/git
	mkdir project.git
	cd project.git
	git init --bare
	```

2. 本地添加远程库
	```shell
	cd yourproject
	git remote add origin user@gitserver:/opt/git/project.git
	````

3. 推送本地代码到远程库
	```shell
	git push origin master
	```