---
title: MVC，MVP 和 MVVM 的图示
---
![GitHub Logo](/img/vue/20170925123312.jpg)
复杂的软件必须有清晰合理的架构，否则无法开发和维护。MVC（Model-View-Controller）是最常见的软件架构之一，业界有着广泛应用

+ <!-- more -->

## MVC

MVC模式的意思是，软件可以分成三个部分。
![GitHub Logo](/img/vue/bg2015020104.png)
```
视图（View）：用户界面。
控制器（Controller）：业务逻辑
模型（Model）：数据保存
```
![GitHub Logo](/img/vue/bg2015020105.png)

```
View 传送指令到 Controller
Controller 完成业务逻辑后，要求 Model 改变状态
Model 将新的数据发送到 View，用户得到反馈
```

所有通信都是单向的。

## 互动模式

接受用户指令时，MVC 可以分成两种方式。一种是通过 View 接受指令，传递给 Controller。

![GitHub Logo](/img/vue/bg2015020106.png)

另一种是直接通过controller接受指令。
![GitHub Logo](/img/vue/bg2015020107.png)


## 实例：Backbone
![GitHub Logo](/img/vue/bg2015020108.png)

```
用户可以向 View 发送指令（DOM 事件），再由 View 直接要求 Model 改变状态。
用户也可以直接向 Controller 发送指令（改变 URL 触发 hashChange 事件），再由 Controller 发送给 View。
Controller 非常薄，只起到路由的作用，而 View 非常厚，业务逻辑都部署在 View。所以，Backbone 索性取消了Controller，只保留一个 Router（路由器） 。
```

## MVP

MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。

![GitHub Logo](/img/vue/bg2015020109.png)
```
各部分之间的通信，都是双向的。
View 与 Model 不发生联系，都通过 Presenter 传递。
View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而Presenter非常厚，所有逻辑都部署在那里。
```


## MVVM

MVVM 模式将 Presenter 改名为 ViewModel，基本上与 MVP 模式完全一致。

![GitHub Logo](/img/vue/bg2015020110.png)

唯一的区别是，它采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然。Angular 和Ember 都采用这种模式。


