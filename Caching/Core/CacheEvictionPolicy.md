# Cache Eviction Policy 

**Q. Why we required this policy ?**\
Caches have limited memory, so they need a strategy for deciding which entries to remove when full.
These strategies are called eviction policies.

### Least Recently Used  [ LRU ]

**Q. How it works ?**
1) LRU evicts the item that has <span style="color:red;font-weight: bold;">not been accessed for the longest time.</span>
2) It <span style="color:red;font-weight: bold;"> tracks access order using a linked list or ring buffer </span> so the least recently used item can be removed in constant time.

**Q. Where it Used?**\
It is the default in many systems because it adapts well to most workloads where recently used data is likely to be used again.

### Least Frequently Used  [ LFU ]
**Q. How it works ?**
1) LFU evicts the item that <span style="color:red;font-weight: bold;">has been accessed the least.</span>
2) It maintains a counter for each key and removes the one with the lowest frequency.
3) Some implementations use approximate LFU to avoid the cost of precise frequency tracking.

**Q. Where it Used?**\
This works well when certain keys are consistently popular over time, like trending videos or top playlists.



### First In First Out  [ FIFO ]
**Q. How it works ?**
1) FIFO evicts the <span style="color:red;font-weight: bold;">oldest item in the cache based only on insertion time. </span>
2) It can be implemented with a simple queue, but it ignores usage patterns.

**Q. Why it is not used?**\
Because it may evict items that are still hot, it is rarely used in real systems beyond simple caching layers.

### Time To Live [ TTL ]

**Q. How it works ?**
1) TTL is not an eviction policy by itself. 
2) Instead, it sets an expiration time for each key and removes entries that are too old. 
3) It is often combined with LRU or LFU to balance freshness and memory usage.

**Q. When it Used?**\
TTL is a must have when data must eventually refresh, like API responses or session tokens.
