---
layout:     post
title:      "Java 软件工程技术 面试 个人指南 (二)"
subtitle:   "\"一切都是为了做个不后悔的自己\""
date:       2018-03-24 12:00:00
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
* [synchronized和volatile](http://blog.csdn.net/ztchun/article/details/60778950)
* [可重入锁](https://www.cnblogs.com/dj3839/p/6580765.html)
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
  * 继承
  * 多态
  * 封装
* final, finally, finalize 的区别
   * Final
	  * Final成员
	     * 作为变量一旦被初始化便不可改变（对于基本类型，指的是值不变；对于对象类型，指的是引用不变），初始化只可能在两个地方：定义处和构造函数。
	     * 作为方法参数对于基本类型，定义成final参数没有什么意义，因为基本类型就是传值，不会影响调用语句中的变量；对于对象类型，在方法中如果参数确认不需要改变时，定义成final参数可以防止方法中无意的修改而影响到调用方法。
	  * Final方法
	     * 不可覆写
	     * 编译器将对此方法的调用转化成行内（inline）调用，即直接把方法主体插入到调用处（方法主体内容过多的时候反而会影响效率）
	  * Final类
		     * 不可继承 

   * Finally
     * 异常处理关键字，finally中的主体总会执行，不管异常发生是否。
   
   * Finalize
     * 类的Finalize方法，可以告诉垃圾回收器应该执行的操作，该方法从Object类继承而来。在从堆中永久删除对象之前，垃圾回收器调用该对象的Finalize方法。注意，无法确切地保证垃圾回收器何时调用该方法，也无法保证调用不同对象的方法的顺序。即使一个对象包含另一个对象的引用，或者在释放一个对象很久以前就释放了另一个对象，也可能会以任意的顺序调用这两个对象的Finalize方法。如果必须保证采用特定的顺序，则必须提供自己的特有清理方法。
* int 和 Integer 有什么区别
 * 存储原理不一样： 
 
		int：属于简单类型，不存在“引用”这个概念；其数据是存储在栈空间中； 
		
		Integer：属于继承自Object的类，是按照java存储对象的内存模型来存储的；引用存储在栈中，对象数据存储在堆中； 
		
		基于这个原理不同，所以在进行参数传递的时候，int是值传递，其在栈中的数据不可变； 
		
		而Integer类型是引用传递，引用指向的内存地址中的数据是可以变化的，但是栈中的引用是不变的；

 * 缺省值不一样 

		int的初始化值是0 ，Integer初始化的值是null。 
		你不能把null值赋给int；

 * 泛型支持不一样 
 
		泛型支持Integer，并不支持int 
		如： 
		ArrayList list = new ArrayList(); 
		你不能在泛型中写int

 * 行为不一样 

		int a =10; 
		Integer b= new Integer(10); 
		
		在方法调用中： 
		
		a是基本类型，并没有什么方法可言；因为方法是类的特性。 
		b有很多方法，因为方法是对象中定义的；一些转换操作，如转为字符串等
		
* 重载和重写的区别
 * override（重写）

　　 1、方法名、参数、返回值相同。

　　 2、子类方法不能缩小父类方法的访问权限。

　　 3、子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。

　　 4、存在于父类和子类之间。

　　 5、方法被定义为final不能被重写。

*  overload（重载）

　　1、参数类型、个数、顺序至少有一个不相同。 

　　2、不能重载只有返回值不同的方法名。

　　3、存在于父类和子类、同类中。
　　

* 抽象类和接口有什么区别
  * 1.一个类可以实现多个接口 ，但却只能继承最多一个抽象类。
  * 2.抽象类可以包含具体的方法 ， 接口的所有方法都是抽象的。
  * 3.抽象类可以声明和使用字段 ，接口则不能，但接口可以创建静态的final常量。
  * 4.接口的方法都是public的，抽象类的方法可以是public，protected，private或者默认的package；
  * 5.抽象类可以定义构造函数，接口却不能。 
 
* 说说反射的用途及实现
  * 反射机制的主要功能主要有：提高了程序的灵活性和扩展性，降低耦合性，提高自适应能力。它允许程序创建和控制任何类的对象，无需提前硬编码目标类；
  * 实现：①得到一个对象所属的类，②获取一个类的所有成员变量和方法，③在运行时创建对象，调用对象的方法。
 
* 说说自定义注解的场景及实现

  * @Target；
     * 1. CONSTRUCTOR:用于描述构造器 
     * 2. FIELD:用于描述域 
     * 3. LOCAL_VARIABLE:用于描述局部变量 
     * 4. METHOD:用于描述方法 
     * 5. PACKAGE:用于描述包 
     * 6. PARAMETER:用于描述参数 
     * 7. TYPE:用于描述类、接口(包括注解类型) 或enum声明
  * @Retention；
  * @Documented；
  * @Inherited 
  
* HTTP 请求的 GET 与 POST 方式的区别
  * Get:
  
·        GET请求能够被缓存

·        GET请求会保存在浏览器的浏览记录中

·        以GET请求的URL能够保存为浏览器书签

·        GET请求有长度限制

·        GET请求主要用以获取数据

  * Post:
  
·        POST请求不能被缓存下来

·        POST请求不会保存在浏览器浏览记录中

·        以POST请求的URL无法保存为浏览器书签

·        POST请求没有长度限制


* session 与 cookie 区别
   * session保存在服务器，客户端不知道其中的信息；cookie保存在客户端，服务端可以知道其中的信息
   * session中保存的是对象，cookie中保存的是字符串
   * session不能区分路径，同一个用户在访问一个网站期间，所有的session在任何一个地方都可以访问到；而cookie中如果设置了路径参数，那么同一个网站中不同路径下的cookie互相是访问不道德
   
* session 分布式处理
  * session同步法：多台web-server相互同步数据
  * 客户端存储法：一个用户只存储自己的数据
  * 反向代理hash一致性：四层hash和七层hash都可以做，保证一个用户的请求落在一台web-server上
  * 后端统一存储：web-server重启和扩容，session也不会丢失
  
* JDBC 流程
  * 加载JDBC驱动程序,Class.forName
  * 提供JDBC连接的URL,jdbc:mysql:
  * 创建数据库的连接,getConnection
  * 创建一个Statement 
     * 执行静态SQL语句。通常通过Statement实例实现。   
     * 执行动态SQL语句。通常通过PreparedStatement实例实现。   
     * 执行数据库存储过程。通常通过CallableStatement实例实现
  * 执行SQL语句,execute
  * 处理结果,getString 
  * 关闭JDBC对象,close
    
* MVC 设计思想
  * MVC是一个架构模式，它分离了表现与交互。它被分为三个核心部件：模型、视图、控制器
    * 所有的终端用户请求被发送到控制器。
    * 控制器依赖请求去选择加载哪个模型，并把模型附加到对应的视图。
    * 附加了模型数据的最终视图做为响应发送给终端用户。
    
* equals 与 == 的区别
  * equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自java.lang.Object类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。
  * == 比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。
 
**集合**

* List 和 Set 和Map区别

List：
 
1.可以允许重复的对象。   
2.可以插入多个null元素。   
3.是一个有序容器，保持了每个元素的插入顺序，输出的顺序就是插入的顺序。   
4.常用的实现类有 ArrayList、LinkedList 和 Vector。ArrayList 最为流行，它提供了使用索引的随意访问，而 LinkedList 则对于经常需要从 List 中添加或删除元素的场合更为合适。
        
Set：

1.不允许重复. 
2.无序容器，你无法保证每个元素的存储顺序，TreeSet通过 Comparator  或者 Comparable 维护了一个排序顺序。  
3.只允许一个 null 元素.  
4.Set 接口最流行的几个实现类是 HashSet、LinkedHashSet,TreeSet。最流行的是基于 HashMap 实现的 HashSet；TreeSet 还实现了 SortedSet 接口，因此 TreeSet 是一个根据其 compare() 和 compareTo() 的定义进行排序的有序容器。
        
Map:

1.List和Set集合继承Collection.  
2.Map集合不继承Collection.  
3.Map是一种以键值对形式存储的集合

* Arraylist 与 LinkedList 区别

1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。   
2.对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。   
3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。  

* ArrayList 与 Vector 区别

1）  Vector的方法都是同步的(Synchronized),是线程安全的(thread-safe)，而ArrayList的方法不是，由于线程的同步必然要影响性能，因此,ArrayList的性能比Vector好。   
2） 当Vector或ArrayList中的元素超过它的初始大小时,Vector会将它的容量翻倍,而ArrayList只增加50%的大小，这样,ArrayList就有利于节约内存空间。

* HashMap 和 Hashtable 的区别
  * Hashtable的方法是同步的，Hashmap的方法是不同步的，所以多线程场合要手动同步HashMap，这个区别就像是Vecgtor和ArrayList一样
  * Hashtable不允许Null值（Key 和Value都不行），Hashmap允许Null值（key和value可以）
  * 两个遍历方式有差别，Hashtable仅仅比HashMap多一个elements方法。hashtable和hashmap都可以通过values（）返回一个set，然后进行遍历处理
  * hashtable使用enumeration，hashmap使用iterator
  * 哈希值使用不同，hashtable直接使用对象的hashcode，而hashmap重新计算hash值，并且用于代替求模
  * hashtable中的hash数组默认大小为11，增加的方式是old*2+1,hashmap中hash数组默认是16，而且一定是2的指数
  * hashtable基于dictionary类，而hashmap基于abstractmap
  
* HashSet 和 HashMap 区别
 * HashMap实现了Map接口	HashSet实现了Set接口
 * HashMap储存键值对	HashSet仅仅存储对象
 * 使用put()方法将元素放入map中	使用add()方法将元素放入set中
 * HashMap中使用键对象来计算hashcode值	HashSet使用成员对象来计算hashcode值，对于两个对象来说hashcode可能相同，所以equals()方法用来判断对象的相等性，如果两个对象不同的话，那么返回false
HashMap比较快，因为是使用唯一的键来获取对象

* HashMap 和 ConcurrentHashMap 的区别
 * ConcurrentHashMap HashEntry中的value以及next都被volatile修饰 
 * 当链表长度过长的时候，会转换为TreeNode。但是与HashMap不相同的是，它并不是直接转换为红黑树，而是把这些结点包装成TreeNode放在TreeBin对象中，由TreeBin完成对红黑树的包装。而且TreeNode在ConcurrentHashMap集成自Node类，而并非HashMap中的集成自LinkedHashMap.Entry<K,V>类，也就是说TreeNode带有next指针，这样做的目的是方便基于TreeBin的访问。
 * TreeBin这个类并不负责包装用户的key、value信息，而是包装的很多TreeNode节点。它代替了TreeNode的根节点，也就是说在实际的ConcurrentHashMap“数组”中，存放的是TreeBin对象，而不是TreeNode对象，这个类还带有了读写锁
 * 支持多线程进行扩容，并发扩容
     * 第一部分是构建一个nextTable,它的容量是原来的两倍，这个操作是单线程完成的。这个单线程的保证是通过RESIZE_STAMP_SHIFT这个常量经过一次运算来保证的
     * 第二个部分就是将原来table中的元素复制到nextTable中，这里允许多线程进行操作。

`//如果遍历到的节点为空 则放入ForwardingNode
else if ((f = tabAt(tab, i)) == null)advance = casTabAt(tab, i, null, fwd);
//如果遍历到ForwardingNode节点  说明这个点已经被处理过了 直接跳过  这里是控制并发扩容的核心`

 * ConcurrentHashMap 使用3个CAS操作来确保node的一些操作的原子性，这种方式代替了锁。
* ConcurrentHashMap sizeCtl的不同值来代表不同含义，起到了控制的作用。
    * 负数代表正在进行初始化或扩容操作
    * -1代表正在初始化
    * -N 表示有N-1个线程正在进行扩容操作
    * 正数或0代表hash表还没有被初始化，这个数值表示初始化或下一次进行扩容的大小，这一点类似于扩容阈值的概念。它的值始终是当前ConcurrentHashMap容量的0.75倍，这与loadfactor是对应的。
* HashMap在JDK7和JDK8区别
 * jdk8table变node
 * jdk8 indefFor()方法消失了，直接用(tab.length-1)&hash
 * jdk8扰动函数变了
 * jdk7中resize，只有当 size>=threshold并且 table中的那个槽中已经有Entry时，才会发生resize。即有可能虽然size>=threshold，但是必须等到每个槽都至少有一个Entry时，才会扩容。
 * JDK7中HashMap采用的是位桶+链表的方式，而JDK8中采用的是位桶+链表/红黑树（单链表节点不小于8时变红黑树）（最大区别）
 * jdk8 treeifyBin()就是将链表转换成红黑树。
* HashMap 的工作原理及代码实现
* ConcurrentHashMap 的工作原理及代码实现

**线程**

* 创建线程的方式及实现
    * 继承Thread类创建线程类
    * 通过Runable接口创建线程类
    * 通过Callable和FutureTask创建线程
    * 通过线程池创建线程 
* sleep() 、join（）、yield（）有什么区别
    * join()方法会使当前线程等待调用join()方法的线程结束后才能继续执行
	 * sleep()方法需要指定等待的时间，它可以让当前正在执行的线程在指定的时间内暂停执行，进入阻塞状态，该方法既可以让其他同优先级或者高优先级的线程得到执行的机会，也可以让低优先级的线程得到执行机会。但是sleep()方法不会释放“锁标志”，也就是说如果有synchronized同步块，其他线程仍然不能访问共享数据。 
	 * wait()方法与sleep()方法的不同之处在于，wait()方法会释放对象的“锁标志”。当调用某一对象的wait()方法后，会使当前线程暂停执行，并将当前线程放入对象等待池中，直到调用了notify()方法后，将从对象等待池中移出任意一个线程并放入锁标志等待池中，只有锁标志等待池中的线程可以获取锁标志，它们随时准备争夺锁的拥有权。当调用了某个对象的notifyAll()方法，会将对象等待池中的所有线程都移动到该对象的锁标志等待池。
	   
* 说说 CountDownLatch 原理
    * 网址：https://www.cnblogs.com/200911/p/6059719.html
CountDownLatch 是一个同步工具类，允许一个线程或者多个线程等待其他线程完成操作，再执行。
    * CountDownLatch和CyclicBarrier的区别：
        * CountDownLatch 的作用是允许1或者多个线程，等待另外N个线程完成某件事情之后，这1个或者多个线程才能执行。
        * CyclicBarrier 是N个线程相互等待，任何一个线程完成任务之前，所有的线程必须等待。
        * CountDownLatch 计数器是一次性的，无法被重置的，而CyclicBarrier的计数器在调用reset方法之后，还可以重新使用，因此被称为循环的barrier。
        
* 说说 CyclicBarrier 原理
* 说说 Semaphore 原理
     * Semaphore是计数信号量。Semaphore管理一系列许可证。每个acquire方法阻塞，直到有一个许可证可以获得然后拿走一个许可证；每个release方法增加一个许可证，这可能会释放一个阻塞的acquire方法。然而，其实并没有实际的许可证这个对象，Semaphore只是维持了一个可获得许可证的数量。
     * Semaphore经常用于限制获取某种资源的线程数量。下面举个例子，比如说操场上有5个跑道，一个跑道一次只能有一个学生在上面跑步，一旦所有跑道在使用，那么后面的学生就需要等待，直到有一个学生不跑了，
     
* 说说 Exchanger 原理
     * 网址：https://www.cnblogs.com/zaizhoumo/p/7787169.html
     * 用于线程间数据的交换。它提供一个同步点，在这个同步点，两个线程可以交换彼此的数据。这两个线程通过exchange方法交换数据，如果第一个线程先执行exchange()方法，它会一直等待第二个线程也执行exchange方法，当两个线程都到达同步点时，这两个线程就可以交换数据，将本线程生产出来的数据传递给对方。
     * Exchanger 可被视为 SynchronousQueue 的双向形式
     * Exchanger在遗传算法和管道设计等应用中很有用。
     * 内存一致性：对于通过 Exchanger 成功交换对象的每对线程，每个线程中在 exchange() 之前的操作 happen-before 从另一线程中相应的 exchange() 返回的后续操作。
* 说说 CountDownLatch 与 CyclicBarrier 区别
* ThreadLocal 原理分析
    * https://www.cnblogs.com/xzwblog/p/7227509.html
    * 局部线程变量
      * 网址：https://blog.csdn.net/lhqj1992/article/details/52451136
      * 概述：
      * 翻译过来的大概意思就是：ThreadLocal类用来提供线程内部的局部变量。这些变量在多线程环境下访问(通过get或set方法访问)时能保证各个线程里的变量相对独立于其他线程内的变量，ThreadLocal实例通常来说都是private static类型。
      * 总结：ThreadLocal不是为了解决多线程访问共享变量，而是为每个线程创建一个单独的变量副本，提供了保持对象的方法和避免参数传递的复杂性。
      * ThreadLocal的主要应用场景为按线程多实例（每个线程对应一个实例）的对象的访问，并且这个对象很多地方都要用到。例如：同一个网站登录用户，每个用户服务器会为其开一个线程，每个线程中创建一个ThreadLocal，里面存用户基本信息等，在很多页面跳转时，会显示用户信息或者得到用户的一些信息等频繁操作，这样多线程之间并没有联系而且当前线程也可以及时获取想要的数据。
    * 实现原理ThreadLocal可以看做是一个容器，容器里面存放着属于当前线程的变量。ThreadLocal类提供了四个对外开放的接口方法，这也是用户操作ThreadLocal类的基本方法：
      * void set(Object value)设置当前线程的线程局部变量的值。
      * public Object get()该方法返回当前线程所对应的线程局部变量。
      * public void remove()将当前线程局部变量的值删除，目的是为了减少内存的占用，该方法是JDK 5.0新增的方法。需要指出的是，当线程结束后，对应该线程的局部变量将自动被垃圾回收，所以显式调用该方法清除线程的局部变量并不是必须的操作，但它可以加快内存回收的速度。
      * protected Object initialValue()返回该线程局部变量的初始值，该方法是一个protected的方法，显然是为了让子类覆盖而设计的。这个方法是一个延迟调用方法，在线程第1次调用get()或set(Object)时才执行，并且仅执行1次，ThreadLocal中的缺省实现直接返回一个null。
      * 可以通过上述的几个方法实现ThreadLocal中变量的访问，数据设置，初始化以及删除局部变量，那ThreadLocal内部是如何为每一个线程维护变量副本的呢？
      * 其实在ThreadLocal类中有一个静态内部类ThreadLocalMap(其类似于Map)，用键值对的形式存储每一个线程的变量副本，ThreadLocalMap中元素的key为当前ThreadLocal对象，而value对应线程的变量副本，每个线程可能存在多个ThreadLocal。
   * 内存泄漏问题（参考其他博文）
       * 在上面提到过，每个thread中都存在一个map, map的类型是ThreadLocal.ThreadLocalMap. Map中的key为一个threadlocal实例. 这个Map的确使用了弱引用,不过弱引用只是针对key. 每个key都弱引用指向threadlocal. 当把threadlocal实例置为null以后,没有任何强引用指向threadlocal实例,所以threadlocal将会被gc回收. 但是,我们的value却不能回收,因为存在一条从current thread连接过来的强引用. 只有当前thread结束以后, current thread就不会存在栈中,强引用断开, Current Thread, Map, value将全部被GC回收.
       * 所以得出一个结论就是只要这个线程对象被gc回收，就不会出现内存泄露，但在threadLocal设为null和线程结束这段时间不会被回收的，就发生了我们认为的内存泄露。其实这是一个对概念理解的不一致，也没什么好争论的。最要命的是线程对象不被回收的情况，这就发生了真正意义上的内存泄露。比如使用线程池的时候，线程结束是不会销毁的，会再次使用的。就可能出现内存泄露。
       
* 讲讲线程池的实现原理
   * 网址：https://blog.csdn.net/gol_phing/article/details/49032055
   * 在面向对象编程中，创建和销毁对象是很费时间的，因为创建一个对象要获取内存资源或者其它更多资源。在Java中更是如此，虚拟机将试图跟踪每一个对象，以便能够在对象销毁后进行垃圾回收。
   * 所以提高服务程序效率的一个手段就是尽可能减少创建和销毁对象的次数，特别是一些很耗资源的对象创建和销毁。如何利用已有对象来服务就是一个需要解决的关键问题，其实这就是一些”池化资源”技术产生的原因。
   * 例如Android中常见到的很多通用组件一般都离不开”池”的概念，如各种图片加载库，网络请求库，即使Android的消息传递机制中的Meaasge当使用Meaasge.obtain()就是使用的Meaasge池中的对象，因此这个概念很重要。本文将介绍的线程池技术同样符合这一思想。
   * 线程池的优点:
重用线程池中的线程,减少因对象创建,销毁所带来的性能开销;
能有效的控制线程的最大并发数,提高系统资源利用率,同时避免过多的资源竞争,避免堵塞
能够多线程进行简单的管理,使线程的使用简单、高效。
   * 线程池框架Executor
java中的线程池是通过Executor框架实现的，Executor 框架包括类：Executor，Executors，ExecutorService，ThreadPoolExecutor ，Callable和Future、FutureTask的使用等。

   * ThreadPoolExecutor类构造器语法形式ThreadPoolExecutor（corePoolSize,maxPoolSize,keepAliveTime,timeUnit,workQueue,threadFactory,handle);
     *  方法参数：
         *  corePoolSize：核心线程数
         *  maxPoolSize：最大线程数
         *  keepAliveTime：线程存活时间corePore<*<maxPoolSize情况下有用）
         *  timeUnit：存活时间的时间单位
         *  workQueue：阻塞队列（用来保存等待被执行的任务
         
* 线程池的几种方式
   * 网址：https://www.cnblogs.com/aaron911/p/6213808.html
   * 常用的几种线程池
       * newCachedThreadPool
           * 创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。
           * 这种类型的线程池特点是：
              * 工作线程的创建数量几乎没有限制(其实也有限制的,数目为Interger. MAX_VALUE), 这样可灵活的往线程池中添加线程。
              * 如果长时间没有往线程池中提交任务，即如果工作线程空闲了指定的时间(默认为1分钟)，则该工作线程将自动终止。终止后，如果你又提交了新的任务，则线程池重新创建一个工作线程。
              * 在使用CachedThreadPool时，一定要注意控制任务的数量，否则，由于大量线程同时运行，很有会造成系统瘫痪。
        * newFixedThreadPool
            * 创建一个指定工作线程数量的线程池。每当提交一个任务就创建一个工作线程，如果工作线程数量达到线程池初始的最大数，则将提交的任务存入到池队列中。
        * FixedThreadPool
            * 是一个典型且优秀的线程池，它具有线程池提高程序效率和节省创建线程时所耗的开销的优点。但是，在线程池空闲时，即线程池中没有可运行任务时，它不会释放工作线程，还会占用一定的系统资源。
        * newSingleThreadExecutor
            * 创建一个单线程化的Executor，即只创建唯一的工作者线程来执行任务，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。如果这个线程异常结束，会有另一个取代它，保证顺序执行。单工作线程最大的特点是可保证顺序地执行各个任务，并且在任意给定的时间不会有多个线程是活动的。

        * newScheduleThreadPool
            * 创建一个定长的线程池，而且支持定时的以及周期性的任务执行，支持定时及周期性任务执行。

* 线程的生命周期
   * 网址
   * https://blog.csdn.net/pange1991/article/details/53860651
   * 大体可分为5种状态。
      * 新建(NEW)：新创建了一个线程对象。
      * 可运行(RUNNABLE)：线程对象创建后，其他线程(比如main线程）调用了该对象的start()方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取cpu 的使用权 。
      * 运行(RUNNING)：可运行状态(runnable)的线程获得了cpu 时间片（timeslice） ，执行程序代码。
      * 阻塞(BLOCKED)：阻塞状态是指线程因为某种原因放弃了cpu 使用权，也即让出了cpu timeslice，暂时停止运行。直到线程进入可运行(runnable)状态，才有机会再次获得cpu timeslice 转到运行(running)状态。
    * 阻塞的情况分三种：
      * 等待阻塞：运行(running)的线程执行o.wait()方法，JVM会把该线程放入等待队列(waitting queue)中。
      * 同步阻塞：运行(running)的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池(lock pool)中。
      * 其他阻塞：运行(running)的线程执行Thread.sleep(long ms)或t.join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入可运行(runnable)状态。
      * 死亡(DEAD)：线程run()、main() 方法执行结束，或者因异常退出了run()方法，则该线程结束生命周期。死亡的线程不可再次复生。

![](https://note.youdao.com/yws/public/resource/857e1d9dbf63d5b27bcb1702160fa40b/xmlnote/9B39469515B84092A6E1BB5F21629C26/2062)

**锁机制**

* 说说线程安全问题
* volatile 实现原理
* synchronize 实现原理
* synchronized 与 lock 的区别
* CAS 乐观锁
* ABA 问题
* 乐观锁的业务场景及实现方式


* 说说线程安全问题
https://www.cnblogs.com/IUbanana/p/7112296.html

什么是线程安全

多个线程在执行同一段代码的时候，每次的执行结果和单线程执行的结果都是一样的，不存在执行结果的二义性，就可以称作是线程安全的。

是指多线程环境下对共享资源的访问可能会引起此共享资源的不一致性。因此，为避免线程安全问题，应该避免多线程环境下对此共享资源的并发访问。
线程安全问题多是由全局变量和静态变量引起的，当多个线程对共享数据只执行读操作，不执行写操作时，一般是线程安全的；当多个线程都执行写操作时，需要考虑线程同步来解决线程安全问题。

线程同步（synchronized/lock）
线程同步：将操作共享数据的代码行作为一个整体，同一时间只允许一个线程执行，执行过程中其他线程不能参与执行。目的是为了防止多个线程访问一个数据对象时，对数据造成的破坏。

同步方法（synchronized）

对共享资源进行访问的方法定义中加上synchronized关键字修饰，使得此方法称为同步方法。可以简单理解成对此方法进行了加锁，其锁对象为当前方法所在的对象自身。多线程环境下，当执行此方法时，首先都要获得此同步锁（且同时最多只有一个线程能够获得），只有当线程执行完此同步方法后，才会释放锁对象，其他的线程才有可能获取此同步锁，以此类推..


同步代码块（synchronized）

使用同步方法时，使得整个方法体都成为了同步执行状态，会使得可能出现同步范围过大的情况，于是，针对需要同步的代码可以直接另一种同步方式——同步代码块来解决。

同步锁（Lock）

使用Lock对象同步锁可以方便地解决选择锁对象的问题，唯一需要注意的一点是Lock对象需要与资源对象同样具有一对一的关系。Lock对象同步锁一般格式为：


什么时候需要同步：

可见性同步：在以下情况中必须同步： 
1）读取上一次可能是由另一个线程写入的变量 ；
2）写入下一次可能由另一个线程读取的变量

一致性同步：当修改多个相关值时，您想要其它线程原子地看到这组更改—— 要么看到全部更改，要么什么也看不到。
这适用于相关数据项（如粒子的位置和速率）和元数据项（如链表中包含的数据值和列表自身中的数据项的链）。
在某些情况中，您不必用同步来将数据从一个线程传递到另一个，因为 JVM 已经隐含地为您执行同步。

这些情况包括：

由静态初始化器（在静态字段上或 static{} 块中的初始化器）
初始化数据时
访问 final 字段
在创建线程之前创建对象时
线程可以看见它将要处理的对象时
锁的原理：
Java中每个对象都有一个内置锁
当程序运行到非静态的synchronized同步方法上时，自动获得与正在执行代码类的当前实例（this实例）有关的锁。获得一个对象的锁也称为获取锁、锁定对象、在对象上锁定或在对象上同步。
当程序运行到synchronized同步方法或代码块时才该对象锁才起作用。
一个对象只有一个锁。所以，如果一个线程获得该锁，就没有其他线程可以获得锁，直到第一个线程释放（或返回）锁。这也意味着任何其他线程都不能进入该对象上的synchronized方法或代码块，直到该锁被释放。
释放锁是指持锁线程退出了synchronized同步方法或代码块。

锁的类型

公平锁/非公平锁
非公平锁是指多个线程获取锁的顺序并不是按照申请锁的顺序，有可能后申请的线程比先申请的线程优先获取锁。有可能，会造成优先级反转或者饥饿现象。

可重入锁
可重入锁又名递归锁，是指在同一个线程在外层方法获取锁的时候，在进入内层方法会自动获取锁。

独享锁/共享锁
独享锁是指该锁一次只能被一个线程所持有。共享锁是指该锁可被多个线程所持有。

锁与同步要点：


只能同步方法，而不能同步变量和类；
每个对象只有一个锁；当提到同步时，应该清楚在什么上同步？也就是说，在哪个对象上同步？

不必同步类中所有的方法，类可以同时拥有同步和非同步方法。

如果两个线程要执行一个类中的synchronized方法，并且两个线程使用相同的实例来调用方法，那么一次只能有一个线程能够执行方法，另一个需要等待，直到锁被释放。也就是说：如果一个线程在对象上获得一个锁，就没有任何其他线程可以进入（该对象的）类中的任何一个同步方法。

如果线程拥有同步和非同步方法，则非同步方法可以被多个线程自由访问而不受锁的限制。

线程睡眠时，它所持的任何锁都不会释放。
线程可以获得多个锁。比如，在一个对象的同步方法里面调用另外一个对象的同步方法，则获取了两个对象的同步锁。

同步损害并发性，应该尽可能缩小同步范围。同步不但可以同步整个方法，还可以同步方法中一部分代码块。
在使用同步代码块时候，应该指定在哪个对象上同步，也就是说要获取哪个对象的锁。

同步静态方法，需要一个用于整个类对象的锁，这个对象是就是这个类（XXX.class)。

线程不能获得锁会怎么样：如果线程试图进入同步方法，而其锁已经被占用，则线程在该对象上被阻塞。实质上，线程进入该对象的的一种池中，必须在哪里等待，直到其锁被释放，该线程再次变为可运行或运行为止。
线程死锁：当两个线程被阻塞，每个线程都在等待另一个线程时就发生死锁。有一些设计方法能帮助避免死锁，如始终按照预定义的顺序获取锁这一策略。

线程同步小结

线程同步的目的是为了保护多个线程反问一个资源时对资源的破坏。
线程同步方法是通过锁来实现，每个对象都有且仅有一个锁，这个锁与一个特定的对象关联，线程一旦获取了对象锁，其他访问该对象的线程就无法再访问该对象的其他同步方法。

对于静态同步方法，锁是针对这个类的，锁对象是该类的Class对象。静态和非静态方法的锁互不干预。一个线程获得锁，当在一个同步方法中访问另外对象上的同步方法时，会获取这两个对象锁。

对于同步，要时刻清醒在哪个对象上同步，这是关键。
编写线程安全的类，需要时刻注意对多个线程竞争访问资源的逻辑和安全做出正确的判断，对“原子”操作做出分析，并保证原子操作期间别的线程无法访问竞争资源。

当多个线程等待一个对象锁时，没有获取到锁的线程将发生阻塞。
死锁是线程间相互等待锁锁造成的，在实际中发生的概率非常的小。真让你写个死锁程序，不一定好使，呵呵。但是，一旦程序发生死锁，程序将死掉。

* volatile 实现原理

网址
http://ifeve.com/volatile/
https://www.cnblogs.com/chenssy/p/6379280.html

volatile作用

保证可见性

保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量的值，这新值对其他线程来说是立即可见的。
禁止进行指令重排序。
不能保证原子性（但可以通过synchronized和lock进行加锁）

保证有序性

禁止指令重排序有两层意思：
当程序执行到volatile变量的读操作或者写操作时，在其前面的操作的更改肯定全部已经进行，且结果已经对后面的操作可见；在其后面的操作肯定还没有进行；
在进行指令优化时，不能将在对volatile变量的读操作或者写操作的语句放在其后面执行，也不能把volatile变量后面的语句放到其前面执行。

volatile实现原理

网站
http://ifeve.com/volatile/（涉及到汇编）
https://www.cnblogs.com/paddix/p/5428507.html

可见性实现

线程本身并不直接与主内存进行数据的交互，而是通过线程的工作内存来完成相应的操作。这也是导致线程间数据不可见的本质原因。因此要实现volatile变量的可见性，直接从这方面入手即可。对volatile变量的写操作与普通变量的主要

区别有两点：

修改volatile变量时会强制将修改后的值刷新的主内存中。

修改volatile变量后会导致其他线程工作内存中对应的变量值失效。因此，再读取该变量值的时候就需要重新从读取主内存中的值。　　

通过这两个操作，就可以解决volatile变量的可见性问题。

有序性实现

Happen-before规则

通俗一点说就是如果a happen-before b，则a所做的任何操作对b是可见的。（这一点大家务必记住，因为happen-before这个词容易被误解为是时间的前后）

同一个线程中的，前面的操作 happen-before 后续的操作。（即单线程内按代码顺序执行。但是，在不影响在单线程环境执行结果的前提下，编译器和处理器可以进行重排序，这是合法的。换句话说，这一是规则无法保证编译重排和指令重排）。

监视器上的解锁操作 happen-before 其后续的加锁操作。（Synchronized 规则）

对volatile变量的写操作 happen-before 后续的读操作。（volatile 规则）（重排序分为编译器重排序和处理器重排序。为了实现volatile内存语义，JMM会对volatile变量限制这两种类型的重排序。下面是JMM针对volatile变量所规定的重排序规则表：）

线程的start() 方法 happen-before 该线程所有的后续操作。（线程启动规则）

线程所有的操作 happen-before 其他线程在该线程上调用 join 返回成功后的操作。

如果 a happen-before b，b happen-before c，则a happen-before c（传递性）。

内存屏障

为了实现volatile可见性和happen-befor的语义。JVM底层是通过一个叫做“内存屏障”的东西来完成。内存屏障，也叫做内存栅栏，是一组处理器指令，用于实现对内存操作的顺序限制。

下面是完成上述规则所要求的内存屏障：

使用条件

要使 volatile 变量提供理想的线程安全，必须同时满足下面两个条件：
对变量的写操作不依赖于当前值

该变量没有包含在具有其他变量的不变式中。

实际上，这些条件表明，可以被写入 volatile 变量的这些有效值独立于任何程序的状态，包括变量的当前状态。第一个条件的限制使 volatile 变量不能用作线程安全计数器。虽然增量操作（x++）看上去类似一个单独操作，实际上它是一个由（读取－修改－写入）操作序列组成的组合操作，必须以原子方式执行，而 volatile 不能提供必须的原子特性。实现正确的操作需要使x 的值在操作期间保持不变，而 volatile 变量无法实现这点。（然而，如果只从单个线程写入，那么可以忽略第一个条件。）

反例

大多数编程情形都会与这两个条件的其中之一冲突，使得 volatile 变量不能像 synchronized 那样普遍适用于实现线程安全。

* synchronize 实现原理

网址
http://www.cnblogs.com/chenssy/p/4701027.html

http://www.cnblogs.com/GnagWang/archive/2011/02/27/1966606.html

http://blog.csdn.net/javazejian/article/details/72828483

synchronized的三种应用方式

修饰实例方法，作用于当前实例加锁，进入同步代码前要获得当前实例的锁
所谓的实例对象锁就是用synchronized修饰实例对象中的实例方法，注意是实例方法不包括静态方法

当一个线程正在访问一个对象的 synchronized 实例方法，那么其他线程不能访问该对象的其他 synchronized 方法，毕竟一个对象只有一把锁，当一个线程获取了该对象的锁之后，其他线程无法获取该对象的锁，所以无法访问该对象的其他synchronized实例方法，但是其他线程还是可以访问该实例对象的其他非synchronized方法，当然如果是一个线程 A 需要访问实例对象 obj1 的 synchronized 方法 f1(当前对象锁是obj1)，另一个线程 B 需要访问实例对象 obj2 的 synchronized 方法 f2(当前对象锁是obj2)，这样是允许的，因为两个实例对象锁并不同相同，此时如果两个线程操作数据并非共享的，线程安全是有保障的，遗憾的是如果两个线程操作的是共享数据，那么线程安全就有可能无法保证了

修饰静态方法，作用于当前类对象加锁，进入同步代码前要获得当前类对象的锁
当synchronized作用于静态方法时，其锁就是当前类的class对象锁。由于静态成员不专属于任何一个实例对象，是类成员，因此通过class对象锁可以控制静态 成员的并发操作。

需要注意的是如果一个线程A调用一个实例对象的非static synchronized方法，而线程B需要调用这个实例对象所属类的静态 synchronized方法，是允许的，不会发生互斥现象，因为访问静态 synchronized 方法占用的锁是当前类的class对象，而访问非静态 synchronized 方法占用的锁是当前实例对象锁，

修饰代码块，指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁。

在某些情况下，我们编写的方法体可能比较大，同时存在一些比较耗时的操作，而需要同步的代码又只有一小部分，如果直接对整个方法进行同步操作，可能会得不偿失，此时我们可以使用同步代码块的方式对需要同步的代码进行包裹，这样就无需对整个方法进行同步操作了

synchronize底层语义原理

http://blog.csdn.net/javazejian/article/details/72828483

final域

final域的重排序规则

在构造函数内对一个final域的写入，与将final对象赋值给引用变量，这两个操作之间不能重排序
初次读取final域的对象引用，与初次读取final域对象，这两个操作之间不能重排序

写final域的重排序规则

JMM禁止编译器把final域的写重排序到构造函数之外
JMM会在final域的写之后，构造函数return之前，插入一个storestore屏障。禁止final域的写重排序到构造函数之外
写final域的重排序规则确保：在对象引用为任意线程可用之前，对象的final域已经被正确初始化，普通域不具有这个保障。

读final域的重排序规则

读final域的重排序规则保证：在读一个final域之前，一定先读该final域的对象的引用。

final域为引用类型

在构造函数内对一个final引用的对象的成员域的写入，与随后在构造函数外把构造的对象的引用赋值给一个引用变量，这两个操作之间不能重排序。


JSR-133为什么要增强final语义

只要对象是正确构造的（被构造对象的引用在构造函数中没有溢出），那么不需要使用同步（指lock与volatile的使用）就可以保证任意函数都可以看到final域在构造函数内被初始化后的值。

* synchronized 与 lock 的区别

网址
https://www.cnblogs.com/handsomeye/p/5999362.html

区别

Lock是一个接口，而synchronized是Java中的关键字，synchronized是内置的语言实现，synchronized是在JVM层面上实现的，不但可以通过一些监控工具监控synchronized的锁定，而且在代码执行时出现异常，JVM会自动释放锁定，但是使用Lock则不行，lock是通过代码实现的，要保证锁定一定会被释放，就必须将 unLock()放到finally{} 中；

synchronized在发生异常时，会自动释放线程占有的锁，因此不会导致死锁现象发生；

而Lock在发生异常时，如果没有主动通过unLock()去释放锁，则很可能造成死锁现象，因此使用Lock时需要在finally块中释放锁；

Lock可以让等待锁的线程响应中断，线程可以中断去干别的事务，而synchronized却不行，使用synchronized时，等待的线程会一直等待下去，不能够响应中断；

通过Lock可以知道有没有成功获取锁，而synchronized却无法办到。
Lock可以提高多个线程进行读操作的效率。

在性能上来说，如果竞争资源不激烈，两者的性能是差不多的，而当竞争资源非常激烈时（即有大量线程同时竞争），此时Lock的性能要远远优于synchronized。

所以说，在具体使用时要根据适当情况选择。

举个例子：当有多个线程读写文件时，读操作和写操作会发生冲突现象，写操作和写操作会发生冲突现象，但是读操作和读操作不会发生冲突现象。

但是采用synchronized关键字来实现同步的话，就会导致一个问题：

如果多个线程都只是进行读操作，所以当一个线程在进行读操作时，其他线程只能等待无法进行读操作。

因此就需要一种机制来使得多个线程都只是进行读操作时，线程之间不会发生冲突，通过Lock就可以办到。

另外，通过Lock可以知道线程有没有成功获取到锁。这个是synchronized无法办到的

* synchronized与volatile

synchronized关键字解决的是执行控制的问题，它会阻止其它线程获取当前对象的监控锁，这样就使得当前对象中被synchronized关键字保护的代码块无法被其它线程访问，也就无法并发执行。更重要的是，synchronized还会创建一个内存屏障，内存屏障指令保证了所有CPU操作结果都会直接刷到主存中，从而保证了操作的内存可见性，同时也使得先获得这个锁的线程的所有操作，都happens-before于随后获得这个锁的线程的操作。

volatile主要用在多个线程感知实例变量被更改了场合，从而使得各个线程获得最新的值。它强制线程每次从主内存中讲到变量，而不是从线程的私有内存中读取变量，从而保证了数据的可见性。

比较：
volatile轻量级，只能修饰变量。synchronized重量级，还可修饰方法
volatile只能保证数据的可见性，不能用来同步，因为多个线程并发访问volatile修饰的变量不会阻塞。

synchronized不仅保证可见性，而且还保证原子性，因为，只有获得了锁的线程才能进入临界区，从而保证临界区中的所有语句都全部执行。多个线程争抢synchronized锁对象时，会出现阻塞。

volatile本质是在告诉jvm当前变量在寄存器（工作内存）中的值是不确定的，需要从主存中读取； synchronized则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。

volatile不会造成线程的阻塞；synchronized可能会造成线程的阻塞。

volatile标记的变量不会被编译器优化；synchronized标记的变量可以被编译器优化

* CAS 乐观锁

网址
https://www.cnblogs.com/qjjazry/p/6581568.html

乐观锁和悲观锁：

悲观锁：总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁。传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。再比如Java里面的同步原语synchronized关键字的实现也是悲观锁。　

乐观锁：顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于write_condition机制，其实都是提供的乐观锁。

在Java中java.util.concurrent.atomic包下面的原子变量类就是使用了乐观锁的一种实现方式CAS实现的。

乐观锁的一种实现方式-CAS(Compare and Swap 比较并交换)：

锁存在的问题:

Java在JDK1.5之前都是靠 synchronized关键字保证同步的，这种通过使用一致的锁定协议来协调对共享状态的访问，可以确保无论哪个线程持有共享变量的锁，都采用独占的方式来访问这些变量。这就是一种独占锁，独占锁其实就是一种悲观锁，所以可以说synchronized 是悲观锁。

悲观锁机制存在以下问题：　
　
在多线程竞争下，加锁、释放锁会导致比较多的上下文切换和调度延时，引起性能问题。

一个线程持有锁会导致其它所有需要此锁的线程挂起。

如果一个优先级高的线程等待一个优先级低的线程释放锁会导致优先级倒置，引起性能风险。

对比于悲观锁的这些问题，另一个更加有效的锁就是乐观锁。其实乐观锁就是：每次不加锁而是假设没有并发冲突而去完成某项操作，如果因为并发冲突失败就重试，直到成功为止。

乐观锁：

乐观锁（ Optimistic Locking ）在上文已经说过了，其实就是一种思想。相对悲观锁而言，乐观锁假设认为数据一般情况下不会产生并发冲突，所以在数据进行提交更新的时候，才会正式对数据是否产生并发冲突进行检测，如果发现并发冲突了，则让返回用户错误的信息，让用户决定如何去做。

上面提到的乐观锁的概念中其实已经阐述了它的具体实现细节：主要就是两个步骤：冲突检测和数据更新。其实现方式有一种比较典型的就是 Compare and Swap ( CAS )。

CAS：

CAS是乐观锁技术，当多个线程尝试使用CAS同时更新同一个变量时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。
　　　
CAS 操作中包含三个操作数 —— 需要读写的内存位置（V）、进行比较的预期原值（A）和拟写入的新值(B)。如果内存位置V的值与预期原值A相匹配，那么处理器会自动将该位置值更新为新值B。否则处理器不做任何操作。无论哪种情况，它都会在 CAS 指令之前返回该位置的值。（在 CAS 的一些特殊情况下将仅返回 CAS 是否成功，而不提取当前值。）CAS 有效地说明了“ 我认为位置 V 应该包含值 A；如果包含该值，则将 B 放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可。 ”这其实和乐观锁的冲突检查+数据更新的原理是一样的。这里再强调一下，乐观锁是一种思想。CAS是这种思想的一种实现方式。

ABA 问题（乐观锁缺点）

　比如说一个线程one从内存位置V中取出A，这时候另一个线程two也从内存中取出A，并且two进行了一些操作变成了B，然后two又将V位置的数据变成A，这时候线程one进行CAS操作发现内存中仍然是A，然后one操作成功。尽管线程one的CAS操作成功，但可能存在潜藏的问题。如下所示：

现有一个用单向链表实现的堆栈，栈顶为A，这时线程T1已经知道A.next为B，然后希望用CAS将栈顶替换为B：head.compareAndSet(A,B);
在T1执行上面这条指令之前，线程T2介入，将A、B出栈，再pushD、C、A，此时堆栈结构如下图，而对象B此时处于游离状态：

此时轮到线程T1执行CAS操作，检测发现栈顶仍为A，所以CAS成功，栈顶变为B，但实际上B.next为null，所以此时的情况变为：

其中堆栈中只有B一个元素，C和D组成的链表不再存在于堆栈中，平白无故就把C、D丢掉了。

* 乐观锁的业务场景及实现方式

乐观锁：比较适合读取操作比较频繁的场景，如果出现大量的写入操作，数据发生冲突的可能性就会增大，为了保证数据的一致性，应用层需要不断的重新获取数据，这样会增加大量的查询操作，降低了系统的吞吐量。
实现方式
CAS


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

