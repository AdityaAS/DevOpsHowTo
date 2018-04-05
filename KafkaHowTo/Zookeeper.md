#### General Info
* Introduction to Zookeeper: [https://intellipaat.com/blog/what-is-apache-zookeeper/](https://intellipaat.com/blog/what-is-apache-zookeeper/)
* A good answer on StackOverflow: [https://stackoverflow.com/questions/3662995/explaining-apache-zookeeper](https://stackoverflow.com/questions/3662995/explaining-apache-zookeeper)
* Cloudera Blog: [https://blog.cloudera.com/blog/2013/02/how-to-use-apache-zookeeper-to-build-distributed-apps-and-why/](https://blog.cloudera.com/blog/2013/02/how-to-use-apache-zookeeper-to-build-distributed-apps-and-why/)

* In a multinode kafka cluster zookeeper as the name suggests makes sure that there is a proper synchronization among all the brokers. In lay terms all the current and consistent information about partitions, topics, offsets in partitions etc is accessible via the Zookeeper. At times a stale zookeeper configuration can lead to a lot of weird problems. More in the Issues.md file
