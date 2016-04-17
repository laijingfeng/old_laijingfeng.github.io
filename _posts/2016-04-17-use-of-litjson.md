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
using System.Collections.Generic;
using System.IO;

public class Test : MonoBehaviour
{
    void Start()
    {

    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.A))
        {
            ShowClassData(Str2Class(GetStrDataFromFile()));
            ClassA testA = MakeClassData();
            ShowClassData(testA);
            SaveStrDataToFile(Class2Str(testA));
        }
    }

    /// <summary>
    /// 类A
    /// </summary>
    private class ClassA
    {
        public int id;
        public string name;
        public int[] count;
        public ClassB[] classB;

        public int ClassBCount()
        {
            if (classB == null)
            {
                return 0;
            }
            return classB.Length;
        }
    };

    /// <summary>
    /// 类B
    /// </summary>
    private class ClassB
    {
        public int num;
        public string address;

        public int FuncNumPlus()
        {
            return num + 1;
        }
    };

    #region GetStrData

    private string GetStrDataFromWeb()
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

    private string GetStrDataFromPlayerPrefs()
    {
        string data = PlayerPrefs.GetString("LocalData", string.Empty);
        return data;
    }

    private string GetStrDataFromFile()
    {
        string filePath = Application.dataPath + "/../TestData";

        string strData = string.Empty;

        FileInfo fileInfo = new FileInfo(filePath);
        if (!fileInfo.Exists)
        {
            return strData;
        }

        try
        {
            StreamReader streamReader = File.OpenText(filePath);
            strData = streamReader.ReadToEnd();
            streamReader.Close();
        }
        catch (System.Exception ex)
        {
            Debug.LogError("error:" + ex.Message);
        }

        return strData;
    }

    #endregion

    #region SaveStrData

    private void SaveStrDataToPlayerPrefs(string strData)
    {
        PlayerPrefs.SetString("LocalData", strData);
    }

    private void SaveStrDataToFile(string strData)
    {
        string filePath = Application.dataPath + "/../TestData";
        try
        {
            FileStream fileStream = new FileStream(filePath, FileMode.Create);
            StreamWriter streamWriter = new StreamWriter(fileStream);

            streamWriter.Write(strData);

            streamWriter.Close();
            fileStream.Close();
        }
        catch (System.Exception ex)
        {
            Debug.LogError("error:" + ex.Message);
        }
    }

    #endregion

    private string Class2Str(ClassA classData)
    {
        string strData = LitJson.JsonMapper.ToJson(classData);
        return strData;
    }

    private ClassA Str2Class(string strData)
    {
        ClassA classA = null;
        try
        {
            classA = LitJson.JsonMapper.ToObject<ClassA>(strData);
        }
        catch (System.Exception ex)
        {
            Debug.LogError("error:" + ex.Message);
        }
        return classA;
    }

    private ClassA MakeClassData()
    {
        ClassA classData = new ClassA();
        classData.id = 1;
        classData.name = "test";

        List<ClassB> listB = new List<ClassB>();
        for (int i = 0; i < 3; i++)
        {
            ClassB tb = new ClassB();
            tb.num = i;
            tb.address = "test_" + i.ToString();
            listB.Add(tb);
        }
        classData.classB = listB.ToArray();

        classData.count = new int[2] { 1, 2 };

        return classData;
    }

    private void ShowClassData(ClassA data)
    {
        Debug.LogError("===ShowData===");
        if (data == null)
        {
            return;
        }

        Debug.LogError("id=" + data.id + " name=" + data.name);

        for (int i = 0, imax = (data.count == null) ? 0 : data.count.Length; i < imax; i++)
        {
            Debug.LogError("count[" + i + "]:" + data.count[i]);
        }

        Debug.LogError("Cnt=" + data.ClassBCount());

        for (int i = 0, imax = (data.classB == null) ? 0 : data.classB.Length; i < imax; i++)
        {
            Debug.LogError("ClassB[" + i + "]" + " num=" + data.classB[i].num + " address=" + data.classB[i].address);
        }
    }
}
```

## 说明

> 1. 是用字段名索引的，有的话就填充，没有就忽略，所以不管是类还是数据属性更多或少都没有关系，当然，如果一个名字类型不一致匹配就要报错了。
> 1. 数据类可以包含方法。
> 1. 要用到不定组数据，就要用数组属性。
> 1. 可以用来解析协议数据，也可以用来做本地数据存档。
> 1. 不限于Unity，.Net平台即可用。

## 参考

- [.NET平台开源JSON库LitJSON的使用方法](http://www.jiaonan.tv/html/blog/1/27727.htm)
- [LitJSON Quickstart Guide](http://lbv.github.io/litjson/docs/quickstart.html)