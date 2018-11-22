---
title: kafka 설치 및 구동
---
date: 2018-11-22 14:35:57

## 설치
```bash 
> brew install kafka
..... 
생략
... 
  brew services start kafka
Or, if you don't want/need a background service you can just run:
  zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties & kafka-server-start /usr/local/etc/kafka/server.properties
==> Summary
🍺  /usr/local/Cellar/kafka/2.0.0: 160 files, 46.8MB
==> Caveats
==> zookeeper
To have launchd start zookeeper now and restart at login:
  brew services start zookeeper
Or, if you don't want/need a background service you can just run:
  zkServer start
==> kafka
To have launchd start kafka now and restart at login:
  brew services start kafka
Or, if you don't want/need a background service you can just run:
  zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties & kafka-server-start /usr/local/etc/kafka/server.properties
```
## 주키퍼 구동
 ```bash
jake.ko@jakekoui-MacBook-Pro  ~  zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
[2018-11-22 14:39:11,550] INFO Reading configuration from: /usr/local/etc/kafka/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
[2018-11-22 14:39:11,553] INFO autopurge.snapRetainCount set to 3 (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-11-22 14:39:11,553] INFO autopurge.purgeInterval set to 0 (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-11-22 14:39:11,555] INFO Purge task is not scheduled. (org.apache.zookeeper.server.DatadirCleanupManager)
[2018-11-22 14:39:11,555] WARN Either no config or no quorum defined in config, running  in standalone mode (org.apache.zookeeper.server.quorum.QuorumPeerMain)
[2018-11-22 14:39:11,571] INFO Reading configuration from: /usr/local/etc/kafka/zookeeper.properties (org.apache.zookeeper.server.quorum.QuorumPeerConfig)
생략...
  
```

## 카프카 구동
 ```bash
jake.ko@jakekoui-MacBook-Pro  ~  kafka-server-start /usr/local/etc/kafka/server.properties
[2018-11-22 14:39:25,676] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)
[2018-11-22 14:39:26,191] INFO starting (kafka.server.KafkaServer)
[2018-11-22 14:39:26,192] INFO Connecting to zookeeper on localhost:2181 (kafka.server.KafkaServer)
[2018-11-22 14:39:26,208] INFO [ZooKeeperClient] Initializing a new session to localhost:2181. (kafka.zookeeper.ZooKeeperClient)
[2018-11-22 14:39:26,215] INFO Client environment:zookeeper.version=3.4.13-2d71af4dbe22557fda74f9a9b4309b15a7487f03, built on 06/29/2018 00:39 GMT (org.apache.zookeeper.ZooKeeper)
[2018-11-22 14:39:26,215] INFO Client environment:host.name=172.26.113.148 (org.apache.zookeeper.ZooKeeper)
[2018-11-22 14:39:26,215] INFO Client environment:java.version=1.8.0_161 (org.apache.zookeeper.ZooKeeper)
[2018-11-22 14:39:26,215] INFO Client environment:java.vendor=Oracle Corporation (org.apache.zookeeper.ZooKeeper)
[2018-11-22 14:39:26,215] INFO Client environment:java.home=/Library/Java/JavaVirtualMachines/jdk1.8.0_161.jdk/Contents/Home/jre (org.apache.zookeeper.ZooKeeper)
생략...
```

## 토픽 생성
```bash
jake.ko@jakekoui-MacBook-Pro  ~  kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
Created topic "test".
```

## 토픽 보내기(produce)
```bash
 jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-producer --broker-list localhost:9092 --topic test
>aaa
>bbb
>ccc
>

```

### 토픽 수신(consume)
```bash
 jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-consumer --bootstrap-server localhost:9092 --topic test --from-beginning
aaa
bbb
ccc
```
tags: kafka, mac, install

