# Creating Models
Now we'll define your models - essentially, your database layout, with additional metadata.

## Philosophy
* A model is the single, definitive source of truth about your data. It contains the essential fields and behaviors of the data you're storing. Django follows the DRY Principle. The goal is to define the data model in one place and automatically derive things from it

## Example - Polls
* polls/models.py
```python
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
* Each field is represented by an instance of a **Field** class - e.g., **CharField** for character fields and **DateTimeField** for datetimes.

### Explanation
* Each model is represented by a class that subclasses **django.db.models.Model**.
* Each model has a number of class variables, each of which represents a database field in the model

## Activating Models
* Create a database schema (CREATE TABLE statements) for this app
* Create a Python database-access API for accessing **Question** and **Choice** objects.
* Note: Django apps are "pluggable"; You can use an app in multiple projects, and you can distribute apps, because they don't have to be tied to a given Django installation
