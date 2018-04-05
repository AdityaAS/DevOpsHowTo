* **The following examples assume that broker is hosted at localhost:9092 and zookeeper is hosted at localhost:2181**
* **Working directory is the kafka directory**

### Create a new topic
**bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic test_topic**

* **Replication factor** is used to specify how many replicas for each message are required. High replication is suggested if the data is highly important but there is a trade off for replication v/s space. So choose it accordingly. In general a replication factor of 1/2 is good
* **Partitions** allows you to parallelize a topic by splitting a topic across multiple brokers. Each partition can be hosted on a separate machine in case of a multi node kafka cluster. Partitions enable multiple consumers to read data parallely from a given topic. Increase in partitions could lead to higher throughput

### List existing topics
**bin/kafka-topics.sh --zookeeper localhost:2181 --list**

### Describe an existing topic
**kafka-topics.sh --describe --zookeeper localhost:2181 --topic test_topic**

### Delete a topic
**bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic test_topic**

* In order for a topic to be successfully and completely deleted the config **delete.topic.enable** must be set to **true**. Otherwise the topic is marked for deletion but is not actually deleted.

### Start a producer and send messages
**bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test_topic**

* This command will open a console where the typed information is sent as a message

**bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test_topic < file.txt**

* Use the above command to send a file a message

### Start a consumer
**bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning**

* The flag --from-beginning makes sure that the consumer receives all the messages from the start (as the name suggests). It can be removed if that functionality is not needed.

