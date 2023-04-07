



# ***Hadoop+HDFS***

1. hadoop概述？

```java
hadoop是什么：
Hadoop是Apache下的使用Java语言开发的一个分布式计算框架，它可以存储和处理大规模的数据。允许使用简单的编程模型在大量计算机集群上对大型数据集进行分布式处理。
狭义上说，Hadoop指Apache这款开源框架。
 
核心组件有：
（1）HDFS（分布式文件系统）：解决海量数据存储
（2）MAPREDUCE（分布式运算编程框架）：解决海量数据计算
（3）YARN（作业调度和集群资源管理的框架）：解决资源任务调度

hadoop的起源：
    Hadoop起源于Apache Nutch项目，始于2002年，是Apache Lucene的子项目之一，2004年，Google在“操作系统设计与实现”（Operating System Design and Implementation，OSDI）会议上公开发表了题为MapReduce：Simplified Data Processing on Large Clusters（Mapreduce：简化大规模集群上的数据处理）的论文之后，受到启发的Doug Cutting等人开始尝试实现MapReduce计算框架，并将它与NDFS（Nutch Distributed File System）结合，用以支持Nutch引擎的主要算法 [2]  。由于NDFS和MapReduce在Nutch引擎中有着良好的应用，所以它们于2006年2月被分离出来，成为一套完整而独立的软件，并被命名为Hadoop。到了2008年年初，hadoop已成为Apache的顶级项目。

 hadoop特点：
    扩容能力（Scalable）：Hadoop是在可用的计算机集群间分配数据并完成计算任务的，这些集群可用方便的扩展到数以千计的节点中。
	成本低（Economical）：Hadoop通过普通廉价的机器组成服务器集群来分发以及处理数据，以至于成本很低。
	高效率（Efficient）：通过并发数据，Hadoop可以在节点之间动态并行的移动数据，使得速度非常快。
	可靠性（Rellable）：能自动维护数据的多份复制，并且在任务失败后能自动地重新部署（redeploy）计算任务。所以Hadoop的按位存储和处理数据的能力值得人们信赖。
 
 版本：
    1.Hadoop 0.x：Hadoop的最初版本，于2006年发布，包括HDFS、MapReduce和Hadoop Common组件。这个版本的Hadoop已经停止维护，不再被推荐使用。
	2.Hadoop 1.x：于2009年发布，包括了HDFS、MapReduce和Hadoop Common组件。这个版本的Hadoop使用了JobTracker和TaskTracker来管理MapReduce作业，但是在大规模集群中存在性能瓶颈。这个版本的Hadoop已经停止维护。
	3.Hadoop 2.x：于2012年发布，截止2023年，被企业使用最广泛的版本，是Hadoop的重大升级版本，包括了HDFS、YARN和MapReduce组件。YARN是一个新的资源管理器，支持Hadoop上运行的其他计算框架，例如Apache Spark、Apache Flink等。这个版本的Hadoop使用了ResourceManager和NodeManager来管理资源和作业。
	4.Hadoop 3.x：于2017年发布，是Hadoop的最新版本，包括了HDFS、YARN和MapReduce组件。这个版本的Hadoop引入了许多新特性，例如Erasure Coding、Container Executor、GPU支持等等。它还提供了更好的容错性、可扩展性和性能。
	除了官方发布的版本之外，Hadoop的社区还有一些发行版，例如Cloudera CDH、Hortonworks 等(cdh版本兼容性更好，Hortonworks文档写的好)。这些发行版通常包括了Hadoop的官方组件以及一些第三方组件，例如Apache Hive、Apache Pig、Apache Spark等等，以提供更丰富的功能和工具。
    
 hadoop官网:https://hadoop.apache.org/

hadoop在国内外的应用：
国内企业：
	阿里巴巴：使用Hadoop构建了自己的大数据平台Aliyun ODPS，用于支持阿里巴巴内部和外部的大数据应用。
	腾讯：使用Hadoop搭建了自己的分布式存储和计算平台Tencent TDS，用于支持腾讯内部的数据处理和分析工作。
	百度：使用Hadoop构建了自己的大数据平台Baidu BDP，用于支持百度内部的大数据应用和产品。
	新浪微博：使用Hadoop构建了自己的大数据平台Weibo Bigdata，用于支持微博的数据处理和分析工作。
	华为：使用Hadoop搭建了自己的大数据平台FusionInsight，用于支持华为内部和外部的大数据应用。
国外企业：
	谷歌：使用Hadoop构建了自己的大数据平台Google Cloud，用于支持谷歌内部和外部的大数据应用。
	Facebook：使用Hadoop搭建了自己的分布式存储和计算平台Hive，用于支持Facebook内部的数据处理和分析工作。
	苹果：使用Hadoop构建了自己的大数据平台Apple Big Data，用于支持苹果内部的数据处理和分析工作。
	亚马逊：使用Hadoop构建了自己的大数据平台Amazon EMR，用于支持亚马逊内部和外部的大数据应用。
	美国宇航局（NASA）：使用Hadoop搭建了自己的分布式计算平台Nebula，用于支持NASA内部的科学计算和数据分析工作。
    
```

   2.Hadoop有哪些组件（hadoop的架构）？

```
Hadoop包含以下主要组件：HDFS、MapReduce、YARN、ZooKeeper等。其中，HDFS和MapReduce是Hadoop的核心组件，用于数据存储和分布式计算；YARN是Hadoop的资源管理系统，用于管理集群中的资源；HBase是一个分布式的NoSQL数据库，用于存储非结构化数据；ZooKeeper是一个分布式的协调服务，用于管理分布式应用程序。

以hadoop2.X高可用版本架构举例：
1.NameNode：在Hadoop分布式文件系统(HDFS)中，NameNode是主要的命名空间管理者，负责存储文件系统的元数据信息和文件块的位置信息。在高可用模式下，HDFS中有两个NameNode，其中一个是Active NameNode，负责对外提供服务，而另一个是Standby NameNode，用于备份Active NameNode的数据。Active NameNode会将元数据信息和文件块位置信息同步到Standby NameNode上，以保证数据的高可用性和容错性。
2.JournalNode：JournalNode是HDFS高可用模式中的关键组件，它用于保存NameNode的元数据信息和操作日志。多个JournalNode可以组成一个JournalNode集群，以保证数据的高可靠性和一致性。
3.ZooKeeper：ZooKeeper是一个分布式的协调服务，可以用于Hadoop集群的高可用管理。在Hadoop高可用模式下，ZooKeeper主要用于实现Active和Standby NameNode之间的选举、存储元数据信息和监控NameNode的状态。
4.DataNode：DataNode是Hadoop集群中负责存储文件块的节点，它在高可用模式下并没有什么特殊的变化。
5.ResourceManager：在Hadoop集群中，ResourceManager是主要的资源管理者，负责为应用程序分配资源。在高可用模式下，ResourceManager也有两个实例，其中一个是Active ResourceManager，而另一个是Standby ResourceManager，用于备份Active ResourceManager的数据。Active ResourceManager会将应用程序的状态同步到Standby ResourceManager上，以保证数据的高可用性和容错性。
6.NodeManager：NodeManager是Hadoop集群中的一个组件，负责管理和监控节点上的应用程序和容器。在高可用模式下，NodeManager并没有什么特殊的变化。
```

