# Avoid using `RUN chown ...` in Dockerfiles

When trying to make a Dockerfile not run as root, it's common to use `RUN chown` to change file ownership to a particular user and group. This creates another layer and when run recursively over a ton of files (`node_modules` for instance) this can take a long, long time. Luckily [Docker just introduced in 17.09](https://github.com/moby/moby/pull/34263) a new argument to the `ADD` and `COPY` commands: `--chown`. Here is an example that saved a client project of mine a bunch of uneeded Docker build work:

```docker
# Previously
ADD $application_dir $application_dir
RUN chown -R node:node $application_dir

# Now with `--chown`
ADD --chown=node:node $application_dir $application_dir
```
