# System-Design-Notes
System Design Notes

## I. Design a Key-Value Store 
* Reference
http://blog.gainlo.co/index.php/2016/06/14/design-a-key-value-store-part-i/
http://blog.gainlo.co/index.php/2016/06/21/design-key-value-store-part-ii/

#### 1. Simple Idea: Hashtable to store key-value pairs.

1.1 Problem: Hash table usually means you need to store everything in memory.

1.2 Simple Solution: Compressing data and storing in a disk

1.3 Solution: Distributed Key-value storage

* Sharding: 
Suppose we are storing keys like URLs, we can divide them by the first character, like g for google, but it's not well balanced. So make it randomly(Hash) or try to use a counter(发号器), then divide them into several machines. When we need to find them, we can use reverse hash or mod % 26.
Keyword: Balance(负载均衡)

* Replica(Availability)
Availability, consistency are the most important metric in system design.
Sometimes our server will crash for some reason, so create some replicas may lower down the crash rate, then increase the availability of our system. "Sharding is basically used to splitting data to multiple machines since a single machine cannot store too much data. Replica is a way to protect the system from downtime."

* Consistency
Consistency has been my questions for a long time. Feel free to provide some advice to me.
First approach is to keep a copy in coordinator. The coordinator will keep the copy of updated version when update a resource.
Second approach(Make sense to me) is commit log like git, every node machine will keep commit log for every operation. And a seperate program will process all commit logs in order using a queue, whenever an operation fails, the program can easily recover it.

* Performance (Read Throughput)
Using a cache, may refer to  [Design a cache system](http://blog.gainlo.co/index.php/2016/05/17/design-a-cache-system/)
and [LRU Design in Leetcode](https://leetcode.com/problems/lru-cache/#/description)