![](.\hadoop架构.png)



![](.\hadoop-NameNode高可用.png)





3.hadoop优缺点？

```
Hadoop具有以下优点：

（1）高可靠性：Hadoop的设计理念就是通过数据冗余来保证数据的可靠性，可以在节点故障时自动恢复。
（2）高扩展性：Hadoop是基于分布式计算的架构，可以通过添加节点来实现横向扩展，提高系统的处理能力。
（3）高效性：Hadoop利用了MapReduce框架来实现数据的并行处理，可以在多个节点上同时处理数据，大大提高了处理效率。
（4）低成本：Hadoop使用廉价的硬件节点组成集群，与传统的高性能计算系统相比，可以大大降低成本。
（5）高灵活性：Hadoop可以处理各种格式的数据，包括结构化、半结构化和非结构化数据，并且可以集成多种数据处理和分析工具。
（6）开源性：Hadoop是一种开源框架，可以免费使用和修改。

Hadoop也具有以下缺点：
（1）实时性差：Hadoop的处理模式是批处理，对于实时性要求较高的应用场景，性能可能不够理想。
（2）复杂性高：Hadoop集群的搭建、配置和维护都需要一定的专业知识和经验，学习成本较高。
（3）适用场景受限：Hadoop适用于大规模的批量数据处理，对于小规模数据处理和实时数据处理，可能不够适用。
（4）内存限制：Namenode需要将HDFS中的所有元数据加载到内存中进行管理，因此Namenode的内存容量会限制HDFS的文件数和块数。
hadoop可以说是初代框架，随着大数据需求与技术的不断发展，以spark、Flink为代表的第2、3代框架也逐步取代MR应用于离线、实时等场景。
```

   

4.hadoop主要版本以及更新内容？

```
Hadoop 0.1.0（2006年12月）：这是Hadoop的第一个版本，包括HDFS和MapReduce两个核心组件，以及一些基础设施。
Hadoop 0.20.0（2009年9月）：这个版本引入了许多新特性，包括新的任务调度器，以及对MapReduce和HDFS的各种改进。
Hadoop 0.21.0（2010年7月）：这个版本增加了对Hadoop安全性的支持，包括用户认证和授权，以及许多其他的改进和新功能。
Hadoop 0.22.0（2011年11月）：这个版本加入了一些新的特性，包括新的文件系统API和MapReduce API，以及对HDFS和MapReduce的各种改进。

Hadoop 1.0.0（2011年12月）：这个版本是Hadoop的一个重要的里程碑，标志着Hadoop从一个实验性项目进化为一个稳定的、可用的大规模分布式系统。

Hadoop 2.0.0-alpha（2012年5月）：这个版本引入了许多新特性，包括新的资源管理器YARN，以及对HDFS和MapReduce的各种改进。
Hadoop 2.2.0（2013年10月）：这个版本增加了对YARN的各种改进和新功能，以及对HDFS和MapReduce的各种改进。
Hadoop 2.7.0（2015年4月）：这个版本增加了许多新特性和改进，包括新的快照功能、动态资源池和分布式缓存的各种优化。

Hadoop 3.0.0（2017年12月）：这个版本引入了许多新特性，包括新的分布式文件系统HDFS Erasure Coding、对YARN的各种改进和新功能、以及对MapReduce的各种改进和新功能。
```

5.hadoop需要哪些配置文件，作用是什么？

```
在 Hadoop 中，需要配置一系列的配置文件（${HADOOP_HOME}/etc/hadoop/目录下），以便不同组件之间能够协同工作，完成大数据处理任务。下面是 Hadoop 中常见的配置文件以及它们的作用：
core-site.xml：配置 Hadoop 的核心参数，如默认文件系统、HDFS 的文件副本数、RPC 的端口号等。
hdfs-site.xml：配置 HDFS 的相关参数，如 NameNode 的地址、副本策略、块大小等。
mapred-site.xml：配置 MapReduce 的相关参数，如 JobTracker 的地址、任务并行度、Reduce 任务数等。
yarn-site.xml：配置 YARN 的相关参数，如 ResourceManager 的地址、NodeManager 的地址、任务内存大小等。
hadoop-env.sh：配置 Hadoop 运行环境的相关参数，如 Java 安装路径、Hadoop 的安装路径等。
hdfs-env.sh：配置 HDFS 运行环境的相关参数，如 NameNode 和 DataNode 的 Java 堆大小、HDFS 文件缓存大小等。
mapred-env.sh：配置 MapReduce 运行环境的相关参数，如 JobTracker 和 TaskTracker 的 Java 堆大小、任务的 Java 类路径等。
yarn-env.sh：配置 YARN 运行环境的相关参数，如 ResourceManager 和 NodeManager 的 Java 堆大小、YARN 应用程序的 Java 类路径等。
这些配置文件在 Hadoop 的不同版本中可能会有所不同，但它们的作用都是为了让 Hadoop 各个组件之间能够协同工作，完成大规模数据处理任务。
```

6.正常工作的hadoop集群需要启动哪些进程，作用是什么？

```
1.NameNode：负责管理HDFS元数据，包括文件和目录的命名空间，块的位置以及文件的访问权限等。
2.DataNode：负责存储实际的数据块，向客户端和其他DataNode提供读写数据块的服务。
3.ResourceManager：负责管理YARN集群资源的分配和调度，以及协调各个NodeManager之间的任务执行。
4.NodeManager：运行在每个节点上，负责启动和监控容器，执行具体的任务。
5.SecondaryNameNode：定期合并和压缩NameNode的编辑日志，帮助恢复NameNode故障时的数据。
6.JournalNode：运行在一个独立的进程中，协助NameNode进行HA（高可用）工作，确保元数据的持久化和可恢复性。
7.ZooKeeper：在Hadoop 2.x及以后版本中，ZooKeeper用于协助ResourceManager和NodeManager进行HA工作，确保资源管理器的可用性。
除了上述进程，还有一些辅助进程，如JobHistoryServer、HttpServer等，用于支持集群的管理、监控和调试等操作。
总之，上述进程共同协作，组成了一个完整的Hadoop集群，实现了数据存储、分布式计算和资源调度等功能，支持各种大数据应用的运行。
```

7. hadoop集群相关的端口号？

```
Hadoop中常用的端口号如下：

NameNode：50070（Web UI）、8020（RPC）
DataNode：50075（Web UI）、50010（数据块复制）、50020（心跳）
ResourceManager：8088（Web UI）、8030（RPC）
NodeManager：8042（Web UI）、8040（RPC）
SecondaryNameNode：50090（Web UI）
JobHistoryServer：19888（Web UI）
HttpServer：50070（Web UI，默认和NameNode端口号一样）

这些端口号可以通过修改配置文件来自定义，但是建议保持默认值，以便管理和维护。同时，这些端口号只是Hadoop集群中的一部分，还有其他进程和服务也可能使用不同的端口号，需要根据实际情况进行配置和管理。
```

8.为什么HDFS中块的大小设计为128M？

