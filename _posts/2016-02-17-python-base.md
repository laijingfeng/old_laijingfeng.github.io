---
layout: post
title: Python基础
date: 2016-02-17 00:00:00
categories: Python
excerpt : Python
---

* content
{:toc}

玩一玩Python。

## string

书写时单引号和双引号都可以

要和内部引号不一样，或者内部引号转义

真正的引号是什么，单引号优先，有内部引号的则和内部引号相反

转义只能用在第一层，超过和转义符一起显示

> egs:
>
> 'lai'->'lai'
>
> "lai"->'lai'
>
> "lai'jing"->"lai'jing"
>
> 'lai\'jing'->"lai'jing"
>
> "\"hello\"lai"->'"hello"lai'
>
> 'lai"a\'aa"'->'lai"a\'aa"'

可用\n换行

字符串可以+、*运算

**字符串索引**

str[idx]

str[idx1:idx2]

超出范围的不计，idx1默认0，idx2默认len

![stringIdx](/assets/blog-images/2016-02/stringIdx.png)

r去除转义

### string.format

```python
output:1 and hello and 1.1
print '{} and {} and {}'.format(1, 'hello', 1.1)
print '{0} and {1} and {2}'.format(1, 'hello', 1.1)
print '{one} and {two} and {three}'.format(one=1, two='hello', three=1.1)
print '{0} and {1} and {three}'.format(1, 'hello', three=1.1)

'12'.zfill(5) => '00012'
'-3.14'.zfill(7) => '-003.14'

print '{0:2d}'.format(1)
print 'PI:{0:.3f}'.format(3.14159) => PI:3.142
print '{0:10}'.format('test')
```

**旧模式**

print 'PI:%5.3f' % 3.14159261

**对齐**

- str.ljust(x)
- str.rjust(x)
- str.enter(x)

## 基本操作

**注释**

- `#行注释`
- `两个'''或"""之间块注释`

**变量定义赋值**

- flag = 0
- a, b = 0, 1 # 多变量赋值

**指定编码格式**

`# -*- coding: UTF-8 -*-`

**常用函数**

- 绝对值 abs()
- 长度 len(xx)

**类型转换**

- int()
- long()
- float()
- 

**输出**

print 'xxx'

后面加逗号可以让下一次输出同行

print xx1, xx2

输出时两个参数之间会默认加一个空格

整数，非0为True，其他为False

**算术比较**

- `>`
- `<`
- `==`
- `<=`
- `>=`
- `!=`

**逻辑运算**

- and

## 数据结构

### List

定义并初始化

a = ['lai', 'jing', 'feng', 1, 2, 3]

类型可混合使用

索引规则同字符串

支持*、+运算

元素可以是List，List为元素时长度算1个单位

#### 内置函数

- list.count(x)
	- 计算x的数量
- list.append(x)
	- 附加一个元素，等同a[len(a):] = [x]
- list.extend(L)
	- 附加一个List，等同a[len(a):] = L
- list.insert(i, x)
	- 插入，a.insert(len(a), x)等同a.append(x)
- list.remove(x)
	- 移除第一个x，如果x不存在将报错
- list.pop([i])
	- 移除并返回i位置的元素，无参数a.pop()则是最后一个元素
- list.index(x)
	- 返回第一个x的索引，x不存在将报错
- list.sort()
	- 升序排序
- list.reverse()
	- 反转

一些操作：

- 修改
	- a[0] = ‘xxx’
- 替换
	- a[0:2] = [xxa, xxb]
- 删除部分
	- a[0:2] = []
- 插入
	- a[1:1] = [xxa, xxb]
- 清空
	- a[:] = []
- 长度
	- len(a)
	
#### deque

List当栈使用方便，当队列使用效率比较低，可以使用deque，见代码

![stringIdx](/assets/blog-images/2016-02/deque.png)

deque的更多用法

- append/appendleft 在右/左边附加一个元素
- clear 清空
- count
- extend/extendleft 在右/左边扩展一个List
- maxlen/pop/popleft/remove/reverse
- rotate索引前挪一位

#### del

del a[0] 删除一个元素

del a[0:2] 删除一些元素

del a 删除变量

### Tuple

a = (1, 2, 'lai')

括号可以省略

零元素和单元素tuple，a = ()；a = 'lai',

### Set

...

### Dictionary

#### 创建

```python
dict = {'name':'laijingfeng', 'year':2016}
print dict['name']
```

#### 修改

...

