[TOC]

# References


- Hadoop学习路线


## What Is Apache Hadoop?
The Apache™ Hadoop® project develops open-source software for reliable, scalable, distributed computing.

Apache™Hadoop®项目开发用于可靠，可扩展，分布式计算的开源软件。

The Apache Hadoop software library is a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage. Rather than rely on hardware to deliver high-availability, the library itself is designed to detect and handle failures at the application layer, so delivering a highly-available service on top of a cluster of computers, each of which may be prone to failures.

Apache Hadoop软件库是一个框架，允许使用简单的编程模型在大量计算机上对大型数据集进行分布式处理。 它旨在从单个服务器扩展到数千台机器，每台机器都提供本地计算和存储。 库本身不是依靠硬件来提供高可用性，而是设计用于检测和处理应用程序层的故障，因此在一组每个计算机都可能出现故障的集群上提供高可用性服务。

The project includes these modules:

- **Hadoop Common:** The common utilities that support the other Hadoop modules.
支持其他Hadoop模块的常用工具。
- **Hadoop Distributed File System (HDFS™):** A distributed file system that provides high-throughput access to application data.
分布式文件系统，提供对应用程序数据的高吞吐量访问。
- **Hadoop YARN:** A framework for job scheduling and cluster resource management.
作业调度和集群资源管理的框架。
- **Hadoop MapReduce:** A YARN-based system for parallel processing of large data sets.
一种基于YARN的大型数据集并行处理系统。

Other Hadoop-related projects at Apache include:

- *Ambari™*: A web-based tool for provisioning, managing, and monitoring Apache Hadoop clusters which includes support for Hadoop HDFS, Hadoop MapReduce, Hive, HCatalog, HBase, ZooKeeper, Oozie, Pig and Sqoop. Ambari also provides a dashboard for viewing cluster health such as heatmaps and ability to view MapReduce, Pig and Hive applications visually alongwith features to diagnose their performance characteristics in a user-friendly manner.
用于配置，管理和监控Apache Hadoop集群的基于Web的工具，其中包括支持Hadoop HDFS，Hadoop MapReduce，Hive，HCatalog，HBase，ZooKeeper，Oozie，Pig和Sqoop。 Ambari还提供了一个用于查看集群健康状况的仪表板，例如散热图，以及可视化查看MapReduce，Pig和Hive应用程序以及以用户友好的方式诊断其性能特征的功能的功能。
- *Avro™*: A data serialization system.
数据序列化系统
- *Cassandra™*: A scalable multi-master database with no single points of failure.
可扩展的多主数据库，没有单点故障。
- *Chukwa™*: A data collection system for managing large distributed systems.
用于管理大型分布式系统的数据收集系统。
- *HBase™*: A scalable, distributed database that supports structured data storage for large tables.
可扩展的分布式数据库，支持大型表格的结构化数据存储。
- *Hive™*: A data warehouse infrastructure that provides data summarization and ad hoc querying.
数据仓库基础设施，提供数据汇总和即席查询。
- *Mahout™*: A Scalable machine learning and data mining library.
可扩展机器学习和数据挖掘库。
- *Pig™*: A high-level data-flow language and execution framework for parallel computation.
用于并行计算的高级数据流语言和执行框架。
- *Spark™*: A fast and general compute engine for Hadoop data. Spark provides a simple and expressive programming model that supports a wide range of applications, including ETL, machine learning, stream processing, and graph computation.
用于Hadoop数据的快速和通用的计算引擎。 Spark提供了一个简单而富有表现力的编程模型，支持各种应用，包括ETL，机器学习，流处理和图形计算。
- *Tez™*: A generalized data-flow programming framework, built on Hadoop YARN, which provides a powerful and flexible engine to execute an arbitrary DAG of tasks to process data for both batch and interactive use-cases. Tez is being adopted by Hive™, Pig™ and other frameworks in the Hadoop ecosystem, and also by other commercial software (e.g. ETL tools), to replace Hadoop™ MapReduce as the underlying execution engine.
一个基于Hadoop YARN的通用数据流编程框架，它提供了一个强大而灵活的引擎来执行任意DAG的任务来处理批量和交互式用例的数据。 Tez被Hive™，Pig™和Hadoop生态系统中的其他框架以及其他商业软件（例如ETL工具）所采用，以替代Hadoop™MapReduce作为底层执行引擎。
- *ZooKeeper™*: A high-performance coordination service for distributed applications.
分布式应用程序的高性能协调服务。

## General

The followings steps are for Linux only

### Setting up a Single Node Cluster

#### Required software for Linux include:

1. Java™ must be installed. Recommended Java versions are described at HadoopJavaVersions.

2. ssh must be installed and sshd must be running to use the Hadoop scripts that manage remote Hadoop daemons if the optional start and stop scripts are to be used. Additionally, it is recommmended that pdsh also be installed for better ssh resource management.

#### Installing Software

If your cluster doesn’t have the requisite software you will need to install it.

For example on Ubuntu Linux:

```shell
  $ sudo apt-get install ssh
  $ sudo apt-get install pdsh
```

#### Download

To get a Hadoop distribution, download a recent stable release from one of the Apache Download Mirrors.

#### Prepare to Start the Hadoop Cluster

Unpack the downloaded Hadoop distribution. In the distribution, edit the file etc/hadoop/hadoop-env.sh to define some parameters as follows:

```shell
  # set to the root of your Java installation
  export JAVA_HOME=/usr/java/latest
```
**Notice:** 

```shell
Do not use : export JAVA_HOME=${JAVA_HOME} !

否则后面在执行shell脚本时，会报：

localhost: Error: JAVA_HOME is not set.
```

Try the following command:

```shell
$ bin/hadoop
```

