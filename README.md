# django-discard

A simple package to add discard (soft-delete) functionality to desired models.

## Installing

`pip install django-discard`

## Quick start

```
>>> from django_discard.models import DiscardableModel

>>> class User(DiscardableModel):
>>>     email = models.EmailField(max_length=255, unique=True)

>>> User.objects.create(email="email_1@example.com")
>>> User.objects.create(email="email_2@example.com")
>>> User.objects.create(email="email_3@example.com")
```

### Discarding objects

```
>>> user = User.objects.last()
>>> user.discard()
```

### Discarded and kept check

```
>>> user.is_discarded()
True

>>> user.is_kept()
False
```

### Undiscarding objects

```
>>> user.undiscard()
```

### Discarding and undiscarding sets of objects

```
>>> User.objects.all().discard()

>>> User.objects.all().undiscard()
```

### Querying discarded and kept objects

```
>>> User.objects.all().discarded()

>>> User.objects.all().kept()
```