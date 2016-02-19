---
layout: post
title: 游戏工程管理
date: 2016-01-11 00:00:00
categories: Game
excerpt : Game
---

* content
{:toc}

## 概述

一个简单的游戏项目管理方案。

## 方案

具体看结构

- client 客户端（程序使用）
- editor 编辑器（策划/美术同学使用）
- table 表格（做为client和editor的submodule，程序和策划都可能配置表格）
- runtime 核心/公用代码库（一方面因为要支持client和enditor而整合到一起，另一方面核心代码做一定的查看权限）
	- RuntimeClient（生成client用的库）
	- RuntimeEditor（生成editor用的库）

## 一些配置技术细节

### runtime生成的DLL自动拷贝到工程中

### Git的SubModule使用

参考：[Git的submodule功能详解](http://www.linuxidc.com/Linux/2014-04/99328.htm)

### VS库工程添加现有文件夹

参考：[如何使用vs将现有的项目或者文件夹（尤其是多层目录的）添加到项目中](http://www.cnblogs.com/24la/p/vs-contain-existed-folder.html)
