---
uuid: bbaef9f5-c0ab-11ec-92a1-7557b2313227
title: Dockerfile常用命令
tags:
  - Dockerfile
categories: Docker
abbrlink: 1cedfdb9
date: 2022-03-19 15:07:59
---

## dockerfile 的命令
[菜鸟教程链接](https://www.runoob.com/docker/docker-dockerfile.html)

- FROM- 镜像从那里来
- MAINTAINER- 镜像维护者信息
- RUN- 构建镜像执行的命令，每一次RUN都会构建一层
- CMD- 容器启动的命令，如果有多个则以最后一个为准，也可以为ENTRYPOINT提供参数
- VOLUME- 定义数据卷，如果没有定义则使用默认
- USER- 指定后续执行的用户组和用户
- WORKDIR- 切换当前执行的工作目录
- HEALTHCHECH- 健康检测指令
- ARG- 变量属性值，但不在容器内部起作用
- EXPOSE- 暴露端口
- ENV- 变量属性值，容器内部也会起作用
- ADD- 添加文件，如果是压缩文件也解压
- COPY- 添加文件，以复制的形式
- ENTRYPOINT- 容器进入时执行的命令

### dockerfile实践
> https://www.cnblogs.com/aaronlinv/p/15213211.html

### docker compose实践
> https://www.cnblogs.com/aaronlinv/p/15270704.html


---15270704.html


---