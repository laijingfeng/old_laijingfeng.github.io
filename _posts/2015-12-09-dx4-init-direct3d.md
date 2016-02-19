---
layout: post
title: DirectX入门系列（四）：初始化Direct3D
date: 2015-12-09 00:00:00
categories: DirectX
excerpt : DirectX
---

* content
{:toc}

## Direct3D概述

Direct3D是一种低层图形API，它能让我们利用3D硬件加速来渲染3D世界。

Application -> Direct3D -> HAL -> Graphics Device

> HAL(Hardware Abstraction Layer):硬件抽象层，来统一不同显卡的接口。
>
> 调用HAL中没有实现的Direct3D函数将会出错(顶点处理操作例外，该功能可以软件模拟)，因此使用一些少数显卡支持的高级特性时，必须检测设备是否支持。

### REF Device

REF设备用软件模拟了所有的Direct3D API，允许写并测试显卡不支持的Direct3D特性的代码。

和DirectX SDK一起被装载，不会发布给用户。

### D3DDEVTYPE

设备类型，包括：

- D3DDEVTYPE_HAL
- D3DDEVTYPE_REF

## COM

组件对象模型(COM，Component Object Model)是一种能使DirectX独立于编程语言和具有向下兼容的技术。我们通常把COM对象作为一个接口，可以把它当作达到某种目的的C++类来使用。

用完某个接口后，调用他的Release方法比直接Delete它更好。COM对象具有自己的内存管理。

COM接口都具有前缀大写字母“I”，如表面的COM接口叫IDirect3DSurface9。

## 一些准备工作



## 初始化Direct3D

### 获得IDirect3D9接口

{% highlight c++ %}
IDirect3D9* _d3d9;
_d3d9 = Direct3DCreate9(D3D_SDK_VERSION);
{% endhighlight %}

IDirect3D9对象用途：

- 设备列举
- 创建IDirect3DDevice9对象

### 检测硬件顶点处理

{% highlight c++ %}
HRESULT IDirect3D9::GetDeviceCaps(
	UNIT Adapter, // 显示适配器，可用D3DADAPTER_DEFAULT
	D3DDEVTYPE DeviceType, // 设备类型
	D3DCAPS9 *pCaps // 返回设备的技术特性
);
{% endhighlight %}

{% highlight c++ %}
D3DCAPS9 caps;
d3d9->GetDeviceCaps(D3DADAPTER_DEFAULT, deviceType, &caps);

int vp = 0;
if(caps.DevCaps & D3DDEVCAPS_HWTRANSFORMANDLIGHT)
{
	vp = D3DCREATE_HARDWARE_VERTEXPROCESSING;
}
else
{
	vp = D3DCREATE_SOFTWARE_VERTEXPROCESSING;
}
{% endhighlight %}

- D3DCREATE_HARDWARE_VERTEXPROCESSING:硬件顶点处理
- D3DCREATE_SOFTWARE_VERTEXPROCESSING:软件顶点处理

### 填充D3DPRESENT_PARAMETERS结构

该结构用于设定我们将要创建的IDirect3DDevice9对象的一些特性。

- UNIT BackBufferWidth:后备缓冲表面的宽度（以像素为单位）
- UNIT BackBufferHeight:后备缓冲表面的高度（以像素为单位）
- D3DFORMAT BackBufferFormat:后备缓冲表面的像素格式（如：32位像素格式为D3DFMT_A8R8G8B8）
- UNIT BackBufferCount:后备缓冲表面的数量，通常设为“1”，即只有一个后备表面
- D3DMULTISAMPLE_TYPE MultiSampleType:全屏抗锯齿的类型
- DWORD MultiSampleQuality:全屏抗锯齿的质量等级
- D3DSWAPEFFENT SwapEffect:指定表面在交换链中是如何被交换的，取D3DSWAPEFFECT枚举类型中的一个成员，其中D3DSWAPEFFECT_DISCARD是最有效的
- HWND hDeviceWindow:与设备相关的窗口句柄
- BOOL Windowed:true为窗口模式，false为全屏模式
- BOOL EnableAutoDepthStencil:true则D3D将自动创建深度/模版缓冲
- D3DFORMAT AutoDepthStencilFormat:深度/模版缓冲的格式
- DWORD Flags:一些附加特性，设为0或D3DPRESENTFLAG类型的一个成员
	- D3DPRESENTFLAG_LOCKABLE_BACKBUFFER:设定后备表面能够被锁定，这会降低应用程序的性能
	- D3DPRESENTFLAG_DISCARD_DEPTHSTENCIL:深度/模版缓冲在调用IDirect3DDevice9::present方法后将被删除，这有利于提升程序性能
- UNIT FullScreen_RefreshRateInHz:刷新率，设定D3DPRESENT_RATE_DEFAULT使用默认刷新率
- UNIT PresentationInterval:交换速度
	- D3DPRESENT_INTERVAL_IMMEDIATE:立即交换
	- D3DPRESENT_INTERVAL_DEFAULT:D3D选择交换速度，通常等于刷新率

### 创建IDirect3DDevice9对象

{% highlight c++ %}
HRESULT IDirect3D9::CreateDevice(
	UNIT Adapter,
	D3DDEVTYPE DeviceType,
	HWND hFocusWindow,
	DWORD BehaviorFlags,
	D3DPRESENT_PARAMETERS *pPresentationParameters,
	IDirect3DDevice9** ppReturnedDeviceInterface
);
{% endhighlight %}

## 一个框架

[OneFrame](https://github.com/laijingfeng/DirectX/tree/master/OneFrame)

- d3dUtility.h/cpp
	- InitD3D:初始化Direct3D
	- EnterMsgLoop:处理消息
	- Colors:预定义颜值值
	- Lights:灯光处理
	- Materials:材质处理
	- Textures:贴图处理
- workSpace.cpp:具体工作环境
	- WinMain:主函数，相当于Unity中Awake
	- Setup:设置，相当于Unity中Start
	- Display:每一帧处理，相当于Unity中Update
	- Cleanup:清理，相当于Unity中OnDispose
- myLog.h/cpp:打印日志，MyLog::Log("test %d\n",1);
- cube.h/cpp:一个立方体类
- vertex.h/cpp:顶点结构









