# Design Instagram : The 6 Step's Framework

1) [Clarify Requirements](#clarify-requirements)
2) [Define APIS and workflow]()
3) [High level design]()
4) [Deep Dive on Components]()
5) [Scalability and bottlenecks]()
6) [TradeOffs and Improvements]()



## Design Instagram

### Functional Requirements of Instagram

1) **User management :** Secure registration and Multi-Device sign-in
2) **Media Sharing :** Uploading and viewing Photos, Videos, and Text posts.
3) **Social Graph :** Ability to Follow/Unfollow users and manage private/public profile.
4) **User Feed :** A personalized, chronologically-ordered or ranked "Home Feed"
5) **Real-Time Messaging :** Low-latency 1 to 1 private chat (One to One messaging).
6) **Discovery :** Search functionality for users and hashtags.

### Non-Functional Requirements of Instagram

1) **Global Coverage :** Low latency for users worldwide (requires CDNs and Multi-region deployment)
2) **High Availability (99.99%) :** The system must be "Always On". Being down is worse than being slightly out of sync
3) **Scalability :** Ability to handle 500M+ DAU and massive spikes during global events.
4) **Celebrity support :** Handling "The Justin Bieber Effect" (Millions of followers without crashing the feed).
5) **Durability :** Once a photo is uploaded it should be never lost.
6) **Eventual Consistency :** A "like" or "follow" doesn't need to be visible globally in milliseconds 1-2 seconds is acceptable.

### Capacity Estimation for Instagram
1) **Traffic Volume :** DAU 500 million
2) **Avg. daily uploads :** 50 Million photos/videos.
3) **Read/Write ratio :** 100:1 (Heavy read system)
4) **Storage Calculations :**
   - Photos : 50M * 2MB= 100 TB per day
   - Videos : 10M * 20MB = 200 TB per day
   - Total storage (5 Years) : ~547 Petabytes (Requires S3/ cold storage strategy)
5) **Network Bandwidth :**
   - Ingress: ~3.5GB/s
   - Egress: ~350 GB/s (This justifies why we must use a CDN)

## Step 2: Define API's and Data flow
1) API contract design
2) Data Models and schemas
3) High level data flow

### API contract design
1) Use RESTful naming conventions (e.g. POST/v1/posts).
2) Define Request parameters (Header, Query Params, Path Variables)
3) Specify Response Codes (200 OK, 201 Created, 429 To Many Requests)
4) Mention Versioning (v1 vs v2) to ensure backward compatibility.

eg :**According to Functional Requirements we generate this**

**User Management**
- POST /v1/auth/register
- POST /v1/auth/login

**Media sharing**
- POST /v1/media/upload
- GET /v1/media/{id}

**Social graph**
- POST /v1/users/{id}/follow
- GET /v1/users/{id}/followers
- GET /v1/users/{id}/following

**User feed**
- GET /v1/feed

**Real-time messaging**
- WSS /v1/chat/connect
- GET /v1/messages

**Discovery**
- GET /v1/search

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



