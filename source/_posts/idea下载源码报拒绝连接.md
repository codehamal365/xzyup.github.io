---
title: idea下载源码报拒绝连接
tags: idea
abbrlink: 6fd1
date: 2022-04-13 16:24:50
---

大家用idea开发的时候，下载源码可能出现`Caused by: java.rmi.ConnectException: Connection refused to host: 127.0.0.1`的错误。可在idea中做如下配置解决问题。

`Preferences`->`Build`->`Build Tools`->`Maven`->`Importing`->`JDK for importer`做修改了在尝试。

![image-20220413163757010](https://raw.githubusercontent.com/xzyup/image/master/202204131637914.png)

