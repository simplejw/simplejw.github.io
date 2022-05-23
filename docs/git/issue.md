---
layout: post
title:  Issue
date:   2021-12-27 21:02:12 +0800
categories: git command
parent: Git
nav_order: 2
---

# GitHub 问题

1. git push失败

	```
	git@github.com: Permission denied (publickey).
	fatal: Could not read from remote repository.

	Please make sure you have the correct access rights
	and the repository exists.
	```

	提示：在大多数系统中，默认私钥（~/.ssh/id_rsa 和 ~/.ssh/identity）会自动添加到 SSH 身份验证代理中。 **应无需运行 ssh-add path/to/key，除非在生成密钥时覆盖文件名。**

	- 解决方案：[link](https://stackoverflow.com/questions/56464757/trouble-implementing-specifically-just-the-docs-theme-using-jekyll)