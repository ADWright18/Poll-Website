# Views

## Overview
* A view is a "type" of web page in your Django application that generally serves a speific function and has a specific template. For example, in a blog application, you might have the following views
  * Blog Homepage - display the latest few entries
  * Entry "detail" page - permalink page for a single entry
  * Year-based archive page - displays all months with entries in the given year
  * Month-based archive page - displays all days with entries in the given month
  * Day-based archive page - displays all entries in the given day
  * Comment action - handles posting comments to a given entry.

* In our poll application, we'll have the following four views
  * Question "index" page - displays the latest few questions
  * Question "detail" page - displays a question text, with no results with a form to vote
  * Question "results" page - displays results for a particular question
  * Vote action - handles voting for a particular choice in a particular question

## Writing a View
* **polls/views.py**
```python
def detail(request, question_id):
  return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
  response = "You're looking at the results of question %s."
  return HttpResponse(response % question_id)

def vote(request, question_id):
  return HttpResponse("You're voting on question %s." % question_id)  
```

* Wire these new views into the polls.urls module by adding the following path() calls
* **polls/urls.py**
```python
from django.urls import path

from . import views

urlpatterns = [
  # ex: /polls/
  path('', views.index, name='index'),
  # ex: /polls/5/
  path('<int:question_id>/', views.detail, name='detail'),
  # ex: /polls/5/results/
  path('<int:question_id>/results/', views.result, name='results'),
  # ex: /polls/5/vote/
  path('<int:question_id/vote/>', views.vote, name='vote'),
]
```

## Add Functionality to Views
* Each view is responsible for doing one of two things: returning an HttpResponse object containing the content for the requested page, or raising an exception such as Http404.
* You can read records from a database, or not. It can use a template system such as Django's - or not
* **polls/views.py (Hard-Coding w/ Python)**
```python
from django.http import HttpResponse

from .models import Question

def index(request):
  latest_question_list = Question.objects.order_by('-pub_date')[:5]
  output = ', '.join([q.question_text for q in latest_question_list])
  return HttpResponse(output)
```

* Or you can use a template
* **polls/templates/polls/index.html**
```html
{% if latest_question_list %}
  <ul>
    {% for question in latest_question_list %}
      <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
  </ul>
{% else %}
  <p>No polls are available.</p>
{% endif %}  
```

* Update the **index** view in **polls/views.py** to use the template
```python
from django.http import HttpResponse
from django.template import loader

from .models import Question

def index(request):
  latest_question_list = Question.objects.order_by('-pub_date')[:5]
  template = loader.get_template('polls/index.html')
  context = {
    'latest_question_list': latest_question_list,
  }
  return HttpResponse(template.render(context, request))
```

* That code loads the template called **polls/index.html** and passes it a context. The context is a dictionary mapping template variable names to Python objects.
