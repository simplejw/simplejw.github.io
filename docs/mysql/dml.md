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
=======
2. 不同表中的一个字段的值复制给另一个字段
	```sql
	UPDATE student AS s, city AS c SET s.name = c.name, s.title = c.title WHERE s.id = c.id

	UPDATE student AS s SET s.name = (SELECT name from city WHERE id = s.id)
	```

3. 两表求差集
	```sql
	SELECT
		s.num 
	FROM
		schedul AS s
		LEFT JOIN record AS r ON s.num = r.num 
	WHERE
		r.num IS NULL 
	```

4. DISTINCT 和 GROUP BY 并存
	```sql
	SELECT DISTINCT
	    code
	FROM
	    (
	    SELECT
	        code,
	        id,
	        COUNT(id)
	    FROM
	        `table`
	    WHERE
	        `deleted_at` IS NULL
	    GROUP BY
	        code,
	        id
	    HAVING
	        COUNT(id) > 1
	) AS t1
	```
