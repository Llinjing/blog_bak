---
title: Linux文件操作
date: 2017-05-04 00:00:00
categories: File
tags:
 - linux
 - grep
 - awk
---

Linux文件操作
 
 <!--more-->

### 文件处理字符串

1. 根据特殊字符串，输出该字符串共多少个
当用户访问一个页面，就会相应打印该页面的地址，为了统一周内，该网站每个页面的访问次数，需要取出log文件中所有的'##'前的字符串
> **log文件示例**：
t_daily_article##
SQL Request:
**处理命令**：grep "##" online-8182-out-2.log > result.log

 
 
 
 
 
 
 
 
 