```
首先，较大的块大小可以减少寻道时间，因为磁盘读取速度的瓶颈在于磁头移动到正确位置的时间。如果块的大小较小，需要读取的块数量就会增多，磁头的移动时间也会增加，从而导致读取速度变慢。相反，如果块的大小较大，读取的块数量就会减少，磁头的移动时间也会减少，从而读取速度会变快。

其次，较大的块大小可以降低存储开销。在HDFS中，每个块都会有一个元数据来描述它的大小、位置等信息。如果块的大小较小，需要管理的元数据就会变得更多，从而增加了存储开销。而较大的块大小可以减少元数据的数量，从而降低存储开销。

最后，较大的块大小可以提高并行性。在Hadoop中，MapReduce任务的并行性是通过将输入数据划分为多个块来实现的。如果块的大小较小，划分的块数量也会增多，从而降低了并行性。而较大的块大小可以减少划分的块数量，从而提高了并行性。

同样，如果块设置过大，一方面，从磁盘传输数据的时间会明显大于寻址时间，导致程序在处理这块数据时，变得非常慢；
另一方面，mapreduce中的map任务通常一次只处理一个块中的数据，如果块过大运行速度也会很慢。

那128M是怎么来的呢：
HDFS中平均寻址时间大概为10ms；
经过前人的大量测试发现，寻址时间为传输时间的1%时，为最佳状态；
所以最佳传输时间为10ms/0.01=1000ms=1s
目前磁盘的传输速率普遍为100MB/s；
计算出最佳block大小：100MB/s x 1s = 100MB
所以我们设定block大小为128MB。
实际在工业生产中，磁盘传输速率为200MB/s时，一般设定block大小为256MB，磁盘传输速率为400MB/s时，一般设定block大小为512MB
```





   9.HDFS写文件流程（需要配图）？

```
1.客户端向NameNode请求创建文件，并提供文件名、文件大小和数据块大小等信息。NameNode检查目标文件是否已存在，父目录是否存在，返回是否可以上传
2.客户端请求第一个block该传输到哪些DataNode服务器上（申请若干Datanode组成一条流水线来完成数据的写入）
3.NameNode根据配置文件中指定的备份数量及副本放置策略进行文件分配，返回可用的DataNode的地址，如：A，B，C；
4.客户端的数据以字节（byte）流的形式写入chunk（以chunk为单位计算checksum（校验和））。若干个chunk组成packet，数据以packet的形式从客户端发送到第一个Datanode（A），再由第一个Datanode发送数据到第二个Datanode并完成本地写入，以此类推，直到最后一个Datanode写入本地成功，可以从缓存中移除数据包（packet）。
5.重复步骤2-4，上传第2个block，继续写数据包和回复数据包，直到数据全部写完。
6.客户端向NameNode发送关闭文件的请求，NameNode将文件的元数据更新到本地磁盘上。
```

<img src="C:\Users\1\Desktop\why_bigdata_tools\面试\hdfs-write.png" alt="图片" style="zoom: 67%;" />



  10.HDFS读文件流程？

```
1.客户端向NameNode请求打开文件，并提供文件名。

2.NameNode根据文件名查询该文件的元数据，返回文件的块列表及其所在DataNode的信息给客户端。

3.客户端根据返回的块列表，向离其最近的一个DataNode发起读取请求。

4.DataNode根据请求的块编号，从本地磁盘读取数据块并返回给客户端。

5.客户端收到数据块后，将其存储在本地缓存中，并继续向下一个DataNode请求下一个数据块。

6.重复步骤3~5，直到所有数据块都被读取完毕。

7.客户端关闭文件，并将文件的数据从本地缓存中删除。
```

<img src="C:\Users\1\Desktop\why_bigdata_tools\面试\hdfs-readFile.png" alt="img" style="zoom: 67%;" />

 



 11.HDFS小文件太多会带来什么问题，如何解决？

```
HDFS (Hadoop Distributed File System) 是一种设计用于存储大型数据集的分布式文件系统。HDFS的设计是为了支持大文件的分布式存储和处理，而不是大量小文件的存储。

如果HDFS存储了大量小文件，会导致以下问题：
1.命名空间过大：每个文件都需要占用一个命名空间，大量小文件将导致命名空间的使用增加。当命名空间过大时，namenode 的内存和 CPU 开销将变得非常大，并且可能会导致namenode宕机。
2.存储碎片化：每个文件都需要占用一定的存储空间，即使这些文件非常小。因此，大量小文件会使HDFS存储碎片化，浪费大量存储空间。
3.读写效率低：HDFS是为了大文件的高速读写而设计的，但是当存在大量小文件时，读写效率将大幅降低。由于每个文件都需要占用一个独立的存储块，小文件的读取将涉及多个存储块的读取，这会增加读取的延迟。
因此，当需要存储大量小文件时，建议将它们合并成更大的文件或使用其他存储系统，如HBase或Cassandra，它们专门针对存储大量小文件进行了优化。
```



12.FdImage 和 EditLogs是做什么用的？

```
FdImage和EditLogs是Hadoop分布式文件系统(HDFS)中的两个重要组成部分，用于数据的持久化存储和恢复。

FdImage：FsImage是HDFS的文件系统镜像，保存了整个文件系统的元数据信息，包括文件、目录、块、副本、权限等。它是一个静态的快照，当HDFS启动时，会读取FsImage并将其加载到内存中，以便快速恢复文件系统的状态。在HDFS正常运行时，FsImage通常不会改变，因为文件系统的状态是动态变化的。当需要对文件系统进行备份、恢复、升级等操作时，可以使用FsImage进行操作。

EditLogs：EditLogs是HDFS中用于记录文件系统操作的日志文件。当文件系统发生任何更改操作时，比如创建、修改、删除文件、目录，添加、删除块等操作，都会被记录在EditLogs中。EditLogs是一个追加写日志文件，因此它可以保证数据的一致性和可靠性。当HDFS启动时，会读取EditLogs中的操作记录，并将其应用到内存中的FsImage中，以恢复文件系统的状态。EditLogs中的日志记录是可以删除的，因为它们已经被应用到FsImage中，以保证数据的一致性。

因此，FdImage和EditLogs一起工作，确保了HDFS的元数据信息和操作日志的持久化存储和恢复。
```

13.hadoop 有哪些部署方式？

```
Hadoop可以使用多种不同的部署方式，根据不同的需求和场景进行选择：

1.单机模式（Standalone Mode）：单机模式是最简单的部署方式，所有的Hadoop组件都在一台机器上运行。该模式通常用于测试和开发环境，不适合生产环境。

2.伪分布式模式（Pseudo-distributed Mode）：伪分布式模式是在一台机器上模拟多台机器的运行环境，所有的Hadoop组件都在同一台机器上运行，但它们使用不同的端口和配置文件。该模式通常用于测试、开发和学习目的。

3.分布式模式（Distributed Mode），也叫作集群模式（单节点或高可用方式）：分布式模式是Hadoop最常用的部署方式，将不同的Hadoop组件分布在不同的机器上运行，可以搭建大规模的分布式集群。该模式适合处理大规模数据的生产环境。

云环境部署：Hadoop也可以在云环境中部署，例如Amazon Web Services（AWS）和Microsoft Azure等云服务提供商都提供了Hadoop的云服务。在云环境中部署可以快速搭建Hadoop集群，并且可以根据需要进行灵活扩展和收缩。

容器化部署：使用容器化技术，例如Docker和Kubernetes等，可以将Hadoop组件打包为容器镜像，方便快速部署和管理。这种部署方式适合于需要频繁部署、管理和升级的场景。
```



