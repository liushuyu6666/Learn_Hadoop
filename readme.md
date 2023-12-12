# compatible jdk version
https://cwiki.apache.org/confluence/display/HADOOP/Hadoop+Java+Versions

# set up on a single node
https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SingleCluster.html

# set up as a cluster
https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/ClusterSetup.html



# step
## update apt
```bash
sudo apt update
sudo apt upgrade
```

## install java
[check compatible jdk version](https://cwiki.apache.org/confluence/display/HADOOP/Hadoop+Java+Versions)
```bash
sudo apt install openjdk-8-jdk
```

## download hadoop binary
1. [for arm use aarch64](https://hadoop.apache.org/releases.html)
2. extract
    ```bash
    tar -xzvf hadoop-x.x.x.tar.gz
    ```
3. Edit the `hadoop-env.sh` file to set the Java home:
    ```bash
    echo 'export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-armhf' >> ~/hadoop-3.3.6/etc/hadoop/hadoop-env.sh
    ```

## install it as standalone mode
Q: when we run "bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar grep input output 'dfs[a-z.]+'" command, does the javac in jdk compile the JAR file?
A: No, the javac command is not used to compile the JAR file when you run the bin/hadoop jar command. The javac command is specifically for compiling Java source code into bytecode. When you execute a Hadoop job using the hadoop jar command, it runs a precompiled JAR file containing the Java bytecode.

Here's a breakdown of the process:

Compilation of Java Code:

Before running the Hadoop job, the MapReduce example programs (like the Grep program in this case) are typically written in Java and compiled into bytecode (.class files) using the javac command. This compilation step is separate from the Hadoop job execution.
Creation of JAR File:

Once the Java code is compiled, the resulting bytecode files are usually packaged into a JAR file using the jar command. The JAR file contains the compiled classes and other resources needed for the Hadoop job.
Execution using hadoop jar Command:

The hadoop jar command is used to execute the Hadoop job by specifying the path to the JAR file, the main class, and any required input/output paths or parameters. Hadoop takes care of distributing the JAR file and the necessary files across the cluster and executing the job.
So, in summary, the javac command is used during the development phase to compile Java source code into bytecode, and the resulting bytecode is packaged into a JAR file. The hadoop jar command is then used to execute the compiled and packaged Java code on the Hadoop cluster.

Q: MapReduce:
A: 
MapReduce is a programming model and processing engine for distributed data processing. It is often used for batch processing tasks, and one of its key applications is searching or processing large datasets in parallel. In the context of your description, the "search engine" analogy is appropriate. MapReduce consists of two main phases: the Map phase, where data is processed and transformed in parallel, and the Reduce phase, where the results are aggregated. MapReduce programs are written to perform specific tasks on data distributed across a Hadoop cluster.

Q: I saw some example online and I found Hadoop is used to handle with text-based information?
A: Hadoop, particularly with its traditional MapReduce processing model, is often used for handling and processing large-scale text-based data. Text data is a common use case for Hadoop because:

1. Batch Processing of Large Text Data:
MapReduce is well-suited for batch processing tasks, and many examples and tutorials use text data as it is widely available and easy to work with. Text-based data often includes logs, documents, web pages, or other unstructured or semi-structured information.

2. Distributed Storage and Processing:=
Hadoop Distributed File System (HDFS) is designed to handle the storage and retrieval of large files, making it suitable for storing vast amounts of text data. The distributed processing model of MapReduce allows for parallel processing of this data across a Hadoop cluster.

3. Word Count Example:
The famous "Word Count" example, which involves counting the frequency of words in a set of documents, is often used to demonstrate the basic concepts of MapReduce. This example showcases how Hadoop can efficiently process and analyze large amounts of text.

4. Log Analysis:
Many real-world applications involve analyzing log files, which are often in text format. Hadoop can be used to process and analyze log data for various purposes, such as identifying patterns, anomalies, or trends.


While text-based data is a common use case, it's important to note that Hadoop and its ecosystem have expanded to handle a broader range of data types and processing paradigms. For example:

1. Apache Spark: This framework, which works on top of Hadoop, supports a broader set of data processing tasks and has more flexibility in handling various data types, including structured, semi-structured, and unstructured data.

2. Hive and Pig: These are higher-level abstractions built on top of Hadoop that allow users to express data processing tasks using SQL-like or scripting languages, making it easier to work with different data formats.

So, while Hadoop has a strong association with text-based information, its capabilities extend beyond just handling text data. The choice of tools within the Hadoop ecosystem depends on the specific requirements of the data and the processing tasks at hand.
