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

2. 外键约束

> **CASCADE** ：删除或更新父表中的行，并自动删除或更新子表中匹配的行。支持 ON DELETE CASCADE 和 ON UPDATE CASCADE。在两个表之间，不要定义多个作用于父表或子表中的同一列的 ON UPDATE CASCADE 子句。

> **SET NULL** ：从父表中删除或更新行，并将子表中的外键列或列设置为NULL。支持 ON DELETE SET NULL 和 ON UPDATE SET NULL 子句。

> **RESTRICT** ：拒绝对父表的删除或更新操作。指定 RESTRICT（或 NO ACTION）与省略 ON DELETE 或 ON UPDATE 子句相同。

> **NO ACTION** ：来自标准 SQL 的关键字。在 MySQL 中，相当于 RESTRICT。如果引用的表中存在相关的外键值，MySQL Server 将拒绝对父表的删除或更新操作。一些数据库系统有延迟检查，NO ACTION 是延迟检查。在 MySQL 中，立即检查外键约束，因此 NO ACTION 与 RESTRICT 相同。
