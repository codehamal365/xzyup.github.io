---
uuid: bbaf6f29-c0ab-11ec-92a1-7557b2313227
title: rabbitmq 入门
categories: MiddleWare
tags:
  - rabbitmq
abbrlink: 114958f5
---

## 1 MQ引言

> 参考 https://blog.csdn.net/unique_perfect/article/details/109380996

### 1.1 什么是MQ

~~~
MQ(Message Quene) :  翻译为消息队列,通过典型的生产者
和消费者模型,生产者不断向消息队列中生产消息，消费者
不断的从队列中获取消息。因为消息的生产和消费都是异
步的，而且只关心消息的发送和接收，没有业务逻辑的侵
入,轻松的实现系统间解耦。别名为 消息中间件通过利用
高效可靠的消息传递机制进行平台无关的数据交流，并
基于数据通信来进行分布式系统的集成。
~~~

### 1.2 MQ有哪些

~~~
当今市面上有很多主流的消息中间件，如老牌的ActiveMQ、
RabbitMQ，炙手可热的Kafka，阿里巴巴自主开发RocketMQ等。
~~~

### 1.3 不同MQ特点

~~~
1.ActiveMQ
		ActiveMQ 是Apache出品，最流行的，能力强劲的开源
		消息总线。它是一个完全支持JMS规范的的消息中间件。
		丰富的API,多种集群架构模式让ActiveMQ在业界成为老
		牌的消息中间件,在中小型企业 颇受欢迎!

2.Kafka
		Kafka是LinkedIn开源的分布式发布-订阅消息系统，目
		前归属于Apache顶级项目。Kafka主要特点是基于Pull
		的模式来处理消息消费，追求高吞吐量，一开始的目的
		就是用于日志收集和传输。0.8版本开始支持复制，不支
		持事务，对消息的重复、丢失、错误没有严格要求，
		适合产生大量数据的互联网服务的数据收集业务。

3.RocketMQ
		RocketMQ是阿里开源的消息中间件，它是纯Java开发，
		具有高吞吐量、高可用性、适合大规模分布式系统应用
		的特点。RocketMQ思路起源于Kafka，但并不是Kafka
		的一个Copy，它对消息的可靠传输及事务性做了优化，
		目前在阿里集团被广泛应用于交   易、充值、流计算、
		消息推送、日志流式处理、binglog分发等场景。

4.RabbitMQ
		RabbitMQ是使用Erlang语言开发的开源消息队列系统，
		基于AMQP协议来实现。AMQP的主要特征是面向消息、
		队列、路由（包括点对点和发布/订阅）、可靠性、安全。
		AMQP协议更多用在企业系统内对数据一致性、稳定性和
		可靠性要求很高的场景，对性能和吞吐量的要求还在
		其次。

RabbitMQ比Kafka可靠，Kafka更适合IO高吞吐的处理，一般应用
在大数据日志处理或对实时性（少量延迟），可靠性（少量丢数据）
要求稍低的场景使用，比如ELK日志收集。		
~~~

## 2 RabbitMQ 的引言

### 2.1 RabbitMQ

~~~
基于AMQP协议，erlang语言开发，是部署最广泛的开源
消息中间件,是最受欢迎的开源消息中间件之一。
~~~

