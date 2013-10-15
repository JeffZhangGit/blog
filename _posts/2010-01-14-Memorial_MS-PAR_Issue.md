---
author: jeffzhang
comments: true
date: 2010-01-14 18:49:48+00:00
layout: post
title: 纪念MS-PAR的Issue
wordpress_id: 58
categories:
- 挨踢
tags:
- dg
- driver
- ms
- x800
- 杂谈
- 测试环境
---

凌晨2点

连续两个凌晨2点

只为了解决一个Issue

BUG

一个深埋已久匪夷所思鬼使神差般的BUG

言语已经无法形容我们怎么能遇到如此一个BUG

1.当Issue出现，当时Code没有改变，测试环境没有改变，没有人猜想到是认证证书过期的Issue。

2.DirverStore的Issue一般都是用户权限相关，初期调研主要放在这个方面。

3.当常规方法没有解决Issue，ErrorCode是0x800F0247，没有任何ErrorCode相关的资料。我们发现DG中的Driver文件和我们实际测试环境中的时间不同。当替换了Driver文件Issue解决。

4.第二天Issue重新出现，关键在于证书过期的时间就是昨天，2010年1月13日。

5.更改测试环境日期，所有问题终于解决。

Congratulations！For our high quality technology document.
