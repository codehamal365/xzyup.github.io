---
title: mac使用brew管理后台服务
tags:
  - mac
abbrlink: 56df
date: 2022-04-10 18:06:55
---

在编写项目的时候，时常需要开启一些诸如 `nginx`、`mysql`、`redis` 等后台服务，然而每次开机都要重新手动去开启这些服务，而且有些还要保留一些终端窗口去维持服务。这时我们可以用到 `brew services` 来管理这些后台服务。

## 查看services列表

> **brew services list**
>
> Name      Status  User   File
> kafka     none
> openresty none
> redis     started xiewei ~/Library/LaunchAgents/homebrew.mxcl.redis.plist
> zookeeper none

会返回一个表格，可以查看本地下载好的服务。

- Name 服务名称
- Status 服务状态
- User 开启的用户
- Plist 后缀名为`.plist`的xml文件存储的位置

## 常用命令

以mysql为例

~~~bash
brew services run mysql # 启动mysql 服务
brew services start mysql # 启动 mysql 服务，并注册开机自启
brew services stop mysql # 停止 mysql 服务，并取消开机自启
brew services restart mysql # 重启 mysql 服务，并注册开机自启
brew services cleanup # 清除已卸载应用的无用配置
~~~

> 此处注册开机自启后，会自动创建`.plist`文件，取消开机自启后会自动删除该文件

## 与launchtl的关系

mac使用`launchctl`命令加载开机自动运行的服务，那么`launchctl`与`brew services`的关系是啥？

> launchctl list

会返回一串自启的服务，在里面我们可以看到我们用`brew services`设置的自启服务。

> -	0	com.google.keystone.user.agent
> -	0	com.apple.ap.adservicesd
> 12823	0	homebrew.mxcl.redis

由此，我们可以猜测`brew services`是`launchctl`的一个子集。