参考：[Python 字典(Dictionary)操作详解](http://www.jb51.net/article/47990.htm)

## 文件操作

```python
f = open('filename', 'mode')
...
f.close()
```

mode:

- r:只读
- w:只写(覆盖)
- a:附加写
- r+:读写
- 加b是操作二进制文件，如rb，wb

```python
for line in f:
	print line,
```

- f.read([size])
- f.readline()
- f.readlines()或者list(f)

f.write(string)

- f.tell() 文件操作位置
- f.seek(offset, from_what) 改变文件操作位置
	- from_what:0-beginning;1-current;2-end

推荐用法

```python
with open('lai.txt', 'r') as f:
	read_data = f.read()
```

f.closed # 文件是否关闭

### 路径处理

- 获取执行目录:`os.getcwd()`
- 获取当前文件相对目录:`sys.argv[0]`
- 获取当前文件绝对目录:`os.path.abspath(sys.argv[0])`
- python操作Windows目录可以用左斜杠`/`，也可以用`\\`
- `os.path.split(path)`，把path分成路径和文件名两部分

更多参考:[python文件和路径操作](http://www.cnblogs.com/bluescorpio/archive/2009/11/21/1607446.html)

## 控制流

### 条件

```python
if x < 0:
	Print 'if'
elif x == 0:
	print 'elif'
else:
	print 'else'
```

in

if x in (‘xx1’, ‘xx2’, ‘xx3’)

### 循环

```python
words = [‘cat’, ‘windows’, ‘hello’]
for w in words:
print w, len(w)
```

上面for中的words改为words[:]，就可以直接插入等操作words，循环的是旧的枚举器

有break/continue语法

pass为了语法正确暂时没有内容，跳过

- range()
- range(int num) # [0, 1, ..., num-1]
- range(int num1, int num2) # [num1, num1+1, ..., num2-1]
- rang(int num1, int num2, int step) # [num1, num1+step, ..., num1+n*step<=num2-1]

## 模块

filename.py里定义了fun1和fun2函数

在其他脚本里，import filename，然后可以形如filename.funname使用filename.py里的函数

其他形式

```html
from filename import fun1, fun2
fun1(...)

from filename import *
fun1(...)
```

引用会生成.pyc文件，这个是最终需要的

如果有包名，则import xx.xx.filename，使用是xx.xx.filename.funname

包就是一个文件夹，需要包含一个__init__.py文件，可以是空文件

### 标准模块

dir([name])列出[name]模块定义的变量

- sys
- os

sys.path 环境变量

### 函数

```python
def funcName(par1, par2, par3=1, par4=i, par5=9):
	return xx
```

函数不写返回值，默认是None

par4=i，变量参数，会从当前定义的同名取

def fun1(L=[])，L只有第一次调用时会赋值[]，后续调用是在上次调用的基础上操作

Keyword Arguments

参数可以用名称指定，跳跃式赋值

funcName(par2=1, par1=2, par5=44)

主函数

`if __name__ == '__main__':`

函数参数

sys.argv是参数列表，第0个参数是脚本名

exit()退出

### 库安装

1. 源码`Source`安装
	
	下载安装包，解压，里面会有`setup.py`，进入文件夹执行`sudo python install`

1. `pip`安装

	参考：[pip安装使用详解](http://www.ttlsa.com/python/how-to-install-and-use-pip-ttlsa/)
	
## 执行Shell命令

参考:[python中执行shell命令的几个方法小结](http://www.jb51.net/article/55327.htm)

1. `os.system()`
	
	如`os.system('cat /proc/cpuinfo')`，命令执行结果只有0或者1。
1. `os.open()`
	
		output = os.popen('cat /proc/cpuinfo')
		print output.read()
	
	通过os.popen()返回的是file read的对象，对其进行读取read()的操作可以看到执行的输出。但是无法读取程序执行的返回值。
1. `commands.getstatusoutput()`
	
		(status, output) = commands.getstatusoutput('cat /proc/cpuinfo')
		print status, output
		
1. `subprocess`

	直接看一个示例，就是把shell命令按空格拆成args组执行

		import subprocess

		# 执行shell命令，wait，T为同步，F为异步
		def execute_shell_command(args, wait='T'):
			p = subprocess.Popen(args)
			if wait == 'T':
				ret = p.wait()
				return ret
			else:
				return 0
		
		# 一个使用，"rm ${HOME_PATH}/lai.png"
		def one_use():
			args = ['rm', HOME_PATH + '/lai.png']
			execute_shell_command(args, 'F')
