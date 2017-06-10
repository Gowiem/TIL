# Gemfile Quirk with Docker

On Dockerized Ruby projects, it's common to add the `Gemfile` to the repo, do a bundle install, and then add the rest of the code like so:

```docker
COPY Gemfile Gemfile.lock ./
RUN bundle install --binstubs
COPY . .
```

 This caches the Ruby dependencies as a separate layer so that we don't need to rebuild that layer each time we make a code change. One important quirk here is that we need to do a `bundle install` on the host machine to properly setup the `Gemfile.lock` file. Otherwise, our Ruby project will think we haven't installed that Gem even though we did. 
