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