14.SecondaryNameNode 工作机制?

```
1.SecondaryNameNode节点定期从NameNode节点中获取FsImage和EditLogs文件的信息，并将它们复制到本地节点上。此操作可以通过Hadoop配置文件中的dfs.secondary.http.address属性来设置SecondaryNameNode的监听地址和端口。

2.SecondaryNameNode将FsImage和EditLogs文件合并成一个新的FsImage文件，并进行压缩，以减少磁盘空间的占用。此时，SecondaryNameNode称之为checkpoint节点。

3.将新生成的FsImage文件复制到NameNode节点上，替换旧的FsImage文件。这样，NameNode就可以使用新的FsImage文件来处理客户端的请求。同时，NameNode还将EditLogs文件中已经应用到FsImage文件中的操作记录删除，以释放磁盘空间。

4.SecondaryNameNode节点定期执行这个操作，以保证FsImage文件的更新和压缩，并且不会占用过多的磁盘空间。

5.需要注意的是，SecondaryNameNode节点并不是NameNode节点的备份，而只是辅助节点，用于帮助NameNode节点处理元数据信息。因此，如果NameNode节点出现故障，需要手动进行故障转移和恢复操作。
```



如何编译hadoop？？

```
下载Hadoop源代码：从Hadoop官网上下载源代码包，解压缩到本地目录中。

安装Maven：如果本地没有安装Maven，则需要先安装Maven。

配置环境变量：配置Maven和Java的环境变量，以便在命令行中调用。

进入源代码目录：打开命令行，进入Hadoop源代码目录。

执行编译命令：执行以下命令进行编译：
mvn package -Pdist,native -DskipTests -Dtar
这个命令会在本地生成Hadoop的二进制安装包和源代码包，同时生成一些本地代码（例如本地库和JNI头文件）。

-P参数用于指定编译Hadoop的模式，-DskipTests参数用于跳过测试，-Dtar参数用于生成二进制安装包。

安装Hadoop：将编译好的二进制安装包解压缩到目标机器上，并根据需要进行配置。

注意：编译Hadoop需要比较长的时间和大量的计算资源，需要保证本地计算机的配置较高，例如至少16GB的内存和4个CPU核心。如果本地资源不足，也可以使用云计算等技术进行编译。
```



15.概述hadoop安装过程（Apache版本）?

```
Hadoop安装过程涉及以下几个步骤：

确认系统要求：在开始安装之前，请确认系统要求是否满足Hadoop的要求，例如JDK版本、内存、磁盘空间等。

下载Hadoop二进制包：从Hadoop官网上下载适合系统的二进制包，或者从源代码进行编译。

解压缩Hadoop二进制包：将下载的Hadoop二进制包解压缩到本地目录。

配置Hadoop环境变量：设置Hadoop的环境变量，例如HADOOP_HOME、JAVA_HOME、PATH等，以便在命令行中调用Hadoop命令。

配置Hadoop配置文件：进入Hadoop的conf目录，编辑core-site.xml、hdfs-site.xml、mapred-site.xml等配置文件，根据需求进行配置。例如，配置NameNode和DataNode节点、设置HDFS存储目录、设置MapReduce任务分配方式等。

配置SSH免密登录：为了实现集群的远程管理，需要配置SSH免密登录，以便在不同的节点之间进行SSH通信。可以使用ssh-keygen命令生成SSH密钥，并将公钥分发到各个节点上。

启动Hadoop服务：启动Hadoop服务，包括NameNode、DataNode、ResourceManager、NodeManager、JobHistoryServer等，以及其他服务（例如ZooKeeper、Hive等），根据需要启动相应的服务。

测试Hadoop集群：使用Hadoop自带的样例程序进行测试，例如执行WordCount程序，确保Hadoop集群正常运行。

以上是Hadoop安装的基本过程，具体的安装步骤可能会因环境和需求的不同而有所不同。
```





16.概述hadoop安装过程（CDH版本）?

```
CDH（Cloudera's Distribution Including Apache Hadoop）是由Cloudera提供的一种基于Apache Hadoop的发行版。CDH包括多种组件和服务，例如HDFS、YARN、MapReduce、HBase、Spark等。

以下是CDH版本Hadoop的安装步骤：

1.下载CDH发行版：从Cloudera官网上下载适合系统的CDH发行版，例如CDH 5.x、CDH 6.x等。

2.准备安装环境：确认系统要求，例如JDK版本、内存、磁盘空间等。确保系统已经安装了必要的软件，例如MySQL、Python等。

3.安装CDH Manager：将CDH Manager安装到管理节点上，用于集群的配置、管理和监控。安装过程中需要输入MySQL和Cloudera账户信息等。

4.启动CDH Manager：启动CDH Manager，并登录到CDH Manager的Web界面。

5.添加集群：在CDH Manager的Web界面中，添加Hadoop集群，根据提示进行操作。添加集群时需要指定NameNode、DataNode、ResourceManager、NodeManager等角色。

6.配置集群：在CDH Manager的Web界面中，配置Hadoop集群的参数，例如HDFS存储目录、MapReduce作业配置等。

7.安装Hadoop服务：在CDH Manager的Web界面中，选择需要安装的Hadoop服务，例如HDFS、YARN、MapReduce等，进行安装。

8.启动Hadoop服务：在CDH Manager的Web界面中，启动Hadoop服务，例如NameNode、DataNode、ResourceManager、NodeManager等，以及其他服务（例如ZooKeeper、Hive等），根据需要启动相应的服务。

9.测试Hadoop集群：使用CDH自带的样例程序进行测试，例如执行WordCount程序，确保Hadoop集群正常运行。

以上是CDH版本Hadoop的基本安装过程，具体的安装步骤可能会因版本和需求的不同而有所不同。
```



17.hadoop namenode宕机怎么办

```
如果Hadoop的NameNode宕机了，需要采取以下步骤进行恢复：

确认NameNode宕机：首先需要确认NameNode是否真的宕机，可以通过查看日志文件或者在管理节点上使用hdfs haadmin命令检查NameNode的状态。

切换Active NameNode：如果使用了HDFS的HA（高可用）功能，需要手动切换Active NameNode。可以使用hdfs haadmin命令进行切换。

恢复NameNode：如果NameNode宕机是由于软件或硬件故障引起的，需要进行相应的恢复操作。例如，如果NameNode所在的服务器故障，需要更换服务器或修复故障。

恢复HDFS数据：如果NameNode宕机导致了HDFS数据的损失或者丢失，需要进行相应的数据恢复操作。可以使用Hadoop自带的fsck命令进行文件系统检查和修复。

启动NameNode：在确认恢复操作完成之后，需要启动NameNode。可以使用hadoop-daemon.sh脚本启动NameNode，也可以在CDH Manager的Web界面中启动NameNode。

验证集群状态：在NameNode启动之后，需要验证集群状态是否正常。可以使用hdfs dfsadmin命令或者在CDH Manager的Web界面中查看集群状态。

以上是恢复NameNode宕机的基本步骤，具体操作可能会因集群环境和故障原因的不同而有所不同。在操作之前，建议备份重要数据，以避免数据的丢失和损坏。
```



