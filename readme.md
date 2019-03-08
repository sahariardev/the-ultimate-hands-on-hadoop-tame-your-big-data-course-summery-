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

---

   ```
   Section 02
  ```
 #### HDFS
  When data size become so large that it outgrows the storage capacity of a single machine, it becomes necessary to partition it across a number of separate machines. The file system that manages the storage across a network  of machines is called  distributed file system. Developing a distributed file system is more complex than a regular disk filesystem. Hadoop provides us a Distributed file system known a HDFS. When we give a file HDFS is breaks it into a chunk of small files and store it in several machines. They always keep multiple copies of files so that file can be easily recovered when any machine goes down.
#### HDFS Architecture



An HDFS cluster has two types of node. They operate in master-worker patter. 
Namenode: The name node manages the file system namespace. It maintains the filesystem tree and the metadata for all the files and directories in the tree. This information is stored persistently on the local disk in the form of two files 1. the namespace image and  2. the edit log. The namenode also knows the datanodes on which all the blocks for a given file are located; however, it does not store block locations persistently, because this information is reconstructed from datanodes when the system starts. 
Datanode: Datanodes are the workhorses of the filesystem. They store and retrieve blocks when they are told to (by clients or the namenode), and they report back to the namenode periodically with lists of blocks that they are storing.
As the namenode has all the informations of datanodes so without name nodedata can not be accessed. So if namenode fails then the whole system fails. So most of the team make a backup of namenode. But making namenode backup slowdown the process of storing data because when the data is stored it needs to be informed to multiple namenodes.
### Accessing HDFS using Command Line(In Hortonworks)
Connect using SSH:
```
ssh username@ipaddress -p port
password
```
List all files in HDFS:
```
hadoop fs -ls
```
Create a folder in HDFS:
```
hadoop fs -mkdir {folder_name}
```
Copy file from local to HDFS
```
hadoop fs -copyFromLocal {filenamewithpath} {newfilenamewithpath}
```	

