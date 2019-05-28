In a very short time, Apache Spark has emerged as the next generation big data pro‐
cessing engine, and is being applied throughout the industry faster than ever. Spark
improves over Hadoop MapReduce, which helped ignite the big data revolution, in
several key dimensions: it is much faster, much easier to use due to its rich APIs, and
it goes far beyond batch applications to support a variety of workloads, including
interactive queries, streaming, machine learning, and graph processing.


As parallel data analysis has grown common, practitioners in many fields have sought
easier tools for this task. Apache Spark has quickly emerged as one of the most popu‐
lar, extending and generalizing MapReduce. Spark offers three main benefits. First, it
is easy to use—you can develop applications on your laptop, using a high-level API
that lets you focus on the content of your computation. Second, Spark is fast, ena‐
bling interactive use and complex algorithms. And third, Spark is a general engine,
letting you combine multiple types of computations (e.g., SQL queries, text process‐
ing, and machine learning) that might previously have required different engines.
These features make Spark an excellent starting point to learn about Big Data in
general.


Spark’s rich collection of data-focused libraries (like MLlib) makes it easy
for data scientists to go beyond problems that fit on a single machine while using
their statistical background. Engineers, meanwhile, will learn how to write general-
purpose distributed programs in Spark and operate production applications.

If you are a data scientist, we hope that after reading this book you
will be able to use the same mathematical approaches to solve problems, except much
faster and on a much larger scale.


If you are an engineer, we
hope that this book will show you how to set up a Spark cluster, use the Spark shell,
and write Spark applications to solve parallel processing problems.

----------------------------------------------------------------------------------------------

### Chapter 1

The Spark project contains multiple closely integrated components. At its core, Spark
is a “computational engine” that is responsible for scheduling, distributing, and mon‐
itoring applications consisting of many computational tasks across many worker
machines, or a computing cluster. Because the core engine of Spark is both fast and
general-purpose, it powers multiple higher-level components specialized for various
workloads, such as SQL or machine learning.


#### Spark Core
Spark Core contains the basic functionality of Spark, including components for ****task
scheduling, memory management, fault recovery, interacting with storage systems,
and more***. Spark Core is also home to the API that defines resilient distributed data‐
sets (RDDs), which are Spark’s main programming abstraction. ***RDDs represent a
collection of items distributed across many compute nodes that can be manipulated
in parallel. Spark Core provides many APIs for building and manipulating these
collections.***

fault tolerance, throughput, and scalability




For engineers, Spark provides a simple way to parallelize these applications across
clusters, and hides the complexity of distributed systems programming, network
communication, and fault tolerance.

in-memory storage and efficient fault recovery

Storage Layers for Spark

Spark can create distributed datasets from any file stored in the Hadoop distributed
filesystem (HDFS) or other storage systems supported by the Hadoop APIs (includ‐
ing your local filesystem, Amazon S3, Cassandra, Hive, HBase, etc.). It’s important to
remember that Spark does not require Hadoop; it simply has support for storage sys‐
tems implementing the Hadoop APIs. Spark supports text files, SequenceFiles, Avro,
Parquet, and any other Hadoop InputFormat.




At a high level, every Spark application consists of a driver program that launches
various parallel operations on a cluster. The driver program contains your applica‐
tion’s main function and defines distributed datasets on the cluster, then applies oper‐
ations to them. In the preceding examples, the driver program was the Spark shell
itself, and you could just type in the operations you wanted to run.

Driver programs access Spark through a SparkContext object, which represents a
connection to a computing cluster. In the shell, a SparkContext is automatically
created for you as the variable called sc.

Once you have a SparkContext, you can use it to build RDDs. In Examples 2-1 and
2-2, we called sc.textFile() to create an RDD representing the lines of text in a file.
We can then run various operations on these lines, such as count() .

To run these operations, driver programs typically manage a number of nodes called
executors. For example, if we were running the count() operation on a cluster, differ‐
ent machines might count lines in different ranges of the file. Because we just ran the
Spark shell locally, it executed all its work on a single machine—but you can connect
the same shell to a cluster to analyze data in parallel.





While we will cover the Spark API in more detail later, a lot of its magic is that
function-based operations like filter also parallelize across the cluster. That is,
Spark automatically takes your function (e.g., line.contains("Python") ) and ships
it to executor nodes. Thus, you can write code in a single driver program and auto‐
matically have parts of it run on multiple nodes.


