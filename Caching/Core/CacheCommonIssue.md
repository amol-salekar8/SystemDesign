# Common Issues

### Cache stampede  [ Thundering Herd ]
![](Image/Cache_Stampede.png)

**Q.How it generated ?**
1) A cache stampede happens ``when a popular cache entry expires and many requests try to rebuild it at the same time``.
2) There is a brief window, even if only a second, where every request misses the cache and goes straight to the database.
3) Instead of one query, you suddenly have hundreds or thousands, which can overload the database.

**For example,** 
1) Imagine your system caches the homepage feed with a TTL of 60 seconds. 
2) When the cache expires at exactly 12:01:00, every request at that moment misses the cache and queries the database.
3) If traffic is high, this spike can overwhelm the database and cause cascading failures.

**Q.How to handle it?**
1) ``Request coalescing (single flight):`` 
- Allow only one request to rebuild the cache while others wait for the result. 
- This is the most effective solution.
2) ``Cache warming:``
- Refresh popular keys proactively before they expire. 
- This only helps when using TTL-based expiration. 
- If you invalidate cache on writes instead, warming does not prevent stampedes.

### Cache Consistency
**Q.How it generated ?**
1) They happen when the ``cache and database return different values for the same data``.
2) This is common because most systems read from the cache but write to the database first.
3) That creates a window where the cache still holds stale data.

**For example,**
1) If a user updates their profile picture, **the new value is written to the database but the old value might still be in the cache.** 
2) Other users may see the outdated profile picture until the cache eventually refreshes.

**Q. How to handle it ?**

1) ``Cache invalidation on writes:`` Delete the cache entry after updating the database so it gets repopulated with fresh data.
2) ``Short TTLs for stale tolerance:`` Let slightly stale data live temporarily if eventual consistency is acceptable.
3) ``Accept eventual consistency:`` For feeds, metrics, and analytics, a short delay is usually fine.

### Hot Keys

**Q.How it generated ?**
1) A hot key is a **cache entry that receives a huge amount of traffic** compared to everything else.
2) Even if the **cache hit rate is high, a single hot key can overload one cache node** or one Redis shard and become a bottleneck.

**For Example**
- If you are building Twitter and everyone is viewing Taylor Swift’s profile, the cache key for her user data (user:taylorswift) may receive millions of requests per second. 
- That one key can overload a single Redis node even though everything is working correctly.

**Q.How to handle it?**
1) ``Replicate hot keys:`` Store the same value on multiple cache nodes and load balance reads across them.
2) ``Add a local fallback cache:`` Keep extremely hot values in-process to avoid pounding Redis.
3) ``Apply rate limiting:`` Slow down abusive traffic patterns on specific keys.