---
title: kafka基本操作
---
kafka的基本操作，及搭建

+ <!-- more -->

## kafka基本操作
### 启动单节点kafka
bin/kafka-server-start.sh configrver.properties 1>/dev/null 2>&1 &

### 创建topic
binfka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

### 查看所有的topic
binfka-topics.sh --list --zookeeper localhost:2181

### 启动生产者（ctrl+Z结束）
binfka-console-producer.sh --broker-list localhost:9092 --topic test

### 启动消费者（ctrl+Z结束）
binfka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning

### 启动kafka集群
binfka-server-start.sh configrver.properties 1>/dev/null 2>&1 &
binfka-server-start.sh configrver-1.properties 1>/dev/null 2>&1 &
binfka-server-start.sh configrver-2.properties 1>/dev/null 2>&1 &

### 创建有3个副本的topic
binfka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic my-replicated-topic

### 查看每个topic的详细信息
binfka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic

### 使用 Kafka Connect 去导入和导出数据
bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-source.properties config/connect-file-sink.properties
