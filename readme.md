
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
+ Pig: It allows us to write sql code to chain together queries and get complex answers without writing python and java code.
+ Hive: Similar to pig but makes system look like a sql database.
+ Apache Ambari: Apache Ambari sits on top of everything and it gives us a view of cluster and let us visualize what's running on the cluster,what system and resources are being used. Hortonworks uses Amabari.
+ Apache Storm:  Storm is basically a way of processing streaming data. Spark Streaming is an alternative for Storm.
+ Oozie: Oozie is just a way of scheduling jobs on cluster.
+ Zookeeper: It is basically a technology for coordinating everything on the cluster. It used to keep track of which nodes are up and nodes are down.
+ Flume : Flume is a distributed, reliable, and available service for efficiently collecting, aggregating, and moving large amounts of log data. It has a simple and flexible architecture based on streaming data flows. 
+ Sqoop : Sqoop is a tool designed to transfer data between Hadoop and relational database servers.

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
Delete file from HDFS
```
hadoop fs -rm {filenamewithpath}
```	
Delete folder from HDFS
```
hadoop fs -rmdir {foldername}
```
MapReduce
```
MapReduce is a processing technique and a program model for distributed computing based on java. The MapReduce algorithm contains two important tasks, namely Map and Reduce. Map takes a set of data and converts it into another set of data, where individual elements are broken down into tuples (key/value pairs). Secondly, reduce task, which takes the output from a map as an input and combines those data tuples into a smaller set of tuples. As the sequence of the name MapReduce implies, the reduce task is always performed after the map job.
```
+ MapReduce is natively java
+ Streaming allows interfacing to other language

Install Environment inside HDP 2.5
+ PIP
```
cd /etc/yum.repos.d
cp sandbox.repo /tmp
rm sandbox.repo
cd ~
yum install python-pip
```
+ MRJob
```
pip install google-api-python-client==1.6.4
pip install mrjob==0.5.11
```
+ Nano
```
yum install nano
```

MapReduce Example in Python(2.6)

Problem: Find the number of movies of each rating(rating frequency) from movie data set
+ Data Set definition
```
UserID MovieID Rating   TimeStamp
196	242	3	881250949
186	302	3	891717742
22	377	1	878887116
244	51	2	880606923
166	346	1	886397596
298	474	4	884182806
```
Code
```Python
from mrjob.job import MRJob
from mrjob.step import MRStep

class RatingsBreakdown(MRJob):
    def steps(self):
        return [
            MRStep(mapper=self.mapper_get_ratings,
                   reducer=self.reducer_count_ratings)
        ]
    #Mapper
    def mapper_get_ratings(self, _, line):
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield rating, 1
    #Reducer
    def reducer_count_ratings(self, key, values):
        yield key, sum(values)

if __name__ == '__main__':
    RatingsBreakdown.run()
```
Problem: Find the Movie Popularity list
Data Set: Same data set used here as previous.
```Python
from mrjob.job import MRJob
from mrjob.step import MRStep

class PopularMoviesList(MRJob):
    def steps(self):
        return [
            MRStep(mapper=self.mapper_get_movies,
                   reducer=self.reducer_count_movies),
            MRStep(reducer=self.final_reducer)       
        ]

    def mapper_get_movies(self, _, line):
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield movieID, 1

    def reducer_count_movies(self, key, values):
        yield str(sum(values)).zfill(5),key
    def final_reducer(self,count,movies):
	for movie in movies:
	    yield movie, count

if __name__ == '__main__':
    PopularMoviesList.run()
```



