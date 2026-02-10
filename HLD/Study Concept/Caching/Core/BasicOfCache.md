# Caching 
***RESOURCES***<br/>
[Youtube Resource Link](https://www.youtube.com/watch?v=1NngTUYPdpI)<br/>
[Documentation_Resource](https://www.hellointerview.com/learn/system-design/core-concepts/caching)



#### Q.Why we need ?
1) Reading a user profile from Postgres may take 50 milliseconds, but reading from an in-memory cache like Redis takes just 1 millisecond. That's a 50x improvement in latency. Databases store data on disk, and every query pays the cost of disk access. Memory sits much closer to the CPU and avoids that entirely.

#### Q.Why we Used ?
1) Caching is temporary storage that keeps recently used data handy so you can get it
much faster next time.
2) Caches are essential for scalable systems. 
3) They reduce load on the database and cut latency dramatically. 
4) But they also create new challenges around invalidation and failure handling.

***PROS***\
As it maximizes resource utilization, reduces server loads and enhances overall scalability, caching is a helpful technique in software development.
1) ```Improved performance```: By significantly reducing down on the time it takes to get frequently used data, caching can enhance system responsiveness and performance.
2) ```Reduced load on the original source```: By significantly reducing down on the time it takes to get frequently used data, caching can enhance system responsiveness and performance.
3) ```Cost savings```: Caching can reduce the need for expensive hardware or infrastructure upgrades by improving the efficiency of existing resources.

***CONS***
1) ```Data inconsistency```: If cache consistency is not maintained properly, caching can introduce issues with data consistency.
2) ```Cache eviction issues```: If cache eviction policies are not designed properly, caching can result in performance issues or data loss.
3) ```Additional complexity```: Caching can add additional complexity to a system, which can make it more difficult to design, implement and maintain.

***Q 1. When to bring up caching ?***
- Read heavy workload
- Expensive quries
- High database CPU
- Latency requirement

***Q2. How to introduce caching ?***
1) Identidy the bottolnecks
2) Decide what to cache
3) Choose your cache architechture
4) Set an eviction policy
5) Address the downside.

#