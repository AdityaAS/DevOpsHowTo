### A few common issues that I've faced and how I solved them

### Zookeeper related issues

At times a stale zookeeper configuration can lead to a lot of weird problems.

1. For storing messages Kafka ultimately makes use of the file system. The path of the directory where kafka stores the messages and logs can be set by the config **log.dirs**
It should be made sure that each broker in a multi node kafka cluster has its own directory. In case of a distributed cluster where each node has its own local file system (not the shared file system) a path in the local file system should be a good choice (For example /kafka-logs). Basically it should be made sure that physically each broker writes to a different directory.

	* In a case where it is required that the kafka logs directory be setup in a shared file system it is suggested that a sym link be created for each node where say the path /kafka-logs corresponds to different directories in different nodes. This situation might occur when you want to use kafka for big data applications and the local storage is not sufficient.