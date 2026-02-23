# Redis Replication
1) Every main instance of Redis has a **replication ID and an offset**.
2) These two pieces of data are critical to figure out a point in time where a **replica can continue its replication process or to determine if it needs to do a complete sync**.
3) This **offset is incremented for every action** that happens on the main Redis deployment.

**Q. How Redis Replication works ?**
1) **Case 1 :** Replica instance is just a few offsets behind the main instance
    1) When the Redis **replica instance is just a few offsets behind the main instance**, it receives the remaining commands from the primary which is then replayed on its dataset until it is in sync.
    2) **Full synchronization :** If the two instances cannot agree on a replication ID or the offset is unknown to the main instance, the replica will then request a full synchronization.
    3) This involves a primary instance **creating a new RDB snapshot** and sending it over to the replica.
    4) While this transfer is happening, the main instance is buffering all the intermediate updates between the snapshot cut-off and current offset to send to the secondary once it is in sync with the snapshot. Once complete, replication can continue as normal.
2) **Case 2:** Instance has the same replication ID and offset
    1) If an instance has the same replication ID and offset, they have precisely the same data.
    2) **Why a replication ID is required. ?**
        1) When a Redis instance is promoted to primary or restarts from scratch as a primary, it is given a new replication ID.
        2) This is used to infer the prior primary instance from which this newly promoted secondary was replicating.
        3) This allows for the ability to perform a partial synchronization (with other secondaries) since the new primary instance remembers its old replication ID.
    3) **For Example :**
        1) Two instances, primary and secondary, have the **identical replication ID but offsets that differ** by a few hundred commands, meaning that if those were replayed on the instance that is just behind in offset, they would have the same dataset.
        2) Now if the **replication IDs differ entirely, and when we are unaware of the previous replication ID** (no common ancestor) of the newly demoted (and rejoining) secondary. We will need to perform an **expensive full sync**.
        3) Alternatively if we are **aware of previous replication ID** we can then reason about how to get the data in sync since we are able to reason about common ancestor they both shared and the offset is again meaningful for a partial sync.
