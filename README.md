[![](https://img.shields.io/badge/released-2021.6.17-green.svg?longCache=True)](https://pypi.org/project/django-command-error/)
[![](https://img.shields.io/badge/license-Unlicense-blue.svg?longCache=True)](https://unlicense.org/)

### Installation
```bash
$ pip install django-command-error
```

### How it works
+   multiple implementations:
    +   `BaseCommand` management command class
    +   `ErrorMixin` management command mixin
    +   `@command_error` decorator
+   admin interface

#### `settings.py`
```python
INSTALLED_APPS+=['django_command_error']
```

#### `migrate`
```bash
$ python manage.py migrate
```

### Examples
`ErrorCommand`
```python
from django_command_error.management.base import ErrorCommand

class Command(LockCommand):
    def handle(self,*args,**options):
        # your code
```

`@command_error`
```python
from django_command_error.decorators import command_error

class Command(BaseCommand):
    @command_error
    def handle(self,*args,**kwargs):
        ...
```
```python
class BaseCommand(BaseCommand):
    def execute(self,*args,**kwargs):
        return command_error(self.handle)(self,*args,**kwargs)
```

`call_command`
```python
from django.core.management import call_command

command_error(call_command)(name,*args,**options)
```

