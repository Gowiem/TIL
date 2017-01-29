# Linking containers together through docker-compose

When multiple containers run through compose need to communicate with one another it can be accomplished via the [`links`](https://docs.docker.com/compose/compose-file/#/links) field. This exposes both ENV variables and adds the linked containers (specified via the `container_name` field) to the consuming container's `/etc/hosts` file. The exposed information is detailed [here](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/#/communication-across-links).

Here is an example taken from [Gowiem/mpskill.com](https://github.com/Gowiem/mpskill.com):

`docker-compose.yml`:
```yaml
website:
  container_name: website
  build: .
  ports:
    - 80:80
    - 443:443
    - 4567:4567
  links:
    - sinatra_app
sinatra_app:
  container_name: sinatra_app
  build: ./sinatra-app/
```

`nginx.conf`:
```conf
...

server {
    listen 4567 ssl;
    ...

    location / {
        proxy_pass http://sinatra_app:4567;
    }
}
```
