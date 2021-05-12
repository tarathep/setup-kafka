# Setup Kafka Introduction
Introduction how and step to setting up kafka stack with docker

## Agenda

1.Overview Kafka Basic
2.What is Docker
3.Setup Kafka
4.Try to use & Demo Apps
5. Q/A

## Overview Kafka

*Overview: Producer, Consumer Broker Cluser, Group Consumer,*

<img src="/images/overview.JPG" width="400px">

*Partition ,Topic, Storage Log*

<img src="/images/figure.JPG" width="400px">

## What is Docker

*Overview Docker Engine*

<img src="/images/docker.JPG" width="80%">


## 3.Setup Kafka

*Arch*
<img src="/images/arch.JPG" width="100%">

**Install Zookeeper at Server1** 

```bash
sudo docker run --rm --name zookeeper -e ALLOW_ANONYMOUS_LOGIN=yes  -p 2181:2181 bitnami/zookeeper:latest
```

**Install Kafka Broker 1001,1002,1003 at Server 1,2,3**


*on server 1*

```sh
sudo docker run --name kafka1 -e KAFKA_CFG_ZOOKEEPER_CONNECT=192.168.88.201:2181 -e ALLOW_PLAINTEXT_LISTENER=yes -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.88.201:9092 -p 9092:9092 bitnami/kafka:latest
```

*on server 2*

```sh
sudo docker run --name kafka2 -e KAFKA_CFG_ZOOKEEPER_CONNECT=192.168.88.201:2181 -e ALLOW_PLAINTEXT_LISTENER=yes -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.88.203:9092 -p 9092:9092 bitnami/kafka:latest
```
*on server 3*

```sh
sudo docker run --name kafka3 -e KAFKA_CFG_ZOOKEEPER_CONNECT=192.168.88.201:2181 -e ALLOW_PLAINTEXT_LISTENER=yes -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.88.202:9092 -p 9092:9092 bitnami/kafka:latest
```

**Setup Kafdrop Kafka Managing GUI Tool**

<img src="/images/kafdrop.JPG" width="400px">


```sh
sudo docker run -it --rm -p 9000:9000 -e KAFKA_BROKERCONNECT=192.168.88.201:9092,192.168.88.203:9092,192.168.88.202:9092 -e JVM_OPTS="-Xms32M -Xmx64M" -e SERVER_SERVLET_CONTEXTPATH="/" obsidiandynamics/kafdrop:latest
```


## Try to use & Demo Apps

- with producer.js
- with consumer.js

## Q/A