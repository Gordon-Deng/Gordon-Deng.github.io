---
layout:     post
title:      "metaq对比kafka"
subtitle:   "\"消息队列小思考\""
date:       2024-03-20 12:00:00
author:     "Gordon"
header-img: "img/in-post/2020-01-20-todo/todo-bg.jpg"
catalog: true
tags:
    - 消息队列
---


# 消息队列

消息队列是一个用于接收消息、存储消息并且转发消息的中间件，主要是用于解决如下的场景：

* 异步：A服务做了一些事情，异步发送消息给服务B；
* 削峰/限流：类似一个蓄水池，比如说有些服务（例如电商服务的秒杀），请求量很高，服务端处理不过来，那么请求先放到消息队列里面，然后服务端按照自己的能力来消费处理；
* 解耦：应用之间减少代码的耦合，使得应用的部署更加灵活；
 

消息队列有几个重要的概念模型：消息、队列、生产者、消费者，下面将介绍这几个基本概念：

* 消息：消息是消息队列中的最基本概念，其本质上是一段数据，能够被多个应用程序所理解，是应用程序之间传递信息的载体，消息一般是由消息描述符和消息体组成；
* 队列：队列是一种先进先出的数据结构，队列是由队列头部和队列尾部组成，一般需要在队列尾部进行插入，在队列头部进行删除；
* 生产者：生产者主要是用来产生消息，并将消息放入队列的尾部；
* 消费者：消费者主要是用来消费队列头部的消息；
 

# MetaQ介绍

目前常用的消息中间件有kafka、RocketMQ和ActiveMQ等；今天我们将介绍MetaQ，MetaQ也是消息队列中间件，属于阿里内部的RocketMQ，下面将介绍MetaQ的相关概念：


## NameServer

命名服务，内部维护了topic和broker之间的对应关系，并且和所有broker保持心跳连接，在producer和consumer需要发布或者消费消息的时候，向nameserver发出请求来获取连接的broker的信息；

NameServer可以部署多个，每个之间互相独立，其他角色同时向多个NameServer机器上报状态信息，从而达到热备份的目的；

NameServer类似kafka中zookeeper的角色，那为什么不直接采用ZooKeeper角色呢，那是因为ZooKeeper有自动选举Master的功能，MetaQ的架构设计上决定了它不需要进行Master选举，而只需要使用一个轻量级的元数据服务器就可以了。

 

## Broker

MetaQ的服务器，负责消息的中转、存储和转发，Broker可以分为Master和Slave，一个Master可以对接多个Slave，但是一个Slave只能对接一个Master，Master与Slave之间可以通过指定相同的BrokerName，不同的BrokerId来定义，BrokerId为0表示Master，不为0的表示Slave。

Master可以部署多个，每个Broker和NameServer集群中的所有节点建立长连接，定期的注册Topic信息到所有的NameServer上。

消息会发送到Master上，一旦Master上面记录成功，就直接返回成功，不用等待slave上面是否记录成功，slave会定时的去获取消息记录，所以slave和master上面会有一些时间差异；slave可以作为consumer的服务提供者，意思就是如果写入必须通过master，消费的时候则可以直接从slave上面获取。Master和slave都需要注册到nameserver上面，一旦master无法使用，客户端可以使用与之对应的slave。

每个Broker与Name Server集群中的所有节点建立长连接，定时(每隔30s)注册Topic信息到所有Name Server。Name Server定时(每隔10s)扫描所有存活broker的连接，如果Name Server超过2分钟没有收到心跳，则Name Server断开与Broker的连接。


## Topic

Topic，即为发布或者订阅的主题，topic一般由多个队列组成，队列会平均的散列到多个Broker上面。Producer的发送机制会保证消息尽量平均的散列到所有队列上面去，最终的效果是所有的消息会平均的落在每个Broker上面。

Tag属于子Topic，主要的作用是给业务提供更大的灵活性，用以分流信息。

## Producer

