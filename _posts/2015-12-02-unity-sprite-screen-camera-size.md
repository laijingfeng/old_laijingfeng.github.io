---
layout: post
title: Unity中相机、屏幕、贴图大小的关系
date: 2015-12-02 00:00:00
categories: Unity
excerpt : Unity
---

* content
{:toc}

## 引子

- Sprite(2D and UI)中有一个“Pixels Per Unit”
- 屏幕可以设置宽和高(编辑器中Game面板可以设置预览屏幕大小，WebPlayer的PlayerSettings.Resolution可以设置发布屏幕大小)
- Camera有一个参数是“Size”

它们有什么关系，我要如何设置才能使得显示刚刚好。

## 详解

Camera中的Size指的是高的半长，如Size是2.56那么相机拍摄的高是5.12个单位。

相机图像根据屏幕的宽高比（如960*640）映射到屏幕上。(这样我们看到，相机的高先保证)

Sprite(2D and UI)中的“Pixels Per Unit”，Unit和相机Size的单位是一个概念，假设它是Unity单位，就是“一个Unity单位放我的多少像素”。

## 举例

一个具体的Sprite大小是288*512像素大小，Scale设置为Vector3.one。

Camera的Size是2.56单位。

Sprite(2D and UI)的“Pixels Per Unit”设置100。

这样，相机的高向是可以放5.12*100=512个该图像素，Sprite的高向是会刚好充满相机的，也将充满屏幕，宽向要看屏幕的宽高比。

屏幕宽高比是288:512则刚好充满，小于则宽向有部分Sprite在视野外，大于则宽向两侧有露出背景。

## 补充

同理，positon移动一个单位就是512像素。

如果父节点放了NGUI的UIRoot等有了scale，那么，子节点的scale和position是要乘以这个量才是实际的量。