This will display the usage documentation for the hadoop script.

Now you are ready to start your Hadoop cluster in one of the three supported modes:

- Local (Standalone) Mode
- Pseudo-Distributed Mode(伪分布模式)
- Fully-Distributed Mode

#### Standalone Operation

By default, Hadoop is configured to run in a non-distributed mode, as a single Java process. This is useful for debugging.

The following example copies the unpacked conf directory to use as input and then finds and displays every match of the given regular expression. Output is written to the given output directory.

```shell
  $ mkdir input
  $ cp etc/hadoop/*.xml input
  $ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-<version>.jar grep input output 'dfs[a-z.]+'
  $ cat output/*
```

	 Pseudo-Distributed Operation

Hadoop can also be run on a single-node in a pseudo-distributed mode where each Hadoop daemon runs in a separate Java process.

##### Configuration

Use the following:

```shell
#etc/hadoop/core-site.xml:

<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>

#etc/hadoop/hdfs-site.xml:

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>

```
##### Setup passphraseless(免密码) ssh

```shell
#Now check that you can ssh to the localhost without a passphrase(密码):

$ ssh localhost

#If you cannot ssh to localhost without a passphrase, execute the following commands:

$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys

```

##### Execution

The following instructions are to run a MapReduce job locally. If you want to execute a job on YARN, see YARN on Single Node.

```shell
#1.Format the filesystem:

$ bin/hdfs namenode -format

#2.Start NameNode daemon and DataNode daemon:

$ sbin/start-dfs.sh

#The hadoop daemon log output is written to the $HADOOP_LOG_DIR directory (defaults to $HADOOP_HOME/logs).

#3.Browse the web interface for the NameNode; by default it is available at:

NameNode - http://localhost:9870/
```

**Notice:** 

这里是最新文档，如果你用的是Hadoop 3.0 之前的版本应为http://localhost:50070/，localhost也要换成相应的IP。

```shell
#4.Make the HDFS directories required to execute MapReduce jobs:

$ bin/hdfs dfs -mkdir /user
$ bin/hdfs dfs -mkdir /user/<username>
#这里的username指你的操作系统用户，这里没有创建后面创建input目录时会报错。

#5.Copy the input files into the distributed filesystem:

$ bin/hdfs dfs -mkdir input
#相对路径创建，/user/<username>/input
$ bin/hdfs dfs -put etc/hadoop/*.xml input

#6.Run some of the examples provided:

$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-<version>.jar grep input output 'dfs[a-z.]+'

#7.Examine the output files: Copy the output files from the distributed filesystem to the local filesystem and examine them:

$ bin/hdfs dfs -get output output
$ cat output/*

#or
#View the output files on the distributed filesystem:

$ bin/hdfs dfs -cat output/*

#8.When you’re done, stop the daemons with:

$ sbin/stop-dfs.sh
```

##### YARN on a Single Node

You can run a MapReduce job on YARN in a pseudo-distributed mode by setting a few parameters and running ResourceManager daemon and NodeManager daemon in addition.

The following instructions assume that 1. ~ 4. steps of the above instructions are already executed.

Configure parameters as follows:

```shell
#etc/hadoop/mapred-site.xml:

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>

#etc/hadoop/yarn-site.xml:

<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.env-whitelist</name>
        <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
    </property>
</configuration>

#Start ResourceManager daemon and NodeManager daemon:

$ sbin/start-yarn.sh

#Browse the web interface for the ResourceManager; by default it is available at:

ResourceManager - http://localhost:8088/

# Run a MapReduce job.

When you’re done, stop the daemons with:

$ sbin/stop-yarn.sh
```


##### Build instructions for Hadoop



##### Hadoop Commans Guide

#### Overview
All of the Hadoop commands and subprojects follow the same basic structure:

Usage: shellcommand [SHELL_OPTIONS]  [COMMAND]  [GENERIC_OPTIONS]  [COMMAND_OPTIONS]

Field | Description
---|---
shellcommand | The command of the project being invoked.For example,Hadoop common uses *hadoop*,HDFS uses *hdfs*,and YARN uses *yarn*.


#### 本地模式、伪分布式模式和分布式模式

本地模式，使用的是本地文件系统。在该模式下，执行Hadoop job时，Map task和Reduce task在同一进程中执行。

真实的集群配置的都是分布式模式，其中所有没有完整URL指定的路径默认都是分布式文件系统（通常是HDFS）中的路径，而且由JobTracker服务来管理job，不同的task在不同的进程中执行。

对于在个人计算机上工作的开发者来说，一个进退两难的实际问题是，本地模式并不能真实地反映真实集群的行为状况，这个是测试程序时需要记住的事情。为了解决这个需求，一台物理机可以配置成在伪分布式模式下执行。这种模式下执行的行为和在分布式模式下的行为是一致的。也就是说，引用的文件系统默认为分布式文件系统，而且由JobTracker服务来管理job，但是实际上只有一台物理机。因此，例如，HDFS文件块冗余数这时限制为一个备份。换句话说，行为类似于只有一个节点的“集群”。


#### COMMAND

当你发现需要频繁地使用hadoop dfs命令时，最好为这个命令定义一个别名（例如，alias hdfs=”hadoop dfs”）。
对于非常大的文件，当你只想查询其开始或者结尾部分信息时，这里没有提供-more,-head,或者-tail子命令。替代方式是，将-cat命令的输出通过管道传递给shell中的more、head或者tail命令，例如，hadoop dfs -cat wc-out/* | more。

# Common

# HDFS

HDFS里没有用户系统，不能创建用户，用户组

用户来源于操作的客户端用户，组是来源于上层目录的组

# MapReduce

# YARN

# Tools

# Reference

# Configuration