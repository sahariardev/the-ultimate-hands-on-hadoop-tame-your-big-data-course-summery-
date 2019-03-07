## The ultimate hands on hadoop tame your big data(Course Handson and Summery)
```
Section 01
```
Resource Link: https://sundog-education.com/hadoop-materials/

### Definition of Hadoop

An open source software platform for distributed storage and distributed processing of very large data set on computer cluster built on commodity hardware 

### Hadoop Ecosystem
+ HDFS: Hadoop distributed file system. Primary distributed data storage used by Hadoop applications. 
+  Yarn: Yet another resource negotiator. Yarn basically is the system that manages the resources on computing cluster. It decides what task to run when, what nodes are available for extra work, what nodes are down and so on.
+ Map Reduce: A programming model that allows us to process data across an entire cluster. It consist of mapper and reducers.
+ Pig: Allow us to write sql code to chain together queries and get complex answers without writing python and java code.
+ Hive: Similar to pig but make system look like a sql database.
+ Apache Ambari: Apache Ambari sits on top of everything and it gives us a view of cluster and let us visualize what's running on the cluster,what system and resources are being used. Hortonworks uses Amabari.
+ Apache Storm:  Storm is basically a way of processing streaming data. Spark Streaming is an alternative for Storm.
+ Oozie: Oozie is just a way of scheduling jobs on cluster.
+ Zookeeper: It is basically a technology for coordinating everything on the cluster. It used to keep track of which nodes are up and nodes are down. 

Mesos: An alternative to yarn.
   