18.什么是hadoop脑裂？如何避免？

```
在HA架构中有一个非常重要的问题，同一时刻必须保证2个NameNode只有一个处于Active状态，另一个
处于Standby状态.否则就会出现2个NameNode同时修改命名空间的问题，即发生脑裂.
脑裂的HDFS集群很可能执行错误的指令，造成数据块丢失等.
为了防止脑裂的情况，HDFS提供了三个级别的隔离机制（fencing）：
1.客户端隔离：同一时间只允许一个NameNode响应客户端的请求。
2.DataNode隔离：同一时间只允许一个NameNode向DataNode发送指令，如删除、复制数据块等.
3.共享存储隔离：同一时间只允许一个NameNode向JournallNodes写人edits日志数据.
```



19.简述HDFS的副本机制？

```
HDFS的副本机制是指将数据文件分成多个块，并在集群中的多台机器上复制多份块，以提高数据的可靠性和容错性。HDFS的副本机制是Hadoop分布式存储的核心特性之一。

当一个文件被存储到HDFS上时，它会被分割成多个固定大小的块，每个块都有一个唯一的标识符。这些块被复制到集群中的多台机器上，其中一份是原始块，其余是副本块。默认情况下，HDFS在三台不同的机器上创建三个副本，以确保数据的可靠性和容错性。这些副本被存储在不同的机架上，以防止机架级故障。

当一个块的副本发生故障时，HDFS会从其他机器上复制该块的副本来替换损坏的副本。如果没有其他可用的副本，那么HDFS会从原始块复制一个新的副本。这个过程被称为块复制，它保证了在出现硬件故障或其他异常情况时，数据仍然可以被访问和恢复。

HDFS的副本机制可以有效地提高数据的可靠性和可用性，同时也对集群的存储空间和网络带宽产生了一定的压力。因此，在实际应用中，需要根据实际需求和集群规模来调整HDFS的副本数和块大小等参数，以达到最佳的性能和资源利用率。

HDFS机架感知：
HDFS的机架感知（Rack Awareness）是指Hadoop集群的节点分布在不同的机架上，HDFS可以根据节点所在的机架信息进行数据的存储和访问，以提高数据的读写效率和网络带宽利用率。

HDFS的机架感知主要涉及到三个概念：

1.机架：Hadoop集群中的节点被组织成多个机架，每个机架包含多个节点，通常是物理上相邻的服务器架构。
2.数据块复制：HDFS存储数据时会将数据切分成多个块，并复制到不同的节点上，通常是在不同的机架上创建多个副本。
3.客户端访问：客户端在访问数据时需要与存储该数据块的节点进行通信，HDFS可以根据节点所在的机架信息选择合适的节点进行访问。

HDFS的机架感知通过将节点分配到不同的机架上，并根据节点所在的机架信息选择存储数据块和访问数据节点，从而减少了数据在机架之间传输的开销，提高了数据的访问速度和网络带宽利用率。同时，机架感知还可以提高Hadoop集群的容错性和可用性，以应对机架级别的故障。
```

































Hadoop和Spark有什么区别？

```
Hadoop和Spark都是大数据处理的常用工具，但有以下区别：

（1）计算模型不同：Hadoop使用MapReduce计算模型，而Spark使用基于内存的计算模型。
（2）实时性不同：Hadoop的处理模式是批处理，而Spark支持流式处理和实时处理。
（3）适用场景不同：Hadoop适用于大规模的批量数据处理，而Spark适用于实时数据处理和机器学习等场景。
（4）资源利用率不同：Spark能够更好地利用集群中的资源，执行速度相对更快。
```

























14.SecondaryNameNode 工作机制?


16.





###### 





# 重点：MapReduce

简述mapreduce的设计思想?

```
MapReduce是一种用于处理大规模数据集的编程模型和软件框架，它的设计思想是将计算任务分为多个小任务，将这些小任务并行处理，然后将结果合并起来形成最终的结果。MapReduce的设计思想包括以下几个方面：

1.分布式处理：MapReduce采用分布式处理的方式，将大规模数据集划分为多个小数据块，每个小数据块由一个Map任务处理，然后将处理结果汇总到Reduce任务中进行最终的结果生成。

2.映射和归约：MapReduce将计算任务分为两个阶段：映射（Map）和归约（Reduce）。映射阶段负责将输入数据分解成小块，然后将这些小块交给不同的处理器进行并行处理，每个处理器输出一个键值对。归约阶段将映射阶段输出的键值对进行汇总和聚合，生成最终的结果。

3.容错性和可扩展性：MapReduce提供了容错机制和可扩展性，使得其能够应对大规模的数据处理任务。如果某个处理器出现故障，MapReduce可以自动将其替换，而不会影响整个系统的运行。同时，MapReduce可以在需要时动态地增加或减少处理器，以满足不同的数据处理需求。

4.简化编程：MapReduce的设计使得程序员可以专注于计算逻辑的实现，而无需考虑分布式处理和容错机制等底层实现细节。这使得开发人员可以更快地开发出高质量的程序，并且更容易维护。

总之，MapReduce的设计思想是将大规模数据集分为多个小块进行并行处理，并提供容错性和可扩展性，从而简化了大规模数据处理的编程和实现。

一个常见的例子是用MapReduce处理网站的日志文件以提取有用的信息。假设一个网站有数百万的访问者，每个访问者都会在服务器上留下一条日志记录。这些日志记录可能包含大量信息，包括用户的IP地址、访问时间、访问页面等等。

要从这些日志记录中提取有用的信息，可以使用MapReduce。首先，将日志文件分成多个小块，每个小块由一个Map任务处理。在Map阶段，Map函数会解析每条日志记录并提取出有用的信息，例如用户的IP地址、访问时间和访问页面。Map函数会将提取出的信息转换成键值对，并输出到中间结果文件中。

在Reduce阶段，Reduce函数会从中间结果文件中读取Map函数输出的键值对，并进行聚合。例如，可以统计每个IP地址的访问次数，每个页面的访问次数等等。最终的结果可以以表格或图形的形式呈现，帮助网站管理员更好地了解网站的访问情况，并作出相应的决策。
```







MapTask工作机制？



MapTask的个数由什么决定？

```

```

10.NameNode的工作机制？NameNode 和 SecondaryNameNode的区别？ NameNode宕机如何解决？

```

```

11.DataNode的工作机制？



15.Map和Reduce的执行步骤？



如何决定一个job的map和reduce的数量?



ReduceTask工作机制



请描述mapReduce有几种排序及排序发生的阶段。

简述

介绍下大数据中的canal：

