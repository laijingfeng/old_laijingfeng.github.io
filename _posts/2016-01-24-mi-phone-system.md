---
layout: post
title: 小米刷机（一）
date: 2016-01-24 00:00:00
categories: Life
excerpt : Life
---

* content
{:toc}

## 我的手机

小米2s 32G 标准版，2013年国庆入手，入手不久就线刷了开发版，一直跟着更新...

后面感觉慢慢的就出了一些问题

- 系统存储只有3.7GB，经常装软件提示系统存储不足
- 电脑USB充电一直闪屏，基本就是无法连电脑了
- 有时卡死，或者屏幕抖动，进一步乱跳

昨天卡刷了一个MIUI7的稳定版(miui_MI2_V7.0.4.0.LXACNCI_affeb213b3_5.0.zip)，结果内置存储为零了，这样不行，刷老一点的版本吧，然后遇到一些问题，小记备忘。

## 刷机工具

- Miflash20141107.zip 线刷工具
- 卡刷系统
	- miui_MI2_V7.0.4.0.LXACNCI_affeb213b3_5.0.zip MIUI7稳定版 来源：http://www.miui.com/download-2.html
- 线刷系统
	- aries_images_JLB54.0_4.1_cn_2eda98ac63.tgz MIUI5稳定版JLB54.0 

我的工具获取地址：[360云盘·我的工具](https://yunpan.cn/crBt2XPXc4eI6)(访问密码:c039)

## 线刷和卡刷以及一些好帖

- 三清 http://zhidao.baidu.com/question/1830995094858025660.html
- [[经验技巧] DYP手把手教你扩大系统分区（没有镊子导线，纯软件操作...)](http://www.miui.com/thread-1764438-1-1.html) 没试过
- 线刷 [如何使用小米手机刷机工具MiFlash](http://jingyan.baidu.com/article/39810a23e92787b636fda615.html)
- 卡刷 [小米手机卡刷MIUI 4.0卡刷图文教程](http://android.tgbus.com/xiaomi/pojie/422954.shtml)

## 刷机经验

我下的MIUI5稳定版JLB54.0（aries_images_JLB54.0_4.1_cn_2eda98ac63.tgz，来源：[[ROM] MI2/2S最新线刷包下载地址，另附线刷教程和工具](http://www.miui.com/thread-1051198-1-1.html)）

线刷

报错：`未指定的错误(0x800040005):Failed(remote partition table doesnt exist)`

找到帖子[[经验技巧] 线刷报错 remote:partition table doesn't exist 解决](http://www.miui.com/thread-2358721-1-1.html)

下载了`recovery-boot（通过boot方式启动rec）.rar`，运行后不知该怎么样，好像没有出问题，还是留在`fastboot`界面。

直到25楼的出现，[[经验技巧] 小米2s从V6、V7降级V5的方法](http://www.miui.com/thread-2612393-1-1.html)，用了方式二`二、 手机是合并分区`，顺利拯救。

## 说明

粗略记录，有时间再深入学习