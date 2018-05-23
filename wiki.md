# POSTGRES

### Terminate all sessions
```
SELECT pid, pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = current_database() AND pid <> pg_backend_pid();
```

# LINUX

### Compress folder with tar
`tar czf name_of_archive_file.tar.gz name_of_directory_to_tar`

### Unpack .tar.gz archives
`tar -xzf example.tar.gz`

### Exclude some files while compressing
`tar -zc -f test.tar.gz --exclude='*.xdr' /test/`


# JETBRAINS

Snippets and hacks for JetBrains products


## Pycharm polish spellchecking
### Generate polish dict with aspell
#### Install aspell
    sudo apt install apsell aspell-pl
#### Generate dict in proper format
    aspell --lang pl dump master | aspell --lang pl expand | tr ' ' '\n' > pl.dic

### Configure Pycharm

#### Copy file to desired location
Move the `pl.dic` to the desired location eg. `~/.dicts/pl`

#### Select location in Pycharm settings
    settings>editor>spelling>dictionaries>+(green plus in right top)
and add chosen before path


## Shortcuts

- `crel+e` - recent files
- `alt+insert` - create new file
- `shft+ctrl+<arrow>` - resize window
- `alt+enter -> inject language` - inject piece of code eg. json
- `alt+slash` - cyclic expand word
- `alt+home` - focus nav bar
- `alt+9` - open version control window

- `ctrl+ pageUp/PageDown` (chrome) switch tab


# MISC

### Setting up sentry

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

#### Configure django

Use instruction from [link](https://docs.sentry.io/clients/python/integrations/django/).

# DOCKER

### Copy files from and to containter
`docker cp <containerId>:/file/path/within/container /host/path/target`
`docker cp /host/path/target <containerId>:/file/path/within/container`


### stop all containers:
`docker kill $(docker ps -q)`

### remove all containers
`docker rm $(docker ps -a -q)`

### remove all docker images
`docker rmi $(docker images -q)`


# DJANGO

## Chainable managers

```python
import datetime
from django.db import models
from django.db.models.query import QuerySet

class PostQuerySet(QuerySet):
    def live(self):
        """Filter out posts that aren't ready to be published"""
        now = datetime.datetime.now()
        return self.filter(date_published__lte=now, status="published")

class PostManager(models.Manager):
    def get_query_set(self):
        return PostQuerySet(self.model)
    def __getattr__(self, attr, *args):
        # see https://code.djangoproject.com/ticket/15062 for details
        if attr.startswith("_"):
            raise AttributeError
        return getattr(self.get_query_set(), attr, *args)

class Post(models.Model):
    # field definitions...
    objects = PostManager()
```

## convinient object url property

```python
from rest_framework import reverse as api_reverse
class SomeModel(models.Model):
    ...
    def get_url(self, request=None):
        api_reverse('some_name_space', kwargs={'pk': self.pk}, request=request)
```

## Timezone aware datetime object
```python
from django.utils import timezone

d = timezone.now()
```

## See sql queries:
```python
from django.db import connection
print(connection.queries)
```

# ANGULAR

## How to add bootsrap to angular?
1. `npm install --save bootstrap@4.0.0-alpha.6 font-awesome`

2. Add to `src/styles.css`
```
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~font-awesome/css/font-awesome.css";
```