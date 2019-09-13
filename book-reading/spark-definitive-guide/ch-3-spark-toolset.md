https://learning.oreilly.com/library/view/spark-the-definitive/9781491912201/ch03.html

### Running Production Applications
Spark makes it easy to develop and create big data programs. Spark also makes it easy to turn your interactive exploration into production applications with spark-submit, a built-in command-line tool. 

spark-submit does one thing: it lets you send your application code to a cluster and launch it to execute there. Upon submission, the application will run until it exits (completes the task) or encounters an error. You can do this with all of Spark’s support cluster managers including Standalone, Mesos, and YARN.


spark-submit offers several controls with which you can specify the resources your application needs as well as how it should be run and its command-line arguments.

You can write applications in any of Spark’s supported languages and then submit them for execution. The simplest example is running an application on your local machine.

We’ll show this by running a sample Scala application that comes with Spark, using the following command in the directory where you downloaded Spark:

`
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master local \
  ./examples/jars/spark-examples_2.11-2.2.0.jar 10
  
`
  
This sample application calculates the digits of pi to a certain level of estimation. Here, we’ve told spark-submit that we want to run on our local machine, which class and which JAR we would like to run, and some command-line arguments for that class.

By changing the master argument of spark-submit, we can also submit the same application to a cluster running Spark’s standalone cluster manager, Mesos or YARN.

-----------------------------------------------------------------------------------------------------------------

### Datasets: Type-Safe Structured APIs
The first API we’ll describe is a type-safe version of Spark’s structured API called Datasets, for writing statically typed code in Java and Scala. The Dataset API is not available in Python and R, because those languages are dynamically typed.


Recall that DataFrames, which we saw in the previous chapter, are a distributed collection of objects of type Row that can hold various types of tabular data. The Dataset API gives users the ability to assign a Java/Scala class to the records within a DataFrame and manipulate it as a collection of typed objects, similar to a Java ArrayList or Scala Seq. The APIs available on Datasets are type-safe, meaning that you cannot accidentally view the objects in a Dataset as being of another class than the class you put in initially. This makes Datasets especially attractive for writing large applications, with which multiple software engineers must interact through well-defined interfaces.


One great thing about Datasets is that you can use them only when you need or want to. For instance, in the following example, we’ll define our own data type and manipulate it via arbitrary map and filter functions. After we’ve performed our manipulations, Spark can automatically turn it back into a DataFrame, and we can manipulate it further by using the hundreds of functions that Spark includes. This makes it easy to drop down to lower level, perform type-safe coding when necessary, and move higher up to SQL for more rapid analysis. 


One final advantage is that when you call collect or take on a Dataset, it will collect objects of the proper type in your Dataset, not DataFrame Rows. This makes it easy to get type safety and securely perform manipulation in a distributed and a local manner without code changes:


---------------------------------------------------------------------------------------------------------------

Because you’re likely running this in local mode, it’s a good practice to set the number of shuffle partitions to something that’s going to be a better fit for local mode. 

This configuration specifies the number of partitions that should be created after a shuffle. By default, the value is 200, but because there aren’t many executors on this machine, it’s worth reducing this to 5. 

spark.conf.set("spark.sql.shuffle.partitions", "5")


--------------------------------------------------------------------------------------------------------------------


### Lower-Level APIs
Spark includes a number of lower-level primitives to allow for arbitrary Java and Python object manipulation via Resilient Distributed Datasets (RDDs). Virtually everything in Spark is built on top of RDDs. As we will discuss in Chapter 4, DataFrame operations are built on top of RDDs and compile down to these lower-level tools for convenient and extremely efficient distributed execution. There are some things that you might use RDDs for, especially when you’re reading or manipulating raw data, but for the most part you should stick to the Structured APIs. RDDs are lower level than DataFrames because they reveal physical execution characteristics (like partitions) to end users.


One thing that you might use RDDs for is to parallelize raw data that you have stored in memory on the driver machine. For instance, let’s parallelize some simple numbers and create a DataFrame after we do so. We then can convert that to a DataFrame to use it with other DataFrames:

// in Scala
spark.sparkContext.parallelize(Seq(1, 2, 3)).toDF()











