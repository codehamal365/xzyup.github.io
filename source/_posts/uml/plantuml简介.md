---
uuid: bbaf6f22-c0ab-11ec-92a1-7557b2313227
title: plantuml 简介
categories: Uml
tags:
  - plantuml
abbrlink: '245017e5'
---


# PlantUML 简介

[PlantUML](https://links.jianshu.com/go?to=http%3A%2F%2Fplantuml.com%2F) 是一个开源项目，支持快速绘制时序图、用例图、类图、活动图、组件图、状态图、对象图、部署图等。同时还支持非 UML 图的甘特图、架构图等。例如下面等用例图：

![image-20211028134337523](https://raw.githubusercontent.com/xzyup/image/master/202203191658878.png)

~~~
@startuml
P: PENDING
P: Pending for result

N: NO_RESULT_YET
N: Did not send the KYC check yet 

Y: APPROVED
Y: KYC check successful

R: REJECTED
R: KYC check found the applicant's 
R: information not correct 

X: EXPIRED
X: Proof of Address (POA) too old

[*] --> N : Card application received
N --> P : Submitted the KYC check
P --> Y
P --> R
P --> X : Proof of Address (POA) too old
P --> X : explicitly by KYC
Y --> [*]
R --> [*]
X --> [*]
@enduml
~~~

![image-20211028134433980](https://raw.githubusercontent.com/xzyup/image/master/202203191659925.png)

~~~
@startuml

skinparam rectangle {
    BackgroundColor DarkSeaGreen
    FontStyle Bold
    FontColor DarkGreen
}

:User: as u
rectangle Tool as t
rectangle "Knowledge Base" as kb
(Robot Framework) as rf
(DUT) as dut

note as ts
    test script
end note

note as act
    query
    &
    action
end note

note as t_cmt
    - 执行测试脚本
    - 按照知识库响应消息
end note

note as kb_cmt
    - 根据当前消息确定响应方法
    - 根据上下文填充消息
    - 保存信息到相关上下文
end note

u --> rf
rf =right=> ts
ts =down=> t

kb <=left=> act
act <=up=> t

t = dut

t_cmt -- t
kb_cmt -left- kb
@enduml
~~~

![image-20211028134522066](https://raw.githubusercontent.com/xzyup/image/master/202203191659326.png)

~~~
@startuml
interface Command {
    execute()
    undo()
}
class Invoker{
    setCommand()
}
class Client
class Receiver{
    action()
}
class ConcreteCommand{
    execute()
    undo()
}

Command <|-down- ConcreteCommand
Client -right-> Receiver
Client --> ConcreteCommand
Invoker o-right-> Command
Receiver <-left- ConcreteCommand
@enduml
~~~

一款还算不错的绘图工具-- Plantuml, 它本质上是也算一门可以快速画图的设计语言，学习起来也很方便。可以在[http://plantuml.com/](https://links.jianshu.com/go?to=http%3A%2F%2Fplantuml.com%2F)网站上体验一下。 在vscode, webstorm都有相关的插件可以使用。

# 时序图

时序图相对来说是平常比较经常画的一种设计图稿，在这里记录一下plantuml中相关的语法。

## 基本用法

~~~
@startuml
A -> B: do something
B -> A: do something
@enduml
~~~

![image-20211028134701752](https://raw.githubusercontent.com/xzyup/image/master/202203191659299.png)

## 设置不同的角色

时序图角色可以分为: actor, boundary, control, entity, database，每种角色呈现的图形也是不一样的。

~~~
@startuml
actor Foo1
boundary Foo2
control Foo3
entity Foo4
database Foo5
collections Foo6
Foo1 -> Foo2 : To boundary
Foo1 -> Foo3 : To control
Foo1 -> Foo4 : To entity
Foo1 -> Foo5 : To database
Foo1 -> Foo6 : To collections

@enduml
~~~

![image-20211028134748732](https://raw.githubusercontent.com/xzyup/image/master/202203191659968.png)

## 不用的箭头样式

~~~
@startuml
Bob ->x Alice
Bob -> Alice
Bob ->> Alice
Bob -\ Alice
Bob \\- Alice
Bob //-- Alice

Bob ->o Alice
Bob o\\-- Alice

Bob <-> Alice
Bob <->o Alice
Bob -[#red]> Alice : hello
Alice -[#0000FF]->Bob : ok
@enduml
~~~

![image-20211028134906473](https://raw.githubusercontent.com/xzyup/image/master/202203191659658.png)

## 分页

~~~
@startuml

Alice -> Bob : message 1
Alice -> Bob : message 2

newpage

Alice -> Bob : message 3
Alice -> Bob : message 4

newpage A title for the\nlast page

Alice -> Bob : message 5
Alice -> Bob : message 6
@enduml
~~~

![image-20211028135036412](https://raw.githubusercontent.com/xzyup/image/master/202203191659447.png)

## 分段

~~~
@startuml

== Initialization ==

Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

== Repetition ==

Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response

@enduml
~~~

![image-20211028135145988](https://raw.githubusercontent.com/xzyup/image/master/202203191700518.png)

## 生命线

~~~
@startuml
participant User

User -> A: DoWork
activate A #FFBBBB

A -> A: Internal call
activate A #DarkSalmon

A -> B: << createRequest >>
activate B

B --> A: RequestCreated
deactivate B
deactivate A
A -> User: Done
deactivate A

@enduml
~~~

![image-20211028135346014](https://raw.githubusercontent.com/xzyup/image/master/202203191700717.png)

## 图例注脚等

~~~
@startuml

header Page Header
footer Page %page% of %lastpage%

title Example Title

Alice -> Bob : message 1
note left: this is a first note

Alice -> Bob : message 2

@enduml
~~~

![image-20211028135444347](https://raw.githubusercontent.com/xzyup/image/master/202203191700245.png)

# C4架构图

C4 model是一种软件架构图的设计方法，具体介绍可以参考[C4 architecture model](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.infoq.cn%2Farticle%2FC4-architecture-model)。利用[C4-PlantUML](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FRicardoNiepel%2FC4-PlantUML)工具，可以画出很多很不错的架构图。 C4模型分为Context, Container, Component和Code 4个组成部分，我们一般在画图的时候主要用到前三个组成部分。

~~~
@startuml C4_Elements
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Context.puml
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Container.puml
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Component.puml

System(systemAlias, "System", "这可以看作系统上下文(Context)")
Container(containerAlias, "Container", "这是Container")
Person(personAlias, "Person", "这可以看作是组件(Component)")

Rel(personAlias, containerAlias, "Label", "设置关联关系")
@enduml
~~~
