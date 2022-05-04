---
uuid: bbaf2110-c0ab-11ec-92a1-7557b2313227
title: shell 脚本三种执行方式
categories: Linux
tags:
  - linux
  - shell
abbrlink: e96baa13
---

# 执行shell脚本三种方法的区别：（sh、exec、source）

#### 1. sh 方式

使用$ sh script.sh执行脚本时，当前shell是父进程，生成一个子shell进程，在子shell中执行脚本。脚本执行完毕，退出子shell，回到当前shell。
 ./script.sh与 sh script.sh等效。

#### 2. source方式

使用$ source script.sh方式，在当前上下文中执行脚本，不会生成新的进程。脚本执行完毕，回到当前shell。
 source方式也叫点命令。
 . script.sh与 source script.sh等效。

#### 3. exec方式

使用exec command方式，会用command进程替换当前shell进程，并且保持PID不变。执行完毕，直接退出，不回到之前的shell环境。

二、测试验证
 vi loop.sh

```bash
#!/bin/sh
while [ 1 = 1 ]; do 
    echo $$
    sleep 1
done
```

显示当前进程

```bash
echo $$
6770
```

sh的方式：执行loop.sh打印执行进程

```css
sh loop.sh 
13736
13736
```

source方式：执行loop.sh打印执行进程

```bash
source loop.sh
6770
6770
```

exec方式：执行loop.sh打印执行进程

```bash
exec ./loop.sh
6770
6770
```

按下ctrl+C

```bash
Connection closing...Socket close.
Connection closed by foreign host.
Disconnected from remote host.
Type `help' to learn how to use Xshell prompt.
[~]$ 
```

#### 结论：

**sh方式：父进程是6770，执行loop.sh时的子进程是13736。执行完毕后回到父进程shell。
source方式：父进程和子进程都是6770（执行时没有新的进程），执行完毕会回到父进程shell。
exec方式：进程PID没有改变都是6770，执行完毕（ctrl+C强制关闭）时直接退出了shell。脚本执行时替换了父进程的shell,执行完毕后直接退出，没有回到之前的shell。**

