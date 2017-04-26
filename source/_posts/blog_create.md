---
title: hexo+github搭建博客步骤
tags:
- hexo
- github pages
---

一时兴起，想搭建一个自己的博客，就动手搭建了一个，这里做一个记录，记录下自己踩得坑，以免自己以后忘记

## 整个搭建流程总览

``` 
创建自己的github账号
创建username.github.io的项目
创建本地hexo项目
将本地hexo项目发布到github
```
+ <!-- more -->
## 具体操作流程


### 创建github账号

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

更多细节，不再赘述，可以参考: http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more