```
Canal是阿里巴巴开源的一种基于MySQL数据库的增量数据同步组件，它可以实时地捕获MySQL数据库的变更日志，将数据变更信息解析为逻辑事件，并将这些逻辑事件传输到下游消费端。Canal可以将MySQL数据库的增量数据同步到其他MySQL数据库或者NoSQL数据库，例如HBase、MongoDB等。
Canal的工作原理如下：
1.Canal通过解析MySQL数据库的binlog日志，捕获增量数据变更的信息。
2.Canal将捕获的数据变更信息解析为逻辑事件，并将这些事件存储到自己的内存缓存中。
3.Canal通过TCP协议将这些逻辑事件传输到下游消费端。
4.下游消费端从Canal中获取逻辑事件，并将其应用到目标数据库中。

Canal的主要特点包括：
1.高性能：Canal通过多线程和异步处理机制，能够高效地捕获和传输MySQL数据库的增量数据变更。
2.可靠性：Canal使用基于时间戳的位点机制来记录同步进度，保证同步的可靠性。
3.灵活性：Canal支持多种消费端，包括Kafka、RocketMQ等消息队列，以及Hadoop、HBase、MongoDB等NoSQL数据库，可以满足不同场景下的数据同步需求。
4.易用性：Canal提供了简单易用的管理界面和API，可以方便地进行配置和管理。

总的来说，Canal是一种高效、可靠、灵活和易用的增量数据同步组件，可以在大数据环境中提供可靠的数据同步解决方案。
```

什么是ETL？：

```mysql
ETL的全称是Extract, Transform, Load，即数据抽取、转换和加载。它是一种常用的数据集成方式，用于将数据从一个或多个源系统中抽取出来，经过转换后加载到目标系统中，以支持数据分析、报表生成、业务流程等需求。

具体来说，ETL包括以下三个过程：

1.数据抽取（Extract）：从源系统中抽取数据，并将数据存储在一个临时区域中，通常是一个数据仓库或者数据湖。数据抽取的方式可以是基于时间、基于事件或者基于增量等方式。

2.数据转换（Transform）：对抽取的数据进行清洗、加工、合并、过滤等一系列处理，以便将其转换为符合业务需求的格式。数据转换可以使用各种工具和技术，例如SQL、Python、Spark等。

3.数据加载（Load）：将转换后的数据加载到目标系统中，以供后续的数据分析、报表生成、业务流程等使用。数据加载的方式可以是全量加载、增量加载、实时加载等方式。

ETL是数据集成的核心技术之一，常用于数据仓库、数据湖、数据集市等大数据架构中，以实现不同数据源之间的数据集成和交换。随着大数据技术的不断发展，ETL技术也在不断创新和演化，例如ELT（Extract, Load, Transform）、DataOps等，以满足不同场景下的数据集成需求。
```

介绍下大数据中的OGG组件

```mysql
OGG（Oracle GoldenGate）是一种数据集成工具，可用于大数据环境中的数据复制和数据同步。OGG提供了可靠、高效、实时的数据复制和数据同步解决方案，支持异构数据库之间的数据交换，同时不会对源系统的性能产生影响。

OGG包括多个组件，其中最核心的是 Extract、Replicat、Manager 和 Trail。下面分别对这些组件进行介绍：

1.Extract：该组件用于从源数据库中捕获数据，并将其转换为OGG内部格式的数据。Extract组件可以通过多种方式捕获数据，例如从日志文件中捕获、使用SQL查询捕获等。

2.Replicat：该组件用于将OGG内部格式的数据应用到目标数据库中。Replicat组件可以根据需要执行数据转换，例如进行数据过滤、数据映射等。

3.Manager：该组件用于管理OGG进程，例如启动/停止进程、监控进程、配置参数等。Manager组件还可以与其他OGG组件通信，例如通过Replicat组件向源数据库发送心跳信号，以确保源系统的可用性。

4.Trail：该组件用于存储OGG内部格式的数据，以便Extract和Replicat组件可以读取和写入数据。Trail组件可以存储在文件系统或数据库中，也可以分布在多个节点上以提高可伸缩性和容错性。

以上是OGG的主要组件。在大数据环境中，OGG通常与Hadoop、Hive、Kafka等大数据技术一起使用，以提供可靠的数据复制和数据同步解决方案。
```



**2.查询平均成绩大于60分的学生的学号姓名和各学科平均成绩,并按成绩降序排序（简单，第二道重点）**

```mysql
SELECT 
st.s_id,st.s_name,t.avg_score
FROM 
Student st 
inner join (SELECT s_id ,AVG(s_score) as avg_score FROM Score s group by s_id HAVING AVG(s_score)>60) t
ON st.s_id = t.s_id 
ORDER by avg_score DESC;
```

**3、查询所有学生的学号、姓名、选课数、总成绩（不重要）**

```mysql
SELECT st.s_id,st.s_name ,B.classNum,B.sumScore FROM Student st
inner Join(SELECT s_id,COUNT(c_id) as classNum,SUM(s_score) as sumScore FROM Score  group by s_id ) B 
ON  st.s_id = B.s_id;
```

**4.查询姓“李”的老师的个数（不重要）**

```mysql
SELECT COUNT(t_name) FROM Teacher t where t_name like '李%';
```

**4.1查询姓“李”且名字只有2个字的老师的个数（不重要）**

```mysql
SELECT COUNT(t_name) FROM Teacher t where t_name like '李_';
```



**5.查询没学过“张三”老师课的学生的学号、姓名（重点）**

```mysql
SELECT s_name FROM Student s2 
left join 
(SELECT stu.s_name as stu_name 
FROM Score sc
left join Course c on sc.c_id  = c.c_id 
left join Student stu  on stu.s_id  = sc.s_id 
left join Teacher tea   on tea.t_id  = c.t_id
WHERE t_name ="张三") temp
ON  s2.s_name = temp.stu_name
where temp.stu_name IS NULL ;

或：
SELECT s_id ,s_name FROM Student s2 
where s_id not in 
(SELECT s_id  
FROM Score sc
join Course c on sc.c_id  = c.c_id 
join Teacher tea   on tea.t_id  = c.t_id
WHERE t_name ="张三");

```

**6.查询学过“张三”老师所教的所有课的同学的学号、姓名（重点）**

```mysql
SELECT s_id ,s_name FROM Student s2 
where s_id  in 
(SELECT s_id  
FROM Score sc
join Course c on sc.c_id  = c.c_id 
join Teacher tea   on tea.t_id  = c.t_id
WHERE t_name ="张三");
```

7.**查询学过编号为“01”的课程并且也学过编号为“02”的课程的学生的学号、姓名（重点）**

```
SELECT s_id,s_name
FROM 
Student  
where s_id in(
SELECT 
a.s_id 
FROM(
(SELECT s_id FROM Score  where c_id = '01')a
JOIN (
SELECT s_id FROM Score  where c_id = '02')b
ON a.s_id = b.s_id));
```

**8.查询课程编号为“02”的课程的名称和总成绩（不重点）**

```mysql
SELECT 
c.c_name ,SUM( s.s_score) 
FROM Score s join Course c on s.c_id  = c.c_id 
where s.c_id ="02";
```

**9.查询所有课程成绩小于60分的学生的学号、姓名(和题目二类似,略)**

**10.查询没有学全所有课的学生的学号、姓名(重点)**

```mysql
SELECT s.s_name,sc.s_id ,COUNT(DISTINCT sc.c_id) FROM Score sc 
join Student s 
on sc.s_id = s.s_id 
group by sc.s_id 
HAVING COUNT( c_id) < (SELECT COUNT(c_id)  FROM Course c)
```

**11.查询至少有一门课与学号为“01”的学生所学课程相同的学生的学号和姓名（重点）**

