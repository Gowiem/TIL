# Confirm Redis is Accessible/Up without Redis-CLI

You can use `netcat` to check if Redis is up and running a particular host via: `(printf "PING\r\n";) | nc $HOSTNAME 6379`. So for example, to test the ability for one Docker container to talk to a Redis container (named `redis` in compose.yml), you can run:

```bash
$ docker-compose exec service_name bash
$ (printf "PING\r\n";) | nc redis 6379
```

You should see 'PONG' as the response from this command if everything is up and running.
