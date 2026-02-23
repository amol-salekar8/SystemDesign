# Redis Persistence

**Define**
Persistence refers to the **writing of data to durable storage**, such as a solid-state disk (SSD). Redis provides a range of persistence options. 

**Options :**
1) [RDB (Redis Database)](#rdb-redis-database)
2) [AOF (Append Only File)](#aof-append-only-file) 
3) [No persistence](#no-persistence)

![persistanceModel](image/persistenceModel.png)

### RDB (Redis DataBase)
1) RDB persistence performs point-in-time snapshots of your dataset at specified intervals.

***RDB Advantages***
1) RDB is a very compact single-file point-in-time representation of your Redis data.
2) RDB is very good for disaster recovery, being a single compact file that can be transferred to far data centers, or onto Amazon S3
3) RDB allows faster restarts with big datasets compared to AOF.
4) RDB files are perfect for backups.

***RDB Disadvantages***
1) RDB is NOT good if you need to minimize the chance of data loss in **case Redis stops working (for example after a power outage)**. 
   - You can configure different save points where an RDB is produced (for instance after at least five minutes and 100 writes against the data set, you can have multiple save points). 
   - However you'll usually create an RDB snapshot every five minutes or more, so in case of Redis stopping working without a correct shutdown for any reason you should be prepared to lose the latest minutes of data.

### AOF (Append Only File)
1) AOF **persistence logs every write** operation received by the server. 
2) These operations can then be replayed again at server startup, reconstructing the original dataset. 
3) Commands are logged using the same format as the Redis protocol itself.

***AOF Advantage***
1) AOF log is an append-only log, so there are **no seeks, nor corruption problems if there is a power outage**. Even if the log ends with a half-written command for some reason (disk full or other reasons) the redis-check-aof tool is able to fix it easily.
2) Redis is able to automatically rewrite the AOF in background when it gets too big.
3) The rewrite is completely safe as while Redis continues appending to the old file, a completely new one is produced with the minimal set of operations needed to create the current data set, and once this second file is ready Redis switches the two and starts appending to the new one.

***AOF Disadvantage***
1) AOF **files are usually bigger than the equivalent RDB files** for the same dataset.
2) AOF can be **slower than RDB** depending on the exact fsync policy.
3) In general with fsync set to every second performance is still very high, and with fsync disabled it should be exactly as fast as RDB even under high load.

### No Persistence
1) If you wish, you can disable persistence altogether. 
2) This is the fastest way to run Redis and has no durability guarantees.

### Ok, so what should I use?
1) The general indication you should use both persistence methods is if you want a degree of data safety comparable to what PostgreSQL can provide you.
2) If you care a lot about your data, but still can live with a few minutes of data loss in case of disasters, you can simply use RDB alone.
3) **There are many users using AOF alone, but we discourage it since to have an RDB snapshot from time to time** is a great idea for doing database backups, for faster restarts, and in the event of bugs in the AOF engine.

## Reference
**[Official Documentation](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/)**