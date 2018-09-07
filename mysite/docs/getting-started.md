# Django - Getting Started

This is a basic overview of the Django framework. Instructions for starting and creating your first application in Django will be available.

## Requirements
* Python - 3.5 and up
* Django - 2.1 (Preferably)
* Pipenv

## Installation
* In the project directory:
```
$ pipenv install django
$ pipenv shell
$ django-admin startproject (project-name)
```
* Navigate to mysite (project-name) directory
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

## Development
* Execute the following commands to run the development server (after installation):
```
$ cd mysite
$ pipenv shell
$ python manage.py runserver
```
* Note: By Default, the **runserver** command starts the dev server on the internal IP at port 8000. If you want to change the server's port, pass it as a command-line argument
```
python manage.py runserver 8080
```

### Projects vs. Apps
* What’s the difference between a project and an app? An app is a Web application that does something – e.g., a Weblog system, a database of public records or a simple poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

### File Explanation
* The outer **mysite/** root directory is the container for the project. This can be renamed to anything.
* **manage.py**: A command-line utility that let's you interact with the Django project.
* The inner **mysite/** directory is the actual Python package for the project. Its name is the Python package name you'll need to import anything inside it (e.g. **mysite.urls**)
* **mysite/settings.py**: Settings/configuration for the project.
* **mysite/urls.py**: The URL declarations for the project.
* **mysite/wsgi.py**: An entry-point for WSGI-compatible web servers to serve your project.

## Creating an App
* To create your app, type this command:
```
python manage.py startapp polls
```
* You should see the following directory structure:
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

## Database Setup
Go to mysite/settings.py to configure database settings
* **ENGINE** - Either **'django.db.backends.sqlite3'**, **'django.db.backends.postgresql'**, **'django.db.backends.mysql'**, or **'django.db.backends.oracle'**
* **NAME** - The name of your database. If you're using SQLite, the database will be a file on your computer; in that case, **NAME** should be the full absolute path, including filename, of that file. The default value, **os.path.join(BASE_DIR, 'db.sqlite3')**, will store the file in your project directory.
* Note: If you are not using SQLite as your database, additional settings such as **USER**, **PASSWORD**, and **HOST** must be added

## Time Zone Configuration
* While you're editing mysite/settings.py, set TIME_ZONE to your time zone

## Installed Applications (INSTALLED_APPS)
* polls.apps.PollsConfig - Custom App Config
* django.contrib.admin - The admin site.
* django.contrib.auth - An authentication system
* django.contrib.contenttypes - A framework for content types
* django.contrib.sessions - A session framework
* django.contrib.messages - A messaging framework
* django.contrib.staticfiles - A framework for managing static files

* Note: Some of these applications make usre of at least one database table, though, so we need to create the tables in the database before we can use them. Run the following command:
```
$ python manage.py migrate
```

* The **migrate** command looks at the **INSTALLED_APPS** setting and creates any necessary database tables according to the database settings in your mysite/settings.py file and the database migrations shipped with the app
* Run this command to include the changes to the models in the **polls** app:
```
$ python manage.py makemigrations polls
```

and (sqlmigrate takes migration names and returns their SQL)

```
$ python manage.py sqlmigrate polls 0001
```
* Lastly, Run the **migrate** command to apply the changes and create the models in the database.
