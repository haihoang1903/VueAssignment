# *Technical Assignment #1*

Redis is a popular in-memory data structure store that is widely used in many applications, either as cache, complex data structure, or store application data itself.

In this assignment, your task is to build a simple, stripped-down version of Redis named Ledis (for light-weight Redis). Your Ledis app can run entirely on a single web page, meaning you do not need a webserver/backend.

You need to implement these functionalities:

- Data structures: String, Set
- Special features: Expire, snapshots
- A simple web CLI (similar to redis-cli)

## **Commands**

Your Ledis should be able to handle the following. Note that these are modeled after Redis commands, so feel free to refer to Redis manual when you have questions.

### **String**

- `SET key value`: set a string value, always overwriting what is saved under key
- `GET key`: get a string value at key

### **Set**

Set is an unordered collection of unique string values (duplicates not allowed).

- `SADD key value1 [value2...]`: add values to set stored at key
- `SREM key value1 [value2...]`: remove values from set. (Bonus: Show values are not removed (not exist) from set)
- `SMEMBERS` *key*: return an array of all members of a set
- `SINTER [key1] [key2] [key3] ...`: *(bonus)* set intersection among all set stored in specified keys. Return array of members of the result set. Ex: a: [1, 2, 3, 4], b: [2, 3, 4, 5], c: [3, 4, 5, 6]. The result of `SINTER a b c` is [3, 4]

### **Data Expiration**

- `KEYS`: List all available keys
- `DEL key`: delete a key
- `EXPIRE key seconds`: set a timeout on a key, *seconds* is a positive integer (by default a key has no expiration). Return the number of seconds if the timeout is set
- `TTL key`: query the time remaining of a key. Return a message if key does not have timeout.

### **Snapshot (bonus)**

- *SAVE*: save the current state in a snapshot
    - key1: ‘a’
    - key2: 1 2 3 4 5
- *RESTORE*: restore from the last snapshot,

### **Error Handling**

When an error happens, simply return “ERROR”, together with the cause of the error if possible. Example: *“ERROR: Key not found”*

## **Web CLI**

Please build a simple web-based CLI interface that allows users to enter commands and displays the result (this is just an example, you could build a different UI):

![ledis](https://user-images.githubusercontent.com/57028282/164689756-6babc215-b773-485f-841a-6bbae9ef27db.png)

## **Notes**

- You are required to implement the core logic by yourself, without the help of any other database systems (PostgreSQL, MySQL, Redis itself, etc).
- I recommend using FE frameworks like Vue, React, Svelte,...to implement Ledis UI. Because our command palette will use Vue so it’s great if you have experience with these UI frameworks.
- You’re not allowed to seek other people’s help with the assignment. You’re allowed to consult Google and we can help you clarify the requirements. You’re allowed to pick any existing frameworks or libraries to help you with certain tasks.

## **Submissions**

Please describe your design, your thought process, and your implementations, also discuss any challenges or interesting points (related to your project and/or Redis) along the way.

### **Please submit:**

- (important) A short writeup describing your submission
- The project source code on Github
- (optional) A deployed site (deployed on Heroku or some temporary server) for us to review. Don’t invest in the deployment process or good servers, we will only manually take a look without running any load/performance testing.
