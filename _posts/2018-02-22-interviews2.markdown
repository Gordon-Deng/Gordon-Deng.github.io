---
layout:     post
title:      "Java 软件工程技术 面试 个人指南#2"
subtitle:   "一切都是为了做个不后悔的自己"
date:       2018-02-24 12:00:00
author:     "Gordon"
header-img: "img/in-post/2018-02-24-interviews2/interviews2-bg.jpg"
catalog: true
tags:
    - Java
    - Interview
---

# 操作系统
* [页面置换算法](http://blog.csdn.net/u011080472/article/details/51206332)
* [作业调度算法](http://c.biancheng.net/cpp/html/2595.html)
* [线程进程区别](http://blog.csdn.net/yanxiaolx/article/details/51763372)

### 计算机网络
* [七层模型](https://www.cnblogs.com/lemo-/p/6391095.html)
* [三次握手](https://www.zhihu.com/question/24853633)
* [四次挥手](https://www.zhihu.com/question/24853633)
* [拥塞控制](https://www.cnblogs.com/losbyday/p/5847041.html)
* [get和post区别](https://www.cnblogs.com/longm/p/7205318.html?utm_source=itdadao&utm_medium=referral)
* [http、RPC基础](http://blog.csdn.net/xlgen157387/article/details/53543009)
* [TCP打开/关闭](http://blog.csdn.net/wdscq1234/article/details/52422657)


### 数据结构
* 链表常规操作
* 环链判定
* 二叉树
* B树（结合数据库索引、存储）
* 红黑树几乎没涉及

### 数据库
* 四大特性，原子性需要特别注意
* mybatis和hibernate的知识（pojo、映射…）
* 读写分离，非常常用
* 服务器负载均衡（随机、轮询、活跃度调用、一致性哈希）
* 机房备份之类的就是比较常用的，但是很简单的，实际生产很常用。

### 常见算法
* 排序
* top K问题

### linux
* chmod
* top 
* grep

### jvm
* 分区
* 垃圾判定
* 分代模型
* 类加载过程
* 双亲委派

### java基础
* 继承封装多态深拷贝
* 重载重写
* java接口弥补没有多继承
* 静态绑定和动态绑定
* 值传递/引用传递
* final和static
* hashcode和equals（重写问题）
* hashmap源码（jdk1.8变动）
* hashmap和hashtable区别
* 线程（启动方式、状态切换）
* synchronized和volatile、可重入锁

### spring
* ioc和aop（反射和动态代理）
* 注入方式（设值、构造）
* 注解和配置

### 设计模式
* 单例、工厂必会
* 观察者装饰器，这种有点难度，但也常用的
* 其他都得了解

### 前沿技术
* 负载均衡（高可用）
* 服务化
* 容器化
* rpc调用
* 消息
* 机器学习
* 函数式编程（虽不常用但是有些新代码会有，关键是看你对新技术的嗅觉和自觉学习的心态）
* 模块化（java发展大势所趋）

### 其他
* 项目
* 论文
* 成绩

### 进阶
* [中间件](http://blog.csdn.net/erlian1992/article/details/53906210)（maven核心之pom）
* spring （阿里内部框架是spring大改之后重做的服务化的框架
* 最新的微服务框架（Dubbo、 SpringCloud、thrift、Hessian）基于springCloud这种，容器也在不断的被强调。开源的dubbo和pouch都有很多很棒的源码。