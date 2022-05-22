---
layout: post
title:  dependency
date:   2022-05-22 12:00:00 +0800
categories: go doc
parent: Go
nav_order: 2
---


# go依赖包管理
---

1. 初始化包管理

	```shell
	go mod init example/mymodule
	```

2. 新增依赖包

	```shell
	#要为模块中的包添加所有依赖项，请运行如下命令（“.”指当前目录中的包）
	go get .
	```

	```shell
	#添加特定依赖项
	go get example.com/theirmodule
	```

	```shell
	#获取指定版本
    go get example.com/theirmodule@v1.3.4
	```

    ```shell
	#最新版本 @latest
    go get example.com/theirmodule@latest
	```

	```shell
	#修稿 go.mod file 引入包
	require example.com/theirmodule v1.3.4
	```

3. 发现可用更新

	```shell
	#当前模块中所有最新可用更新列表
	go list -m -u all
	```

	```shell
	#显示指定模块的可用更新
	go list -m -u example.com/theirmodule
	```

4. 同步代码的依赖包

	```shell
	go mod tidy
	```

5. 针对未发布的模块代码进行开发和测试

	```go
	module example.com/mymodule

	go 1.16

	require example.com/theirmodule v0.0.0-unpublished

	replace example.com/theirmodule v0.0.0-unpublished => ../theirmodule


	//设置 require/replace 对时，使用 go mod edit 和 go get 命令确保文件描述的需求保持一致
	go mod edit -replace=example.com/theirmodule@v0.0.0-unpublished=../theirmodule
    
    go get -d example.com/theirmodule@v0.0.0-unpublished
	```


