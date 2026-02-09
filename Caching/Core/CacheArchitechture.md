# Cache Architechture

## Cache aside 
![](Image/Cache_aside.png)
**Q.How it works?**
1) Application checks the cache.
2) If the data is there, return it.
3) If not, fetch from the database, store.
4) it in the cache, and return it.

## Write-Through Caching
![](Image/Write_Through_cache.png)
**Q. How it Works ?**
1) With write-through caching, the application writes only to the cache.
2) The cache then synchronously writes to the database before returning to the application.
3) The write operation does not complete until both the cache and database are updated.

**Q.When to Use?**\
Use this when reads must always return fresh data and your system can tolerate slightly slower writes.

**Q.How it Implements**
1) In practice, this requires a cache implementation that supports write-through, like a caching library with a data store plugin. 
2) When you write to the cache, the library handles calling your database write logic before acknowledging the write. 
3) Redis itself does not natively support write-through, so you need application code or a framework to implement this pattern.

**CONS**
1) The tradeoff is slower writes because the application must wait for both the cache update and the database write to complete. Write-through can also pollute the cache with data that may never be read again.
2) Write-through still suffers from the dual-write problem. If the cache update succeeds but the database write fails, or vice versa, the systems can end up inconsistent. You need retry logic, error handling, or eventually accept that perfect consistency is difficult without distributed transactions.

## Write-Behind (Write-Back) Caching
![](Image/Write_behind.png)

**How It Works**
1) With write-behind caching, the application writes only to the cache.
2) The cache batches and writes the data to the database asynchronously in the background.

**Q. When to use ?**\
Use this when you need high write throughput and eventual consistency is acceptable.
Common in analytics and metrics pipelines.

**Where it Impelemented ( Example)** 
1) CDNs are a form of read-through cache.
2) When a CDN gets a cache miss, it fetches from your origin server, caches the result, and returns it.
3) But for application-level caching with Redis, cache-aside is far more common.

## Read through
![](Image/Read_Through_Cache.png)

**Q. How it works ?**
1) With read-through caching, the cache acts as a smart proxy.
2) Your application never talks to the database directly.
3) On a cache miss, the cache itself fetches from the database, stores the data, and returns it.

**How it Impelemented ( Example)**
1) This is the read equivalent of write-through.
2) In both patterns, the cache acts as an intermediary that handles database operations.
3) Read-through manages reads, write-through manages writes. Systems often combine both patterns.


