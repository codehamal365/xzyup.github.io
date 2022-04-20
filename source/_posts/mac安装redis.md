---
uuid: bbaed2e4-c0ab-11ec-92a1-7557b2313227
title: mac安装redis
categories: MiddleWare
tags:
  - mac
abbrlink: 983ced43
date: 2022-04-10 17:34:00
---

## 使用homebrew安装

~~~bash
brew install redis
~~~

## 查看安装和配置文件路径

- 安装路径`/usr/local/Cellar/redis/6.2.6`
- redis的配置文件`redis.conf`存放在`/usr/local/etc/redis.conf`

## 启动redis服务

>// 方式一 后台启动
>
>brew services start redis
>
>// 方式二 前台启动
>
>redis-server /usr/local/etc/redis.conf

## 查看redis服务进程

~~~bash
ps axu | grep redis
~~~

## redis-cli连接redis服务

~~~bash
redis-cli -h 127.0.0.1 -p 6379
~~~

可以看到如下

> [17:45:53] xiewei :: xw  ➜  kafka/3.1.0/bin » redis-cli -h 127.0.0.1 -p 6379
>
> 127.0.0.1:6379> ping
> PONG
> 127.0.0.1:6379>

## 关闭redis服务

- 正确停止redis的方式应该是像redis发送`SHUTDOWN`命令

  ~~~bash
  redis-cli shutdown
  ~~~

- 也可以通过`homebrew`命令停止

  ~~~bash
  brew services stop redis
  ~~~

- 强行终止

  ~~~bash
  sudo pkill redis-server
  ~~~

## 注意

使用`redis-server`默认是前台启动，如果想以后台方式运行，可以在`redis.conf`中将`daemonize no`改为`daemonize yes`。
`daemonize yes`。
