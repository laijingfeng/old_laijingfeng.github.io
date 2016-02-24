---
layout: post
title: Gearman小探
date: 2016-02-24 00:00:00
categories: Gearman
excerpt : Gearman小探
---

* content
{:toc}

## 概述

[Gearman](http://gearman.org/)是一个简单的分布式框架，支持多语言，Client+Job+Worker，盗几张官网的图来示意。

![stack](/assets/blog-images/2016-02/stack.png)

![flow](/assets/blog-images/2016-02/flow.png)

![cluster](/assets/blog-images/2016-02/cluster.png)

## Mac安装php扩展小记

1. 下载gearman-1.1.2.tgz

	推荐地址：
	
	- http://pecl.php.net/get/gearman-1.1.2.tgz
	- http://download.csdn.net/detail/clevercode/8698699
	- https://yunpan.cn/cxXRsE8GhLgC9（访问密码:0101）

1. 安装

		tar zxf gearman-1.1.2.tgz
		cd gearman
		phpize
	
	> 一个报错
	>
	>	grep: /usr/include/php/main/php.h: No such file or directory
	>	grep: /usr/include/php/Zend/zend_modules.h: No such file or directory
	>	grep: /usr/include/php/Zend/zend_extensions.h: No such file or directory
	>	Configuring for:
	>	PHP Api Version:
	>	Zend Module Api No:
	>	Zend Extension Api No:
	>	
	> 网上的说法一般是，例如[Mac系统升级到10.9(mavericks)时安装php扩展问题解决](http://my.oschina.net/Twitter/blog/287543?fromerr=wRzSpPrz)
	>	
	>	sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk/usr/include /usr/include
	>	
	> 然而没有权限，因为系统引入了SIP的特性无法修改系统目录，rootless特性，参考：[Mac上搭建scheme环境，终端报出Operation not permitted](https://segmentfault.com/q/1010000003958979)
	>	
	> 那就不管它，继续下面的步骤
	
		./configure
		make
	
	> 又报错，找不到`php.h`
	>	
	> 它还是去`/usr/include下找的`
	>	
	>	sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk/usr/include /usr/local/include
	>	
	> 把`Makefile`里的`/usr/include`替换成`/usr/local/include`
	
		make install
	
	> 报错，`/usr/lib/php/extension...`目录也不能写
	>
	> 修改`Makefile`转到`/opt/lb/php/extension...`
	>
	> 继续`make install`
		
	`php.ini`增加extension=/opt/lb/php/extension.../gearman.so
	
1. 测试

		# vi test.php
		<?php print gearman_version()."\n";?>
		# php test.php
		1.1.2

	