Producer，即消息的生产者，负责生产消息，producer的和Name server集群中随机的一个节点建立长连接，定期从nameServer中获取Topic路由信息，并向提供topic服务的master broker建立长连接，并定时向master发送心跳。producer会发布消息到master上面，然后由master同步给所有的slave。

Producer每隔30s从Name server获取所有topic队列的最新情况，这意味着如果Broker不可用，Producer最多30s能够感知，在此期间内发往Broker的所有消息都会失败。

Producer每隔30s向所有关联的broker发送心跳，Broker每隔10s中扫描所有存活的连接，如果Broker在2分钟内没有收到心跳数据，则关闭与Producer的连接。


## Consumer

Consumer，即消息的消费者，负责消费消息，consumer与nameserver集群中的随机一个节点建立长连接，定期的从nameServer中获取topic路由信息，并向提供Topic服务的Master、Slave建立长连接，并且定时向Master、Slave发送心跳。Consumer既可以从Master上面订阅消息，也可以从Slave上面订阅消息，订阅规则由Broker配置决定。

Consumer每隔30s从Name server获取topic的最新队列情况，这意味着Broker不可用时，Consumer最多最需要30s才能感知。

Consumer每隔30s（由ClientConfig中heartbeatBrokerInterval决定）向所有关联的broker发送心跳，Broker每隔10s扫描所有存活的连接，若某个连接2分钟内没有发送心跳数据，则关闭连接；并向该Consumer Group的所有Consumer发出通知，Group内的Consumer重新分配队列，然后继续消费。


## ConsumerGroup
ConsumerGroup，即消费者集群，多个消费者可以组成一个分组，拥有一个共同的分组名称，来共同消费一个topic下的消息，每个消费者消费部分消息。

## Message
Message，即生产或者消费的消息，负载用户的数据并且在producer、broker和consumer之间传输。

## Offset
消息在Broker上的每个分区都是组织成一个文件列表，消费者拉取数据的时候需要知道数据在文件中的偏移量，这个偏移量就是offset。Offset是一个绝对的偏移量，服务器会将offset转化为具体文件的相对偏移量。

# Kafka和MetaQ之对比

## Kafka和MetaQ存储机制

### Kafka存储机制

Kafka和MetaQ一样，都是采用topic作为发布和订阅的主题，topic是个逻辑概念，而partition是物理上面的概念，每个partition对应一个log文件，该log文件中存储的就是producer生产的数据。producer生产的数据会被不断追加到log文件的末端，且每条数据都有自己的offset。

每个Partition都会有自己的副本，Kafka会尽量的使所有的分区均匀的分布到集群中的所有节点而不是集中在某些节点上，另外主从关系也尽量均衡这样每个几点都会担任一定比例的分区的leader。


每个partition以目录的形式存储在broker上，该目录底下存储着的是该partition内容被平均分配成的多个大小相等的数据文件，我们称之为segment(段)。每个segment文件分为两个部分，index file和data file，此两个文件一一对应，后缀".index"和".log"分别表示segment的索引文件和数据文件。文件的命名规则为partition全局的第一个segment为0开始，后续每个segment文件名为上一个全局partion的最大offset(偏移message数)。每个segment中存储很多条消息，消息id由其逻辑位置决定，即从消息id可直接定位到消息的存储位置，避免id到位置的额外映射。

segment index file采取稀疏索引存储方式，它减少索引文件大小，通过mmap可以直接内存操作，稀疏索引为数据文件的每个对应message设置一个元数据指针,先通过index文件中获取该message的一个位置范围，然后根据这个位置范围在log文件中找到该message的信息。

### MetaQ存储机制

MetaQ的消息存储方式和kafka的partition存放方式类似，在MetaQ中消息的存放分为物理队列和逻辑队列。

物理队列：物理队列我们一般用commitlog来表示，在一个broker上面，所有发到broker上的信息都会按顺序写入物理队列中，物理队列又由许多文件组成，当一个文件被写满（默认大小为1G）时，则创建一个新的文件继续写入，文件以offset的方式来命名，与kafka中的partition命名类似。

