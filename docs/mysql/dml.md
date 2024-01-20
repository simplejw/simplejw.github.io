---
layout: post
title:  dml
date:   2022-06-24 20:31:00 +0800
categories: mysql doc
parent: MySQL
nav_order: 3
---


# MySQL DML

1. 同一个表中的一个字段的值复制给另一个字段
	```sql
	UPDATE mytable SET tax = amount WHERE id <= 20
	```

2. 不同一个表中的一个字段的值复制给另一个字段
    ```sql
    UPDATE student AS s, city AS c SET s.title = c.title, s.age = c.age WHERE s.id = c.id
    ```