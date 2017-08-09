---
title: 解决kafka topic 删除重建后，状态依旧为删除的问题
---
在kafka的测试中，发现当删除一个topic后，想重建它，但是重建后的状态依旧为"marked for deletion"，查询资料后，终于解决

+ <!-- more -->

## 删除kafka topic
1. 在kafka删除
bin/kafka-topics.sh  --delete --zookeeper localhost:2181,localhost:2182,localhost:2183  --topic test
2. 在kafka查看topic是否存在
bin/kafka-topics.sh --list --zookeeper localhost:2181,localhost:2182,localhost:2183
3. 在zk安装目录执行
bin/zkCli.sh
4. 查看topic
ls /brokers/topics
5. 删除zktopic
deleteall /brokers/topics/test
deleteall /config/topics/test
deleteall /admin/delete_topics/test

最后重建测试，一切正常
