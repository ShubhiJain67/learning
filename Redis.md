# Redis

Is **REmote DIctionary Sevrer**
- In memory data structure store
- No SQL Database - allows user to store vast data without the limitations of relation DB
- Cache
- Message broker


Supports-
- Hashes
- Sets
- Lists
- Strings
- Sorted Sets
- Bitmaps
- etc

2 main components -
1. Redis Client
2. Redis Server

They can be on same or differnet computers
Can be configured as master slave

Features
- Open source
- Very good speed - Whole data is in primary memory hence exponentially fast, can perform `110000 SETs/ sec` an `81000 GETs/sec`
- Changes are asynchronously saved on the database
- Multiple values can be get and set in a single command to speed up communication.
- All operations are atomic hence ensuring that if 2 clients the redis server will receive the updated value
- Allows storing KV Pairs > 512MB upto 1GB
- Uses own hashing mechanism `Redis Hasing`
- Offers Data Replicatioon - Runs on a master slave cache node. Slaves always listen to the master node. When ever th master node gets updated the slaves also get updated. It can update the slaves asynchronously as well.Thus can withstand failures.
- Offers pub/sub messaging system
- Supports A LOT of Languages

### Some Commands
```
redis-server
redis-cli (default port 6379)
```

```
set <string name> <string value>
get <string name> -> <string value> or nil
getrange <string name> <starting index> <ending index> -> value.substring(starting string, ending string)
mset <string name1> <string value1> <string name2> <string value2> <string name3> <string value3>
mget <string name1> <string name2> <string name3>
strlen <string name> -> value.length()

set <string name> <int value>
incr <string nmame> -> Increments the value by 1 (valid for integer, float values)
incrby <string name> count
decr <string nmame> -> Derements the value by 1 (valid for integer, float values)
decrby <string name> count
incrbyfloat
decrbyfloat
```

### Time to live
```
expire <string name> <time in seconds>
ttl <string name> -> tells the ttl time
setex <key> <ttl in sec> <value>
```

### Fluss all data in redis
```
flushall
```

```
keys * -> gives all keys
```
