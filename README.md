# Redis-In-Depth

+ [**Introduction**](#introduction)
+ [**Basic**](#basic)
+ [**Keys**](#keys)
+ [**Shutdown**](#shutdown)
+ [**String**](#string)
+ [**List**](#list)
+ [**Hash**](#hash)

# introduction

+ In memmory DB
+ NoSQL DB (key-val store)
+ Caching & message broker (communication between client & application)
+ Written in ANSI C
+ Stores data in ram rather than hard disk
+ It supports data structures like: str, hash, list, sort, set, sorted set with range queries, bitmaps, hyperloglogs.

# basic

+ **key type**

    ```text
    type key
    ```

+ **set key val**

    ```text
    set key val
    ```

+ **set multiple key val**

    ```text
    set key1 val1 key2 val2 key3 val3 ...
    ```

+ **set key val if not exists**

    ```text
    // for single key-val

    set key1 val1 nx

    // for multiple key-val

    msetnx key1 val1 key2 val2 key3 val3 ...
    ```

+ **overwite val if only the key exists**

    ```text
    // for single key-val

    set key1 val1 xx
    ```

+ **set expiration**

    ```text
    set key val ex 10   // key will expire in 10 sec
    ttl key             // how many sec are left to expire
    persist key         // remove expiration
    ```

+ **get val**

    ```text
    get key
    ```

+ **get multiple key val**

    ```text
    mget key1 key2 key3 ...
    ```

+ **replace oldVal**

    ```text
    // replace oldVal with newVal

    getset key val
    ```

+ **save data**

    ```text
    dump key
    ```

+ **del key**

    ```text
    del key
    del key1 key2 key...n
    ```

+ **exist key**

    ```text
    exists key
    exists key1 key2 key...n
    ```

+ **restore data**

    ```text
    restore key 0 serialized-value
    ```

+ **append data in key**

    ```text
    append key val
    ```

+ **increment value of a key** ( ```must be int``` )

    ```text
    // by default the value will be incremented by 1

    incr key

    // custom val to increment

    incrby key value
    incrbyfloat key value
    ```

+ **derement value of a key** ( ```must be int``` )

    ```text
    // by default the value will be decremented by 1

    decr key

    // custom val to decrement

    decrby key value
    ```

# keys

+ **set some keys as example**

    ```text
    set hallo 1
    set hello 2
    set hrllo 3
    set heello 4
    set hijkllo 5
    ```

+ **keys pattern**

    ```text
    keys h?llo      // keys with length 5:hallo,hello,hrllo
    keys h*llo      // keys with any length
    keys h[a-r]llo  // keys between a to r that postion: hallo, hello, hrllo
    keys h[ae]llo   // keys with a or r:hallo,hello
    keys h[^e]llo   // keys except e char
    keys *l*        // any keys contains i
    keys h????      // keys with 5 char starting with h
    keys ?????      // any key with length 5
    ```

+ **keys cmd**

    ```text
    keys *                  // list of keys
    randomkey               // any random key
    rename oldKey newkey    //reanme key  
    unlink key              // del key asynchronously without blocking current thread. Faster than del & useful for large data.  
    type key                // key datatype
    ```

# shutdown

+ **save/unsave data on disk**

    ```text
    shutdown save/nosave    // save/nosave:optional
    ```

# string

+ **slice**

    ```text
    // upper limit inclusive

    getrange key startPos endPos
    getrange key 0 5

    // -1: last pos

    getrange key startPos endPos
    getrange key 0 -1
    getrange key -3 -1
    ```

+ **replace by pos**

    ```text
    setrange key pos val
    ```

# list

> Redis list is implemented by LinkedList.

+ **lpush**

    ```text
    // last element will be 1st one

    lpush key val1 val2 val3 ... valn
    ```

+ **rpush**

    ```text
    // last element will be last one

    rpush key val1 val2 val3 ... valn
    ```

+ **get list**

    ```text
    lrange key startPos endPos
    ```

+ **push val if key exists**

    ```text
    // last element will be last one

    lpushx key val1 val2 val3 ... valn
    rpushx key val1 val2 val3 ... valn
    ```

+ **remove element**

    ```text
    // remove element from left side
    lpop key

    // remove element from right side
    rpop key

    // remove all element except these range
    ltrim key startPos endPos
    ltrim key 1 -2
    ```

+ **remove element by cond**

    ```text
    // remove that particular element from list
    lrem key 0 val
    ```

+ **change the element by pos**

    ```text
    lset key index val
    ```

+ **get the element by pos**

    ```text
    lindex key index
    ```

+ **insert val in list**

    ```text
    linsert key before/after matchingVal newVal
    ```

# hash

+ every hash can store up to **2<sup>32</sup>-1** field-val pairs(more than 4 billion)

+ set one field val

    ```text
    // if field exists then update otherwise insert

    hset key field value
    // ex: hset student name samrat
    ```

+ set multiple field val

    ```text
    hmset key field1 value1 field2 value2 field...n value...n

    // ex: hmset student name samrat profession "Data Engineer"
    ```

+ get one val

    ```text
    hget key field

    // ex: hset student name
    // output: samrat
    ```

+ get multiple val

    ```text
    hmget key field1 field2 field...n

    // ex: hmget student name profession
    // output: samrat "Data Engineer"
    ```

+ get all keys

    ```text
    hkeys key
    ```

+ get all val

    ```text
    hvals key

    // ex: hvals student
    // output: all val
    ```

+ get all field-val

    ```text
    hgetall key
    ```

+ check field exists or not

    ```text
    hexists key field
    ```

+ length of key

    ```text
    hlen key
    ```

+ length of particular field

    ```text
    hstrlen key field
    ```

+ insert field if not exists

    ```text
    hsetnx key field value
    ```

+ delete field

    ```text
    hdel key field1 field2 field...n
    ```

+ increment field val ( ```must be int/float``` )

    ```text
    // only int type
    hincrby key field val increment

    // can be used in both float and int type
    hincrbyfloat key field val increment
    ```
