---
layout:     post
title:      "Java 软件工程技术 面试 个人指南 (二)"
subtitle:   "\"一切都是为了做个不后悔的自己\""
date:       2018-02-24 12:00:00
author:     "Gordon"
header-img: "img/in-post/2018-02-24-interviews2/interviews2-bg.jpg"
catalog: true
tags:
    - Java
    - Interview
---

> by : 法源(蚂蚁金服)

## 操作系统
* [页面置换算法](http://blog.csdn.net/u011080472/article/details/51206332)
* [作业调度算法](http://c.biancheng.net/cpp/html/2595.html)
* [线程进程区别](http://blog.csdn.net/yanxiaolx/article/details/51763372)

## 计算机网络
* [七层模型](https://www.cnblogs.com/lemo-/p/6391095.html)
* [三次握手](https://www.zhihu.com/question/24853633)

为什么连接建立需要三次握手，而不是两次握手？ 防止失效的连接请求报文段被服务端接收，从而产生错误。PS：失效的连接请求：若客户端向服务端发送的连接请求丢失，客户端等待应答超时后就会再次发送连接请求，此时，上一个连接请求就是『失效的』。若建立连接只需两次握手，客户端并没有太大的变化，仍然需要获得服务端的应答后才进入

ESTABLISHED状态，而服务端在收到连接请求后就进入ESTABLISHED状态。此时如果网络拥塞，客户端发送的连接请求迟迟到不了服务端，客户端便超时重发请求，如果服务端正确接收并确认应答，双方便开始通信，通信结束后释放连接。此时，如果那个失效的连接请求抵达了服务端，由于只有两次握手，服务端收到请求就会进入ESTABLISHED状态，等待发送数据或主动发送数据。但此时的客户端早已进入CLOSED状态，服务端将会一直等待下去，这样浪费服务端连接资源。

* [四次挥手](https://www.zhihu.com/question/24853633)

**为什么A要先进入TIME-WAIT状态，等待2MSL时间后才进入CLOSED状态？**

为了保证B能收到A的确认应答。 
若A发完确认应答后直接进入CLOSED状态，那么如果该应答丢失，B等待超时后就会重新发送连接释放请求，但此时A已经关闭了，不会作出任何响应，因此B永远无法正常关闭。

挥手次数比握手多一次，是因为握手过程，通信只需要处理连接。而挥手过程，通信需要处理数据+连接。

* [拥塞控制](https://www.cnblogs.com/losbyday/p/5847041.html)
* [滑动窗口流量控制](https://www.cnblogs.com/woaiyy/p/3554182.html)
* [关于tcp中time_wait状态的4个问题](https://www.cnblogs.com/mfmdaoyou/p/6715422.html )
* [get和post区别](https://www.cnblogs.com/longm/p/7205318.html?utm_source=itdadao&utm_medium=referral)
* [http、RPC基础](http://blog.csdn.net/xlgen157387/article/details/53543009)
* [TCP打开/关闭](http://blog.csdn.net/wdscq1234/article/details/52422657)

## 数据结构
* [链表常规操作](http://blog.csdn.net/kangaroo_07/article/details/77726071)
* [环链判定](http://blog.csdn.net/u010098159/article/details/44956621)
* [二叉树](http://blog.csdn.net/fengrunche/article/details/52305748)
* [B树（结合数据库索引、存储）](http://blog.csdn.net/wwh578867817/article/details/50493940)
* 红黑树几乎没涉及

## 数据库
* [四大特性](https://www.jianshu.com/p/b0d0c0b04fb7)
 - [原子性](http://blog.sina.com.cn/s/blog_70555f1701017kw7.html)
* [mybatis](https://www.w3cschool.cn/mybatis/)
* [hibernate](https://www.zhihu.com/question/21104468)（pojo、映射…）
* [读写分离](http://blog.csdn.net/justdb/article/details/17331569)，非常常用
* [服务器负载均衡](https://www.cnblogs.com/xrq730/p/5154340.html)（随机、轮询、活跃度调用、一致性哈希）
   * [一致性哈希](http://blog.csdn.net/gerryke/article/details/53939212)
   * 随机，没啥好说的
   * [轮询](http://blog.csdn.net/liupeng_family/article/details/73162326)
   * [Dubbo的四个负载均衡算法](http://blog.csdn.net/revivedsun/article/details/71330126)
   * [活跃度调用by Dubbo](http://blog.csdn.net/revivedsun/article/details/71330126)
* [负载均衡之一致Hash](http://blog.csdn.net/lihao21/article/details/54193868)
* [redis为什么快](http://blog.csdn.net/ysc1123/article/details/64438888)
    * [Redis快的主要原因是：](http://blog.csdn.net/wwd0501/article/details/78959481)
        * 基于内存的采用的是单进程单线程模型的KV数据库
        * 完全基于内存
        * 数据结构简单，对数据操作也简单
        * 使用多路 I/O 复用模型
* Nginx：多进程单线程模型
* 机房备份之类的就是比较常用的，但是很简单的，实际生产很常用。

## 常见算法
* 排序
![](/img/in-post/2018-02-24-interviews2/suanfa.jpg)
* [top K问题](http://blog.csdn.net/Healist/article/details/56928503)

## linux
* [chmod](http://www.runoob.com/linux/linux-comm-chmod.html)
* [top](http://www.runoob.com/linux/linux-comm-top.html) 
* [grep](http://man.linuxde.net/grep)
* [基本问题](http://blog.csdn.net/zhang_guyuan/article/details/60467007)

## [jvm](http://raising.iteye.com/blog/2377709)
* [分区](http://www.blogjava.net/abin/archive/2013/11/09/406159.html)
* [垃圾判定](https://baijiahao.baidu.com/s?id=1589450732159463534&wfr=spider&for=pc)
* [分代模型](https://www.jianshu.com/p/f6197bfc61b0)
* [java垃圾回收算法之-标记清除](http://blog.csdn.net/linsongbin1/article/details/51577310)
* [java垃圾回收算法之-coping复制](http://blog.csdn.net/linsongbin1/article/details/51668859)
* [java垃圾回收算法之-标记__清除_压缩](http://blog.csdn.net/linsongbin1/article/details/51668525)
* [标记-压缩中怎么实现压缩](http://blog.csdn.net/njys1/article/details/53725240)
* [java垃圾回收算法之-CMS(并发标记清除)](http://blog.csdn.net/zhaozhenzuo/article/details/76769196)
* [类加载过程](http://blog.csdn.net/boyupeng/article/details/47951037)
* [双亲委派](https://www.cnblogs.com/lanxuezaipiao/p/4138511.html)
* 面试题：能不能自己写个类叫java.lang.System？

答案：通常不可以，但可以采取另类方法达到这个需求。 
解释：为了不让我们写System类，类加载采用委托机制，这样可以保证爸爸们优先，爸爸们能找到的类，儿子就没有机会加载。而System类是Bootstrap加载器加载的，就算自己重写，也总是使用Java系统提供的System，自己写的System类根本没有机会得到加载。

但是，我们可以自己定义一个类加载器来达到这个目的，为了避免双亲委托机制，这个类加载器也必须是特殊的。由于系统自带的三个类加载器都加载特定目录下的类，如果我们自己的类加载器放在一个特殊的目录，那么系统的加载器就无法加载，也就是最终还是由我们自己的加载器加载。

Bootstrap Loader（启动类加载器） ：加载System.getProperty(“sun.boot.class.path”)所指定的路径或jar 
Extended Loader（标准扩展类加载器ExtClassLoader） ：加载System.getProperty(“java.ext.dirs”)所指定的路径或jar。在使用Java运行程序时，也可以指定其搜索路径，例如：java -Djava.ext.dirs=d:\projects\testproj\classes HelloWorld 
AppClass Loader（系统类加载器AppClassLoader） ：加载System.getProperty(“java.class.path”)所指定的路径或jar。在使用Java运行程序时，也可以加上-cp来覆盖原有的Classpath设置，例如： java -cp ./lavasoft/classes HelloWorld 
特点

* [synchronized的底层](https://www.cnblogs.com/paddix/p/5367116.html)

## java基础
* 继承封装多态
* [深拷贝浅拷贝](http://blog.csdn.net/XIAXIA__/article/details/41652057)
* 重载重写
* java接口弥补没有多继承
* [静态绑定和动态绑定](https://droidyue.com/blog/2014/12/28/static-biding-and-dynamic-binding-in-java/)
* [值传递/引用传递](http://blog.csdn.net/zhzhao999/article/details/53449504)
* [final和static](https://www.cnblogs.com/author-zr/p/5486609.html)
* [hashcode和equals](http://blog.csdn.net/u013679744/article/details/57074669)（重写问题）

   * 若对象是相等的，那么对这两个对象中的每个对象调用 hashCode 方法都必须生成相同的整数结果。
   * 对象不相等，那么对这两个对象中的任一对象上调用 hashCode 方法不要求一定生成不同的整数结果。
   * 但为不相等的对象生成不同整数结果可以提高哈希表的性能，避免冲突
   * hashset 先用hash看曹位是否有重复，在用equal看entry链路中是否重复

* [hashmap源码（jdk1.8变动）](http://blog.csdn.net/unscdf117/article/details/78729674?locationNum=2&fps=1)
* [超级详细的hashcode（）和hash（）讲解](https://www.cnblogs.com/tonyluis/p/5671873.html)
* [hashmap和hashtable区别](http://blog.csdn.net/fujiakai/article/details/51585767)

  * Hashtable的方法是同步的，Hashmap的方法是不同步的，所以多线程场合要手动同步HashMap，这个区别就像是Vecgtor和ArrayList一样
  * Hashtable不允许Null值（Key 和Value都不行），Hashmap允许Null值（key和value可以）
  * 两个遍历方式有差别，Hashtable仅仅比HashMap多一个elements方法。hashtable和hashmap都可以通过values（）返回一个set，然后进行遍历处理
  * hashtable使用enumeration，hashmap使用iterator
  * 哈希值使用不同，hashtable直接使用对象的hashcode，而hashmap重新计算hash值，并且用于代替求模
  * hashtable中的hash数组默认大小为11，增加的方式是old*2+1,hashmap中hash数组默认是16，而且一定是2的指数
  * hashtable基于dictionary类，而hashmap基于abstractmap

**HashMap线程不安全的原因** 

HashMap在使用put方法时会调用这个方法,具体为addEntry(hash, key, value, i); 
此时如果有两个线程T1和T2,两个线程同时对一个数组位置调用addEntry方法,T1和T2都能获得相同槽位(bucketIndex)的Node

* [线程（启动方式、状态切换）](https://segmentfault.com/a/1190000005006079)
* [Java中的NIO（非同步用塞），BIO（同步用塞），AIO（异步）](https://www.cnblogs.com/2017112wu/p/6835956.html)
* [NIO BIO AIO链接2](https://baijiahao.baidu.com/s?id=1573998393898438&wfr=spider&for=pc)
   * BIO 做完一件事再去做另一件事，一件事一定要等前一件事做完
   * 
* [synchronized和volatile、可重入锁](http://blog.csdn.net/ztchun/article/details/60778950)
* [乐观锁的一种实现方式——CAS](http://www.importnew.com/20472.html)

## spring
* [ioc加载,和作业很像，有话可以说](https://www.cnblogs.com/chenjunjie12321/p/6124649.html)
* [aop（反射和动态代理）](http://blog.csdn.net/donggua3694857/article/details/52752503)
* [注入方式（设值、构造）](http://blog.csdn.net/wu631464569/article/details/51906959)
* 注解和配置

## 设计模式
* 单例、工厂必会
* 观察者装饰器
* 其他

## 前沿技术
* 负载均衡（高可用）
* 服务化
* 容器化
* rpc调用
* 消息
* 机器学习
* 函数式编程
* 模块化

## 其他
* 项目
* 论文
* 成绩

## 进阶
* [中间件](http://blog.csdn.net/erlian1992/article/details/53906210)（maven核心之pom）
* spring （阿里内部框架是spring大改之后重做的服务化的框架
* 最新的微服务框架（Dubbo、 SpringCloud、thrift、Hessian）基于springCloud这种，容器也在不断的被强调。开源的dubbo和pouch都有很多很棒的源码。

## 补充阿里Java面试要点汇集

> 原文地址：[Java面试通关要点汇总集](https://juejin.im/post/5a94a8ca6fb9a0635c049e67)
> 作者：梁桂钊 @ 阿里后端工程狮

### 基础篇

**基本功**

* 面向对象的特征
* final, finally, finalize 的区别
* int 和 Integer 有什么区别
* 重载和重写的区别
* 抽象类和接口有什么区别
* 说说反射的用途及实现
* 说说自定义注解的场景及实现
* HTTP 请求的 GET 与 POST 方式的区别
* session 与 cookie 区别
* session 分布式处理
* JDBC 流程
* MVC 设计思想
* equals 与 == 的区别

**集合**

* List 和 Set 区别
* List 和 Map 区别
* Arraylist 与 LinkedList 区别
* ArrayList 与 Vector 区别
* HashMap 和 Hashtable 的区别
* HashSet 和 HashMap 区别
* HashMap 和 ConcurrentHashMap 的区别
* HashMap 的工作原理及代码实现
* ConcurrentHashMap 的工作原理及代码实现

**线程**

* 创建线程的方式及实现
* sleep() 、join（）、yield（）有什么区别
* 说说 CountDownLatch 原理
* 说说 CyclicBarrier 原理
* 说说 Semaphore 原理
* 说说 Exchanger 原理
* 说说 CountDownLatch 与 CyclicBarrier 区别
* ThreadLocal 原理分析
* 讲讲线程池的实现原理
* 线程池的几种方式
* 线程的生命周期

**锁机制**

* 说说线程安全问题
* volatile 实现原理
* synchronize 实现原理
* synchronized 与 lock 的区别
* CAS 乐观锁
* ABA 问题
* 乐观锁的业务场景及实现方式

### 核心篇

**数据存储**

* MySQL 索引使用的注意事项
* 说说反模式设计
* 说说分库与分表设计
* 分库与分表带来的分布式困境与应对之策
* 说说 SQL 优化之道
* MySQL 遇到的死锁问题
* 存储引擎的 InnoDB 与 MyISAM
* 数据库索引的原理
* 为什么要用 B-tree
* 聚集索引与非聚集索引的区别
* limit 20000 加载很慢怎么解决
* 选择合适的分布式主键方案
* 选择合适的数据存储方案
* ObjectId 规则
* 聊聊 MongoDB 使用场景
* 倒排索引
* 聊聊 ElasticSearch 使用场景

**缓存使用**

* Redis 有哪些类型
* Redis 内部结构
* 聊聊 Redis 使用场景
* Redis 持久化机制
* Redis 如何实现持久化
* Redis 集群方案与实现
* Redis 为什么是单线程的
* 缓存奔溃
* 缓存降级
* 使用缓存的合理性问题

**消息队列**

* 消息队列的使用场景
* 消息的重发补偿解决思路
* 消息的幂等性解决思路
* 消息的堆积解决思路
* 自己如何实现消息队列
* 如何保证消息的有序性

### 框架篇

**Spring**

* BeanFactory 和 ApplicationContext 有什么区别
* Spring Bean 的生命周期
* Spring IOC 如何实现
* 说说 Spring AOP
* Spring AOP 实现原理
* 动态代理（cglib 与 JDK）
* Spring 事务实现方式
* Spring 事务底层原理
* 如何自定义注解实现功能
* Spring MVC 运行流程
* Spring MVC 启动流程
* Spring 的单例实现原理
* Spring 框架中用到了哪些设计模式
* Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）

**Netty**

* 为什么选择 Netty
* 说说业务中，Netty 的使用场景
* 原生的 NIO 在 JDK 1.7 版本存在 epoll bug
* 什么是TCP 粘包/拆包
* TCP粘包/拆包的解决办法
* Netty 线程模型
* 说说 Netty 的零拷贝
* Netty 内部执行流程
* Netty 重连实现

### 微服务篇

**微服务**

* 前后端分离是如何做的
* 微服务哪些框架
* 你怎么理解 RPC 框架
* 说说 RPC 的实现原理
* 说说 Dubbo 的实现原理
* 你怎么理解 RESTful
* 说说如何设计一个良好的 API
* 如何理解 RESTful API 的幂等性
* 如何保证接口的幂等性
* 说说 CAP 定理、 BASE 理论
* 怎么考虑数据一致性问题
* 说说最终一致性的实现方案
* 你怎么看待微服务
* 微服务与 SOA 的区别
* 如何拆分服务
* 微服务如何进行数据库管理
* 如何应对微服务的链式调用异常
* 对于快速追踪与定位问题
* 微服务的安全

**分布式**

* 谈谈业务中使用分布式的场景
* Session 分布式方案
* 分布式锁的场景
* 分布是锁的实现方案
* 分布式事务
* 集群与负载均衡的算法与实现
* 说说分库与分表设计
* 分库与分表带来的分布式困境与应对之策

**安全问题**

* 安全要素与 STRIDE 威胁
* 防范常见的 Web 攻击
* 服务端通信安全攻防
* HTTPS 原理剖析
* HTTPS 降级攻击
* 授权与认证
* 基于角色的访问控制
* 基于数据的访问控制

**性能优化**

* 性能指标有哪些
* 如何发现性能瓶颈
* 性能调优的常见手段
* 说说你在项目中如何进行性能调优

### 工程篇

**需求分析**

* 你如何对需求原型进行理解和拆分
* 说说你对功能性需求的理解
* 说说你对非功能性需求的理解
* 你针对产品提出哪些交互和改进意见
* 你如何理解用户痛点

**设计能力**

* 说说你在项目中使用过的 UML 图
* 你如何考虑组件化
* 你如何考虑服务化
* 你如何进行领域建模
* 你如何划分领域边界
* 说说你项目中的领域建模
* 说说概要设计

**设计模式**

* 你项目中有使用哪些设计模式
* 说说常用开源框架中设计模式使用分析
* 说说你对设计原则的理解
* 23种设计模式的设计理念
* 设计模式之间的异同，例如策略模式与状态模式的区别
* 设计模式之间的结合，例如策略模式+简单工厂模式的实践
* 设计模式的性能，例如单例模式哪种性能更好。

**业务工程**

* 你系统中的前后端分离是如何做的
* 说说你的开发流程
* 你和团队是如何沟通的
* 你如何进行代码评审
* 说说你对技术与业务的理解
* 说说你在项目中经常遇到的 Exception
* 说说你在项目中遇到感觉最难Bug，怎么解决的
* 说说你在项目中遇到印象最深困难，怎么解决的
* 你觉得你们项目还有哪些不足的地方
* 你是否遇到过 CPU 100% ，如何排查与解决
* 你是否遇到过 内存 OOM ，如何排查与解决
* 说说你对敏捷开发的实践
* 说说你对开发运维的实践
* 介绍下工作中的一个对自己最有价值的项目，以及在这个过程中的角色

**软实力**

* 说说你的亮点
* 说说你最近在看什么书
* 说说你觉得最有意义的技术书籍
* 工作之余做什么事情
* 说说个人发展方向方面的思考
* 说说你认为的服务端开发工程师应该具备哪些能力
* 说说你认为的架构师是什么样的，架构师主要做什么
* 说说你所理解的技术专家

