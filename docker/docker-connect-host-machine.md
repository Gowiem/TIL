# Allow Docker Container to make requests against the Host Machine

I thought I needed this for a small side project, but ended up not needing it. To allow the Docker container to make requests against anything running on `localhost` on the machine running the Docker daemon. This is accomplished through [Docker Container Networking](https://docs.docker.com/engine/userguide/networking/).

1. Create a new network: `docker network create -d bridge --subnet 192.168.0.0/24 --gateway 192.168.0.1 dockernet`

Now each container on that machine can connect to the host under the fixed IP `192.168.0.1` if they're on the dockernet network.

2. Ensure the containers are on the dockernet network via `docker-compose.yml` file:
```
version: '2'
services:
  db:
    image: some/image
    networks:
      - dockernet
networks:
  dockernet:
    external: true
```

This info is pulled from [here](https://forums.docker.com/t/accessing-host-machine-from-within-docker-container/14248/5).
