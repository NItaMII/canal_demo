# chapter_03: 搭建dev-kafka容器
![canal-docker-demo-搭建](/res/p_00.png)

```sh
docker run --rm -d --name dev-zookeeper --network container:dev zookeeper:3.4

docker run --rm -d --name dev-kafka --network container:dev --env ZOOKEEPER_IP=127.0.0.1 ches/kafka
```

dev-kafka容器启动完成后，还需要给前面canal-server的example监听实例，创建一个名为example的topic。


```sh
# 建topic
docker run --rm --network container:dev -e JMX_PORT=7204 ches/kafka \
    kafka-topics.sh --create --topic example --replication-factor 1 --partitions 1 --zookeeper 127.0.0.1:2181
Created topic 'example'

# producer
docker run --rm --interactive --network container:dev -e JMX_PORT=7205 ches/kafka \
    kafka-console-producer.sh --topic example --broker-list 127.0.0.1:9092

# consumer
docker run --rm --network container:dev -e JMX_PORT=7204 ches/kafka \
    kafka-console-consumer.sh --topic example --from-beginning --bootstrap-server 127.0.0.1:9092
```
