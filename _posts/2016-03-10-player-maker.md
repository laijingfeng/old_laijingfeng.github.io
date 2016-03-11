---
layout: post
title: PlayerMaker
date: 2016-03-10 23:00:00
categories: Game
excerpt : PlayerMaker
---

* content
{:toc}

## 概述

PlayerMaker可以快速创建状态机，制作游戏Demo。

下载分享：[360云盘](https://yunpan.cn/cYrZRdkGUEPjK)（访问密码：0be9）

快速了解：

- [Playmaker Input篇教程之Playmaker购买下载和导入](http://my.oschina.net/u/1585857/blog/417643)
- [Playmaker Input篇教程之PlayMaker菜单概述](http://my.oschina.net/u/1585857/blog/418091)
- [Playmaker Input篇教程之引入的核心概念](http://my.oschina.net/u/1585857/blog/418586)
- [Playmaker全面实践教程之playMaker编辑器](http://my.oschina.net/u/1585857/blog/419610)
- [Playmaker全面实践教程之简单的使用Playmaker示例](http://my.oschina.net/u/1585857/blog/419983)
- [Playmaker全面实践教程之Playmaker常用工具](http://my.oschina.net/u/1585857/blog/420460)

> 备注：本文使用版本Unity5.3.1f1和PlayerMaker1.7.7f6

## 细节

流程：[GlobalEvent->]State(Actions)->(Event)->State(Actions)

常用Actions：

- SetProperty
- TestBool
- Random

脚本触发状态机：

FSM.SendEvent
