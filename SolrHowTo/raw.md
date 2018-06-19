#### Solr
* How to take Solr backup in plaintext (Snapshot): [https://blog.cloudera.com/blog/2017/05/how-to-backup-and-disaster-recovery-for-apache-solr-part-i/](https://blog.cloudera.com/blog/2017/05/how-to-backup-and-disaster-recovery-for-apache-solr-part-i/)
* Solr Collections API: [https://lucene.apache.org/solr/guide/6_6/collections-api.html](https://lucene.apache.org/solr/guide/6_6/collections-api.html)
* To dump a solr collection into file system acc to specified query (DONOT USE THE COLLECTIONS API FOR THIS TASK, IT IS VERY INEFFICIENT) use the package at [https://github.com/ubleipzig/solrdump](https://github.com/ubleipzig/solrdump). Uses cursors which is an efficient retrieval mechanism.
* Solr Paging and Deep Paging: [http://yonik.com/solr/paging-and-deep-paging/](http://yonik.com/solr/paging-and-deep-paging/) and [https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html](https://lucene.apache.org/solr/guide/6_6/pagination-of-results.html)
##### Notes / Guidelines 
* Never create collections with a single shard / multiple shards on the same node. Always make sure that the collection is distributed. Increase the number of shards as the size of collection keeps increasing. (example: If you have a collection of 500K documents split it into 2-3 shards)
* For important data always make sure that atleast one replica exists. Don't create too many replicas too. Just the right amount. 1 replica is good enough. If your collection is very very important then may be create 2 replicas.
* If indeed you make the mistake of creating a really large collection on a single shard (don't worry, we all screw up sometimes) follow the steps below:
	- Split the collection into multiple shards using [https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-splitshard](https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-splitshard)
	- Replicate the newly created (split) shard onto a different node using [https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-addreplica](https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-addreplica)
	- Delete the old shard (only when you are sure that the replica has been successfully created in another node) using [https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-deleteshard](https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-deleteshard)
* To change the leader node in Solr Server:
	- Use the following API function - [https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-RebalanceLeaders](https://lucene.apache.org/solr/guide/6_6/collections-api.html#CollectionsAPI-RebalanceLeaders)
	- The IP Address should be the ip of the node that is needed to be converted to leader
	- If the leader node goes down, the replication node becomes the leader node. Once the ex-leader node comes up, it resumes its leadership.

