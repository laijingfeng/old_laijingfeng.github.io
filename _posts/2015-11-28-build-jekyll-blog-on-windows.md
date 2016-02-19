---
layout: post
title: Windows下创建Jekyll博客
date: 2015-11-28 00:00:00
categories: Blog
excerpt : Blog, Github, Jekyll
---

* content
{:toc}

## 工具准备

下面列的是我搭建时用到的工具，此时可能不是最新的，需要的可自行寻找最新的工具，下面具体章节中会列出一些软件的来源，供参考。

我的工具获取地址：[360云盘·我的工具](http://yunpan.cn/c3AdVxC7GRtC7)(访问密码:da74)

- rubyinstaller-2.2.3-x64.exe
- DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe
- ez_setup-0.9.tar.gz

## 步骤

- 安装python
- 安装ruby和DevKit
- 安装easy_install
- 安装Pygments
- 安装Jekyll

备注：有参考[windows下安装jekyll](http://jingyan.baidu.com/article/925f8cb8f6422ac0dde056ee.html)，细节上有些补充和修正。

### 安装python

查看python版本：

![python_version](/assets/blog-images/view_python_version.png)

### 安装ruby和DevKit

1. 安装rubyinstaller-2.2.3-x64.exe，记得勾上“Add Ruby executables to your PATH”，就是添加环境变量。
1. 运行解压DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe到某个英文无空格路径下。
1. 创建config.yml，打开命令行，进入DevKit的解压目录，`ruby dk.rb init`初始化创建config.yml文件。
	1. 如果报错说ruby命令找不到，注意是打开命令行进入到DevKit目录，不能直接在DevKit目录打开命令行。
1. NotePad++打开DevKit目录下的config.yml，添加ruby的安装路径，如下图：![config.yml](/assets/blog-images/config.yml.png)
1. 原来的命令行窗口，输入`ruby dk.rb install`。

参考：

- [Ruby 安装 - Windows](http://www.runoob.com/ruby/ruby-installation-windows.html)
- [Windows下安装ruby](http://jingyan.baidu.com/article/48b558e33558ac7f38c09aee.html)
- rubyinstaller下载地址：[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)
- [DevKit及rails的安装](http://blog.csdn.net/dyllove98/article/details/8580731)

### 安装easy_install

解压ez_setup-0.9.tar.gz，进入到文件夹里，打开命令行，执行`python ez_setup.py`。

可以查看python安装目录下是否生成了Scripts目录，目录下是否有easy_install.exe等文件。

把Scripts目录添加到环境变量。

参考：

- ez_setup下载地址：[https://pypi.python.org/pypi/ez_setup](https://pypi.python.org/pypi/ez_setup)
- [【安装】win7下 easy_install 的安装](http://www.douban.com/group/topic/50677015/?type=like)
- [python3.4学习笔记(十六) windows下面安装easy_install和pip教程](http://www.cnblogs.com/zdz8207/p/python_learn_note_16.html)
- [Windows 下 Python easy_install 的安装---转载](http://blog.csdn.net/A8572785/article/details/10945237)

### 安装Pygments

这个是高亮插件。

它需要在网站的配置文件_config.yml里将highlighter的值设置为pygments。

在DevKit下的命令行，执行`easy_install Pygments`。

### 安装Jekyll

在DevKit下的命令行，执行`gem install jekyll`。

可能遇到gem命令不能用的问题，

	ERROR:  While executing gem ... (Gem::RemoteFetcher::FetchError)
		Errno::ECONNABORTED: An established connection was aborted by the software i
	n your host machine. - SSL_connect (https://api.rubygems.org/quick/Marshal.4.8/j
	ekyll-3.0.1.gemspec.rz)

下面是解决办法：

原因是ruby的gem被和谐了，现在淘宝的ruby工程师架设了rubygems的国内镜像。使用方法如下：

	$ gem sources --remove https://rubygems.org/
	$ gem sources -a https://ruby.taobao.org/
	$ gem sources -l
	*** CURRENT SOURCES ***

	https://ruby.taobao.org

现在再执行`gem install jekyll`。
	
参考：

- [解决国内gem不能用的问题](http://www.haorooms.com/post/gem_not_use)

## 搭建博客

选择一个目录，命令行执行`jekyll new your_blog_name`，就创建了一个博客站。

`jekyll server`，启动服务，网站地址：http://127.0.0.1:4000/。

## github的博客在本地运行

到github的本地仓库目录，执行`jekyll server`，会生成_site目录，就是解析后的网站，可在本地访问。

遇到的问题：

- pygments着色报错，解析失败，把_config.yml的`highlighter: pygments`用#注释掉。
	- 后面又好了
- 文章页面的导航头异常。

