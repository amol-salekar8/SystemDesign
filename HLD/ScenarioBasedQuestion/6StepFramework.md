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

