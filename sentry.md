## HOW TO SET UP?

#### Create docker-compose.yml

I used template from [docker-compose.yml sentry template](https://gist.github.com/denji/b801f19d95b7d7910982c22bb1478f96).
In template i have changed few things:
1. Added specific environments for `nginx-gen` and `nginx-letsencrypt`
2. Change exposed port

and follow instruction from link included above.

#### Add all 3 `nginx` containers to `sentry_default` network
    docker network connect sentry_default nginx
    docker network connect sentry_default nginx-gen
    docker network connect sentry_default nginx-letsencrypt

#### Create project on serenity
Log in with created account and add projects and teams.

### Configure django

Use instruction from [link](https://docs.sentry.io/clients/python/integrations/django/).