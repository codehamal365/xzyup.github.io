---
uuid: bbaed2e2-c0ab-11ec-92a1-7557b2313227
title: mac安装常用软件
categories: MiddleWare
tags:
  - mac
abbrlink: b8a54843
date: 2022-04-10 16:19:02
---







# MAC常见编程软件安装



mac系统可以使用`homebrew`工具进行安装，如果没有安装该工具，可以执行如下命令。

> /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

## 安装kafka

使用`homebrew`安装kafka

~~~bash
brew install kafka
~~~

安装完成后可以使用

~~~bash
brew info kafka
~~~

可以查看安装路径`/usr/local/Cellar/kafka/3.1.0`和配置路径`/usr/local/etc/kafka/server.properties`

### 启动kafka

kafka依赖zookeeper，而kafa默认以安装依赖zookeeper.

进入目录`/usr/local/Cellar/kafka/3.1.0/bin`执行脚本，启动zookeeper。

~~~bash
zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
~~~

在另外一个窗口，进入同样的目录`/usr/local/Cellar/kafka/3.1.0/bin`执行脚本

~~~bash
kafka-server-start /usr/local/etc/kafka/server.properties
~~~

### 测试消息

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

### 注意事项 

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



## 安装nginx

使用`$ brew install nginx`安装nginx，安装过程中报错

```
tar: Error opening archive: Failed to open '/Users/xiewei/Library/Caches/Homebrew/downloads/a70cee0678540d0eff9f1fe99b798891029e5142a719e17cf30a4f57cb5ddba6--pcre-8.45.big_sur.bottle.tar.gz'
```

需要替换homebrew-bottles

首先要区分mac使用的是哪种终端环境，如果是`bash`,则执行

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
 
source ~/.bash_profile
```

如果是`zsh`，则执行

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
 
source ~/.zshrc
```

重新执行`brew install nginx`就可以了。

其他镜像替换

- 替换 brew.git

  ```
  git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git
  ```

- 替换 homebrew-core.git

  ```
  git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
  ```

- 替换 homebrew-cask.git

  ```
  git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
  ```

  备注：Homebrew 主要由四个部分组成: brew、homebrew-core 、homebrew-cask、homebrew-bottles，它们对应的功能如下：

  | 组成             | 功能                                |
  | ---------------- | ----------------------------------- |
  | Homebrew         | 源代码仓库                          |
  | homebrew-core    | Homebrew 核心源                     |
  | homebrew-cask    | 提供macos应用和大型二进制文件的安装 |
  | homebrew-bottles | 预编译二进制软件包                  |

安装完成后：

使用`brew info nginx`查看nginx相关信息

```
xiewei@xw ssl % brew info nginx

nginx: stable 1.21.2 (bottled), HEAD
HTTP(S) server and reverse proxy, and IMAP/POP3 proxy server
https://nginx.org/
/usr/local/Cellar/nginx/1.21.2 (26 files, 2.2MB) *
  Poured from bottle on 2021-09-07 at 09:40:33
From: https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git/Formula/nginx.rb
License: BSD-2-Clause
==> Dependencies
Required: openssl@1.1 ✔, pcre ✔
==> Options
--HEAD
	Install HEAD version
==> Caveats
Docroot is: /usr/local/var/www

The default port has been set in /usr/local/etc/nginx/nginx.conf to 8080 so that
nginx can run without sudo.

nginx will load all files in /usr/local/etc/nginx/servers/.

To start nginx:
  brew services start nginx
Or, if you don't want/need a background service you can just run:
  /usr/local/opt/nginx/bin/nginx -g daemon off;
==> Analytics
install: 36,549 (30 days), 108,707 (90 days), 503,356 (365 days)
install-on-request: 36,473 (30 days), 108,471 (90 days), 500,591 (365 days)
build-error: 0 (30 days)
```

可以使用`brew list nginx`查看nginx文件的位置

```
xiewei@xw ssl % brew list nginx

/usr/local/Cellar/nginx/1.21.2/.bottle/etc/ (15 files)
/usr/local/Cellar/nginx/1.21.2/bin/nginx
/usr/local/Cellar/nginx/1.21.2/homebrew.mxcl.nginx.plist
/usr/local/Cellar/nginx/1.21.2/homebrew.nginx.service
/usr/local/Cellar/nginx/1.21.2/html -> ../../../var/www
/usr/local/Cellar/nginx/1.21.2/share/man/man8/nginx.8
/usr/local/Cellar/nginx/1.21.2/share/nginx/ (2 files)
```

由`brew info nginx`可以知道nginx的一些配置路径

```
/usr/local/etc/nginx/nginx.conf （配置文件路径）
/usr/local/var/www （服务器默认路径）
/usr/local/Cellar/nginx/1.19.10 （安装路径）
nginx日志log的目录路径
/usr/local/var/log/nginx
```

可以查看nginx安装路径`open /usr/local/Cellar/nginx`

配置nginx环境变量：`vim ~/.zshrc`

```
export NGINX_HOME=/usr/local/Cellar/nginx/1.21.2
export PATH=$NGINX_HOME/bin:$GO_HOME/bin:$JAVA_HOME/bin:$M2_HOME/bin:$FLUTTER_HOME/bin:$PATH
```

然后`source ~/.zshrc`

`nginx` 启动nginx，nginx其他相关命令

```bash
nginx -s stop
nginx -s reload
```

查看nginx相关日志

```bash
cd /usr/local/var/log/nginx
# 查看访问日志
cat access.log
# 查看错误日志
cat error.log 	
```

相关nginx启动等命令

```bash
ps -ef | grep nginx
# 查看配置 brew info nginx
nginx -t
# 启动
$ sudo brew services start nginx

# 暂停
$ nginx -s stop

# 重载配置文件
$ nginx -s reload

# 退出：
$ nginx -s quit 

# 重启：
$ nginx -s reopen	
```



## 安装redis

执行命令`brew install redis`

### 查看安装和配置文件路径

- 安装路径`/usr/local/Cellar/redis/6.2.6`
- redis的配置文件`redis.conf`存放在`/usr/local/etc/redis.conf`

### 启动redis服务

>// 方式一 后台启动
>
>brew services start redis
>
>// 方式二 前台启动
>
>redis-server /usr/local/etc/redis.conf

### 查看redis服务进程

~~~bash
ps axu | grep redis
~~~

### redis-cli连接redis服务

~~~bash
redis-cli -h 127.0.0.1 -p 6379
~~~

可以看到如下

> [17:45:53] xiewei :: xw  ➜  kafka/3.1.0/bin » redis-cli -h 127.0.0.1 -p 6379
>
> 127.0.0.1:6379> ping
> PONG
> 127.0.0.1:6379>

### 关闭redis服务

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

### 注意事项

使用`redis-server`默认是前台启动，如果想以后台方式运行，可以在`redis.conf`中将`daemonize no`改为`daemonize yes`。
`daemonize yes`。
