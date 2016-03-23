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

PlayerMaker可以快速创建状态机，制作游戏，尤其适合做Demo。

下载分享：[360云盘](https://yunpan.cn/cYrZRdkGUEPjK)（访问密码：0be9）

快速了解：

- [Playmaker全面实践教程Input篇](http://wenku.it168.com/d_001616632.shtml)
- [Playmaker Input篇教程之Playmaker购买下载和导入](http://my.oschina.net/u/1585857/blog/417643)
- [Playmaker Input篇教程之PlayMaker菜单概述](http://my.oschina.net/u/1585857/blog/418091)
- [Playmaker Input篇教程之引入的核心概念](http://my.oschina.net/u/1585857/blog/418586)
- [Playmaker全面实践教程之playMaker编辑器](http://my.oschina.net/u/1585857/blog/419610)
- [Playmaker全面实践教程之简单的使用Playmaker示例](http://my.oschina.net/u/1585857/blog/419983)
- [Playmaker全面实践教程之Playmaker常用工具](http://my.oschina.net/u/1585857/blog/420460)

官网：

- [官网](http://www.hutonggames.com/)
- [Samples](http://www.hutonggames.com/samples.php)
	- [M2H GAME EXAMPLES](https://hutonggames.fogbugz.com/default.asp?W880)
		- [Res](https://www.assetstore.unity3d.com/en/#!/content/116)
- [2D教程](https://github.com/jeanfabre/PlayMaker--UnityLearn--2dPlatformer)
- [User Totorials](https://hutonggames.fogbugz.com/default.asp?W548)
- [FQA](https://hutonggames.fogbugz.com/default.asp?W624)

> 备注：本文使用版本Unity5.3.1f1和PlayerMaker1.7.7f6

## 细节

流程：[GlobalEvent->]State(Actions)->(Event)->State(Actions)

### Action

#### 常用Actions

- SetProperty
- Random
- SetAnimatorValue
- GetKeyDown 按键输入
- PlayAnimation 播放动画，可以使用Blend过渡两个动画
- GetAxisVector 获得Horizontal和Vertical
- ControllerSimpleMove 控制移动
- LookAt 面向某个方向
- SendEvent 发送事件，可以发送给指定的FSMComponent
- PlaySound 播放音效
- 数值
	- IntAdd 增加int值
	- IntCompare 比较int值
	- TestBool 查看bool值
- Random
	- SelectRandomString 在设置好的字符串中根据权重选择一个
	- RandomFloat 在一个范围随机一个浮点数
- MousePick 鼠标选中
- FindClosest
- SetFsmFloat
- GameObjectChanged 指定的GameObject发生了变化
- GameObjectCompareTag 比较GameObject的Tag
- GameObjectTagSwitch
- SetMouseCursor 设置鼠标状态
- GetStringLength
- GetStringLeft 截取字符串
- SetPosition
- ActiveGameObject
- GetName
- Translate
- SmoothLookAtDirection
- TriggerEvent

一个状态的Actions就是这个状态要做的事，一般只做一次，若是设置EveryFrame则是每帧执行

#### 自定义Action



### Event

系统Events：

- FINISHED
- MOUSE_OVER
- MOUSE_EXIT

脚本触发状态机：

FSM.SendEvent
