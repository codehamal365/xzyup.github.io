---
title: mac 安装nginx
tags:
  - mac
abbrlink: 2c6b
---

# mac安装nginx

使用`$ brew install nginx`安装：
安装过程中报错

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
