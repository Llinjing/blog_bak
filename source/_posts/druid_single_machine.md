---
title: druid.io历史最详细单机搭建流程
tags: druid.io
---

  druid使用也有一年了，踩过的坑无数，现在虽然线上服务已经稳定，但是还是使用的小白，觉得还是有必要把搭建的流程记录下。
  单机版的搭建流程十分简单，适合机器资源不是很充足，或者对druid使用方法测试阶段。其实步骤跟官网上介绍的流程一样的，实时加载使用druid+tranquility，离线数据加载使用druid的batch加载方式。用的很简单，有不足的地方，望指教。

+ <!-- more -->
  
## 准备工作 

``` bash
druid
tranquility
zookeeper
```


## druid集群启动

### 准备机器（一台）

```bash
Java 8 或者更高版本
Linux, Mac OS X, 或者其他 Unix-like OS (Windows不支持，可以使用虚拟机)
8G内存
2核cpu
```

### 下载druid
```bash
curl -O http://static.druid.io/artifacts/releases/druid-0.10.0-bin.tar.gz
tar -xzf druid-0.10.0-bin.tar.gz
cd druid-0.10.0
```

### 启动zk（根据自己的习惯，将zk放在合适的地方）
```
curl http://www.gtlib.gatech.edu/pub/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz -o zookeeper-3.4.6.tar.gz
tar -xzf zookeeper-3.4.6.tar.gz
cd zookeeper-3.4.6
cp conf/zoo_sample.cfg conf/zoo.cfg
./bin/zkServer.sh start
```

### 初始化一些文件夹（druid运行过程中，需要生成的文件存放的地方）
```
在druid文件的根目录下执行：bin/init
```

### druid单机版集群启动命令
```
java `cat conf-quickstart/druid/historical/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/historical:lib/*" io.druid.cli.Main server historical
java `cat conf-quickstart/druid/broker/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/broker:lib/*" io.druid.cli.Main server broker
java `cat conf-quickstart/druid/coordinator/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/coordinator:lib/*" io.druid.cli.Main server coordinator
java `cat conf-quickstart/druid/overlord/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/overlord:lib/*" io.druid.cli.Main server overlord
java `cat conf-quickstart/druid/middleManager/jvm.config | xargs` -cp "conf-quickstart/druid/_common:conf-quickstart/druid/middleManager:lib/*" io.druid.cli.Main server middleManager
```

以上，就是druid单机版的测试版本配置和启动的过程，其中，注意启动用户的权限，如果用户没有创建文件夹的权限，记得提高用户的权限。有了上述的工作，我们就有了一个单机版的druid测试集群，接下来我们要启动tranquility服务，用来接收实时数据流。


## tranquility启动

### 下载tranquility
```
curl -O http://static.druid.io/tranquility/releases/tranquility-distribution-0.8.0.tgz
tar -xzf tranquility-distribution-0.8.0.tgz
cd tranquility-distribution-0.8.0
```

### 启动tranquility服务
/conf-quickstart/tranquility/server.json 是实时流加载配置文件
```
bin/tranquility server -configFile <path_to_druid_distro>/conf-quickstart/tranquility/server.json
```

### 一个测试的实时流数据
```
bin/generate-example-metrics | curl -XPOST -H'Content-Type: application/json' --data-binary @- http://localhost:8200/v1/post/metrics
```
如果收到{"result":{"received":25,"sent":25}}的结果，证明成功了


### 查询
8082端口是druid集群的broker节点的接口,wikiticker-top-pages.json为查询命令文件。这里是用户以二进制文件的方式提交一个post请求
```
curl -L -H'Content-Type: application/json' -XPOST --data-binary @quickstart/wikiticker-top-pages.json http://localhost:8082/druid/v2/?pretty
```

结束语：
  以上，用实时的方式加载数据到druid的单机测试已经完成，这只是一个简单的练手，通过这个测试，我们可以对druid的加载方式有个简单的了解，druid集群，有5个节点，coordinater+overlord属于集群的master，起到控制的作用，middlemanager为task管理，historical为历史节点，也可以进行数据的查询，但是只能查询到已经做了落地的数据，实时数据不能查询到，broker为client的访问接口，通过这个节点，可以访问到实时数据和历史数据。


友情链接：http://druid.io














