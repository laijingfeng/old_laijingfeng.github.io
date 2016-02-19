---
layout: post
title: 波波课程笔记（一）：3D渲染管线基础
date: 2015-12-03 00:00:00
categories: DirectX
excerpt : DirectX, Course
---

* content
{:toc}

## 图元

- 三角形(Triangle):基本图元
- 顶点(Vertex):三角形的顶点
- 像素(Pixel):显示的最小单元

## 坐标系

### Model Space

建模时，顶点数据都是基于模型坐标系，一般原点在脚底

### World Space

把多个模型放在场景中，要区分它们，必须转化为世界坐标系

> 坐标系有左手和右手之分，矩阵没有

### View Space (Camera Space)

两者是互为逆矩阵

基于像机观察点的坐标系

### Project Space

透视像机的视野是一个锥体，有z-near和z-far两个平面，和视角，只有视锥内的物体可见

投影映射不再是正交映射，而是映射到视锥

### Screen Space

显示到屏幕上，还要做一次变换

视点发出的一条射线，z-near和z-far之间的线段在屏幕上是同一个点

> 屏幕也有Z轴，是一个盒子

## BUFFER

数据存储在显卡（VedioCard）中

### Frame Buffer (帧缓冲)

一般是双缓冲，front/back两个Buffer交替使用，显示front，绘制back，绘制完成交换

一个缓冲大小和屏幕像素数一样大

> 垂直同步
>
> 显示过程是，屏幕从下往上行扫描front-buffer，没有垂直同步是back-buffer绘制好就切换，扫描线继续扫描，这样可能显示的一部分是原front的，另一部分是现front的。
>
> 加入垂直同步则是扫描到顶端后，产生一个信号，此时才切换buffer

### Z Buffer

和屏幕像素数一样大，记录每个像素当前绘制点的深度，处理遮挡关系

绘制顺序?从前往后or从后往前

### Stencil Buffer

可以产生很多效果，如阴影等

## 光照

光源和材质

- 光源(L)的颜色
- 材质(M)对光的吸收和反射

黄色的铜镜和黄色的布料，看着是不一样的，和材质本身的属性还有关系

光照模型：环境光(ambient) + 漫反射(diffuse) + 镜面反射(specular)

### 环境光

对间接光照的模拟

### 漫反射

![漫反射](/assets/blog-images/2015-12-04_001.png)

和夹角相关，夹角越大，光照越弱（平行时最弱，照不到）

(n dot L) * L * M

### 镜面反射

![镜面反射1](/assets/blog-images/2015-12-04_002.png)

光照强度和r与v的夹角有关，夹角越大，光照越弱

为了简化计算，也用下面的近似算法，h是l和v的角平分线，即半角向量，用h和n的夹角

![镜面反射2](/assets/blog-images/2015-12-04_003.png)

(n dot h) * L * M (h:半角向量)

### 简单光照模型

![简单光照模型](/assets/blog-images/2015-12-04_004.png)

镜面反射中有一个n次方，这是光的聚合程度，越大越聚合，反射线周围的光越少，强度越弱

## 着色模型

- 顶点光
	- Flat
	- Gouraund
- 像素光
	- Phong

### Flat

三角形内的颜色取顶点颜色的均值

### Gouraund

![Gouraund](/assets/blog-images/2015-12-04_005.png)

如上图，不是简单取均值，每个顶点有不同的权重，权重值是顶点对面的面积的大小

### Phong

不是对顶点颜色插值，而是对法线差值，每一个点再各自计算光照

像素光，开销大

> 和Gouraund相比，可以保留高光的效果，如下图：
> 
> ![Phong](/assets/blog-images/2015-12-04_006.png)
>
> 一个近似球体的物体，在Phong光照下，看着就是球体了

## 纹理

顶点数据中包含纹理坐标，x和y，范围[0,1]

超出范围怎么填充什么呢？

### Wrap

![Wrap](/assets/blog-images/2015-12-04_007.png)

### Mirror

![Mirror](/assets/blog-images/2015-12-04_008.png)

### Clamp

![Clamp](/assets/blog-images/2015-12-04_009.png)

边界

### Border

![Border](/assets/blog-images/2015-12-04_010.png)

设置边界颜色，超过了填充颜色

### 纹理滤波

图素(Texel)，类似于像素(Pixel)，贴图的一个单元

采色情况如下：

#### 1 Texel : N Pixel

- Point:纹理坐标落在哪个图素就用哪个图素的颜色，可能出现马赛克
- Linear:线性插值，2-Linear，![Linear](/assets/blog-images/2015-12-04_011.png)，采周围4个图素，类似于Gouraund着色，按对面面积算权重

#### N Texel : 1 Pixel

物体走到镜头远处的时候，像素就很少，此时采用Point方式，远处运动物体可能闪动

MipMap，生成贴图的所有除二层级图，采用最贴近的一张贴图来采样，可以计算机生成层级图，常用是美术给出前几张，后面的自动生成

![MipMap](/assets/blog-images/2015-12-04_012.png)

进一步的是用接近的3张层级图插值，每张图用Linear，那就是3-Linear。

## 渲染过程

- 世界是三角形建模的
- 通过坐标系变换转换到屏幕空间
- 采用Phong光照模型打上光
- 将贴图贴到模型上

先打光再贴图吗，贴图的颜色怎么反映？