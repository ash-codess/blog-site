---
author: Ash
pubDatetime: 2025-07-25T1:20:00Z
title: Spark-101
postSlug: Spark -01
featured: true
draft: false
tags:
  - data-engineering
ogImage: ""
description: Spark 101
---

## Intro

When you have small data, it is possible to analyze it with a single computer in a reasonable amount of time. When data is huge, using a single computer to store and analyze that data might take a long time and might be even impossible to analyze and process it. For big data, we may use
Spark. Spark is a tool for analyzing, processing, managing and
coordinating the execution of tasks on big data across a cluster of
computers.

## Overview

A Spark cluster is comprised of a master node (denoted
by a “cluster manager”) and a set of “worker” nodes, which are
responsible for executing tasks submitted by the Spark application
(your application which you want to run on the Spark cluster) and the
cluster manager (which is responsible in managing your application). When Spark cluster is ready and running, then we can
submit Spark applications to these cluster managers which will grant
resources to our application so that we can complete our data
analysis.

In order to do something useful with the Spark cluster, the first thing we have to do is to create an instance of SparkSession and from the
SparkSession we can access the SparkContext object as
an attribute.

```bash
# import required Spark class
from pyspark.sql import SparkSession

# create an instance of SparkSession as spark
spark = SparkSession.builder \
    .master("local") \
    .appName("my-application-name") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()

# to debug SparkSession
print(spark)

# create a reference to SparkContext as sc
# SparkContext is used to create new RDDs
sc = spark.sparkContext

# to debug SparkContext
print(sc)
```

## Spark architecture

![](https://github.com/ash-codess/blog-site/blob/master/public/assets/spark.png)

SparkSession:
It is a class defined in the pyspark.sql package. This
class is the entry point to programming Spark with the
DataSet and DataFrame API. From this class, you may
access to an instance of SparkContext. A SparkSession
can be used create DataFrame, register DataFrame as
tables, execute SQL over tables, cache tables, and read
parquet files.

SparkContext:
It is a class defined in the pyspark package and represents
the connection to a Spark cluster. It is the main entry point
for Spark functionality. It holds a connection with Spark
“cluster manager” (also known as a master node) and can be
used to create RDD and broadcast variables on that cluster.
All Spark applications (including PySpark shell and
standalone Python programs) run as an independent set of
processes. These processes are coordinated by a
SparkContext in a driver program.

Driver:
To submit a standalone Python program to Spark, you need
to write a driver program with PySpark API (or Java or
Scala). A driver program is in charge of the process of
running the main() function of an application and creating the
SparkContext. Also, the driver program is in charge of
creating Spark’s RDDs and DataFrames.

Worker:
In Spark cluster environment, there are two type of nodes:
one (or two — for high availability) master and a set of
workers. A worker, is any node that can run program in the
cluster. If a process is launched for an application, then this
application acquires executors at worker nodes, which carry
out executing Spark’s application tasks.

Spark supports 3 types of data set abstractions:

- RDD (Resilient Distributed Dataset):
  - Low level API
  - Denoted by RDD[T] (each element has type T)
- DataFrame (similar to relational tables):
  - High level API
  - Denoted by Table(column_name_1,column_name_2, ...)
- Dataset (similar to relational tables):
  - High level API (not available in PySpark)

<br/>

Spark provides two types of operations on RDDs:

- Transformations (transforms source RDD to target RDD(s))
- Actions (transforms source RDD to non-RDD object)

<br/>
Spark RDDs are immutable. Once created, it cannot be edited, added or changed. Each Spark transformation creates a new RDD. RDDs are not evaluated until an action is performed on them: this means that transformations are
lazily evaluated. If an RDD fails during a transformation, the data
lineage of transformations rebuilds the RDD. Examples of Spark’s
transformations are: map(), flatmap(), groupByKey(),
reduceByKey(), filter() etc.

<br/>
Actions : 
Spark actions are RDD operations or functions that produce non-
RDD values. Actions may trigger a previously constructed, lazy
RDDs to be evaluated.

<br/>
The groupByKey() which acts as a SQL’s GROUP BY statement,
groups the values for each key in the RDD into a single sequence. The
groupByKey() transformation can cause out of disk problems as data
is sent over the network of Spark servers and collected on the reduce
workers. When the number values per key are in the thousands or
millions, there might be an OOM error.

<br/>
On the other hand using the reduceByKey() transformation, data are
combined at each partition, only one output for one key at each partition
to send over the network of Spark servers. The reduceByKey()
merges the values for each key using an associative and commutative
reduce function. The reduceByKey() transformation is required
combining all values (per key) into another value with the exact same
data type (this is a limitation, in which can be overcome by using
combineByKey() transformation). Overall, the reduceByKey() is
more scalable than the groupByKey().

<br/>
If you have a requirement to manipulate all of your RDD elements, then
rather than using the collect(), you may use some proper
transformations such as map(), filter(), flatMap(), or
foreach(func) to mention a few. To view some elements of your
RDD, you may use RDD.take(N), which returns N elements of RDD.

<br/>

_To be continued.._
