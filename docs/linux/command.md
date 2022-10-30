---
layout: post
title:  Command
date:   2022-04-07 12:00:00 +0800
categories: linux command
parent: Linux
nav_order: 3
---


# Linux 常用命令
--------

- zip 命令

	```shell
	# 将当前目录下的所有文件和文件夹全部压缩成myfile.zip文件,－r表示递归压缩子目录下所有文件.
	zip -r myfile.zip ./myfile/ 
	```

- unzip 命令

	```shell
	# 将压缩文件text.zip在当前目录下解压缩
	unzip test.zip

	# 将压缩文件test.zip在指定目录/tmp下解压缩，如果已有相同的文件存在，要求unzip命令覆盖原先的文件
	unzip -o test.zip -d /tmp/
	```