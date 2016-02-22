---
layout: post
title: Windows下GitHub环境配置
date: 2016-01-23 00:00:00
categories: GitHub
excerpt : GitHub
---

* content
{:toc}

## 工具准备

所列工具版本号是我使用的，供参考。

- msysgit即Git-1.9.5-preview20150319.exe
- TortoiseGit-1.8.9.0-64bit.msi

我的工具获取地址：[360云盘·我的工具](https://yunpan.cn/crx4EiiNVFGRM)(访问密码:96d4)

### 安装msysgit

说明：参考[1. Git安装与配置](http://blog.csdn.net/renfufei/article/details/41647875)

1. 关键步骤(直接看图)

	![001](/assets/blog-images/2016-01/001.png)

	![002](/assets/blog-images/2016-01/002.png)

	![003](/assets/blog-images/2016-01/003.png)

1. 可以在cmd里面测试是否设置了Path，是否安装成功。在CMD中输入`git`或者`git --version`

	设置本地机器默认commit的昵称和Email

		git config --global user.name "laijingfeng"  
		git config --global user.email "337292616@qq.com"  
		git config --global push.default simple

	查看设置

		git config -l

### 安装TortoiseGit

直接安装

## 生成SSH Key

1. 选择Puttygen

	![004](/assets/blog-images/2016-01/004.png)

1. Puttygen是按照鼠标运行的轨迹来计算的，点了Generate之后鼠标在空白区域乱画就行

	把PublicKey（rsa-key-xxxxxxxx之前的部分/好像全部也可以）复制，在github个人设置(`https://github.com/settings/profile`)的SSH keys里增加一条。（github的注册等略过）

	![005](/assets/blog-images/2016-01/005.png)

1. 选择Save private key，保存到一个文件里，后面用。

## 创建工程

1. 在github上创建一个工程，复制地址，记得是SSH地址。

	![006](/assets/blog-images/2016-01/006.png)

1. 在本地创建一个文件夹，建议和github工程同名，选中文件夹，右键`Git Create respository here...`，然后默认OK

1. 进入文件夹，右键`TortoiseGit->Settings`

	![007](/assets/blog-images/2016-01/007.png)

	选择Remote，把地址粘贴在URL和Push URL，Putty选择刚刚保存的private key，确定，会执行一次`fetch`。

	![008](/assets/blog-images/2016-01/008.png)

1. 默认是在本地创建名为`master`的分支，此时直接`TortoiseGit->Pull...`可以在`Remote Branch`选择一个远端分支下载到本地
	
	推荐是先自己创建分支，`TortoiseGit->Switch/Checkout...`，并下载。切分支也是这个命令。
	
	以后还常用的就是:
	
	- 提交:`Git Commit -> "BranchName"...`+`push`
	- 更新:`TortoiseGit->Pull...`

> 注意：如果第一次pull就出错，可能网络设置有问题，我这里重装记住了旧的路径，出现了这个问题，检查`TortoiseGit->Settings->Network->SSH client:`设置的是不是正确的

