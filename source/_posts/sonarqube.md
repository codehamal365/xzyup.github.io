---
title: sonarqube简单使用
tags:
  - sonarqube
abbrlink: 8f28
---

### sonarqube

**登陆：admin/admin**

- 进入sonarqube官网下载zip文件，解压。进入对应文件夹，修改wrapper.conf

  ~~~xml
  # 修改为对应java_home下java命令，请针对不同源码配置不同jdk版本
  wrapper.java.command=/Library/Java/JavaVirtualMachines/jdk-11.0.11.jdk/Contents/Home/bin/java
  ~~~

- 进入bin目录，不同操作系统选择不通目录。本次为macos

  ~~~
  执行
  lsof -i tcp:9000
  kill -9 pid
  ./sonar.sh stop
  ./sonar.sh start
  ~~~

- [进入sonarqube首页](http://localhost:9000/)，依次进入Administration > Security > Force user authentication,将这个配置禁用，方便本地代码检测无密码。

- idea集合sonarlint代码分析

  idea结合sonar的话，可以下载sonarLint插件，操作步骤如下：

  1. 进入idea ，进入插件安装，在插件市场中搜索sonarLint，点击进行安装后重启idea；
  2. 配置sonarLint插件，设置settings中，查找到other settings,然后选择sonarLint General Setting ,在右侧的输入
  3. 接下来输入要连接的服务器的登录信息，如输入token或者是使用账号和密码的方式
  4. 配置当前的项目和sonar的关系,点击进入设置settings->other settings->SonarLint Project Settings
  5. Bind to Server 选择刚才配置的服务器信息。SonarQube project的选择可以点击Search in list查看sonar仓库中配置的项目信息，完成选择以后点击ok即可
  6. 代码分析，可以查看到当前的窗口中多了一个SonarLint的窗口（如无此窗口，可以点击analysis菜单进行查找），在其中选择report，点击文件夹图标，会弹窗提示，点击process之后即可进行项目分析。

- 配置完idea插件后，idea命令行执行

  ~~~
  mvn clean install sonar:sonar
  或者
  mvn sonar:sonar \
   # 以下可以忽略
    -Dsonar.projectKey={project-name} \
    -Dsonar.host.url=http://192.168.30.217:9000 \
    -Dsonar.login=10ac31fd0b091a4e9ee93e7351bc40f90f91acb3
  ~~~

  > 相关参考资料
  >
  > https://www.jianshu.com/p/b357cf94e4d2

- TODO

   - sonarqube与jenkins集合
   - Sonarqube max 开机自启动设置
   - Sonar.scanner 相关配置学习
