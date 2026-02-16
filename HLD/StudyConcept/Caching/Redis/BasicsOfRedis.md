# Redis (REmote DIctionary Service)

![Basic of architechture](image/basicIntroduction.png)

### Content
1) [Resources](#resources)
2) [What is Redis ?](#what-is-redis-)
3) [Redis core data types](RedisDataType.md/#redis-core-data-types)
4) [What make Redis so special](#what-make-redis-so-special)
5) [Redis Architecture](RedisArchitechture.md)
6) [Redis Persistence](RedisPersistence.md)
7) [Concurrent Programming models](#concurrent-programming-models-)
8) [IO Multiplexing (Apparent Concurrency)](#io-multiplexing-apparent-concurrency)
9) [Messaging with Redis](#messaging-with-redis)
10) [Running Redis across multiple servers](#running-redis-across-multiple-servers)
11) [Redis modules](#redis-modules)
12) [Core, cross-cutting concepts](#core-cross-cutting-concepts)

#### Resources
1) [Redis - Hello Interview System Design in a Hurry](https://www.hellointerview.com/learn/system-design/deep-dives/redis)
2) [Introduction_to_redis](https://www.educative.io/courses/building-practical-applications-with-redis-using-go/introduction-to-redis)
3) [Architechture notes (Redis)](https://architecturenotes.co/p/redis)

### What is Redis ?
1) Redis is an open-source, Single threaded, in-memory data structure.
2) It belongs to the NoSQL category of databases and falls under the key-value database umbrella.
3) It has been one of the leading databases in this category, according to DB-Engines ranking.
4) It can be used as Database, Message Broker, Cache, Streaming Engine

### Basic Uses
1) Redis is an in-memory database **used as a cache in front of another "real" database** like MySQL or PostgreSQL to help improve application performance.
2)  It leverages the speed of memory and alleviates load off the central application database for:
    - Data that changes infrequently  and is requested often 
    - Data that is less mission-critical and is frequently evolving.
![](image/traditionallyUses.png)

### What make Redis so special
1) Every Operation in redis is Atomic 
( When command is executing Redis does not context switch and start executing another command )
- putting a key
- adding to list
- set union/intersection
- incrementing the value

### Concurrent Programming models 
Doing multiple things at same time

1) Multithreading 
- Each incoming RQ over the network is accepted by the server and executed in separate thread\
**Q.How to ensure data correctness ?**
  - We have to make other threads wait while one thread is executing the critical section
  - We have safeguard ( Pessimistic locking )
    1) Mutex
    2) Semaphore 

### IO Multiplexing (Apparent Concurrency)
This is How event loop are implemented


### Messaging with Redis
- List :
  - In addition to traditional operations like add, search, delete, etc., lists can be used to implement a consumer-producer pattern for reliable asynchronous job processing, also known as worker queues.
- Pub/Sub:
  - 1) This is an implementation of the Publish/Subscribe messaging paradigm.
    2) Redis allows producers to send data to channels, which can then be received by one or more consumers (subscribers).
  - 1) It provides a high-performance message bus, but it’s ephemeral.
    2) In other words, the messages are not persisted in Redis for offline consumers to receive them after they connect later.
- Streams :
  - 1) Streams also support the producer-consumer pattern, but messages are retained even after they’re consumed and processed.
    2) This is a powerful feature, similar to that of an append-only log structure.
  - 1) It also provides fault tolerance along with the ability to traverse the stream in a flexible way—
    2) for example, processing data from the beginning of a stream, processing only new data, and processing data from a specific point in time.
  
### Running Redis across multiple servers

**Description**
1) Redis is a high performance database, and we can go a long way with a single Redis server. 
2) But, it’s also possible to operate Redis across multiple servers if data requirements exceed the limitations of a single server. 
This also ensures high availability and redundancy.

**Types**
1) Redis Cluster :
   1) A Redis Cluster has multiple nodes and the data is partitioned (or sharded) into these nodes. 
   2) There should be a minimum of three primary nodes in a Cluster and each of them can have one or more replica nodes as well.
2) Redis Sentinel :
    1) This is a high-availability feature but doesn’t provide automatic data partitioning.
    2) The setup involves running a separate Cluster of Sentinel nodes that are configured to monitor a set of Redis servers and perform automatic remediation in case of server crashes or faults.
   3) This is a much more complex system and predates the Redis Cluster, which is the recommended solution for running Redis in a scale-out architecture.
3) Proxy: 
- A proxy setup involves relying on systems that can act as a middleman in front of a fleet of Redis servers. It also takes care of data partitioning using its own custom schemes.
   1) Server-side proxy: 
      - You can set up an intermediate server that speaks the Redis protocol and fans out requests to the appropriate Redis server. 
      - A popular solution is Twemproxy.
      
   2) Client-side proxy:
      - Instead of running a separate fleet of proxy servers, a client-side proxy is aware of all the Redis servers and knows how to partition data for storage and querying. 
      - All the logic is implemented in the client library itself.
### Redis modules
1) Redis modules are an advanced feature.
2) But, in simple terms, they allow you to implement custom data types specific to our use case without needing to change or update the core Redis server.
3) Implementing a new data type with Redis modules is a nontrivial effort.
4) There are many popular and widely used Redis modules to solve problems of full-text search (RediSearch), processing time series data at scale (RedisTimeSeries), native JSON support in Redis (RedisJSON), and much more.


### Core, cross-cutting concepts
1) Redis transactions
   - A transaction allows us to execute a group of actions (Redis commands) in an isolated way.
   - For example, during a transaction, other client requests are not served, and we can be sure that the data is only being accessed by a single client.
2) Pipelines
   - A pipeline can be used to execute multiple operations efficiently.
   - 1) Redis doesn’t return the response to back to the client.
     2) Instead, it queues the response in the memory and returns the responses after all the commands have been executed—this greatly reduces the round-trip time.
3) Lua scripts
   - You can use Lua to write server-side scripts that Redis can execute (similar to stored procedures).
   - This has a few advantages,
     1) atomicity (similar to a transaction, other client requests are blocked during a Lua Script execution),
     2) efficiency (data is processed where it’s present), and
     3) flexibility.