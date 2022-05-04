---
uuid: bbaf210f-c0ab-11ec-92a1-7557b2313227
title: linux scp
categories: Linux
tags:
  - linux
abbrlink: 326eed25
---

在终端里面输入命令【sudo su】，然后输入当前用户的用户密码，就可以获取临时的root权限

在终端里面输入命令【su】，然后输入当前用户的用户密码，就可以获取临时的root权限

可以在想要在终端输入的命令前面添加，【sudo】来达到使用root权限进行执行该命令

```bash
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music 
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music/001.mp3 
scp /home/space/music/1.mp3 www.runoob.com:/home/root/others/music 
scp /home/space/music/1.mp3 www.runoob.com:/home/root/others/music/001.mp3 
```

