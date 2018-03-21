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

