---
layout: post
title: Use of LitJson
date: 2016-04-17 00:00:00
categories: Unity
excerpt : Use of LitJson
---

* content
{:toc}

## 库链接

[LitJson.dll](http://yunpan.cn/cm45mUvwUTtgP)（访问密码： 798c）

## 用法

举个栗子就知道所有的用法了，点包括：属性、数组、结构嵌套。

```c#
using UnityEngine;
using System.Collections;

public class Test : MonoBehaviour
{
    void Update()
    {
        if(Input.GetKeyDown(KeyCode.A))
        {
            DoTest();
        }
    }

    /// <summary>
    /// 测试
    /// </summary>
    private void DoTest()
    {
        C1 c1 = new C1();
        SaveData<C1>(c1, "testData");
        C1 c2 = LoadData<C1>("testData");
        if (c2 != null)
        {
            c2.Print();
        }

        C3 ca = new C3();
        C3 cb = AnalysisData<C3>(ca.GetJsonData());
        if (cb != null)
        {
            cb.Print();
        }
    }

    /// <summary>
    /// 加载数据
    /// </summary>
    /// <typeparam name="T"></typeparam>
    /// <param name="dataName"></param>
    /// <returns></returns>
    private T LoadData<T>(string dataName)
    {
        string strData = PlayerPrefs.GetString(dataName, string.Empty);
        T t = default(T);
        try
        {
            t = LitJson.JsonMapper.ToObject<T>(strData);
        }
        catch (System.Exception ex)
        {
            Debug.LogError("error:" + ex.Message);
        }
        return t;
    }

    /// <summary>
    /// 解析数据
    /// </summary>
    /// <typeparam name="T"></typeparam>
    /// <param name="strData"></param>
    /// <returns></returns>
    private T AnalysisData<T>(string strData)
    {
        T t = default(T);
        try
        {
            t = LitJson.JsonMapper.ToObject<T>(strData);
        }
        catch (System.Exception ex)
        {
            Debug.LogError("error:" + ex.Message);
        }
        return t;
    }

    /// <summary>
    /// 保存数据
    /// </summary>
    /// <typeparam name="T"></typeparam>
    /// <param name="data"></param>
    /// <param name="dataName"></param>
    private void SaveData<T>(T data, string dataName)
    {
        string strData = LitJson.JsonMapper.ToJson(data);
        PlayerPrefs.SetString(dataName, strData);
    }
}
```

```c#
using UnityEngine;
using System.Collections;
using System.Collections.Generic;

/// <summary>
/// 类1
/// </summary>
public class C1
{
    public int ia;
    public uint ib;
    //public long la;
    public ulong lb;
    public string sa;
    //public float fa;
    //public double fb;
    public byte ba;
    public int[] iarr;
    public List<int> ilist;
    public List<C2> c2list;

    public C1()
    {
        ia = 1;
        ib = 2;
        //la = 1;
        lb = 2;
        sa = "hi";
        //fa = 1.0f;
        //fb = 2.0f;
        ba = 3;
        iarr = new int[2] { 1, 2 };
        ilist = new List<int>() { 3, 4 };
        c2list = new List<C2>() { new C2() };
    }

    /// <summary>
    /// 打印
    /// </summary>
    public void Print()
    {
        Debug.LogError(string.Format("ia={0},ba={1}", ia, ba));
    }
}

/// <summary>
/// 类2
/// </summary>
public class C2
{
    public int ia;
    public uint ib;
    public S1 s1;

    public C2()
    {
        ia = 1;
        ib = 2;
        s1.ia = 3;
        s1.ib = 4;
    }
}

/// <summary>
/// 结构体1
/// </summary>
public struct S1
{
    public int ia;
    public uint ib;
}

public class C3
{
    public int id;
    public string name;
    public int[] count;
    public C4[] classB;

    public C3()
    {
        id = 1;
        name = "name";
        count = new int[1] { 1 };
        classB = new C4[1] { new C4() };
    }

    public string GetJsonData()
    {
        string data = @"
        {
            ""id"" : 2015,
            ""name"" : ""jerrylai"",
            ""count"" : [1,2,3],
            ""classB"" : [
                {
                    ""num"" : 10,
                    ""address"" : ""SH""
                },
                {
                    ""num"" : 11,
                    ""address"" : ""NB""
                }
            ]
        }";
        return data;
    }

    /// <summary>
    /// 打印
    /// </summary>
    public void Print()
    {
        Debug.LogError(string.Format("id={0},name={1}", id, name));
    }
}

public class C4
{
    public int num;
    public string address;

    public C4()
    {
        num = 1;
        address = "address";
    }
}
```

## 说明

> 1. 是用字段名索引的，有的话就填充，没有就忽略，所以不管是类还是数据属性更多或少都没有关系，当然，如果一个名字类型不一致匹配就要报错了。
> 1. 数据类可以包含方法。
> 1. 支持有问题的类型：float/double/Dictionary。long在Load的时候，会认为是Int32转Int64报错。
> 1. 可以用来解析协议数据，也可以用来做本地数据存档。
> 1. 不限于Unity，.Net平台即可用。

## 参考

- [.NET平台开源JSON库LitJSON的使用方法](http://www.jiaonan.tv/html/blog/1/27727.htm)
- [LitJSON Quickstart Guide](http://lbv.github.io/litjson/docs/quickstart.html)