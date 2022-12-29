---
title: Hadoop Ecosystem Preliminary Investigation (1)
date: 2022-12-26 22:30:00 -0800
categories: [DATA_ENGINEERING, HADOOP]
tags: [hadoop, hadoop ecosystem]     # TAG names should always be lowercase
image: /assets/local_assets/posts/Hadoop-Ecosystem/core_hadoop_ecosystem.png
---

## Intro

 The article is based on the Udemy course *The Ultimate Hands-On Hadoop: Tame your Big Data!* The instructor of the course is Frank Kane. It shall be noticed that this article is used as a note to generate a brief understanding on **Hadoop** ecosystem, and may contain mispredictons and outdated informations. 

## HDFS

HDFS stands for the **Hadoop distributed file system**. The idea for HDFS is originated from *The Google File System* paper, and it allows us to distribute the storage of big data across our cluster of computers so it makes all of the hard drives on our cluster look like one giant file system. HDFS also manages the backups process to make data highly accessible.

## YARN

YARN means a **Yet Another Resource Negotiator**. It is the system that manages the resources (Eg: nodes) on your computing cluster.

## MapReduce

With the resource negotiator available, we could build apps like **MapReduce** to process data accross the cluster. MapReduce could be considered as a programming model to perform batch operation on scaled data accross nodes on a cluster. It mainly consists of two part: **mapper** and **reducer**. **Mappers** have the ability to transform your data in parallel across your entire computing cluster in a very efficient manner, and **reducers** are would decide how to aggregrate data together to get a result.

MapReduce and YARN were together back in Hadoop 1, but in Hadoop 2 YARN was seperated from MapReduce so that could utilize YARN to create interesting programs.

## Pig

**Apache Pig** is a high level API that sits on top of MapReduce. It allows users to write SQL-like script to query data. It shall be noticed that right now (Pig 0.17.0) **Pig script** would be compiled into a **MapReduce** program to be executed.

Pig's language layer currently consists of a textual language called **Pig Latin**.

## Hive

**Apache Hive** is a data warehouse software that reads, writes, and manages distributed data using SQL structure. It also provides a shell client and also ODBC, so if you have pre-built programs that uses SQL queries to access the data, you could port them through Hive to access data on HDFS even if the underlying data is not structured in SQL.

## Apache Ambari

**Apache Ambari** is an **open source** software that provisions, manages, and monitors Apache Hadoop clusters. It provides a Hadoop management web UI backed by its RESTful APIs. It just gives you a view of your cluster and lets you visualize what's running on your cluster, what systems are using how much resources, and also has some views in it that allow you to actually do things like execute hive queries or import databases into hive or execute Pig queries, etc.

**Apache Ambari** is includede in the **Hortonwork** distribution of Hadoop. Hortonwork's previous competitor and current owner, **Cloudera**, uses **Hue** instead to manage the Hadoop cluster. 

## Mesos

Just like **YARN**, **Apache Mesos** is also a resource negotiator. What makes it famous is that **Apache Spark** used to run on Mesos (Apache Mesos support is deprecated as of Apache Spark 3.2.0, so it's being phased out now). 

PS: There used to be a popular **SMACK(Spark, Mesos, Akka, Cassandra, and Kafka) stack** for realtime big data analysis.

## Spark

**Apache Spark** is a really popular app for Data Engineering. It sits on **YARN** or **Mesos**, and it can perform a lot better than **MapReduce**.

Two key advantages for **Apache Spark** are that:

- **Apache Spark** processes data in **random access memory (RAM)**, while **MapReduce** persists data back to the disk after a map or reduce action.

- **Apache Spark** also uses a **DAG(Directed Acyclic Graph) Scheduler** to optimize the execution. So unlike **MapReduce** that can only run map then reduce sequentially, **Spark** could speed up stages intelligently. 

Spark supports a lot of languages. Spark is written in Scala, but it also supports Java, Python and R. For Python, it has **Pyspark**, and for R, it has **SparkR**.

## Tez

**Apache Tez** is a program that build on top of **YARN** that impelments the logic of **DAG(Directed Acyclic Graph) optimizer**. Normally it would be used in conjuction of **Hive** to accelerate the **Hive** execution.

## Hbase

It exposes data from cluster to outside as a No-SQL database.

## Storm

**Apache Storm** is made for processing streaming data quickly in real time so it doesn't have to be a batch
thing anymore. 

## OOzie

**Oozie** is an app that helps you to schedule jobs on your cluster.

## Zookeeper

**Zookeeper** keeping track of shared states across your cluster that different applications can use, and it could help to maintain reliable and consistent performance across the cluster.

## Sqoop

**Sqoop** is a way of actually binding your Hadoop database into a relational database. Anything that can talk to ODBC or JDBC can be transformed by Sqoop into your HDFS file system. So you can think of **Sqoop** as a connector between Hadoop and your legacy databases.

## Flume

**Flume** is a way of transporting Web logs at a very large scale and very reliably to your cluster. 

If you have a fleet of web servers, **Flume** can actually listen to the web logs coming in from
those web servers in real time and publish them into your cluster in real time for processing by something
like storm or spark streaming.

## Kafka

An application that controls data streaming process. It is really good at handling multiple data producers and multiple data listeners, and listeners are actually having different paces when consuming data streams.