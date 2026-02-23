# Caching Layer

Let’s assume you’re working on a streaming application steadily becoming popular among users. As the number of users grows, so does the application’s design. Ignoring other aspects, let’s see how caching plays a role in this design evolution. Let’s take a step-wise approach and implement caching solutions at different points in the larger System Design.

##### Type of Cache layer
1) Front end caching 
    - Client-side caching [ Browsers cache ]
2) Backend Layer
    - Load balancer caching
    - Web server caching
    - Application server caching
    - Database caching
    - Distribute caching
3)  Network Layer
    - DNS caching
    - Network proxy caching
    - CDN caching

### Where to Cache

##### External Caching
![](Image/External_Cache.png)

**Description**
1) An external cache is a standalone cache service that your application talks to over the network.
2) This is what most people think of when they hear caching.
3) You store frequently accessed data in something like Redis or Memcached so you do not have to hit the database every time.

**PROS**
 - External caches scale well because every application server can share the same cache. 
 - They also support eviction policies like LRU and expiration via TTL so your memory footprint stays controlled.


##### In process Caching
![](Image/In_Process_Caching.png)

**Description**\
The idea is simple if your service keeps requesting the same small pieces of data again and again, store them in a local cache inside the process. Reads from local memory are even faster than reads from Redis because they avoid any network call.

This light-weight form of caching makes sense for small pieces of data that are requested frequently like:

<span style="color:red;font-weight:bold;"> Use in-process caching for small, frequently accessed values that rarely change. It is great for speed but not a replacement for Redis. In system design interviews, mention this only as an optimization layer after you have already introduced an external cache.</span>


**PROS**
1) In-process caching is blazing fast.

**CONS**
1) It comes with obvious limitations. 
2) Each instance of your application has its own cache, so cached data is not shared across servers. 
3) If one instance updates or invalidates a cached value, the others will not know.



##### CDN caching
![](Image/CDN.png)

**Description**
1) A CDN is a geographically distributed network of servers that caches content close to users.
2) Instead of every request traveling to your origin server, a CDN stores copies of your content at edge servers around the world.

**Q. How it works ?**
1) A user requests an image from your app.
2) The request goes to the nearest CDN edge server.
3) If the image is cached there, it is returned immediately.
4) If not, the CDN fetches it from your origin server, stores it, and returns it.
5) Future users in that region get the image instantly from the CDN.

**PROS**
 - Even though modern CDNs can cache API responses and dynamic content. 
 - In system design interviews the safest time to introduce a CDN is when your system serves static media at scale. Start with that reason first, then expand only if the problem calls for more.



##### Client side caching
![](Image/Client_Side_caching.png)

**Description**
1) Client-side caching stores data close to the requester to avoid un-necessary network calls.
2) This usually means the user's device, like a browser (HTTP cache, localStorage) or mobile app using local memory or on-device storage.

**Q. How it is Use ?**
1) But it can also mean caching within a client library. For example, Redis clients cache cluster metadata like which nodes are in the cluster and which slots are assigned to them.
2) That way, the client can route requests directly to the right node without querying the cluster on every operation.