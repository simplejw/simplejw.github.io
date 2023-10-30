---
layout: post
title:  VirtualEnv
date:   2021-12-27 21:02:12 +0800
categories: python doc
parent: Python
nav_order: 2
---

# Python 创建虚拟环境


1. install virtual env

	```shell
	sudo pip3 install virtualenv virtualenvwrapper
	````

2. make virtual dir

	```shell
	mkdir ~/virtualenvs
	```

3. env variable

	```shell
	export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
	export WORKON_HOME=~/virtualenvs
	export PIP_VIRTUALENV_BASE=$WORKON_HOME
	export PIP_RESPECT_VIRTUALENV=true
	source /usr/local/bin/virtualenvwrapper.sh
	```

4. source
	```shell
	source .zshrc
	```

5. doc help
	```shell
	virtualenvwrapper --help #所有的命令可使用进行查看，这里列出几个常用的：

	mkvirtualenv [环境名]  #创建基本环境
	rmvirtualenv [环境名]  #删除环境
	workon       [环境名]  #激活环境
	deactivate            #退出环境
	workon                #列出所有环境
	````

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
<div id="gitalk-container"></div>
<script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>
<script>
    var gitalk = new Gitalk({
        clientID: '6528b5bfa8215216d96b',
        clientSecret: '20a12737fb1bd393d7199f799be4ff95c070f4ab',
        repo: 'jekyll-talk',
        owner: 'simplejw',
        admin: ['simplejw'],
        id: window.location.pathname,
        proxy: 'https://github.com/login/oauth/access_token'
        distractionFreeMode: true
    });
    gitalk.render('gitalk-container')
</script> 