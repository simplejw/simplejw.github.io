---
layout: post
title:  ddl
date:   2022-06-24 20:31:00 +0800
categories: mysql doc
parent: MySQL
nav_order: 2
---


# MySQL DDL

1. 加字段
	```sql
	ALTER TABLE `book` ADD COLUMN `title` varchar(255) NOT NULL DEFAULT '' COMMENT 'title' AFTER `reader`
	```