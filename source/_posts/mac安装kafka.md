---
title: mac安装kafka
tags:
  - mac
abbrlink: 65f6
date: 2022-04-10 16:19:02
---

# 环境要求

- kafka
- mac

# 步骤

## 下载

mac系统可以使用`homebrew`工具进行安装，如果没有安装该工具。可以执行如下命令。

> /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

使用`homebrew`安装kafka

~~~bash
brew install kafka
~~~

安装完成后可以使用

~~~bash
brew info kafka
~~~

可以查看安装路径`/usr/local/Cellar/kafka/3.1.0`和配置路径`/usr/local/etc/kafka/server.properties`

# 启动kafka

kafka依赖zookeeper，而kafa默认以安装依赖zookeeper.

# 启动zookeeper

进入目录`/usr/local/Cellar/kafka/3.1.0/bin`执行脚本

~~~bash
zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
~~~

## 启动kafka

在另外一个窗口，进入同样的目录`/usr/local/Cellar/kafka/3.1.0/bin`执行脚本

~~~bash
kafka-server-start /usr/local/etc/kafka/server.properties
~~~

# 测试

1. 在启动一个控制窗口，进入同样的bin目录，执行命令

   ~~~bash
   kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
   ~~~

   查看主题是否创建成功

   ~~~bash
   kafka-topics --list --bootstrap-server localhost:9092
   ~~~

2. 测试生产者（producer）

   执行如下命令

   ~~~bash
   kafka-console-producer --broker-list localhost:9092 --topic test
   ~~~

3. 测试消费者

   执行如下命令

   ~~~bash
   kafka-console-consumer --bootstrap-server localhost:9092 --topic test --from-beginning
   ~~~

# 注意 

启动zookeeper的时候，可能出现如下的错误

> /usr/local/etc/kafka/zookeeper.properties
> /usr/local/Cellar/kafka/3.1.0/libexec/bin/kafka-run-class.sh: line 342: /usr/local/Cellar/kafka/3.1.0/bin/@@HOMEBREW_JAVA@@/bin/java: No such file or directory
> /usr/local/Cellar/kafka/3.1.0/libexec/bin/kafka-run-class.sh: line 342: exec: /usr/local/Cellar/kafka/3.1.0/bin/@@HOMEBREW_JAVA@@/bin/java: cannot execute: No such file or directory

可以重新执行如下命令

~~~bash
HOMEBREW_BOTTLE_DOMAIN= brew reinstall kafka    
~~~

> 相关的解释，可以参考如下连接
>
> https://github.com/Homebrew/discussions/discussions/2530