```
SELECT stu.s_name,stu.s_id 
FROM 
Student stu 
JOIN
(SELECT DISTINCT s_id FROM Score s 
where c_id IN (SELECT c_id FROM Score s where s_id ='01')AND s_id !='01') temp1 
ON stu.s_id = temp1.s_id;
```

**11.1:查询和01号学员所选课程一模一样的学员的s_id**

```mysql
SELECT s_id FROM Score s4 
GROUP by s_id 
HAVING s_id not in (SELECT s_id FROM Score s3 where c_id  not in (SELECT c_id FROM  Score s2 where s_id = 01))
AND COUNT(*) =  (SELECT COUNT(1) FROM  Score s2 where s_id = 01) AND s_id !='01' ;
```





**12.查找出和01学员所选的课程一模一样的学生的姓名和Id**

```
select t2.s_id from 
# 找到和01号学生选择相同数量课程的同学
(select t1.s_id from (select s_id, count(s_id) count from Score group by s_id) t1 where t1.count = 
	(select count(*) from Score where s_id = '01'))t2
inner join 
# 排除选择其他课程的同学
(select distinct(s_id) from Score where s_id != (select s_id from Score where c_id not in 
	(select c_id from Score where s_id = '01')))t3
on t2.s_id = t3.s_id
where t2.s_id != '01';
```

**13.查询没学过"张三"老师讲授的任一门课程的学生姓名（重点）**

```
SELECT s_id ,s_name 
FROM Student s3 where s_id NOT IN (
SELECT 
DISTINCT s_id 
FROM Score s2 
where c_id in
(SELECT c_id FROM Course c where t_id  = (SELECT t_id FROM Teacher t2 where t_name = '张三'))); 
```

**14.查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩（重点）**

```mysql
SELECT s.s_name ,tempTab.s_id,tempTab.cnt from Student s join
(
SELECT s_id,COUNT( DISTINCT c_id) as cnt FROM Score s  
WHERE s_score < 60  
GROUP BY s_id 
HAVING  COUNT( DISTINCT c_id) >= 2) tempTab
ON s.s_id  = tempTab.s_id;
```

**15.查询每门课程的选课人数**

```mysql
select s.c_id ,c.c_name ,COUNT(*)  FROM Score s 
JOIN Course c 
on s.c_id = c.c_id
group by s.c_id;
```

**16.检索"01"课程分数小于60，按分数降序排列的学生信息（和34题重复，不重点）**

```msql
SELECT s.s_name ,tempTab.s_id,tempTab.s_score from Student s join
(
SELECT s_id ,s_score FROM Score s  
WHERE s_score < 60  AND c_id = '01'
ORDER BY s_score desc 
) tempTab
ON s.s_id  = tempTab.s_id;
```

**17.按平均成绩从高到低显示所有学生的所有课程的总成绩以及平均成绩**

```
SELECT s.s_name,tempTab.s_id,tempTab.av_score,tempTab.sum_score from Student s join
(
SELECT s_id ,AVG(s_score) AS av_score,SUM(s_score) AS sum_score FROM Score s  
GROUP BY s_id 
) tempTab
ON s.s_id  = tempTab.s_id
ORDER BY tempTab.av_score desc ;
```

**17-02.按平均成绩从高到低显示所有学生的每一门成绩以及平均成绩**

```mysql
SELECT stu.s_name,temp.语文,temp.数学,temp.英语 ,temp.avg_sc FROM Student stu
left join (
SELECT IFNULL(s_id,'TOTAL') AS userid,
SUM(IF(`c_id`='01',s_score,0)) AS 语文,
SUM(IF(`c_id`='02',s_score,0)) AS 数学,
SUM(IF(`c_id`='03',s_score,0)) AS 英语,
AVG(s_score) as avg_sc 
FROM Score
GROUP BY s_id 
 )temp
on stu.s_id = temp.userid
ORDER BY temp.avg_sc DESC;
```

**18.查询各科成绩最高分、最低分和平均分：以如下形式显示：课程ID，课程name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率、选课人数，最后结果按照人数降序，相同的话按课程ID升序**

```mysql
SELECT 
s.c_id,
c.c_name ,
COUNT(*) as stuNum, 
MAX(s_score),
MIN(s_score),
AVG(s_score) s_score ,
SUM(case when s_score >=60 then 1 else 0 end)/COUNT(*) as pass_rate , #及格率
SUM(case when s_score between 70 and 79  then 1 else 0 end)/COUNT(*) as secondary ,#中等率
SUM(case when s_score between 80 and 89  then 1 else 0 end)/COUNT(*) as good,
SUM(case when s_score >=90  then 1 else 0 end)/COUNT(*) as excellent
FROM Score s  
join Course c on s.c_id = c.c_id 
GROUP BY s.c_id 
ORDER BY stuNum DESC ,s.c_id;
```

**19.对成绩表里的score进行排序，并显示排名**

```
SELECT s_id ,c_id ,s_score ,row_number() OVER(ORDER BY s_score DESC) as tp FROM Score;
```

 **29.查询名字中含有"风"字的学生信息（不重点）**

```
SELECT * FROM  Student s where s_name like "%风%";
```

**30.查询名字中含有"风"字的学生信息**

```mysql
SELECT * FROM  Student s where s_birth LIKE "1990%";
```

**31.查询1990年出生的学生名单（重点year）**

```mysql
SELECT * FROM  Student s where s_birth LIKE "1990%";

#或者使用SUBSTRING_INDEX方法切割字符串
SELECT * FROM  Student s3 where SUBSTRING_INDEX(s_birth,"-",1) = "1990"; 
```



**32.查询男生女生分别有多少人**

```mysql
SELECT s_sex ,COUNT(*)  FROM  Student s3 group by s_sex ;
```



**33.查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按 课程编号升序排列**

```mysql
SELECT c.c_name ,s2.c_id ,AVG(s_score) as svg_score FROM  Score s2 
JOIN Course c 
on s2.c_id  = c.c_id
group by s2.c_id 
ORDER by svg_score DESC, c.c_id asc;
```



**34.查询平均成绩大于等于 85 的所有学生的学号、姓名和平均成绩,并按平均成绩降序排序**

```mysql
SELECT s.s_name ,s2.s_id,AVG(s2.s_score)as avg_sc FROM  Score s2 
JOIN Student s 
on s2.s_id = s.s_id 
group by s2.s_id 
having avg_sc >85 
order by avg_sc desc;
```



**35.查询课程名称为「数学」，且分数低于 60 的学生姓名和分数**

```mysql
SELECT t_b.s_name ,t_a.* FROM 
(select * from  Score s2 where s_score < 60 AND c_id =(SELECT c_id FROM  Course c where c_name ='数学'))as t_a
JOIN Student t_b 
on t_a.s_id  = t_b.s_id ;
```

**36.查询各科成绩排名前三的学生信息（相同数据排名相同）**

```mysql
SELECT *, RANK ()over(PARTITION by c_id,ORDER by s_score DESC) as rk from Score s2 where rk >=3;
```

# ***Yarn***

dsadassdsadsa

# ***impala***

dsasadadsadsadas



# ***Java&Java操作组件***

**1.什么是javabean**

