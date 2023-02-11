# Redis-In-Depth

+ [**Introduction**](#introduction)
+ [**Restore**](#restore)

# introduction

+ In memmory DB
+ NoSQL DB (key-val store)
+ Caching & message broker (communication between client & application)
+ Written in ANSI C
+ Stores data in ram rather than hard disk
+ It supports data structures like: str, hash, list, sort, set, sorted set with range queries, bitmaps, hyperlologs.

# restore

+ set val

    ```text
    set key val
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
    ```

+ restore data

    ```text
    restore key 0 serialized-value
    ```
