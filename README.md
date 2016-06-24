# flume_kafka_hdfs
easy config for data collection

Features
1、通过简单配置就可以实现数据收集。
2、支持断点续传。


1、Data Stream
data -> flume -> kafka -> flume -> hdfs

2、startup
producer：
nohup bin/flume-ng agent -n tier1 -c conf -f conf/test_producer.conf -Dflume.root.logger=INFO,console 2>&1 1>> /data/logs/flume/test_producer.log &
consumer：
nohup bin/flume-ng agent -n tier1 -c conf -f conf/test_consumer.conf -Dflume.root.logger=INFO,console 2>&1 1>> /data/logs/flume/test_consumer.log &

备注
1、将kafka的数据发送到hdfs的方法有很多种
Linkedin Camus - https://github.com/linkedin/camus 
kafka-hadoop-loader - https://github.com/michal-harish/kafka-hadoop-loader 
hadoop-consumer -  https://github.com/apache/kafka/tree/0.8/contrib/hadoop-consumer

2、断点续传的问题
awk写小数据的时候有缓存，需要调用system("") flush数据。网上的答案基本都是错的，最后在这里找到了答案
http://stackoverflow.com/questions/26870259/tail-f-piped-to-awk-piped-to-file-file-does-not-work

