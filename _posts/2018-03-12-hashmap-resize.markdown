---
layout:     post
title:      "Java 进阶知识（三）- HashMap 扩容 位运算 原理 "
subtitle:   "\"HashMap 扩容 & HashCode 妙用\""
date:       2018-03-12 12:00:00
author:     "Gordon"
header-img: "img/in-post/2018-03-12-hashmap-resize/hashmap-resize-bg.jpg"
catalog: true
tags:
    - Java
---

## 哦？

> HashMap在Java集合里属于使用频率非常高的一种结构，而且面试时常会出现相关问题，其扩容原理使用了位运算，十分精妙，特此记录一番
> 
> JDK为：1.9

HashMap有两个参数影响其性能：初始容量和加载因子。
* 默认初始容量`DEFAULT_INITIAL_CAPACITY`是16 = 1 << 4
* 最大容量`MAXIMUM_CAPACITY`是2^30 = 1,073,741,824
* 默认加载因子`DEFAULT_LOAD_FACTOR`是0.75

![](/img/in-post/2018-03-12-hashmap-resize/hashmap-cap.png)

默认域：
* Entry数组`Node<K,V>[] table`，哈希表，长度必须为2的幂  
* 已存元素的个数`size`
* 下次扩容的临界值`threshold`，size>=threshold就会扩容 

![](/img/in-post/2018-03-12-hashmap-resize/hashmap-fields.png)

HashMap在put元素时，如果哈希表中的条目数超出了加载因子与当前容量的乘积时，通过调用 rehash 方法将容量翻倍。

## 为什么HashMap容量一定要为2的幂呢？

首先来一段源码：

![](/img/in-post/2018-03-12-hashmap-resize/hashmap-&.png)

**看到最后一行了么？位运算！！计算中战斗机，数值转换中的高富帅～**

* e.hash为哈希值
* newCap为目前容量

这块的处理很有玄机，与容量一定为2的幂环环相扣，当容量一定是2^n时，e.hash & (newCap - 1) == e.hash % newCap，它俩是等价不等效的，这不就是求模运算么，不就是哈希寻址么～

如果转为二进制更为清楚明了：

我们知道`2^n`可以看成二进制中`1+n个0`：2^4 = 16 = 00010000 =  '1' + 4个 '0'

所以进行运算时，会出现两种情况：

1. e.hash <= 15,进行运算后还是e.hash本身的值

```
     14 = 0 0 0 0 1 1 1 0
    
 & 16-1 = 0 0 0 0 1 1 1 1
--------------------------
     14 = 0 0 0 0 1 1 1 0
```

2. e.hash > 15,进行运算后就是%运算后的余数

```
     17 = 0 0 0 1 0 0 0 1
    
 & 16-1 = 0 0 0 0 1 1 1 1
--------------------------
      1 = 0 0 0 0 0 0 0 1
```
