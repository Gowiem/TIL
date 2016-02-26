# Remove a bulk set of keys matching a wildcard from Redis on ElastiCache

Simple script to aggregate the keys from a replica and remove them from the primary:

```bash
# Pull all keys matching wildcard from your Replica so you're not using KEYS on your primary.
$ redis-cli -h $ELASTI_CACHE_REPLICA_URL KEYS "*WILDCARD*" > keys.txt

# For each key that has been collected, prepend the DEL command.
$ sed ':a;N;$!ba;s/\n/\n DEL /g' keys.txt > del_keys.txt

# Feed the new DEL commands into your primary. Run via nohup + background as deleting millions of keys can take hours.
$ nohup redis-cli -h $ELASTI_CACHE_URL < del_keys.txt &
```