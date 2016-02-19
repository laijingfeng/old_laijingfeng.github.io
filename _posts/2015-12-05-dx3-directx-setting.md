---
layout: post
title: DirectX入门系列（三）：开发环境配置
date: 2015-12-05 00:00:00
categories: DirectX
excerpt : DirectX
---

* content
{:toc}

## 引子

DX入门以DX9最好，《DirectX 9.0 3D游戏开发编程基础》被奉为“龙书”，可以购为参考。

![dx_book](/assets/blog-images/2015-12-05_001.png)

龙书参考：

- [Directx9.0 龙书 中文.pdf](http://yunpan.cn/c33HINQYsxXBQ)(访问密码:0fcc) 
- [《DIRECTX.9.0 3D游戏开发编程基础》源代码.rar](http://yunpan.cn/c33HpH4npk3IB)(访问密码:ea04)

## 环境配置

### 软件准备

1. 安装DX的SDK库，[DXSDK_Jun10.exe](http://yunpan.cn/c33HjZpVmQjq4)(访问密码:e438)。
1. 安装VS2010

### 环境配置

书中作者(Page.V)对VC6.0和VS2005的配置进行了说明，VS2010相对于VS2005已经有些变化。

VS2010中，新建项目，“Visual C++/win32 项目”+“空项目”，把框架的.h和.cpp添加到“头文件”和“源文件”

> 创建时可以把“未解决方案创建目录”去掉，避免资源没有放在特定文件夹找不到

- 项目名->属性->配置属性
	- VC++目录
		- 「包含目录(Include)」，增加如：D:\Program Files\DirectX\Include
		- 「库目录(Library)」，增加如：D:\Program Files\DirectX\Lib\x86
	- 常规
		- 「字符集」，“使用多字节字符”，不然`wc.lpszClassName	="Direct3D9App"`这样的引号字符串代码不能用
	- 连接器
		- 输入
			- 「附加依赖项」，添加“d3d9.lib;d3dx9.lib;winmm.lib”，不然引起报错“无法解析的外部符号 _Direct3DCreate9@4”

## 错误处理

**VS报错**

新建了一个空白.h文件，一编辑就报下面的错误，然后“停止工作”，“重新启动”。

![VSCrash](/assets/blog-images/2015-12-05_002.png)

是因为安装VS2008修改了注册表导致的，修改如下：

- Win+R运行“regedit”，改默认值。
- 32位机器，[HKEY_CLASSES_ROOT\CLSID\{73B7DC00-F498-4ABD-AB79-D07AFD52F395}\InProcServer32]改为`C:\Program Files\Common Files\Microsoft Shared\MSEnv\TextMgrP.dll`。
- 64位机器，[HKEY_CLASSES_ROOT\Wow6432Node\CLSID\{73B7DC00-F498-4ABD-AB79-D07AFD52F395}\InProcServer32]改为`C:\Program Files (x86)\Common Files\Microsoft Shared\MSEnv\TextMgrP.dll`。

---

**DirectX安装报错S1023**

![SDK_INSTALL_ERROR](/assets/blog-images/2015-12-05_010.png)

出现S1023错误的原因是VC++运行库不能成功安装，而VC++运行库不能安装的原因是系统中已经安装了VC++运行库，并且版本等于或高于要安装的版本。

控制面板卸载下面的组件，只要版本号大于或等于10.0.30319就将其卸载掉。

- Microsoft Visual C++ 2010 x86 redistribuable
- Microsoft Visual C++ 2010 x64 redistribuable

参考:[安装DirectX提示S1023错误怎么办](http://jingyan.baidu.com/article/84b4f565ec699f60f6da32c1.html)

---

**error LNK1123: 转换到 COFF 期间失败: 文件无效或损坏**

编译时报如题错。复制

复制C:\Windows\winsxs\x86_netfx-cvtres_for_vc_and_vb_b03f5f7f11d50a3a_6.1.7601.17514_none_ba1c770af0b2031b\cvtres.exe到[VS2010安装目录]\VC\bin目录下，直接覆盖替换。

参考:[LNK1123: 转换到 COFF 期间失败: 文件无效或损坏](http://www.cnblogs.com/newpanderking/p/4003228.html)

---

**error C1033: 无法打开程序数据库“d:\xxx\debug\vc100.idb”**

清理，重新编译
		
## 参考

- [《DIRECTX.9.0 3D游戏开发编程基础》源代码 ](http://download.csdn.net/download/iduosi/5322143)
- [无法解析的外部符号 Direct3DCreate9@4](http://blog.csdn.net/zggxyx2004/article/details/5307943)
- [在vs2010下学《directx9.0 3D 游戏开发编程基础》](http://blog.csdn.net/yuanyazhen1/article/details/5836075)
- [Visual Studio 遇到了异常。这可能是由某个扩展导致的](http://blog.csdn.net/jinzhilong580231/article/details/6945991)。
- [修改注册表](http://zhidao.baidu.com/link?url=0oufaGASabTwq_JgnQY_np92z8-OrXxMHlyJ_WlQ1PAEdhF9SIJkw6MKqV1kLRBAEpRRAxs7egZumFv6P66Lv_)
