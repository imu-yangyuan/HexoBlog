---
title: kafka
date: 2018-11-02 16:41:59
tags: kafka
---
- kafka是一个分布式消息队列。具有高性能、持久化、多副本备份、横向拓展能力。
- kafka对外使用topic的概念，生产者往topic里写消息，消费者从topic中读消息。一个topic实际是由多个partition组成的，遇到瓶颈时，
可以通过增加partition的数量来进行横向扩容。单个parition内是保证消息有序。

- **Kafka ActiveMQ RabbitMQ对比

**1、 TPS**
- Kafka最高，RabbitMq次之，ActiveMq最差

**2、 吞吐量对比**
kafka具有高的吞吐量，内部采用消息的批量处理，zero-copy机制，数据的存储和获取是本地磁盘顺序批量操作，具有O(1)复杂度，消息处理的效率很高。

Zero-Copy技术
```
通常情况下文件从读取到通过Socket发送进行了4次拷贝：
1、调用read时，文件A拷贝到了kernel模式；
2、CPU控制将kernel模式数据copy到user模式下；
3、调用write时，先将user模式下的内容copy到kernel模式下的socket的buffer中；
4、将kernel模式下的socket buffer的数据copy到网卡设备中传送；

Zero-Copy技术省去了将操作系统的read buffer拷贝到程序的buffer，以及从程序buffer拷贝到socket buffer的步骤，
1、将文件拷贝到kernel buffer中；
2、向socket buffer中追加当前要发生的数据在kernel buffer中的位置和偏移量；
3、根据socket buffer中的位置和偏移量直接将kernel buffer的数据copy到网卡设备（protocol engine）中；
```
**3、在架构模型方面**
RabbitMQ实现了AMQP协议（advanced message queue protocol高级消息队列协议）
RabbitMQ有消息确认机制；
Kafka遵从一般的MQ结构，无消息确认机制。
**4、在可用性方面**
RabbitMQ支持miror的queue，主queue失效，miror queue接管。
Kafka的broker支持主备模式
ActiveMq也支持主备模式

- **Kafka的优缺点**
- 优点：
    + 主要用来解决百万级别的数据中生产者和消费者之间数据传输
    + 可以将一条数据提供给多个接受短做不同的处理
    + 两个系统间的通讯
    + 做为日志的收集的一环
    + kafka吞吐量高，单机吞吐量kafka达十万级，而ActiveMQ，RabbitMQ，RocketMQ的吞吐量为万级。
    + 分布式容灾好
    + 数据量不会影响到KafKa的速度
- 缺点：
    + 不支持事务
    + 重复消息。Kafka保证每条消息至少送达一次，虽然几率很小，但一条消息可能被送达多次
    + 消息乱序。Kafka某一个固定的Partition内部的消息是保证有序的，如果一个Topic有多个Partition，partition之间的消息送达不保证有序。
    + 复杂性。Kafka需要Zookeeper的支持，Topic一般需要人工创建，部署和维护比一般MQ成本更高