逻辑队列：逻辑队列我们一般用consumequeue来表示，在消息被写入物理队列之后，如果消费端想从broker拉取消息，就需要一个索引文件，MetaQ中将每个Topic分为了几个区，每个区对应了一个消费队列，不过这些消费队列只是由一个个索引文件组成。消费端在拉取消息的时候，只要知道自己订阅的Topic从nameserver获取broker地址建立连接之后，就能根据消费队列中的索引文件，去物理队列中获取订阅的消息。

CommitLog以物理文件的方式存放，每台Broker上的CommitLog被本机器上所有的ConsumeQueue共享。在CommitLog中，一个消息的存储长度是不固定的，MetaQ中采取了一些机制，尽量往CommitLog中顺序写，但是可以支持随机读。ConsumeQueue的内容也会被写到磁盘里进行持久存储，但是ConsumeQueue的内容是通过异步刷盘的方式进行。
 

## 为什么MetaQ需要采用这种存储架构呢？

我们知道，磁盘的顺序写比随机写的速度快的很多，目前的高性能磁盘，顺序写的速度可以达到600MB/s，超过了一般的网卡的传输速度，但是磁盘的随机写的速度只有大概100KB/s，和顺序写的性能相差了6000倍，而MetaQ正是利用磁盘顺序写的优势来设计的。

上文说到，MetaQ的主要存储文件包括CommitLog、ConsumeQueue文件，在一个Broker节点上，MetaQ会将所有Topic的消息存储在同一个文件commitlog中，这样能确保producer发送的消息顺序写入commitlog中，能够尽最大的能力确保消息发送的高性能和高吞吐量，接收消息的时候，只有CommitLog是需要同步落盘的。同时使用ConsumeQueue消息队列文件来作为索引文件，每个Topic包含有多个消息消费队列，每一个消息队列就有一个ConsumeQueue消息文件，ConsumeQueue是异步保存的，不需要同步落盘，如果在没有落盘的时候，broker发生宕机，MetaQ可以根据CommitLog来恢复ConsumeQueue。

虽然说在同一个broker上面由于不同的ConsumeQueue访问同一个CommitLog，CommitLog是进行随机读的，但是根据操作系统的局部性原理，也利用操作系统的分页机制，可以批量的从磁盘中获取CommitLog的信息，然后缓存到内存中，更快的进行读取。而对于ConsumeQueue，由于其内部只保存数据的索引信息，所以一般其数据量不大，可以全部读入内存，所以我们可以认为从ConsumeQueue这个中间结构获取数据很快，可以当成从内存读取数据的速度。

在kafka中，当如果一个broker上面有多个partition，如果多个partition并发写入数据，磁盘的访问会有很大的瓶颈，多个文件之间必然会有磁盘的寻道。而MetaQ对于数据来说就只有单文件写入，性能上将优于kafka。

 

## MetaQ为什么不像kafka使用zk作为元数据节点，而要使用自己实现的NameServer？

我们知道，kafka使用zk作为元数据节点，起到了Broker注册、Topic注册、生产者和消费者负载均衡以及使用zk进行leader角色的选举，当leader所在的broker挂了，将会经过以下两步操作重新选举leader：第1步，先通过Zookeeper在所有机器中，选举出一个KafkaController；第2步，再由这个Controller，决定每个partition的Master是谁，Slave是谁。因为有了选举功能，所以kafka某个partition的master挂了，该partition对应的某个slave会升级为主对外提供服务。

MetaQ不具备选举，Master/Slave的角色也是固定的。当一个Master挂了之后，你可以写到其他Master上，但不能让一个Slave切换成Master。那么MetaQ是如何实现高可用的呢，其实很简单，MetaQ的所有broker节点的角色都是一样，上面分配的topic和对应的queue的数量也是一样的，MetaQ只能保证当一个broker挂了，把原本写到这个broker的请求迁移到其他broker上面，而并不是这个broker对应的slave升级为主。

