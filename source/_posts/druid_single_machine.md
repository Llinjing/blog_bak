---
title: druid单机版搭建流程
tags: druid
---

  druid使用也有一年了，踩过的坑无数，现在虽然线上服务已经稳定，但是还是使用的小白，觉得还是有必要把搭建的流程记录下。
  单机版的搭建流程十分简单，适合机器资源不是很充足，或者对druid使用方法测试阶段。其实步骤跟官网上介绍的流程一样的，实时加载使用druid+tranquility，离线数据加载使用druid的batch加载方式。用的很简单，有不足的地方，望指教。

+ <!-- more -->
  
##准备工作 

``` bash
mysql
druid
tranquility
zookeeper （公司已有，没深究如何搭建）
kafka（使用公司已有的，没深究搭建方式）
```


## 具体搭建步骤


### 

``` bash
到https://github.com/注册自己的github账号
```
### 在github中，创建一个仓库，命名为username.github.io (例：miaomiao.github.io)

``` bash
特别说明：如果出现本地hexo服务正常，但是github上的博客项目不能访问，我这里遇到的情况是username没有使用自己github的账号，对项目重命名，就可以了。
```

### 本地hexo项目创建

``` bash
npm install -g hexo-cli (安装hexo)
npm install 
hexo init (初始化hexo 项目)
hexo generate (or hexo g) （生成静态文件）
hexo deploy (or hexo d) (发布本地项目到github)
```





