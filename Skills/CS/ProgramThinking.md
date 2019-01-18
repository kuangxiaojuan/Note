---
title: ProgramThinking
date: 2018-11-21 10:56:52
tags: 
categories: 
    - Engineering
---

**目录 start**
 
1. [开发思想](#开发思想)
    1. [抽象](#抽象)
    1. [命令式编程和响应式编程](#命令式编程和响应式编程)
        1. [命令式编程](#命令式编程)
        1. [响应式编程](#响应式编程)
    1. [面向过程](#面向过程)
    1. [面向对象](#面向对象)
        1. [OOP](#oop)
        1. [面向过程和面向对象的对比](#面向过程和面向对象的对比)
    1. [DDD 领域驱动设计](#ddd-领域驱动设计)
        1. [聚合](#聚合)
        1. [参考实践项目](#参考实践项目)
    1. [数据的操作](#数据的操作)
        1. [CURD](#curd)
        1. [CQRS](#cqrs)
    1. [组件模型](#组件模型)
        1. [SOA](#soa)
        1. [MSA](#msa)
    1. [Other](#other)
        1. [国际化的配置](#国际化的配置)
1. [设计软件的方法](#设计软件的方法)
    1. [契约式设计](#契约式设计)
    1. [精益思想](#精益思想)
1. [编程习惯](#编程习惯)
    1. [晓风轻的经验](#晓风轻的经验)
        1. [接口定义](#接口定义)
        1. [日志建议](#日志建议)
        1. [异常处理](#异常处理)
        1. [工具类规范](#工具类规范)
    1. [代码质量分析](#代码质量分析)
        1. [Checkstyle](#checkstyle)
        1. [FindBugs](#findbugs)
        1. [阿里巴巴的代码检查](#阿里巴巴的代码检查)
    1. [配置文件](#配置文件)

**目录 end**|_2018-12-13 12:06_| [码云](https://gitee.com/gin9) | [CSDN](http://blog.csdn.net/kcp606) | [OSChina](https://my.oschina.net/kcp1104) | [cnblogs](http://www.cnblogs.com/kuangcp)
****************************************
# 开发思想
> 有关开发的理论性思想,编写,测试,部署等

## 抽象
- [码农翻身:抽象：程序员必备的能力 ](https://mp.weixin.qq.com/s?__biz=MzAxOTc0NzExNg==&mid=2665513062&idx=1&sn=a3b4a2962d8e82471192d9606b0a2722&scene=21#wechat_redirect)

> 稍微注意一下就会发现: 抽象层次越高，接口的语意就越模糊，适用的范围就越广，到最后就会变成数学模型或者概念。  
但是抽象成数学模型和算法通常是可遇而不可求的， 这种情况下，我们需要退而求其次，试图抽象成若干个正交的概念，来降低复杂度。  
你在处理x轴相关的事情时，不用考虑其他的y和z 相关的东西，因为你知道他们不会受到影响， 这样问题的复杂度就从3维一下子下降到1维！更容易把握了。  
如果你说了，我的整个系统还没法抽象成正交的概念， 那只好再退一步，在局部使用接口。  
其实 一组定义良好的接口一定是正交的，不然的话接口之间的依赖就会让实现非常麻烦。 
>> 在著名的《设计模式》一书中，其实在反复强调一点: 发现变化并且封装变化，针对接口编程而不是实现编程。 很多人看书是只关注具体的模式，而忽略了模式的本质目的。  

抽象能力的高低，很大程度上反映了一个程序员的能力的高低

- [计算机科学中抽象的好处与问题—伪共享实例分析](http://ifeve.com/%e8%ae%a1%e7%ae%97%e6%9c%ba%e7%a7%91%e5%ad%a6%e4%b8%ad%e6%8a%bd%e8%b1%a1%e7%9a%84%e5%a5%bd%e5%a4%84%e4%b8%8e%e9%97%ae%e9%a2%98-%e4%bc%aa%e5%85%b1%e4%ba%ab%e5%ae%9e%e4%be%8b%e5%88%86%e6%9e%90/)`计算机科学中的任何问题都可以通过加上一层间接层来解决，这是很正确的，但是也正是因为一层一层的抽象和包装，导致出了问题后很难定位，你都不知道问题究竟是出现在哪一层。所以要想提高技术水平不仅要知其然（看得见最顶层的包装）也要知其所以然（看得见底层的包装），每一层如果都懂或者说了解一些，那么出了问题很大程度上都可以凭直觉定位，即使不能凭直觉也可以通过各种手段debug，只会最顶层的抽象很多时候就只能望bug兴叹了。`


## 命令式编程和响应式编程

### 命令式编程
> 编写改变状态的一条条命令

### 响应式编程
> [ReactiveX](http://reactivex.io/intro.html)

组合异步的序列
设计模式是 观察者模式的扩展, 数据结构是序列串流, 避免了并发, 是非阻塞的

数据流驱动


异步
- 非阻塞
    - 不是 (同步非阻塞 : 当时不阻塞后续回调) 而是异步

多路复用

*********************
## 面向过程
> 只有数据和函数, 使用函数改变数据状态

## 面向对象
> OO  Object Oriented

> [参考博客: 再见面向对象编程？](http://www.jdon.com/48231)

> 思考:
>- 遇到需求时, 先分析需要哪些独立的实体, 然后分析用户的行为, 行为就是API
>- 实体的基本属性和行为确定好, 并且确定好各自的生命周期(一般是属性, 状态的变化)
>- 并且要注意设计时要尽量解耦, 即使需求上是和时间, 天气, 等一些外部状态影响的, 但是也应该在此之上抽象, 解耦, 方便测试和开发
>>- 例如 `活动` 具有 开始时间和结束时间 的需求, 如果只用时间去设计行为的话, 测试的时候就需要去模拟那些时间, 如果引入`状态`这个属性(开启,关闭)
>>- 就可以方便的调试了, 只需更改这个状态即可控制 活动 这个对象的行为, 当然, 变化的时间也是通过控制 `状态` 来控制 活动 的

`编写出完成需求的代码不难, 难的是写出, 优雅, 简洁, 设计良好, 可读性, 扩展性高的代码`

### OOP
> [维基 OOP](https://en.wikipedia.org/wiki/Object-oriented_programming) | [中文版](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)

### 面向过程和面向对象的对比
> 示例 把大象塞进冰箱:
>> 面向过程, 冰箱开门() 冰箱装进( 大象) 冰箱关门()
>> 面向对象 冰箱.开门().装入(大象).关门()

- 面向过程
    - 优点：性能比面向对象高，因为类调用时需要实例化，开销比较大，比较消耗资源;比如单片机、嵌入式开发、Linux/Unix等一般采用面向过程开发，性能是最重要的因素。
    - 缺点：没有面向对象易维护、易复用、易扩展
- 面向对象    
    - 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护
    - 缺点：性能比面向过程低

*************************************************
## DDD 领域驱动设计
> [领域驱动设计(DDD:Domain-Driven Design)](http://www.jdon.com/ddd.html)`入门贴`

> [领域驱动设计 软件核心复杂性应对之道 Eric J. Evans 在线阅读](http://ishare.iask.sina.com.cn/f/69200951.html)
> [领域驱动设计精简版 ](http://www.infoq.com/cn/minibooks/domain-driven-design-quickly)

> [参考博客](http://kb.cnblogs.com/page/117717/) | [讨论](http://www.cnblogs.com/netfocus/p/3307971.html) | [基础](http://www.cnblogs.com/netfocus/archive/2011/10/10/2204949.html)

> [参考博客: 危险的DDD聚合根](http://www.cnblogs.com/netfocus/archive/2012/09/08/2676985.html) 初步感受是DDD禁不起变化, 必须要在起初就设计好一个完备的体系
> [参考博客: DDD应用的思考](http://www.jdon.com/47313)`提出了关于领域设计的困惑`

### 聚合
聚合根的修改行为应该属于聚合根实体对象自己，用聚合根行为守护其内部状态的一致性是DDD设计核心，如果聚合根内部的状态直接暴露给外界（通过领域服务）任意修改，那么会导致状态变化混乱，难以调试和跟踪。

- 现在书写的这个项目就和这个理念相一致, 但是总说是OOP 没有提及DDD _TODO_
    - 整个系统中涉及到的实体对象, 需要持久化的属就独立出来作为一个PO对象, 然后Spring Data JPA 接管DAO操作
    - 然后在对象中建立 修改PO对象行为 的方法, 而不是以往 MVC 那样的设计, 业务全在Service里面, 对实体自身属性的基本操作也在Service里面

### 参考实践项目
> [enode](https://github.com/tangxuehua/enode)`C#实现`
> [CQRS](https://github.com/liangzeng/cqrs)

*****************************
## 数据的操作
### CURD
### CQRS
> [www.cqrs.nu](http://www.cqrs.nu/)`CQRS Guides`  
> [event-sourcing](https://docs.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)| [中文版](https://docs.microsoft.com/zh-cn/azure/architecture/patterns/event-sourcing)   `微软关于azure的技术性文档`  

> [event-sourcing-in-practice](https://ookami86.github.io/event-sourcing-in-practice/) 
> [参考博客:  CQRS & Event Sourcing ](https://www.cnblogs.com/netfocus/category/361988.html)  
> [参考博客: 领域驱动设计的实践 – CQRS & Event Sourcing](https://www.jianshu.com/p/9a3f8d514fcd) `图文并茂的讲解CQRS思想`

> [eventapis](https://github.com/kloiasoft/eventapis)`Java实现的CQRS`
> [CQRS journey](http://cqrsjourney.github.io/) `微软团队的项目`

*************************
## 组件模型
### SOA
> [参考博客: SOA面向服务架构](http://www.jdon.com/soa.html)

_[Spring Web 应用的最大败笔](http://www.jdon.com/45857)_
- 传统意义上的SOA 内部封装的是数据表的DTO 也被称为 失血模型,贫血模型,  从而导致SOA服务内部腐烂堵塞，违背SOA自治和可用性等原则约束
    - 我现在使用Java的SpringMVC进行开发的东西, MVC架构, 然后JavaBean, Dao层或者JPA的Repository, Service层, Controller层, 而且还使用了好几年了
    1. Web层负责处理用户输入，并返回正确的响应返回给用户。 web层与服务层通信。
    2. 服务层作为一个事务边界。它也负责授权和包含我们的应用程序的业务逻辑。服务层管理的域模型对象，并与其他服务和存储库层进行通信。
    3. 存储库/数据访问层负责与所使用的数据的存储进行通信。
    - 正如这个毕业设计的项目  [Graduate](https://github.com/Kuangcp/Graduate), 显然的都具有如上提到的各种缺陷, 
    - 每一个 DTO 只具有属性, 而没有方法, 一个DTO就要对应一个服务, 服务之间再相互注入, 就会有很有依赖, 甚至循环依赖

### MSA
> 微服务

>　[参考博客: SOA 与 MSA（微服务架构）](https://blog.csdn.net/ztguang/article/details/52894794)
> [码农翻身:从SOA到微服务](https://mp.weixin.qq.com/s?__biz=MzAxOTc0NzExNg==&mid=2665513674&idx=1&sn=fbc727b7c8ff6d03f5d53478b6d4e585&chksm=80d67a89b7a1f39ff0c3589a4a4076e323fab18379fc8d085c133b88e4db104f87988b29d246&scene=21#wechat_redirect)

- [码农翻身:我是一个函数](https://mp.weixin.qq.com/s?__biz=MzAxOTc0NzExNg==&mid=2665513873&idx=1&sn=2383f099fb353e59649167e723575158&chksm=80d67bd2b7a1f2c4ae61704b8a2bd330764d20f0e2fafa6fdff55c99ea68272b3cff851684cc&scene=21#wechat_redirect) `详解了RPC, 也就是RMI(远程过程调用)规范的实现`

> [微服务 MSA](http://www.spring4all.com/article/609)

## Other
### 国际化的配置
- 将配置文件按语言分别配置
- 然后在加载时设定语言的配置, 然后加载对应文件夹下的配置文件

*****************************************
# 设计软件的方法
## 契约式设计
> Design by Contract  (Dbc)

> [百度百科解释 ](https://baike.baidu.com/item/%E5%A5%91%E7%BA%A6%E5%BC%8F%E8%AE%BE%E8%AE%A1)

## 精益思想
> 持续集成、持续交付、持续部署

********************************
# 编程习惯
## 晓风轻的经验
-  [知乎专栏-程序员你为什么这么累？](https://zhuanlan.zhihu.com/p/28705206) | [该专栏对应的源码](https://github.com/xwjie/PLMCodeTemplate) | [个人站点版, 更为方便](https://xwjie.github.io/rule/)
    1. [接口定义](https://zhuanlan.zhihu.com/p/28708259)
    1. [Controller规范](https://zhuanlan.zhihu.com/p/28717374)
    1. [日志建议](https://zhuanlan.zhihu.com/p/28629319)
    1. [异常处理规范](https://zhuanlan.zhihu.com/p/29005176)
    1. [参数校验和国际化规范](https://zhuanlan.zhihu.com/p/29129469)
    1. [工具类规范](https://zhuanlan.zhihu.com/p/29199049)
    1. [函数编写建议](https://zhuanlan.zhihu.com/p/29390147)
    1. [配置文件的定义](https://zhuanlan.zhihu.com/p/29191233)

- [ ] 详细的阅读

### 接口定义
- 先有统一的接口定义规范，然后有AOP实现。先有思想再有技术。
- 现在知道为什么要返回统一的一个ResultBean了：
    - 为了统一格式
    - 为了应用AOP
    - 为了包装异常信息

### 日志建议

### 异常处理
- 所以，我对开发人员的要求就是，绝大部分场景，不允许捕获异常，不要乱加空判断。只有明显不需要关心的异常，如关闭资源的时候的io异常，可以捕获然后什么都不干，其他时候，不允许捕获异常，都抛出去，到controller处理。空判断大部分时候不需要，你如果写了空判断，你就必须测试为空和不为空二种场景，要么就不要写空判断。
- 强调，有些空判断是要的，如：参数是用户输入的情况下。但是，大部分场景是不需要的（我们的IT系统里面，一半以上不需要），如参数是其它系统传过来，或者其他地方获取的传过来的，99.99%都不会为空，你判断来干嘛？就抛一个空指针到前台怎么啦？何况基本上不会出现。
- 总结：
    - 开发组长定义好异常，异常继承RuntimeException。
    - 不允许开发人员捕获异常。（异常上对开发人员就这点要求！异常都抛出到controller上用AOP处理）
    - 后台（如队列等）异常一定要有通知机制，要第一时间知道异常。
    - 少加空判断，加了空判断就要测试为空的场景！

### 工具类规范
1. 方法参数要抽象(尽量往上找到父类和接口), 返回值要具体
1. 隐藏实现: 不要在业务代码中直接调用三方工具, 应该自己写一个类, 然后调用三方库的方法, 方便以后修改
1. 多使用重载编写功能齐全的对外接口和方法
1. 单独存放, 单独维护, 


*********************************************
> 优先使用组合而不是继承, 继承破坏了封装性, 因为父类的很多细节对子类是可见的, 父类的变化可能极大的影响子类  
> 面向接口编程, 而不是实现编程 

## 代码质量分析
- 测试对代码的覆盖率
- 代码的格式是否清晰，有助于差异比较和可读性
- 是否很可能会出现NPE
- 是否忘记了域对象中的equals和hashCode方法

### Checkstyle

### FindBugs

### 阿里巴巴的代码检查

*********************************

## 配置文件
千万业务代码里面不要和读取配置的代码耦合在一起。切记！