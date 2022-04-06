---
layout: post
title:  MyBatis
date:   2021-12-27 21:02:12 +0800
categories: java doc
parent: Java
nav_order: 4
---

# mybatis 生成代码工具

- [mybatis-generator-gui](https://github.com/zouzg/mybatis-generator-gui)

> Mapper 接口类需要加 @Mapper 注解！！！

```
XljMemberExample xljMemberExample = new XljMemberExample();
xljMemberExample.createCriteria().andOpenIdEqualTo(jsCode).andIsDelEqualTo(false);
List<XljMember> memberList = xljMemberMapper.selectByExample(xljMemberExample);
```

# 获取自增ID

xml sql标签新增属性
```
keyProperty="recordList.id" useGeneratedKeys="true"
```

取的时候 
```
Long last_insert_id = someObject.getId();
```