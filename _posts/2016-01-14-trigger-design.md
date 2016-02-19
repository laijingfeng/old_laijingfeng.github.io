---
layout: post
title: 触发器设计
date: 2016-01-14 00:00:00
categories: Game
excerpt : Game
---

* content
{:toc}

## 触发器概述

游戏中，一个怪物死亡后，会引发生成另一个怪物；玩家进入一个门，会出现一个怪物；进入场景10秒后，会出现一波僵死...

类似于上面的情形，某个条件下，会发生一件事情，称之为触发器。

我把关卡中的非玩家操控类可互动的物体都视为触发器，例如打怪通关游戏，关卡中的每一个怪物都是一个触发器，它们或相互触发，或由玩家触发，或由时间触发，游戏过程就是一个触发的过程。

触发器有一个触发条件属性，它也是一个触发器，姑且命名为Father，当前触发器在Father消亡（OnFinish）时开始（OnTrigger），没有Father的触发器则立即开始（OnTrigger），所以一个关卡中的触发器形成了一个拓扑图，玩家游戏的过程，就是这个拓扑图流动的过程。

按需要，设置了3种触发器：

- TriggerBase
	- TriggerTimer 时间触发器
	- TriggerBoss Boss触发器
	- TriggerRange 范围触发器

## TriggerBase（触发器基类）

我们希望这些效果在client和editor都能真实展示，而且要方便。

client和editor比较：client资源动态加载，editor没有资源加载步骤，直接用Hierarchy里的

因此我们做了下面的设定：

1.触发器引用其他物体的话，配置的肯定的name，在编辑器里拖为子结点，打包资源的时候读取存储name并删除子结点，如下结构：

- xxxTrigger
	- boss/item
	
2.Father属性editor拖过去操作方便，client加载的时候，要先加载所有Father为空的触发器，其他触发器监听父触发器的onTriggerFinish回调。

3.触发器的创建流程

几个关键函数（按执行顺序）：

- Init：初始化，设置属性，client才执行
- Awake：检查是否有配置信息，比如子结点，有则设置为enable=false，editor用，为了默认隐藏有Father的触发器
- Start：没有父节点则进入OnTrigger，有Father则设置监听Father的onTriggerFinish，在回调里执行OnTrigger
- OnTrigger：触发器开始，没有子结点的话加载需要的子结点资源
- OnFinish：触发器结束，设置m_bIsLive来保证只有一次回调，在OnDestroy也执行OnFinish保证一定执行一次

4.其他

client中可能会需要在CopyState知道触发器死亡，用来算积分之类的，为了保持Level的通用性，让Level监听触发器死亡，其他地方再监听Level的回调

## TriggerTimer（时间触发器）

开始时，计时，倒计时结束，则触发器结束

## TriggerBoss（Boss触发器）

Boss死亡时触发器结束，需要boss子节点

## TriggerRange（范围触发器）

需要设置范围BoxCollider2D，主角进入这个范围触发器结束

可以加item子结点成为可视触发器，例如做金币，隐形的比如用做暗门
