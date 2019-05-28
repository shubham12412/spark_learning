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






