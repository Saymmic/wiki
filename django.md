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