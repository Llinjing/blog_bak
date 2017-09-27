---
title: windows10安装vue.js
---
<div align=left>
    <img src="/img/vue/238555602663002408.jpg" width="600" height="400" alt=""/>
</div>
想写下前端的自动定制报表UI，觉得vue不错，就想玩一下，谁知道在win上安装那么麻烦，问题不断，最后终于解决了（网上资料鱼龙混杂，还是要带脑子解决问题才行）。详细安装步骤如下：

+ <!-- more -->

## 总括
避免我写的比较啰嗦，这里是所有的安装步骤，想看详细的，可以跳过这里。
```
到https://nodejs.org/zh-cn/ 下载安装nodejs
npm install -g cnpm --registry=http://registry.npm.taobao.org
cnpm install vue
cnpm install --global vue-cli
```


## 详细步骤

### 1.安装nodejs

windows的在官网上下载，地址
```
https://nodejs.org/zh-cn/
```


我安装的是下图中的版本:
![GitHub Logo](/img/vue/20170927103933.png)

下载以后，双击安装，npm也会同时安装好的。

### 2.安装cnpm

使用npm就行vue的安装，总是会出现各种问题，干脆放弃，直接用cnpm
安装方法，在cmd中执行下面的命令
```
npm install -g cnpm --registry=http://registry.npm.taobao.org
```

等待。。。。。

出现下图，表示安装ok
![GitHub Logo](/img/vue/20170927104442.png)


### 3.安装vue
执行命令
```
cnpm install vue
```
安装好以后，如下图：
![GitHub Logo](/img/vue/20170927105040.png)

有个问题，这个安装好以后，执行vue会出现下图：
![GitHub Logo](/img/vue/20170927105152.png)

这个我直接忽略了，继续安装vue-cli

### 4.安装vue-cli
执行命令：
```
cnpm install --global vue-cli
```
安装成功的图：
![GitHub Logo](/img/vue/20170927105347.png)

好了，到这里，就可以愉快地使用了，心好累。。。。。

记得上面那个问题吗？？解决了，安装个client，就解决了，好无语，等待大神告诉为什么- _ -


## 创建基于webpack的vue project
```
vue init webpack vue_test
cd vue_test
cnpm install
```
![GitHub Logo](/img/vue/20170927144838.png)


## 运行vue project
```
cnpm run dev
```
![GitHub Logo](/img/vue/20170927145044.png)
![GitHub Logo](/img/vue/20170927144950.png)


## 发布
```
cnpm run build
```
发布以后会生成一个dist文件夹，可以直接拿这个文件是发布项目




