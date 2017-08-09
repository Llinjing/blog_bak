---
title: kafka基本操作
---
kafka的基本操作，及搭建

+ <!-- more -->

## kafka基本操作
### 启动单节点zk
nohup bin/zookeeper-server-start.sh config/zookeeper.properties > logs/zk.log 2>&1 &

### 启动单节点kafka
nohup bin/kafka-server-start.sh config/server.properties > logs/server.log 2>&1 &

### 启动kafka集群
nohup bin/kafka-server-start.sh config/server-1.properties > logs/server-1.log 2>&1 &
nohup bin/kafka-server-start.sh config/server-2.properties > logs/server-2.log 2>&1 &

### 检测kafka服务
ps ax | grep -i 'kafka\.Kafka' | grep java | grep -v grep | awk '{print $1}'

### 创建kafka topic
bin/kafka-topics.sh --create --zookeeper localhost:2185 --replication-factor 1  --partitions 1 --topic test

### 查看kafka所有topic
bin/kafka-topics.sh --list --zookeeper localhost:2185

### 启动生产者（ctrl+Z结束）
bin/kafka-console-producer.sh --broker-list  localhost:9092,localhost:9093,localhost:9094 --topic test

### 启动消费者（ctrl+Z结束）
bin/kafka-console-consumer.sh --zookeeper  localhost:2185  --from-beginning --topic test

### 创建有3个副本的topic
bin/kafka-topics.sh --create --zookeeper localhost:2185 --replication-factor 1 --partitions 1 --topic my-replicated-topic

### 查看每个topic的详细信息
binfka-topics.sh --describe --zookeeper localhost:2185 --topic my-replicated-topic

### 使用 Kafka Connect 去导入和导出数据
bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-source.properties config/connect-file-sink.properties

### 删除kafka topic
1. 在kafka删除
bin/kafka-topics.sh  --delete --zookeeper localhost:2185  --topic test
2. 在kafka查看topic是否存在
bin/kafka-topics.sh --list --zookeeper localhost:2185
3. 在zk安装目录执行
bin/zkCli.sh
4. 查看topic
ls /brokers/topics
5. 删除zktopic
deleteall /brokers/topics/test
deleteall /config/topics/test
deleteall /admin/delete_topics/test




