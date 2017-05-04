---
title: druid书--阅读笔记
date: 2017-05-02 00:00:00
categories: druid
tags:
 - druid
 - tranquility
 - OLAP
 - share nothing
---

最开始接触druid是在16年3月份，那时候相关的资料很少，只有官网上的资料，近段时间，发现有人出书了，现在将在读书中遇到的一些小重点记录下来，也算是一种经验的积累（工作是，实时加载用的是Index Service的方式来加载数据）。

 <!-- more -->

## 基本简介
1. druid是一个分布式的支持实时分析的** 数据存储系统 **。
2. 数据集合包括** 时间列（Timestamp）**、** 维度列（Dimension）**、** 指标列（Metrics）**。
3. 数据摄入方式分为** 实时数据摄入**、** 批处理数据摄入**。
4. 实时数据处理部分是面向写多读少的优化，批处理部分是面向读多写少的优化。
5. 整个系统使用Zookeeper进行协调，mysql存储元数据。
6. 不支持JOIN
7. 按时间粒度对数据进行聚合。
8. OLAP（联机分析处理），核心思想是建立多维度的数据立方体，以维度和度量为基本概念，辅以元数据实现可以钻取（Drill-down/up）、切片（Slice）、切块（Dice）的数据展现。
9. Pinot与druid最为相似，整体设计更加完整和系统化
10. druid标签：开源、实时、高效、简洁。

## 架构详解（realtime方式）
1. druid节点
 **实时节点（Realtime Node）**：摄入实时数据，生成segment数据文件
 **历史节点（Historical Node）**：加载已生成好的数据文件，供数据查询
 **查询节点（Broker Node）**：对外提供数据查询服务，并同时从实时节点和历史节点查询数据，合并后，返回给调用方
 **协调节点（Coordinator Node）**：负责历史节点的数据负载均衡，及通过规则（Rule）管理数据的生命周期

2. 外部依赖
**元数据库**：存储druid集群的原数据信息
**分布式协调服务（ZK）**：为druid集群提供一致协调性服务
**数据文件存储库**：存放生成的segment数据文件，供历史节点下载

3. 索引（Index）：加速数据库数据的访问（使用树结构）

4. 总体架构
> 实时数据 --> 加载到 --> 实时节点内存中的堆结构缓存区 --> （满足条件的时候）--> 写进磁盘 --> 形成数据块（segment split）-->（同时）--> 实时节点会立即将新生成的数据块 --> 加载 --> 内存中的非堆区 -->（同时）--> 实时节点周期性的将磁盘同一时间内生成的所有数据块合并为一个大的数据块（Segment Merge） -->（立即）--> 该segment被实时节点上传到数据文件存储库（HDFS...） -->（随后）--> 协调节点（coordinator）-->（指导）--> 历史节点 --> 去文件存储库将新生成的segment下载到本地磁盘中 --> 加载成功 --> historical -->（通过）--> 协调节点（coordinator）--> 声明从此刻开始提供该新生成的segment的查询 --> 实时节点收到声明 --> 声明自己不再提供该segment的查询。
<br />
 > 查询节点会一直从实时节点和历史节点中查询数据，并做整合。

## 实际使用（Index Service方式-tranquility）
1. Master：协调节点（Coordinator）和统治节点（Overlord）
2. Date：历史节点（Historical）和中间管理者（Middlemanager）
3. Query：查询节点（Broker）

## 数据摄入
1.DataSchema
```
{
  "Datasource":"", #string类型，数据源名字
  "parser"："{}", #JSON对象，包含了如何解析数据相关内容
  "metricsSpec":"{}", #list包含了所有的指标列信息
  "graunlaritySpec":" #JSON对象，指明数据的存储和查询力度"
}
```

