---
layout: post
title: Navigation and BlendTree
date: 2016-03-27 00:00:00
categories: Unity
excerpt : Navigation and BlendTree
---

* content
{:toc}

## BleedTree

15(或9)个动作，通过Turn和Forward两个参数融合出各种行走，参数可用Navigation模拟。

| Left180 | Left90 | Forward | Right90 | Right180 |
| :---: | :---: | :---: | :---: | :---: |
| RunLeft180 | RunLeft90 | RunForward | RunRight90 | RunRight180 |
| WalkLeft180 | WalkLeft90 | WalkForward | WalkRight90 | WalkRight180 |
| TurnLeft180 | TurnLeft90 | Idle | TurnRight90 | TurnRight180 |

## Navigation

## 设置Navigation

和Scene关联

## 隔离

OffMeshLink Generatic + Distance

## 自定义隔离路线

OffMeshLink

## 障碍物和动态障碍

Navmesh Obstacle

参考：

- [Unity手游之路<九>自动寻路Navmesh之高级主题](http://blog.csdn.net/janeky/article/details/17492531)
- [分享](https://yunpan.cn/cqyqUKBLTQS76)(访问密码:e32a)