引入zk的主要目的是为了选主，kafka中如果一个broker挂了，这个broker上面的主partition可以通过zk的选举机制在其他broker上面选举主partition，而对于MateQ而言，在部署的时候已经决定了这个Broker是主或者是备了（一个Master可以对接多个Slave，但是一个Slave只能对接一个Master，Master与Slave之间可以通过指定相同的BrokerName，不同的BrokerId来定义，BrokerId为0表示Master，不为0的表示Slave），不能再通过选举变成主（认命吧，无法上位的），所以对于MetaQ，是不需要进行选举的，为了方便集群维护，直接使用NameServer这一个轻量级工具来存储元数据信息即可。

## MetaQ和kafka的部署方式

由上文可知，MetaQ和kafka的元数据节点采用的方式不一样，MetaQ的master和slave都是物理上隔离的，所以对于MetaQ的Broker来说，是支持以下四种方式的部署：

单Master：单机模式, 即只有一个Broker, 如果Broker宕机了, 会导致MetaQ服务不可用, 不推荐使用;
多Master模式： 组成一个集群, 集群每个节点都是Master节点, 配置简单, 性能也是最高, 某节点宕机重启不会影响MetaQ服务；
缺点是如果某个节点宕机了, 会导致该节点存在未被消费的消息在节点恢复之前不能被消费;

多Master多Slave模式，异步复制：每个Master配置一个Slave, 多对Master-Slave, Master与Slave消息采用异步复制方式, 主从消息一致只会有毫秒级的延迟；
优点是弥补了多Master模式（无slave）下节点宕机后在恢复前不可订阅的问题。在Master宕机后, 消费者还可以从Slave节点进行消费。采用异步模式复制，提升了一定的吞吐量。总结一句就是，采用多Master多Slave模式，异步复制模式进行部署，系统将会有较低的延迟和较高的吞吐量；

缺点就是如果Master宕机, 磁盘损坏的情况下, 如果没有及时将消息复制到Slave, 会导致有少量消息丢失；

多Master多Slave模式，同步双写：与多Master多Slave模式，异步复制方式基本一致，唯一不同的是消息复制采用同步方式，只有master和slave都写成功以后，才会向客户端返回成功

* 优点：数据与服务都无单点，Master宕机情况下，消息无延迟，服务可用性与数据可用性都非常高

* 缺点就是会降低消息写入的效率，并影响系统的吞吐量；

 

对于Kafka来说，Broker之间不存在master和slave的区别，每一个Broker之间都是平等的，kafka的partition是有master和slave的区别的，kafka将每个partition数据复制到多个server上,任何一个partition有一个leader和多个follower(可以没有);备份的个数可以通过broker配置文件来设定。leader处理所有的read-write请求,follower需要和leader保持同步。Kafka尽量的使所有分区均匀的分布到集群所有的节点上而不是集中在某些节点上，另外主从关系也尽量均衡这样每个几点都会担任一定比例的分区的leader。

 

## MetaQ和kafka的消息可靠性
在介绍MetaQ和kafka的消息可靠性之前，我们先来介绍一下几个概念：同步异步复制、同步异步刷盘。

1）同步异步复制
同步复制和异步复制的区别在于producer发送消息到master节点之后，是否会等待slave节点复制结束之后再进行返回。

a. 同步复制
当生产者将消息发送到broker的master节点时，master会首先将消息复制到所有的slave节点，等待复制动作完成之后，才会给客户端返回“发送成功”的响应，消息可靠性得到保证


b. 异步复制
当生产者将消息发送到broker的master节点时，并不会等待复制动作的结束，会直接返回一个发送成功的状态响应。当出现网络抖动，会导致消息复制不成功，这个时候消息可靠性不够高，消费者消费消息不及时的情况。


2）同步异步刷盘
同步异步刷盘的区别在于，消息存储在内存（memory）中以后，是否会等待执行完刷盘动作再返回，即是否会等待将消息中的消息写入磁盘中。

a. 异步刷盘
当消息写入到broker的内存中之后即返回写成功状态，并不会等待消息从内存中写入磁盘就返回。所以写操作的返回快，吞吐量大；当内存里的消息量积累到一定程度时，统一触发写磁盘操作，快速写入。