![](https://raw.githubusercontent.com/xzyup/image/master/202203191626795.png)

~~~
AMQP 协议
 	AMQP（advanced message queuing protocol）在2003年
 	时被提出，最早用于解决金融领不同平台之间的消息传递
 	交互问题。顾名思义，AMQP是一种协议，更准确的说是
 	一种binary wire-level protocol（链接协议）。这是其和
 	JMS的本质差别，AMQP不从API层进行限定，而是直接
 	定义网络交换的数据格式。这使得实现了AMQP的
 	provider天然性就是跨平台的。以下是AMQP协议模型:
~~~

![image-20211115164234247](https://raw.githubusercontent.com/xzyup/image/master/202203191627854.png)

### 2.2 RabbitMQ 的安装

~~~
最新版的3.8版本的可以看我这篇文章
https://blog.csdn.net/unique_perfect/article/details/108643804
~~~

#### 2.2.1 下载

![在这里插入图片描述](https://raw.githubusercontent.com/xzyup/image/master/202203191627315.png)

`注意:这里的安装包是centos7安装的包`

#### 2.2.3 安装步骤

~~~
# 1.将rabbitmq安装包上传到linux系统中
	erlang-22.0.7-1.el7.x86_64.rpm  #l7表示是Centosl7,Centosl8表示Centos8
	rabbitmq-server-3.7.18-1.el7.noarch.rpm

# 2.安装Erlang依赖包
	rpm -ivh erlang-22.0.7-1.el7.x86_64.rpm

# 3.安装RabbitMQ安装包(需要联网)
	yum install -y rabbitmq-server-3.7.18-1.el7.noarch.rpm
	注意:默认安装完成后配置文件模板在:/usr/share/doc/rabbitmq-server-3.7.18/rabbitmq.config.example目录中,需要	
	将配置文件复制到/etc/rabbitmq/目录中,并修改名称为rabbitmq.config
# 4.复制配置文件
	cp /usr/share/doc/rabbitmq-server-3.7.18/rabbitmq.config.example /etc/rabbitmq/rabbitmq.config

# 5.查看配置文件位置
	ls /etc/rabbitmq/rabbitmq.config

# 6.修改配置文件(参见下图:)
	vim /etc/rabbitmq/rabbitmq.config 
~~~

![image-20211115164655058](https://raw.githubusercontent.com/xzyup/image/master/202203191627769.png)

~~~
将上图中配置文件中红色部分去掉`%%`,以及最后的`,`逗号 
修改为下图:
~~~

![image-20211115164726573](https://raw.githubusercontent.com/xzyup/image/master/202203191627998.png)

~~~
`或者这两行的注释放开` 不能版本配置文件有差异
loopback_users.guest = true
loopback_users.guest = false
~~~

~~~
# 7.执行如下命令,启动rabbitmq中的插件管理
	rabbitmq-plugins enable rabbitmq_management
	
	出现如下说明:
		Enabling plugins on node rabbit@localhost:
    rabbitmq_management
    The following plugins have been configured:
      rabbitmq_management
      rabbitmq_management_agent
      rabbitmq_web_dispatch
~~~

    The following plugins have been enabled:
      rabbitmq_management
      rabbitmq_management_agent
      rabbitmq_web_dispatch
    
    set 3 plugins.
    Offline change; changes will take effect at broker restart.

# 8.启动RabbitMQ的服务
	systemctl start rabbitmq-server
	systemctl restart rabbitmq-server
	systemctl stop rabbitmq-server


# 9.查看服务状态(见下图:)
	systemctl status rabbitmq-server
  ● rabbitmq-server.service - RabbitMQ broker
     Loaded: loaded (/usr/lib/systemd/system/rabbitmq-server.service; disabled; vendor preset: disabled)
     Active: active (running) since 三 2019-09-25 22:26:35 CST; 7s ago
   Main PID: 2904 (beam.smp)
     Status: "Initialized"
     CGroup: /system.slice/rabbitmq-server.service
             ├─2904 /usr/lib64/erlang/erts-10.4.4/bin/beam.smp -W w -A 64 -MBas ageffcbf -MHas ageffcbf -
             MBlmbcs...
             ├─3220 erl_child_setup 32768
             ├─3243 inet_gethost 4
             └─3244 inet_gethost 4
      .........
~~~

![image-20211115164952765](https://raw.githubusercontent.com/xzyup/image/master/202203191627665.png)

~~~
# 10.关闭防火墙服务
	systemctl disable firewalld  # 需要关闭防火墙，否则访问不了
	Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
	Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
	systemctl stop firewalld   

# 11.访问web管理界面
	http://10.15.0.8:15672/
~~~

![在这里插入图片描述](https://raw.githubusercontent.com/xzyup/image/master/202203191627468.png)

~~~
# 12.登录管理界面
	username:  guest
	password:  guest
~~~

![在这里插入图片描述](https://raw.githubusercontent.com/xzyup/image/master/202203191628472.png)

## 3 RabiitMQ 配置

### 3.1 RabbitMQ 管理命令行

~~~
# 1.服务启动相关
	systemctl start|restart|stop|status rabbitmq-server

# 2.管理命令行  用来在不使用web管理界面情况下命令操作RabbitMQ
	rabbitmqctl  help  可以查看更多命令

# 3.插件管理命令行
	rabbitmq-plugins enable|list|disable 
~~~

### 3.2 web管理界面介绍

#### 3.2.1 overview概览

![image-20211115165516989](https://raw.githubusercontent.com/xzyup/image/master/202203191628049.png)

~~~
connections：无论生产者还是消费者，都需要与RabbitMQ建立连接后才
可以完成消息的生产和消费，在这里可以查看连接情况`

channels：通道，建立连接后，会形成通道，消息的投递获取依赖通道。

Exchanges：交换机，用来实现消息的路由

Queues：队列，即消息队列，消息存放在队列中，等待消费，
消费后被移除队列。
~~~

#### 3.2.2 Admin用户和虚拟主机管理

##### 3.2.2.1 添加用户

![image-20211115165811824](https://raw.githubusercontent.com/xzyup/image/master/202203191628829.png)

~~~
上面的Tags选项，其实是指定用户的角色，可选的有以下几个：

超级管理员(administrator)

可登陆管理控制台，可查看所有的信息，并且可以对用户，
策略(policy)进行操作。

监控者(monitoring)

可登陆管理控制台，同时可以查看rabbitmq节点的相关信息
(进程数，内存使用情况，磁盘使用情况等)

策略制定者(policymaker)

可登陆管理控制台, 同时可以对policy进行管理。但无法查看节点的
相关信息(上图红框标识的部分)。

普通管理者(management)

仅可登陆管理控制台，无法看到节点信息，也无法对策略进行管理。

其他

无法登陆管理控制台，通常就是普通的生产者和消费者。
~~~

##### 3.2.2.2 创建虚拟主机

~~~
虚拟主机
为了让各个用户可以互不干扰的工作，RabbitMQ添加了
虚拟主机（Virtual Hosts）的概念。其实就是一个独立的
访问路径，不同用户使用不同路径，各自有自己的
队列、交换机，互相不会影响。相当于关系型中的数据库
~~~

![image-20211115165945088](https://raw.githubusercontent.com/xzyup/image/master/202203191628947.png)

##### 3.2.2.3 绑定虚拟主机和用户

~~~
创建好虚拟主机，我们还要给用户添加访问权限：

点击添加好的虚拟主机：
~~~

![image-20211115170056567](https://raw.githubusercontent.com/xzyup/image/master/202203191628593.png)

`进入虚拟机设置界面`

![image-20211115172528979](https://raw.githubusercontent.com/xzyup/image/master/202203191629415.png)

## 4 RabbitMQ 的第一个程序

### 4.1 AMQP协议的回顾

![image-20211115173046680](https://raw.githubusercontent.com/xzyup/image/master/202203191629621.png)

### 4.2 RabbitMQ支持的消息模型

![image-20211115173136189](https://raw.githubusercontent.com/xzyup/image/master/202203191629497.png)

![image-20211115173209816](https://raw.githubusercontent.com/xzyup/image/master/202203191629518.png)

### 4.3 引入依赖

~~~xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.7.2</version>
</dependency>
~~~

### 4.4 第一种模型(直连)

![在这里插入图片描述](https://raw.githubusercontent.com/xzyup/image/master/202203191629336.png)

~~~
在上图的模型中，有以下概念：

P：生产者，也就是要发送消息的程序
C：消费者：消息的接受者，会一直等待消息到来。
queue：消息队列，图中红色部分。类似一个邮箱，
可以缓存消息；生产者向其中投递消息，消费者从其中取出消息。
~~~

#### 4.4.1 开发生产者

~~~java
package demo.direct;

import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import common.Constant;
import utils.RabbitMQUtil;

/**
 * 第一种模型(直连)
 *
 * @author xie.wei
 * @date created at 2021-11-15 17:39
 */
public class Producer {

    public static void main(String[] args) {
        // 获取连接
        Connection connection = RabbitMQUtil.getConnection();
        Channel channel = null;
        try {
            // 创建通道、生产者和mq服务所有通信都在channel中完成
            channel = connection.createChannel();

            /**
             *  声明 direct 直连队列
             *  1. queue 队列名称
             *  2. durable 队列是否持久化，mq重启队列还在，不会保证消息的持久化
             *  3. exclusive 是否独占连接，队列只允许在连接中访问，如果连接关闭则队列无法
             *  访问,如果将此参数设置为true可以用于临时队列的创建
             *  4. autoDelete 自动删除,及队列不在使用时自动删除，一般消费者消费完成ACK确认后，
             *  生产消费都断开了连接后，队列自动删除，
             *  5. 参数，可以设置队列的扩展属性，比如：可设置存活时间等
             */
            channel.queueDeclare(Constant.DIRECT_QUEUE, false, false, false,
                    null);

            /**
             * 发布消息
             * 1. exchange 交换机
             * 2. routingKey 路由key，交换机根据key将消息转发到指定队列，如果使用默认交换机
             * 则key就是队列名称
             * 3. props 消息属性，可以设置消息为可持久化，MessageProperties.PERSISTENT_TEXT_PLAIN
             * 4. body 消息内容
             */
            channel.basicPublish("", Constant.DIRECT_QUEUE, null,
                    "hello world".getBytes());

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 关闭通道和连接
            RabbitMQUtil.close(channel, connection);
        }
    }
}
~~~

#### 4.4.2 开发消费者

```java
package demo.direct;

import com.rabbitmq.client.*;
import common.Constant;
import utils.RabbitMQUtil;

import java.io.IOException;

/**
 * 第一种模型(直连)
 *
 * @author xie.wei
 * @date created at 2021-11-15 22:43
 */
@SuppressWarnings("all")
public class Consumer {
    public static void main(String[] args) {
        Connection connection = RabbitMQUtil.getConnection();
        Channel channel = null;
        try {
            channel = connection.createChannel();
            channel.queueDeclare(Constant.DIRECT_QUEUE, false, false, false, null);

            /*
             * 参数明细：
             * 1、queue 队列名称
             * 2、autoAck 自动回复，当消费者接收到消息后要告诉mq消息已接收，
             * 如果将此参数设置为tru表示会自动回复mq，如果设置为false要通过编程实现回复
             * 3、callback，消费方法，当消费者接收到消息要执行的方法
             */
            channel.basicConsume(Constant.DIRECT_QUEUE, true, new DefaultConsumer(channel) {

                /**
                 * 当接收到消息后此方法将被调用
                 * @param consumerTag  消费者标签，用来标识消费者的，
                 *        在监听队列时设置channel.basicConsume
                 * @param envelope 信封，通过envelope
                 * @param properties 消息属性
                 * @param body 消息内容
                 * @throws IOException
                 */
                @Override
                public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                           byte[] body) throws IOException {
                    // key,本例即队列名称
                    String routingKey = envelope.getRoutingKey();
                    // 交换机
                    String exchange = envelope.getExchange();
                    // 消息id，mq在channel中用来标识消息的id，可用于确认消息已接收
                    long deliveryTag = envelope.getDeliveryTag();
                    String msg = new String(body, "utf-8");
                    System.out.printf("routingKey:%s,exchange:%s,deliveryTag:%s,body:%s", routingKey,
                            exchange, deliveryTag, msg);
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // RabbitMQUtil.close(channel, connection);
        }
    }
}
```

### 4.5 第二种模型(working queque)

![img](https://raw.githubusercontent.com/xzyup/image/master/202203191630397.png)

这种模式叫工作队列或者**竞争消费者**模式。

Working queues与入门程序相比，多了一个消费端，两个消费端共同消费同一个队列中的消息，但是**一个消息只能被一个消费者获取**。

这个消息模型在Web应用程序中特别有用，可以处理短的HTTP请求窗口中无法处理复杂的任务。

接下来我们来模拟这个流程：

P：生产者：任务的发布者

C1：消费者1：领取任务并且完成任务，假设完成速度较慢（模拟耗时）

C2：消费者2：领取任务并且完成任务，假设完成速度较快

#### 4.5.1 生成者

```java
package demo.wokerqueue;

import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import common.Constant;
import utils.RabbitMQUtil;

/**
 * working queue 生产者
 *
 * @author xie.wei
 * @date created at 2022-01-06 15:16
 */
public class Producer {

    public static void main(String[] args) {
        // 获取连接
        Connection connection = RabbitMQUtil.getConnection();
        Channel channel = null;
        try {
            // 创建通道、生产者和mq服务所有通信都在channel中完成
            channel = connection.createChannel();

            /*
             *  声明 direct 直连队列
             *  1. queue 队列名称
             *  2. durable 队列是否持久化，mq重启队列还在，不会保证消息的持久化
             *  3. exclusive 是否独占连接，队列只允许在连接中访问，如果连接关闭则队列无法
             *  访问,如果将此参数设置为true可以用于临时队列的创建
             *  4. autoDelete 自动删除,及队列不在使用时自动删除，一般消费者消费完成ACK确认后，
             *  生产消费都断开了连接后，队列自动删除，
             *  5. 参数，可以设置队列的扩展属性，比如：可设置存活时间等
             */
            channel.queueDeclare(Constant.WORKING_QUEUE, false, false, false,
                    null);

            /*
             * 发布消息
             * 1. exchange 交换机
             * 2. routingKey 路由key，交换机根据key将消息转发到指定队列，如果使用默认交换机
             * 则key就是队列名称
             * 3. props 消息属性，可以设置消息为可持久化，MessageProperties.PERSISTENT_TEXT_PLAIN
             * 4. body 消息内容
             */
            for (int i = 0; i < 50; i++) {
                String message = "working queue message: " + i;
                channel.basicPublish("", Constant.WORKING_QUEUE, null,
                        message.getBytes());
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 关闭通道和连接
            RabbitMQUtil.close(channel, connection);
        }
    }
}
```

#### 4.5.2 消费者1

```java
package demo.wokerqueue;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import java.util.concurrent.TimeUnit;
import utils.RabbitMQUtil;

/**
 * working queue consumer one
 *
 * @author xie.wei
 * @date created at 2022-01-06 15:22
 */
public class Consumer1 {
    public static void main(String[] args) {
        Connection connection = RabbitMQUtil.getConnection();
        Channel channel = null;
        try {
            channel = connection.createChannel();
            channel.queueDeclare(Constant.WORKING_QUEUE, false, false, false, null);

            /*
             * 参数明细：
             * 1、queue 队列名称
             * 2、autoAck 自动回复，当消费者接收到消息后要告诉mq消息已接收，
             * 如果将此参数设置为tru表示会自动回复mq，如果设置为false要通过编程实现回复
             * 3、callback，消费方法，当消费者接收到消息要执行的方法
             */
            channel.basicConsume(Constant.WORKING_QUEUE, true, new DefaultConsumer(channel) {

                /**
                 * 当接收到消息后此方法将被调用
                 * @param consumerTag  消费者标签，用来标识消费者的，
                 *        在监听队列时设置channel.basicConsume
                 * @param envelope 信封，通过envelope
                 * @param properties 消息属性
                 * @param body 消息内容
                 * @throws IOException
                 */
                @Override
                public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                           byte[] body) throws IOException {
                    // body 即消息体
                    String msg = new String(body, "utf-8");
                    System.out.println(" [消费者1] received : " + msg + "!");
                    //模拟任务耗时1s
                    try {
                        TimeUnit.SECONDS.sleep(1);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // RabbitMQUtil.close(channel, connection);
        }
    }
}
```

#### 4.5.3 消费者2

```java
package demo.wokerqueue;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * working queue consumer two
 *
 * @author xie.wei
 * @date created at 2022-01-06 15:22
 */
public class Consumer2 {
    public static void main(String[] args) {
        Connection connection = RabbitMQUtil.getConnection();
        Channel channel = null;
        try {
            channel = connection.createChannel();
            channel.queueDeclare(Constant.WORKING_QUEUE, false, false, false, null);

            /*
             * 参数明细：
             * 1、queue 队列名称
             * 2、autoAck 自动回复，当消费者接收到消息后要告诉mq消息已接收，
             * 如果将此参数设置为tru表示会自动回复mq，如果设置为false要通过编程实现回复
             * 3、callback，消费方法，当消费者接收到消息要执行的方法
             */
            channel.basicConsume(Constant.WORKING_QUEUE, true, new DefaultConsumer(channel) {

                /**
                 * 当接收到消息后此方法将被调用
                 * @param consumerTag  消费者标签，用来标识消费者的，
                 *        在监听队列时设置channel.basicConsume
                 * @param envelope 信封，通过envelope
                 * @param properties 消息属性
                 * @param body 消息内容
                 * @throws IOException
                 */
                @Override
                public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                           byte[] body) throws IOException {
                    // body 即消息体
                    String msg = new String(body, "utf-8");
                    System.out.println(" [消费者1] received : " + msg + "!");
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // RabbitMQUtil.close(channel, connection);
        }
    }
}
```

与消费者1基本类似，只是消费者2没有设置消费耗时时间。

接下来，两个消费者一同启动，然后生产者发送50条消息：

![image-20220106153336710](https://raw.githubusercontent.com/xzyup/image/master/202203191630026.png)

![image-20220106153405659](https://raw.githubusercontent.com/xzyup/image/master/202203191630579.png)

**可以发现，两个消费者各自消费了不同25条消息，这就实现了任务的分发。** 

#### 4.5.4 能者多劳

刚才的实现有问题吗？

- 消费者1比消费者2的效率要低，一次任务的耗时较长
- 然而两人最终消费的消息数量是一样的
- 消费者2大量时间处于空闲状态，消费者1一直忙碌

现在的状态属于是把任务平均分配，正确的做法应该是消费越快的人，消费的越多。

怎么实现呢？

通过 BasicQos 方法设置prefetchCount = 1。这样RabbitMQ就会使得每个Consumer在同一个时间点最多处理1个Message。换句话说，在接收到该Consumer的ack前，他它不会将新的Message分发给它。相反，它会将其分派给不是仍然忙碌的下一个Consumer。

**值得注意的是：prefetchCount在手动ack的情况下才生效，自动ack不生效。**

设置prefetchCount和手动ack代码如下：

```java
public static void main(String[] args) throws Exception {
  Connection connection = RabbitMQUtil.getConnection();
  final Channel channel = connection.createChannel();

  channel.queueDeclare(Constant.WORKING_QUEUE, false, false, false, null);
  // 设置每个消费者同时只能处理一条消息，手动ack下生效
  channel.basicQos(1);

  channel.basicConsume(Constant.WORKING_QUEUE, false, new DefaultConsumer(channel) {


    @Override
    public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                               byte[] body) throws IOException {
      // body 即消息体
      String msg = new String(body, "utf-8");
      System.out.println(" [消费者2] received : " + msg + "!");
      channel.basicAck(envelope.getDeliveryTag(), false);
    }
  });
}
```

再次测试：

![image-20220106155103949](https://raw.githubusercontent.com/xzyup/image/master/202203191630941.png)

![image-20220106155123303](https://raw.githubusercontent.com/xzyup/image/master/202203191630053.png)



### 4.6 第三种模型(订阅模型)

**订阅模型分类**
说明下：

1、一个生产者多个消费者
2、每个消费者都有一个自己的队列
3、生产者没有将消息直接发送给队列，而是发送给exchange(交换机、转发器)
4、每个队列都需要绑定到交换机上
5、生产者发送的消息，经过交换机到达队列，实现一个消息被多个消费者消费
例子：注册->发邮件、发短信

**X（Exchanges）**：交换机一方面：接收生产者发送的消息。另一方面：知道如何处理消息，例如递交给某个特别队列、递交给所有队列、或是将消息丢弃。到底如何操作，取决于Exchange的类型。

Exchange类型有以下几种：

**Fanout**：广播，将消息交给所有绑定到交换机的队列

**Direct**：定向，把消息交给符合指定routing key 的队列

**Topic**：通配符，把消息交给符合routing pattern（路由模式） 的队列

**Header**：header模式与routing不同的地方在于，header模式取消routingkey，使用header中的 key/value（键值对）匹配队列。

Header模式不展开了，感兴趣可以参考这篇文章https://blog.csdn.net/zhu_tianwei/article/details/40923131

**Exchange（交换机）只负责转发消息，不具备存储消息的能力，因此如果没有任何队列与Exchange绑定，或者没有符合路由规则的队列，那么消息会丢失！**

#### 4.6.1 Publish/subcribe(交换机类型：fanout，也称广播)

![img](https://raw.githubusercontent.com/xzyup/image/master/202203191630971.png)



##### 生产者

和前面两种模式不同：

- 1） 声明Exchange，不再声明Queue
- 2） 发送消息到Exchange，不再发送到Queue

```java
package demo.pubsub;

import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * 订阅模式：pub/sub 生产者
 *
 * @author xie.wei
 * @date created at 2022-01-06 16:11
 */
public class Producer {

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();

        channel.exchangeDeclare(Constant.FANOUT_EXCHANGE, "fanout");
        String message = "registration success";
        channel.basicPublish(Constant.FANOUT_EXCHANGE, "", null, message.getBytes());

        RabbitMQUtil.close(channel, connection);
    }
}
```

##### 消费者1 （注册成功发给短信服务）

```java
package demo.pubsub;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * pub/sub consumer1
 * 发送短信服务
 *
 * @author xie.wei
 * @date created at 2022-01-06 16:48
 */
public class Consumer1 {

    static String QUEUE = "fanout_exchange_queue_sms";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明队列
        channel.queueDeclare(QUEUE, false, false, false, null);
        // 定义队列消费者
        channel.queueBind(QUEUE, Constant.FANOUT_EXCHANGE, "");

        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [短信服务] received : " + msg + "!");
            }
        };
        channel.basicConsume(QUEUE, true, consumer);
    }
}
```

##### 消费者2（注册成功发给邮件服务）

```java
package demo.pubsub;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * pub/sub consumer2
 * 发送邮件服务
 *
 * @author xie.wei
 * @date created at 2022-01-06 16:48
 */
public class Consumer2 {

    static String QUEUE = "fanout_exchange_queue_email";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明队列
        channel.queueDeclare(QUEUE, false, false, false, null);
        // 定义队列消费者
        channel.queueBind(QUEUE, Constant.FANOUT_EXCHANGE, "");

        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [邮件服务] received : " + msg + "!");
            }
        };
        channel.basicConsume(QUEUE, true, consumer);
    }
}
```

我们运行两个消费者，然后生成者发送1条消息：如果先运行消费者，可能出现exchange不存在的报错，可现在admin页面创建或者先运行生产者。

![image-20220106171011803](https://raw.githubusercontent.com/xzyup/image/master/202203191631939.png)

![image-20220106171035697](https://raw.githubusercontent.com/xzyup/image/master/202203191631763.png)

##### 思考

1、publish/subscribe与work queues有什么区别。

区别：

1）work queues不用定义交换机，而publish/subscribe需要定义交换机。

2）publish/subscribe的生产方是面向交换机发送消息，work queues的生产方是面向队列发送消息(底层使用默认交换机)。

3）publish/subscribe需要设置队列和交换机的绑定，work queues不需要设置，实际上work queues会将队列绑定到默认的交换机 。

相同点：

所以两者实现的发布/订阅的效果是一样的，多个消费端监听同一个队列不会重复消费消息。

2、实际工作用 publish/subscribe还是work queues。

建议使用 publish/subscribe，发布订阅模式比工作队列模式更强大（也可以做到同一队列竞争），并且发布订阅模式可以指定自己专用的交换机。

#### 4.6.2 Routing 路由模型（交换机类型：direct）

![img](https://raw.githubusercontent.com/xzyup/image/master/202203191631447.png)

P：生产者，向Exchange发送消息，发送消息时，会指定一个routing key。

X：Exchange（交换机），接收生产者的消息，然后把消息递交给 与routing key完全匹配的队列

C1：消费者，其所在队列指定了需要routing key 为 error 的消息

C2：消费者，其所在队列指定了需要routing key 为 info、error、warning 的消息

接下来看代码：

##### 生产者

```java
package demo.routing;

import com.rabbitmq.client.BuiltinExchangeType;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * routing路由模式 交换机类型为direct
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:15
 */
public class Producer {
    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明exchange,指明类型为direct
        channel.exchangeDeclare(Constant.DIRECT_EXCHANGE, BuiltinExchangeType.DIRECT);
        // 消息内容
        String message = "注册成功！请短息回复[T]退订";
        // 发送消息，并指定routing key 为sms，只有短信服务才能接受该消息
        channel.basicPublish(Constant.DIRECT_EXCHANGE, "sms", null, message.getBytes());
        System.out.println(" [x] Sent '" + message + "'");

        RabbitMQUtil.close(channel, connection);
    }
}
```

##### 消费者1

```java
package demo.routing;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * routing key路由模式 exchange type: direct
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:23
 */
public class Consumer1 {

    static String QUEUE = "direct_exchange_queue_sms";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();

        // 声明队列
        channel.queueDeclare(QUEUE, false, false, false, null);
        // 绑定交换机,同时指定需要指定的routing key,可以同时指定多个
        channel.queueBind(QUEUE, Constant.DIRECT_EXCHANGE, "sms");

        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [短信服务] received : " + msg + "!");
            }
        };
        // 监听队列，自动ACK
        channel.basicConsume(QUEUE, true, consumer);
    }
}
```

##### 消费者2

```java
package demo.routing;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * routing key路由模式 exchange type: direct
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:23
 */
public class Consumer2 {

    static String QUEUE = "direct_exchange_queue_email";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();

        // 声明队列
        channel.queueDeclare(QUEUE, false, false, false, null);
        // 绑定交换机,同时指定需要指定的routing key,可以同时指定多个
        channel.queueBind(QUEUE, Constant.DIRECT_EXCHANGE, "email");

        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [邮件服务] received : " + msg + "!");
            }
        };
        // 监听队列，自动ACK
        channel.basicConsume(QUEUE, true, consumer);
    }
}
```

我们发送sms的RoutingKey，发现结果：只有指定短信的消费者1收到消息了

![image-20220106173229176](https://raw.githubusercontent.com/xzyup/image/master/202203191631537.png)

#### 4.6.3 Topics 通配符模式（交换机类型：topics）

![img](https://raw.githubusercontent.com/xzyup/image/master/202203191631892.png)

 每个消费者监听自己的队列，并且设置带统配符的routingkey,生产者将消息发给broker，由交换机根据routingkey来转发消息到指定的队列。

Routingkey一般都是有一个或者多个单词组成，多个单词之间以“.”分割，例如：inform.sms

通配符规则：

#：匹配一个或多个词

*：匹配不多不少恰好1个词

举例：

audit.#：能够匹配audit.irs.corporate 或者 audit.irs

audit.*：只能匹配audit.irs

从示意图可知，我们将发送所有描述动物的消息。消息将使用由三个字（两个点）组成的Routing key发送。路由关键字中的第一个单词将描述速度，第二个颜色和第三个种类：“<speed>.<color>.<species>”。

我们创建了三个绑定：Q1绑定了“*.orange.*”，Q2绑定了“.*.*.rabbit”和“lazy.＃”。

Q1匹配所有的橙色动物。

Q2匹配关于兔子以及懒惰动物的消息。

 下面做个小练习，假如生产者发送如下消息，会进入哪个队列：

quick.orange.rabbit       Q1 Q2   routingKey="quick.orange.rabbit"的消息会同时路由到Q1与Q2

lazy.orange.elephant    Q1 Q2

quick.orange.fox           Q1

lazy.pink.rabbit              Q2  (值得注意的是，虽然这个routingKey与Q2的两个bindingKey都匹配，但是只会投递Q2一次)

quick.brown.fox            不匹配任意队列，被丢弃

quick.orange.male.rabbit   不匹配任意队列，被丢弃

orange         不匹配任意队列，被丢弃

下面我们以指定Routing key="quick.orange.rabbit"为例，验证上面的答案

##### 生产者

```java
package demo.topics;

import com.rabbitmq.client.BuiltinExchangeType;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * topics模式
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:41
 */
public class Producer {
    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明exchange，指定类型为topic
        channel.exchangeDeclare(Constant.TOPIC_EXCHANGE, BuiltinExchangeType.TOPIC);
        // 消息内容
        String message = "这是一只行动迅速的橙色的兔子";
        // 发送消息，并且指定routing key为：quick.orange.rabbit
        channel.basicPublish(Constant.TOPIC_EXCHANGE, "quick.orange.rabbit", null, message.getBytes());
        System.out.println(" [动物描述：] Sent '" + message + "'");
        RabbitMQUtil.close(channel, connection);
    }
}
```

##### 消费者1

```java
package demo.topics;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * topics模式
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:46
 */
public class Consumer1 {
    static String QUEUE_NAME = "topic_exchange_queue_Q1";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明队列
        channel.queueDeclare(QUEUE_NAME, false, false, false, null);

        // 绑定队列到交换机，同时指定需要订阅的routing key。订阅所有的橙色动物
        channel.queueBind(QUEUE_NAME, Constant.TOPIC_EXCHANGE, "*.orange.*");


        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [消费者1] received : " + msg + "!");
            }
        };
        // 监听队列，自动ACK
        channel.basicConsume(QUEUE_NAME, true, consumer);

    }
}
```

##### 消费者2

```java
package demo.topics;

