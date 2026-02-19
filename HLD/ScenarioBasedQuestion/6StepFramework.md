# 6 Steps Framework

1) [Clarify Requirements](#step-1-clarify-requirements)
2) [Define APIS and workflow](#step-2-define-apis-and-data-flow)
3) [High level design]()
4) [Deep Dive on Components]()
5) [Scalability and bottlenecks]()
6) [TradeOffs and Improvements]()

## Step 1: Clarify Requirements
1) Functional requirements
2) Non-Functional requirements
3) Capacity estimation

### Functional requirements (the "what")

**Q. What it does ?**
1) It meets of the actual product
2) This defines what your product does and what capability that it serve

**Common Understanding**
1) Identify the core "Happy path" (User uploads, User views feed).
2) Define the secondary feature (Likes, Comments, Shares).
3) Establish the "Out of Scope" list to save time (e.g. We won't handle advertisement in this session)
4) Determine the Client types (Mobile, Web, IoT).

### Non-Functional requirements (The "Ilities")

**Ilities : Availability, Scalability, Maintainability, Observability**
1) Availability : Does the system need 99.999% uptime (High Availability) ?
2) Consistency : Is eventual consistency okay, or do we need ACID compliance ?
3) Latency : What are the target response times ( e.g. < 200ms) ?
4) Scalability : How will the system handle sudden burst (e.g. Super Bowl)?

### Capacity Estimation (The "Scale")

1) **Daily active users (DAU) / Monthly active users (MAU)** (e.g. 500 DAU)
2) **QPS** : Calculate Read QPS vs Write QPS (Usually a 100:1 ratio).
3) **Storage** : Calculate daily data ingestion (e.g. 100M posts x 500 bytes = 50GB/day)
4) **Bandwidth** : Estimate **ingress (traffic comes from user to server)** (upload) vs **egress (traffic goes out from server to user)**(download) traffic.

## Step 2: Define API's and Data flow
1) API contract design
2) Data Models and schemas
3) High level data flow

### API contract design
1) Use RESTful naming conventions (e.g. POST/v1/posts).
2) Define Request parameters (Header, Query Params, Path Variables)
3) Specify Response Codes (200 OK, 201 Created, 429 To Many Requests)
4) Mention Versioning (v1 vs v2) to ensure backward compatibility.

### Data Models and schemas
1) Define the "User" entity (UserID, Name, Email, Creation Date).
2) Define the "Resource" entity (PostID, Content, Timestamp,Metadata).
3) Discuss JSON vs ProtoBuf for payload efficiency.
4) Identify which fields need indexing for last lookups.

### High Level data flow
1) Path of write request (Client -> LB -> Service -> DB)
2) Path of read request ( Client -> CDN/Cache -> Service)
3) Identify where data is transformed or validate.
4) Mention Authentication/Authorization checks at the entry point.

## Step 3: High-Level design
1) Core infrastructure components
2) Storage layer
3) Messaging and delivery

### Core infrastructure components
1) DNS : Routing and service
2) Load balancer : Distributing traffic ( Layer 4 vs Layer 7)
3) API gateway : Handling rate limiting, logging and routing.
4) Microservices : Decoupling logic into specialized services.

### Storage layer
1) **Relational SQL :** When to use for structured data and complex join
2) **NoSql :** When to use high-write throughput and flexible schema.
3) **Object Storage :** S3 / GCS for large blobs like image and videos.
4) **Cache layer :** Redis/Memcached to store "Hot Data"  and reduce DB load

### Messaging and Delivery
1) **Message Queues :** Using Kafka / RabbitMQ for async processing (e.g. sending emails).
2) **CDN :** Using edge locations to serve content closer to the user.
3) **Pub / Sub :** Handling real-time updates for multiple subscribes.
4) **Workers :** Background processes that consume queue tasks.

## Step 4: Deep Dive on components
1) Database Scaling Strategies
2) Advanced Caching Technique
3) Fault Tolerance and internals

### Database Scaling Strategies
1) Vertical Scaling : Incresing CPU/RAM (The limit)
2) Horizontal Scaling : Adding more nodes (The goal).
3) Database Sharding : Partitioning data by UserID or geography
4) Read Replicas : Offloading read traffic from the primary DB.

### Advanced Caching Techniques
1) Cache Eviction policies : LRU, LFU, FIFO
2) Cache Strategies: Write through, Write around, Cache aside.
3) Cache Invalidation : How to handle data update (The "Hardest Problem")
4) Distribute Cache : Managing state across multiple cache nodes.

### Fault Tolerance & Internals
1) Leader Election : How system picks new primary node
2) HeartBeats : Monitoring node health to trigger failover.
3) Quorum : Ensuring enough nodes agree on data write.
4) Data Replication : Synchronous vs Asynchronous replication trade-offs

## Step 5: Scalability & Bottlenecks
1) Solving the 'Celebrity' Problem
2) Network & Security Bottlenecks
3) Reliability & Monitoring

### Solving the 'Celebrity' Problem
1) **Hot Shards :** handling millions of followers on single node.
2) **Consistent Hashing :** Reducing data movements during re-sharding.
3) **Traffic Shaping :** Queuing requests during massive spikes.
4) **Adaptive Throttling:** Rejecting requests based on server health.

### Network & Security Bottlenecks
1) **Rate Limiting :** Protecting services from DDoS and scraping
2) **Connection Pooling :** Managing DB connection efficiently.
3) **TLS Termination :** Handling encryption at the Load Balancer level
4) **Service MESH :** Using Istio/Linked for service-to-service communication.

### Reliability & Monitoring
1) **Circuit Braker :** Preventing cascading failures (Hystrix Problem).
2) **Graceful Degradation :** Showing 'cached' data if the DB is down.
3) **Observability :** Logs, Metrics(Prometheus) and Tracing (Jaeger)
4) **Chaos Engineering :** Intentionally breaking things to test resilience.


## Step 6: Trade -offs & Improvements
1) The "This vs That " table
2) CAP theorem positioning
3) V2 Roadmap & Future Scope

### The "This vs That " table
1) SQL vs NoSQL (Consistency vs Scalability)
2) Polling vs WebSockets (Simplicity vs Real-Time)
3) Batch vs Stream processing ( Latency vs Throughput)
4) Monolith vs Microservice (Deployment speed vs complexity)

### CAP theorem positioning
1) Explaining why your system is AP (Available & Partition tolerant)
2) Explaining why your system is CP (Consistent & Partition tolerant)
3) Discussing 'PACELC' (The modern extension of CAP)
4) Acknowledging the 'Eventual Consistency' trade-off

### V2 Roadmap & Future Scope
1) Implementing Machine learning for better feed ranking.
2) Moving to Multi-Region deployment for disaster recovery.
3) Cost optimization (Cold storage for old data).
4) Improving Developer Experience (SDKs, Documentation).