```mysql
JavaBean是指一种符合Java语言编程规范的Java类，主要用于表示数据或服务的简单Java对象。JavaBean类必须具有无参构造函数，并且可以通过getter和setter方法来访问和设置类中的属性值。

JavaBean通常用于在Java应用程序中传递数据和状态信息。它们可以被序列化为XML或JSON等格式，从而支持数据的持久化和网络传输。JavaBean还可以被用作组件，通过JavaBean API和其他工具来操纵和管理它们的属性和事件。

JavaBean作为Java语言的核心特性之一，被广泛应用于Java图形界面编程、Java Web应用程序开发、企业应用程序开发等领域。
```

一个简单的javaBean

```java
public class Student {
    private String name;
    private int age;
    private String gender;
    public Student() {
        // 无参构造函数
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public String getGender() {
        return gender;
    }
    public void setGender(String gender) {
        this.gender = gender;
    }
}

```





**2.reflect：**

```mysql
"reflect"通常指的是Java中的反射机制，它允许程序在运行时获取类的信息、调用对象的方法和访问对象的属性等。

在Java中，每个类都有一个Class对象来表示该类，反射机制可以通过Class对象来获取类的信息。通过Class对象，程序可以获取类的构造方法、成员变量、方法、注解等信息，并且可以在运行时动态创建对象、调用方法、设置属性等。

反射机制使用Java中的java.lang.reflect包中的类和接口来实现。常用的类包括Class类、Constructor类、Field类和Method类等。

例如，通过Class类可以获取类的名称、修饰符、父类、接口、构造方法、成员变量、方法等信息。Constructor类用于表示类的构造方法，可以获取构造方法的名称、修饰符、参数类型等信息，并且可以通过newInstance方法动态创建对象。Field类用于表示类的成员变量，可以获取成员变量的名称、修饰符、类型等信息，并且可以通过set和get方法修改和获取变量的值。Method类用于表示类的方法，可以获取方法的名称、修饰符、返回类型、参数类型等信息，并且可以通过invoke方法调用方法。

反射机制可以为Java程序带来很大的灵活性和扩展性，但是也存在一些性能问题，因为在运行时需要动态获取类的信息，所以反射操作的效率比直接操作类的性能要低。因此，在使用反射机制时需要考虑性能问题，并且需要避免滥用反射，尽可能使用静态类型检查和编译时检查来保证程序的安全性和可维护性。
```



**（1）每个店铺的UV和PV（访客数、被访问次数）**

```mysql
/*每个店铺的uv和pv
*/
SELECT 
shop ,count(DISTINCT user_id) as uv,COUNT(user_id)as pv 
FROM 
test2
group by shop;
```

**(2)每个店铺访问次数top3的访客信息。输出店铺名称、访客id、访问次数 **

```mysql
#重点是先通过同时对两个字段分组，把每个用户在每个店铺的访问次数字段加上
SELECT 
t2.user_id,t2.shop,t2.cnt, t2.top
FROM 
(SELECT 
t1.user_id,t1.shop,t1.cnt, dense_rank () over(PARTITION by t1.shop ORDER by t1.cnt desc )as top
FROM 
(SELECT user_id,shop,count(*) AS cnt
FROM mianshi.test2
GROUP BY user_id,shop)as t1 
ORDER by shop,top)as t2
WHERE t2.top <=3;
```

**3.已知一个表STG.ORDER，有如下字段:Date，Order_id，User_id，amount。 数据样例:2017-01-01,10029028,1000003251,33.57。 请给出sql进行统计: (1)给出 2017年每个月的订单数、用户数、总成交金额。 (2)给出2017年11月的新客数(指在11月才有第一笔订单) 实现**

```
CREATE TABLE test_sql.test3 (
dt string, order_id string, user_id string, amount DECIMAL ( 10, 2 ) )
ROW format delimited FIELDS TERMINATED BY '\t';
INSERT INTO TABLE test_sql.test3 VALUES ('2017-01-01','10029028','1000003251',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-01-01','10029029','1000003251',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-01-01','100290288','1000003252',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-02-02','10029088','1000003251',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-02-02','100290281','1000003251',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-02-02','100290282','1000003253',33.57);
INSERT INTO TABLE test_sql.test3 VALUES ('2017-11-02','10290282','100003253',234);
INSERT INTO TABLE test_sql.test3 VALUES ('2018-11-02','10290284','100003243',234);
```



***(1)给出 2017年每个月的订单数、用户数、总成交金额。 **

```
SELECT t1.mon, count(t1.order_id) AS order_cnt, count(DISTINCT t1.user_id) AS user_cnt, sum(amount) AS total_amount
FROM
(SELECT order_id, user_id, amount, date_format(dt,'yyyy-MM') mon
FROM mianshi.test3
WHERE date_format(dt,'yyyy') = '2017') t1
GROUP BY t1.mon
```

*** (2)给出2017年11月的新客数(指在11月才有第一笔订单的客户的数量) 实现**

```mysql
SELECT COUNT(*) 
FROM test3 where dt LIKE "2017-11%" AND user_id 
NOT IN(
SELECT 
user_id 
from
(SELECT order_id, user_id, amount, date_format(dt,'MM') m,date_format(dt,'yyyy') y
FROM mianshi.test3)as t1
where t1.y = '2017'AND t1.m <11);

或者（更高效）：
select COUNT(*) 
from test3 group by user_id
having min(date_format(dt,'yyyy-MM'))='2017-11';
```



**4.已知有一个5000万的用户文件(user_id，name，age)，一个2亿记录的用户看电影的记录文件(user_id，url)，统计各个年龄段观看电影的次数并按年龄从小到大排序（每10岁一个年龄段，比如：0-10,11-20,21-30）**

```mysql
CREATE TABLE  mianshi.test4user
(user_id string,name string,age int);
CREATE TABLE  mianshi.test4log
(user_id string,url string);


INSERT INTO TABLE  mianshi.test4user VALUES('001','u1',10);
INSERT INTO TABLE  mianshi.test4user VALUES('002','u2',15);
INSERT INTO TABLE  mianshi.test4user VALUES('003','u3',15);
INSERT INTO TABLE  mianshi.test4user VALUES('004','u4',20);
INSERT INTO TABLE  mianshi.test4user VALUES('005','u5',25);
INSERT INTO TABLE  mianshi.test4user VALUES('006','u6',35);
INSERT INTO TABLE  mianshi.test4user VALUES('007','u7',40);
INSERT INTO TABLE  mianshi.test4user VALUES('008','u8',45);
INSERT INTO TABLE  mianshi.test4user VALUES('009','u9',50);
INSERT INTO TABLE  mianshi.test4user VALUES('0010','u10',65);
INSERT INTO TABLE  mianshi.test4log VALUES('001','url1');
INSERT INTO TABLE  mianshi.test4log VALUES('002','url1');
INSERT INTO TABLE  mianshi.test4log VALUES('003','url2');
INSERT INTO TABLE  mianshi.test4log VALUES('004','url3');
INSERT INTO TABLE  mianshi.test4log VALUES('005','url3');
INSERT INTO TABLE  mianshi.test4log VALUES('006','url1');
INSERT INTO TABLE  mianshi.test4log VALUES('007','url5');
INSERT INTO TABLE  mianshi.test4log VALUES('008','url7');
INSERT INTO TABLE  mianshi.test4log VALUES('009','url5');
INSERT INTO TABLE  mianshi.test4log VALUES('0010','url1');
```

