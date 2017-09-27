---
title: Hexo-Yelee 使用语法总结及注意
date: 2017-04-28 00:00:00
categories: hexo
tags:
 - hexo
 - yelee
+description: "不开心"
---

#### hexo支持的是Github Flavored Markdown语法

先来个more，详情页你不会看到我的啦~~~~

 <!--more-->

 1. 我是table

he | he
---|---
1 | 1


 2. 我是引用
 > 
Tranquility is a Scala library that coordinates streaming ingestion through the Druid indexing service. It exists because the Druid indexing service API is fairly low level. In the indexing service, callers create "tasks" that run on a single machine using a fixed bundle of resources. Indexing tasks start up with a particular configuration and generally this configuration cannot be changed once the task is running.
Tranquility manages creation of Druid indexing tasks, handling partitioning, replication, service discovery, and schema rollover for you, seamlessly and without downtime. You never have to write code to deal with individual tasks directly.

 3. 我是另一个引用
 > 
Tranquility 是一个通过druid indexing service协调实时注入的scala库。它之所以存在是因为druid indexing service的api水平相当地低。对于indexing service,调用者生成tasks，这个tasks运行在一个使用固定的资源包的机器上。Indexing tasks 用一个特定的配置启动，通常tasks一旦启动，这个配置就不能更改了。

 4. 我是注意事项
 ```bash
注意：
行与行之间，不能有多个换行，至多一个
每个命令后面需要跟一个空格，不然命令会不生效
列中穿插别的符号，就会重新开始索引的
```

 5. 我是各种标题
 <pre>
 # 标题1
 ## 标题2
 ### 标题3
 #### 标题4
 ###### 标题5
 ###### 标题6
 
 6. 我是代码段
 ```
 woshi daima
 woshi daima
 woshi daima
 ```
 
 7. 我是加粗字体
 **加粗**

 `你猜我是啥`
 
 8. `下面的是多行代码呀`
 <pre>
 fsdfgrg 
 ewrgrgregregre
 frgr 
 <code>
 
 9. 
 * 1
 * 2
 * 3
 
 10. 下面的我疯啦，你猜他们都是啥
__lalal__
_alalal_
_You **can** combine them_

* Item 1
* Item 2
  * Item 2a
  * Item 2b
  
  
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b
   

I think you should use an
`<addr>` element here instead.


## hexo插入图片，并控制图片大小
```
<div align=left>
    <img src="/img/vue/238555602663002408.jpg" width="600" height="400" alt=""/>
</div>
```

## hexo 一般插入图片简单方法
```
![GitHub Logo](/img/avatar.png)
```


 