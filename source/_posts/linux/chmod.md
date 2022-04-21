---
uuid: bbaf210d-c0ab-11ec-92a1-7557b2313227
title: chmod
categories: Linux
tags:
  - linux
abbrlink: e97af36
---

chmod a+r *：用户自己使用此命令，柯给所有用户添加可读的权限

超级用户给其他用户设置权限：sudo chmod a+rx /home/user  使所有人可以访问，读取文件，bu no Write

指令名称 : chmod
使用权限 : 所有使用者
使用方式 : chmod [-cfvR] [--help] [--version] mode file...
说明 : Linux/Unix 的档案调用权限分为三级 : 档案拥有者、群组、其他。利用 chmod 可以藉以控制档案如何被他人所调用。
参数 :
mode : 权限设定字串，格式如下 : [ugoa...][[+-=][rwxX]...][,...]，其中
u 表示该档案的拥有者，g 表示与该档案的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示这三者皆是。
\+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限。
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。
-c : 若该档案权限确实已经更改，才显示其更改动作
-f : 若该档案权限无法被更改也不要显示错误讯息
-v : 显示权限变更的详细资料
-R : 对目前目录下的所有档案与子目录进行相同的权限变更(即以递回的方式逐个变更)
--help : 显示辅助说明
--version : 显示版本
范例 :将档案 file1.txt 设为所有人皆可读取 :
chmod ugo+r file1.txt 
将档案 file1.txt 设为所有人皆可读取 :
chmod a+r file1.txt 
将档案 file1.txt 与 file2.txt 设为该档案拥有者，与其所属同一个群体者可写入，但其他以外的人则不可写入 :
chmod ug+w,o-w file1.txt file2.txt 
将 ex1.py 设定为只有该档案拥有者可以执行 :
chmod u+x ex1.py 
将目前目录下的所有档案与子目录皆设为任何人可读取 :
chmod -R a+r * 
此外chmod也可以用数字来表示权限如 chmod 777 file
语法为：chmod abc file
其中a,b,c各为一个数字，分别表示User、Group、及Other的权限。
r=4，w=2，x=1
若要rwx属性则4+2+1=7；
若要rw-属性则4+2=6；
若要r-x属性则4+1=7。
范例：
chmod a=rwx file 
和
chmod 777 file 
效果相同
chmod ug=rwx,o=x file 
和
chmod 771 file 
效果相同
若用chmod 4755 filename可使此程序具有root的权限

---root的权限

---