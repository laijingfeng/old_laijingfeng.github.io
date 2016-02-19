---
layout: post
title: 博客修改日志
date: 2016-01-24 00:00:00
categories: Blog
excerpt : Blog
---

* content
{:toc}

## 说明

博客的更新日志

## 2016-01-25 增加favicon

根目录增加favicon.ico

在`_includes\themes\bootstrap-3\default.html`，增加

	<link rel="shortcut icon" href="{{ site.baseurl }}/favicon.ico" />

`_config.yml`增加`baseurl : `

## 2016-01-24 加速

##### 屏蔽评论

在`_includes\themes\bootstrap-3\post.html`

	<!-- 去掉评论，加速 -->
	<!-- {% include JB/comments %} -->

##### jequry.mini.js换国内源

在`_includes\themes\bootstrap-3\default.html`

	<!-- 更换jquery.mini.js地址 -->
	<script src="http://libs.baidu.com/jquery/1.10.2/jquery.min.js"></script>
	<!-- <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script> -->

##### 屏蔽Google分析

在`_includes\themes\bootstrap-3\default.html`

	<!-- 去掉分析，加速 -->
	<!-- {% include JB/analytics %} -->

##### 屏蔽Search

在`_includes\themes\bootstrap-3\default.html`

	<!-- Search好像没有什么用，屏蔽 -->
	<!--
	<form class="navbar-form navbar-right" role="search">
	<div class="form-group">
	  <input type="text" class="form-control" placeholder="Search">
	</div>
	<button type="submit" class="btn btn-default">Submit</button>
	</form>
	-->

##### 屏蔽订阅

在`_includes\themes\bootstrap-3\default.html`

	<!-- atom & rss feed -->
	<!-- <link href="{{ BASE_PATH }}{{ site.JB.atom_path }}" type="application/atom+xml" rel="alternate" title="Sitewide ATOM Feed"> -->
	<!-- <link href="{{ BASE_PATH }}{{ site.JB.rss_path }}" type="application/rss+xml" rel="alternate" title="Sitewide RSS Feed"> -->
