# Redis core data types
1) Redis’ core data types include String, List, Hash, Set, and Sorted Set.
2) Redis also has specialized features such as Redis Streams, Pub/Sub, Geospatial indexes, HyperLogLog, etc.
3) Although it’s an in-memory store, we can choose from a spectrum of persistence options.
4) It can act as a high-performance in-memory cache, a message broker, streaming engine, and can be used to solve a wide range of problems.

![dataType.png](image/dataType.png)

- String :
    - A basic Redis data type commonly used for caching, atomic counters, etc.
- Hash :
    -  A Redis hash can store attribute-value pairs and is commonly used to model objects.
- Set :
    - A set can only contain unique elements, but doesn’t provide any ordering guarantees.
    - It’s generally used to store data when duplicates can’t be tolerated, and it’s also used to represent relationships and execute operations such as union, intersection, etc.
- Sorted Set :
    - Items in a sorted set have a name and score associated with them. It’s similar to a set because it allows unique elements.
    - However, it differs from a set in that it provides ordering guarantees based on the member score—or name, if the scores are the same.
- Geospatial index :
    - This allows you to store and query latitude and longitude data (coordinates).
    - This is very useful for use cases that need to search for locations within a specific area, for example, finding restaurants within a five-mile radius.
- HyperLogLog :
    - This is a probabilistic data structure.
    - Its main use case is to count the unique number of elements.
    - This sounds like a job for Set, but HyperLogLog is much more space-efficient for high data volume (millions of elements), and it sacrifices accuracy for optimizing storage.

**These Data structure Can be used to build variety of application**
- RealTimeChat
- Auth Session store
- Message Buffers
- Gaming leaders
- Media Streaming
- Realtime Analysis
