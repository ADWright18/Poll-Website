# Introduction to Django Admin

## Philosophy
* Generating admin sites for your stuff or clients to add, change, and delete content is tedious work that doesn't require much creativity. For that reason, Django entirely automates creation of admin interfaces for Models

## Creating An Admin User
* Run this command to create a user to login to the admin site:
```
$ python manage.py createsuperuser
```

## Make the Application Modifiable in Admin
* You need to tell the admin that **Question** objects have an admin interface.
* polls/admin.py
```python
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