b. 同步刷盘
当消息被写入到内存之后，会立刻会立刻通知刷盘线程刷盘，然后等待刷盘完成，刷盘线程执行完成后唤醒等待的线程，返回消息写成功的状态。所以当返回写成功状态的时候，消息已经被写入磁盘了。

 
**MetaQ和kafka都支持同步异步复制以及同步异步刷盘。**

MetaQ的同步异步复制是通过Broker的配置文件中的brokerRole参数进行设置的，这个参数可以被设置成ASYNC_MASTER、SYNC_MASTER、SLAVE三个值中的一个。其中ASYNC_MASTER表示的是当前broker的角色是一个异步复制的master，生产者写入消息到Master后无需等待消息复制到slave即可返回；SYNC_MASTER表示当前的broker的角色是一个同步复制的master，Master写入完消息之后，需要等待Slave的复制成功，但是这边注意这里只需要有一个Slave复制成功并成功应答即算成功；SLAVE表示的是当前broker是一个slave。

MetaQ的同步异步刷盘是通过Broker配置文件里的flushDiskType参数设置的，这个参数被设置成SYNC_FLUSH, ASYNC_FLUSH中的一个，其中SYNC_FLUSH表示同步刷盘，ASYNC_FLUSH表示异步刷盘。

Kafka的同步异步复制可以通过acks配置来实现，当acks的参数设置为0，表示生产者把消息发送出去之后，不管消息有没有被接收，直接就认为消息发送成功；当acks的参数设置为1，表示生产者把消息发送出去之后，就认为消息发送成功，而不管其他的slave是否同步这个消息，相当于异步复制，该配置为kafka的默认配置；当acks的参数设置为all，表示生产者把消息发送出去之后，master收到消息之后，还必须等待ISR列表中跟master保持同步的那些slave都进行消息同步之后，才认为消息写入成功，相当于同步复制。

kafka可以通过配置flush.message和flush.ms来设置刷盘策略，如果flush.message设置为5，表示每5条消息进行一次刷盘，如果flush.message设置为1，表示每一条消息都进行一次刷盘。如果flush.ms设置为1000，表示每过1000ms进行一次刷盘，如果flush.ms设置为5000，表示每过5000ms进行一次刷盘。

 
## MetaQ和kafka的消息读写方式

### 零拷贝

我们知道，我们在写数据的时候并不是直接写入到磁盘中去的，而是写入到pageCache中去的，pageCache的主要作用是减少磁盘的I/O操作。

在磁盘写入的时候会写入到pageCache中去的，然后pageCache中可以将一些小的写入合并成一个大的写入，再进行异步刷盘。当然我们也可以使用fsync进行强制刷盘，强制刷盘会影响写入性能。一般为了保证消息的可靠性，我们是会采用多副本来存储消息，而不是采用同步刷盘。

读取消息的时候如果在pageCache中有命中则直接返回，如果在pageCache中无法命中则会产生缺页中断，需要从磁盘中加载数据到缓存中，然后返回数据。并且根据局部性原理，在读数据的时候也会进行预读，把该也相邻的磁盘快读入到页缓存中去。

mmap
由于我们读取数据的时候，需要将数据从磁盘拷贝到pageCache中，但是由于pageCache属于内核空间，用户空间无法访问，所以还需要将数据从内核空间拷贝到用户空间。


所以数据需要两次拷贝应用程序才能够访问的到，我们可以通过mmap来减少数据从内核态到用户态的拷贝。通过将程序虚拟页面映射到页缓存中，这样就不需要将数据从内核态拷贝到用户态，也可以避免产生重复数据。也不必要再通过调用read和write方法对文件进行读写，而是通过映射地址和偏移量来直接操作pageCache。


sendfile
下面我们来看下常规的发送文件的过程中，从磁盘读取消息到发送文件的过程是怎么样的。


DMA Copy是指不需要CPU接入，可以直接读写系统内存，类似显卡、网卡和磁盘都是用到DMA，然而像上下文切换的话就需要有CPU接入。

