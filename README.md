# Redis-In-Depth

+ [**Introduction**](#introduction)
+ [**Basic**](#basic)
+ [**Keys**](#keys)
+ [**Shutdown**](#shutdown)

# introduction

+ In memmory DB
+ NoSQL DB (key-val store)
+ Caching & message broker (communication between client & application)
+ Written in ANSI C
+ Stores data in ram rather than hard disk
+ It supports data structures like: str, hash, list, sort, set, sorted set with range queries, bitmaps, hyperloglogs.

# basic

+ set key val

    ```text
    set key val
    ```

+ set expiration

    ```text
    set key val ex 10   // key will expire in 10 sec
    ttl key             // how many sec are left to expire
    persist key         // remove expiration
    ```

+ get val

    ```text
    get key
    ```

+ save data

    ```text
    dump key
    ```

+ del key

    ```text
    del key
    del key1 key2 keyn
    ```

+ exist key

    ```text
    exists key
    exists key1 key2 keyn
    ```

+ restore data

    ```text
    restore key 0 serialized-value
    ```

# keys

+ set some keys as example

    ```text
    set hallo 1
    set hello 2
    set hrllo 3
    set heello 4
    set hijkllo 5
    ```

+ keys pattern

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

+ keys cmd

    ```text
    keys *                  // list of keys
    randomkey               // any random key
    rename oldKey newkey    //reanme key  
    unlink key              // del key asynchronously without blocking current thread. Faster than del & useful for large data.  
    type key                // key datatype
    ```

# shutdown

+ save/unsave data on disk

    ```text
    shutdown save/nosave    // save/nosave:optional
    ```