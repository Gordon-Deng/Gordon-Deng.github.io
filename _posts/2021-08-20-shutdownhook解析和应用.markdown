---
layout:     post
title:      "优雅关闭核心机制：Shutdownhook-解析和应用"
subtitle:   "\"Hook大法好啊\""
date:       2021-08-20 5:00:00
author:     "Gordon"
header-img: "img/in-post/2020-01-20-todo/todo-bg.jpg"
catalog: true
tags:
    - Java
---

## 前言
> 最近自己在学习手撸一个RPC，个人认为里面有很多点都是大学问，其中的优雅上下线这块涉及到了Hook的运用，自己刚好可以结合起来一起看看


## Hook
### Hook的原理
### Hook的应用

### 优雅启动与Hook


## Shutdownhook
### Shutdownhook机制
### Shutdownhook充当“挡板”原理

## Spring优雅关闭与Shutdownhook
### 灵魂拷问：当服务提供方关闭前，可以先通知注册中心进行下线，然后通过注册中心告诉调用方进行节点摘除

## 延伸学习
自己乱刷知乎的时候，[知乎-并发三高怎么学习](https://www.zhihu.com/question/421237964/answer/1810636619)中出现相关的问题，所以结合起来一起学学

![](img/in-post/2021-08-20-shutdownhook解析和应用/sangao.jpeg)

### 高可用&高并发中的预处理&延后处理