下面我们看看如果采用mmap发送文件之后的流程是怎么样的。

可以看到上下文切换的次数没有变化，但是数据少拷贝了一份，这个和我们上面说到的mmap所能够达到的效果是一样的。


上图中，sendfile采用一次系统调用就完成了发送数据的需求，相比于read+write或者说mmap+write来说上下文切换次数变少了，但是数据还是有冗余的。在linux2.4中采用 sendfile+带[分散-收集]的DMA。真正实现了无冗余的功能。

上面就是我们说的零拷贝，在Java中是通过FileChannal.transferTo()调用的，底层是通过sendfile实现。

## MetaQ和kafka的读写对比

目前kafka支持sendfile的消息读写方式，MetaQ支持mmap的消息读写方式，另外MetaQ还支持sendfile的消息写方式。

### Kafka

读方式：sendfile read

写方式：sendfile write

### MetaQ

读方式：mmap

写方式：mmap/sendfile write

默认情况下，MetaQ不论是在CommitLog或者ComsumerQueue中都是采用mmap来实现消息读写的。在发送消息的时候，通常情况下会将数据拷贝到堆内存中去，然后再塞到响应体中进行发送。当然我们也可以通过参数配置不经过堆，通过mapedBuffer直接发送到SocketBuffer。

当消费消息的时候，严格来说对于CommitLog的读取是随机的，因为CommitLog的消息是混合进行存储的，但是从整体上面来看，消息还是会从CommitLog上顺序读取的，先读取旧数据，然后再读取新数据。消息存进去之后很快就会被消费，这个时候消息还是存放在pageCache中的，所以我们是不需要读取磁盘的。

同时pageCache会定时刷盘，但是刷盘的时机是不可控制的，所以会出现swap等现象。mmap也只是做了映射，如果真正去取数据的时候不在内存中，也会产生缺页中断，需要加载数据到内存中，这个时候也会有一些延时。MetaQ采用文件预分配和文件预热来解决pageCache的不确定性。

kafka的消息写入对于单分区来说是顺序写入的，由上文可知，kafka是有.index索引文件和.log数据文件构成的。其中.index索引文件是采用mmap进行读写的，这对于本地读写索引文件则可以提高读取效率，而.log数据文件则采用sendfile的零拷贝进行实现的。对于消息的写入来说，采用mmap其实并没有什么用，因为消息都是从网络中获取的，采用sendfile来发送消息比mmap+write更能提高效率，因为在内存中少了一个SocketBuffer的拷贝。

另外通过网上研究测试表明，如果读取的数据小于4kb的时候，使用mmap的性能效率比sendfile高，当读取数据大于4kb的时候，sendfile的效率比mmap高；对于写数据，如果写入的数据包小于64kb的时候，mmap的性能效率比sendfile高，当写入数据包大于64kb的时候sendfile的效率比mmap高。

由于kafka主要是用于日志传输，处理海量数据，对于数据的正确度要求不是很高，并且在发送消息的时候一般会进行消息的汇聚，然后批量发送消息，所以整体上来说kafka的读写数据量会比较大，这个时候使用sendfile能够获取更高的性能，而MetaQ主要是用来针对阿里的复杂应用场景，对于数据的可靠性、数据的实时性要求会比较高，由于对数据的实时性要求较高，一般不会进行汇聚批量发送消息，所以读写数据量不会很大，这个时候使用mmap可以获得更好的性能，当如果发现写入的数据量比较大时，也可以切换为sendfile进行写入

# Kafka和MetaQ之数据一致性协议

先说结论，MetaQ没使用Raft，Kafka使用了类Raft，[Raft协议解析动画](https://thesecretlivesofdata.com/raft/)

* MetaQ的设计着重于消息传输和处理的高性能和高可用，而不是强一致性保证，所以没使用Raft，用的是主从同步
* Kafka 2.8.0版本合并了KIP-500提议，引入KRaft协议，但未彻底脱离对Zookeeper的依赖

## 题外话，关于Raft和Paxos