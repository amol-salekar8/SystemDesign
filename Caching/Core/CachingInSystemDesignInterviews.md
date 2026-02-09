# Caching in System Design Interviews

### Q. When to Bring Up Caching?
Bring up caching when you identify one of these problems:
- ``Read-heavy workload: ``
1) We're serving 10M daily active users, each making 20 requests per day.
2) That's 200M reads hitting the database.
3) Even with indexes, we're looking at 20-50ms per query.
4) A cache drops that to under 2ms and takes most of the load off the database.
- ``Expensive queries:``
1) Computing a user's personalized feed requires joining posts, followers, and likes across multiple tables.
2) That query takes 200ms.
3) We can cache the computed feed for 60 seconds and serve it in 1ms from Redis.
- `` High database CPU:``
1) Our database CPU is hitting 80% during peak hours just serving reads.
2) The same queries run over and over. Caching the hot queries will cut database load by 70-80%."
-  ``Latency requirements:``
1) We need sub-10ms response times for the API.
2)  Database queries are taking 30-50ms. We have to cache.

### Q. How to Introduce Caching ?

1. **Identify the bottleneck**
2. **Decide what to cache :**  Not everything should be cached. Focus on data that is read frequently, doesn't change often, and is expensive to fetch or compute.
3. **Choose your cache architecture**
4. **Set an eviction policy**
5. **Address the downsides**
- ``Cache invalidation:``\
  **Q .How do you keep cached data fresh?  Do you invalidate on writes, rely on TTL, or accept eventual consistency?**\
  => When a user updates their profile, we'll delete the cache entry so the next read fetches fresh data from the database.
- ``Cache failures:``\
  **Q. What happens if Redis goes down? Will your database get crushed by the sudden traffic spike?**\
  => If Redis is unavailable, requests will fall back to the database. We'll add circuit breakers so we don't overwhelm the database with a stampede. We might also consider keeping a small in-process cache as a last-resort layer.
- ``Thundering herd:``\
  **Q. What happens when a popular cache entry expires and 1000 requests try to refetch it simultaneously?**\
  => For extremely popular keys, we can use probabilistic early expiration or request coalescing so only one request fetches from the database while others wait for that result.
