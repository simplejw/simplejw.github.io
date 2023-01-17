---
layout: post
title:  MySQL
date:   2022-06-24 20:31:00 +0800
categories: mysql doc
has_children: true
nav_order: 1
---

# MySQL

1. 导入数据库

	```shell
	# database-12(数据库名) /path/database-12(要导入的数据库数据)
	mysql -h 127.0.0.1 -u root -p  -D database-12 < /path/database-12
	```