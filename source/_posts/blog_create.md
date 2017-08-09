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

参考: http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more


## hexo 的yelee主题添加‘置顶文章置顶’方法
修改node_modules\hexo-generator-index\lib\generator.js 中代码，如下：
![GitHub Logo](/img/hello/01.jpg)

```
//文章置顶方法添加
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
var config = this.config;
var posts = locals.posts;
posts.data = posts.data.sort(function(a, b) {
    if(a.top && b.top) { // 两篇文章top都有定义
        if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
        else return b.top - a.top; // 否则按照top值降序排
    }
    else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
        return -1;
    }
    else if(!a.top && b.top) {
        return 1;
    }
    else return b.date - a.date; // 都没定义按照文章日期降序排
});
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```

如果想要置顶某篇文章，就在文章的Front-matter位置，添加一个 top:1000 ,值越大，越靠前，如下图：
![GitHub Logo](/img/hello/02.jpg)



