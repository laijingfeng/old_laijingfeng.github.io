---
layout: post
title: 博客markdown配置
date: 2015-12-10 00:00:00
categories: Blog
excerpt : Blog, Jekyll
---

* content
{:toc}

## 概述

文章所述基于[旧博客](https://github.com/laijingfeng/old_laijingfeng.github.io)

本博客通过[Jekyll Bootstrap](http://jekyllbootstrap.com/)创建，原生对markdown的配置并不全，补充一二。

我用的是bootstrap-3主题，所以下面说的配置都是在这个主题下做的。

## 配置

`\_includes\themes\bootstrap-3\settings.yml`配置markdown。

{% highlight c++ %}
markdown: kramdown
 input:  GFM
 use_coderay: true
{% endhighlight %}

### 表格

表格是支持的，但是显示有些问题，没有分割线

补充css文件，`\assets\themes\bootstrap-3\css\style.css`，加上：

{% highlight css %}
table{
  border-collapse:collapse;
}

table, th, td{
	border: 1px solid black;
}

th{
  background-color:LightGrey;
}
{% endhighlight %}

### 代码着色

1.`\assets\themes\bootstrap-3\css`增加`pygments.css`。

> pyments.css可以自己安装Pyments生成，也可以从这里取：[pygments-css](https://github.com/icco/pygments-css)。

2.标记代码。用`highlight language`和`endhighlight`。

### TOC

显示TOC，并悬浮在左侧，默认隐藏，鼠标移上滑出，鼠标移走再隐藏。

1.`\_includes\themes\bootstrap-3\settings.yml`配置TOC显示的层级。`toc_levels: 2..4`，h2-h4将显示到TOC。

2.设置`\assets\themes\bootstrap-3\css\style.css`，默认位置是`left: -320px`。

{% highlight css %}
#markdown:before {
    content: "目录";
    font-weight: bold;
}
ul#markdown-toc {
    list-style: none;
    position: fixed;
	width: 350px;
    padding: 0px;
    left: -320px;
    top: 60px;
    border-radius: 0.3em;
    box-shadow: rgba(0,0,0,0.15) 0 1px 4px;
    box-sizing: border-box;
    border: #fff 0.5em solid;
    background-color: pink;
}
{% endhighlight %}

3.在`\_includes\themes\bootstrap-3\default.html`中增加移动控制函数。

{% highlight html %}
<script type="text/javascript">
	window.onload = function () {
		var oMK = document.getElementById('markdown-toc');
		oMK.onmouseover = function () {
			shareMove(10);
		}
		oMK.onmouseout = function () {
			shareMove(-320);
		}
	};
	var timer = null;
	function shareMove(end) {
		var oDiv1 = document.getElementById('markdown-toc');
		var speed = 0;
		if (oDiv1.offsetLeft < end) {//根据DIV的offsetLeft距离判断DIV所要走的正负方向
			speed = 20;
		}
		else {
			speed = -20;
		}
		clearInterval(timer);//在一个setInterval开始之前都要先清除之前的setInterval
		timer = setInterval(function () {
			if(speed > 0 && oDiv1.offsetLeft + speed >= end){
				oDiv1.style.left = end + 'px';
				clearInterval(timer);
			}
			else if(speed < 0 && oDiv1.offsetLeft + speed <= end){
				oDiv1.style.left = end + 'px';
				clearInterval(timer);
			}
			else {
				oDiv1.style.left = oDiv1.offsetLeft + speed + 'px'//DIV要走的距离
			}
		}, 30);
	}
</script> 
{% endhighlight %}

4.在要使用TOC的地方加下面标记

{% highlight c++ %}
* TOC
{:toc}
{% endhighlight %}

参考：[为 Octopress 添加 TOC](http://loudou.info/blog/2014/08/01/wei-octopress-tian-jia-toc/)

### 数学公式

在`\_includes\themes\bootstrap-3\default.html`添加：

{% highlight html %}
<script type="text/x-mathjax-config">
	MathJax.Hub.Config({
		tex2jax: {
			inlineMath: [['$','$'], ['\\(','\\)']]
		}
	});
</script>
<script type="text/javascript"
	src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight %}

参考：[Jekyll中使用MathJax](http://www.pkuwwt.tk/linux/2013-12-03-jekyll-using-mathjax/)