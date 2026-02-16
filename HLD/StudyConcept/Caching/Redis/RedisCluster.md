# Redis Cluster  (Sharding)

![](image/clusterArchitecht.png)

1) Redis Cluster allows for the **horizontal scaling** of Redis.
2) once we decide to use Redis Cluster, we have decided to **spread the data we are storing across multiple machines, known as sharding**.
3) So each Redis instance in the cluster is considered a shard of the data as a whole.

**Problem 1 :** If we push a key to the cluster, how do we know which Redis instance (shard) is holding that data?

**Solution :**
1) There are several ways to do this, but **Redis Cluster uses algorithmic sharding.**
2) To find the shard for a given key
    - we hash the key and mod the total result by the number of shards.
    - Then, using a deterministic hash function, meaning that a given key will always map to the same shard, we can reason about where a particular key will be when we read it in the future.

**Problem 2:** What happens when we later want to add a new shard into the system?

**What it is ?**
1) This process is called **resharding**.
2) Example : Assuming the key 'foo' was mapped to shard zero after introducing a new shard, it may map to shard five.
3) Moving data around to reflect the new shard mapping would be slow and unrealistic if we need to grow the system quickly.
4) It also has adverse effects on the availability of the Redis Cluster.

**Solution 2 (Using Hashslot):**
1) Redis Cluster has devised a **solution to this problem called Hashslot**, to which all data is mapped.
2) There are **16K hashslot**. This gives us a reasonable way to spread data across the cluster, and when we add new shards, we simply move hashslots across the systems.
3) By doing this, **we just need to move hashslots from shard to shard** and simplify the process of adding new primary instances into the cluster.


**Example for Solution 2**

**Before adding new instance** 
1) M1 contains hashslots from 0 to 8191.
2) M2 contains hashslots from 8192 to 16383.
3) So to map `foo', we take a deterministic hash of the key (foo) and mod it by the number of hash slots(16K), leading to a mapping of M2. 

**After adding new Instance**
1) M1 contains hashslots from 0 to 5460.
2) M2 contains hashslots from 5461 to 10922.
3) M3 contains hashslots from 10923 to 16383.
4) All the keys that mapped the hashslots in M1 that are now mapped to M2 would need to move. 
5) But the hashing for the individual keys to hashslots wouldn't need to move because they have already been divided up across hashslots. 
6) So this one level of misdirection solves the resharding issue with algorithmic sharding.

### Gossiping

1) Redis Cluster uses gossiping to determine the entire cluster's health. 
2) In the illustration above, we have 3 M nodes and 3 S nodes. All these nodes constantly communicate to know which shards are available and ready to serve requests. 
3) If enough shards agree that M1 isn't responsive, they can decide to promote M1's secondary S1 into a primary to keep the cluster healthy. 
4) The number of nodes needed to trigger this is configurable, and it is essential to get this right. 
5) If you do it improperly, you can end up in situations where the cluster is split if it cannot break the tie when both sides of a partition are equal. 
6) This phenomenon is called split brain. As a general rule, it is essential to have an odd number of primary nodes and two replicas each for the most robust setup.


### Reference
**[Official Documentation](https://redis.io/tutorials/operate/redis-at-scale/scalability/)**