import com.rabbitmq.client.AMQP;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import common.Constant;
import java.io.IOException;
import utils.RabbitMQUtil;

/**
 * topics模式
 *
 * @author xie.wei
 * @date created at 2022-01-06 17:46
 */
public class Consumer2 {
    static String QUEUE_NAME = "topic_exchange_queue_Q2";

    public static void main(String[] args) throws IOException {
        final Connection connection = RabbitMQUtil.getConnection();
        final Channel channel = connection.createChannel();
        // 声明队列
        channel.queueDeclare(QUEUE_NAME, false, false, false, null);

        // 绑定队列到交换机，同时指定需要订阅的routing key。订阅关于兔子以及懒惰动物的消息
        channel.queueBind(QUEUE_NAME, Constant.TOPIC_EXCHANGE, "*.*.rabbit");
        channel.queueBind(QUEUE_NAME, Constant.TOPIC_EXCHANGE, "lazy.＃");

        // 定义队列的消费者
        DefaultConsumer consumer = new DefaultConsumer(channel) {
            // 获取消息，并且处理，这个方法类似事件监听，如果有消息的时候，会被自动调用
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties,
                                       byte[] body) throws IOException {
                // body 即消息体
                String msg = new String(body);
                System.out.println(" [消费者2] received : " + msg + "!");
            }
        };
        // 监听队列，自动ACK
        channel.basicConsume(QUEUE_NAME, true, consumer);

    }
}
```

结果C1、C2是都接收到消息了：

![image-20220106175843295](https://raw.githubusercontent.com/xzyup/image/master/202203191631828.png)

![image-20220106175904638](https://raw.githubusercontent.com/xzyup/image/master/202203191632611.png)

#### 4.6.3 RPC

![img](https://raw.githubusercontent.com/xzyup/image/master/202203191632340.png)

基本概念：

Callback queue 回调队列，客户端向服务器发送请求，服务器端处理请求后，将其处理结果保存在一个存储体中。而客户端为了获得处理结果，那么客户在向服务器发送请求时，同时发送一个回调队列地址reply_to。

Correlation id 关联标识，客户端可能会发送多个请求给服务器，当服务器处理完后，客户端无法辨别在回调队列中的响应具体和那个请求时对应的。为了处理这种情况，客户端在发送每个请求时，同时会附带一个独有correlation_id属性，这样客户端在回调队列中根据correlation_id字段的值就可以分辨此响应属于哪个请求。

流程说明：

当客户端启动的时候，它创建一个匿名独享的回调队列。
在 RPC 请求中，客户端发送带有两个属性的消息：一个是设置回调队列的 reply_to 属性，另一个是设置唯一值的 correlation_id 属性。
将请求发送到一个 rpc_queue 队列中。
服务器等待请求发送到这个队列中来。当请求出现的时候，它执行他的工作并且将带有执行结果的消息发送给 reply_to 字段指定的队列。
客户端等待回调队列里的数据。当有消息出现的时候，它会检查 correlation_id 属性。如果此属性的值与请求匹配，将它返回给应用

### 5 面试题

面试题：

避免消息堆积？

1） 采用workqueue，多个消费者监听同一队列。

2）接收到消息以后，而是通过线程池，异步消费。

如何避免消息丢失？

1） 消费者的ACK机制。可以防止消费者丢失消息。

但是，如果在消费者消费之前，MQ就宕机了，消息就没了？

2）可以将消息进行持久化。要将消息持久化，前提是：队列、Exchange都持久化

交换机持久化
![img](https://raw.githubusercontent.com/xzyup/image/master/202203191632563.png)
队列持久化
![img](https://raw.githubusercontent.com/xzyup/image/master/202203191632941.png)
消息持久化
![img](https://raw.githubusercontent.com/xzyup/image/master/202203191632365.png)

---
91632365.png)

---
