# Django web framework

- [Django](https://www.djangoproject.com/) is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

- [Django web framework](#django-web-framework)
  - [Installation](#installation)
    - [Install Django library](#install-django-library)
    - [Create a new project](#create-a-new-project)
    - [Create a new app](#create-a-new-app)
    - [Run the sever](#run-the-sever)
  - [Project structure](#project-structure)
    - [Views, Routing and URLs](#views-routing-and-urls)
      - [Connecting Views and URLs](#connecting-views-and-urls)
      - [Dynamic Views and URL routing](#dynamic-views-and-url-routing)
      - [Dealing with 404 PageNotFound](#dealing-with-404-pagenotfound)
      - [Redirecting webpages](#redirecting-webpages)

## Installation

### Install Django library

- Install the library: `pip install Django`
- Django library also installs a command line tool called `django-admin`. It facilitates running features from the command line.

### Create a new project

- Create project files using cli: `django-admin startproject <project_name> <project_location>`
- The command will create files and directories that facilitates projects organization.
  - `manage.py`: A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in [django-admin and manage.py](https://docs.djangoproject.com/en/4.0/ref/django-admin/).
  - `db.sqlite3`: It is a testing environment database.
  - `<project_name>/` directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. <project_name>.urls).
    - `__init__.py`: An empty file that tells Python that this directory should be considered a Python package.
    - `urls.py`: The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in [URL dispatcher](https://docs.djangoproject.com/en/4.0/topics/http/urls/).
    - `settings.py`: It contains the settings for the project. It used to manage features, templates, database
    - `asgi.py`: An entry-point for ASGI-compatible web servers to serve your project. See [How to deploy with ASGI](https://docs.djangoproject.com/en/4.0/howto/deployment/asgi/) for more details.
    - `wsgi.py`: It is Web Server Gateway Interface. An entry-point for WSGI-compatible web servers to deploy the project to production. See [How to deploy with WSGI](https://docs.djangoproject.com/en/4.0/howto/deployment/wsgi/) for more details.

### Create a new app

- Create an App (project sub component) files: `django-admin manage.py startapp app_name`
  - `migrations/`:
  - `views.py`:
    - It is responsible for creating the content displayed on the browser.
    - It can be connected to `urls.py` in the project folder, if the project is relatively simple. Or a `urls.py` file should be created in the app folder, that can be connected to the `urls.py` in the project folder.
  - `urls.py`:
    - URLs dictate where that information is shown on the website.
    - These work in concert so you can think of each View/URL pairing as a web page on the website.
    - This file can connect to `urls.py` in the project folder through the use of `path()` and `include()` Django functions.

### Run the sever

- Run server: `python manage.py runserver`
  - Changing the port: `python manage.py runserver 8080`
  - Change the server’s IP: `python manage.py runserver 0:8000`

## Project structure

- Django Projects can have separated components called “apps”.
  - Typically a “web app” describes the full website or mobile application on the web.
  - A “Django app” is a sub-component of a single Django Project (web application).
- Each app should cover a different key functionality for the website.

### Views, Routing and URLs

- A list of view routes is defined in a list variable called `urlpatterns`.

#### Connecting Views and URLs

- Connecting a View to a URL with `path()` function:
  - `route` argument is a string that contains the URL pattern. Django will scan the relevant `urlpatterns` list until it finds a matching string route.
  - `view` argument is a string that points to the `views.py` file which will be connected to the URL pattern found in `route`.
  - `kwargs` is an optional argument. It allows to pass in keyword arguments to the view.
  - `name` is an optional argument. It allows to name the URL for referencing elsewhere in the project.
- Example for Function Based View:
  - In `views.py` file under an App component:

    ```py
    from django.http import HttpResponse

    def simple_view(request):
      return HttpResponse("Simple View")
    ```

  - To connect this view FBV to a URL routing, you need to add it as a `path` function to string `urlpatterns`.
  - In `urls.py` file under App folder:

    ```py
    from django.urls import path
    from . import views

    urlpatterns = [
        # '' is a route for the home page. But since this urls.py file under an app component,
        # the home page for the app. In other words, this is the routing for the webpages after being directed to www.domain.com/my_app/
        path('',views.simple_view)
    ]
    ```

  - To connect the app URLs and Views to the main project. The urls need to be referenced in `urls.py` under project's main folder.

    ```py
    from django.urls import include, path

    urlpatterns = [
        # 'my_app/' is the app folder name.
        # `include('my_app.urls')` includes all URLs routing that can be found in my_app.urls file
        path('my_app/', include('my_app.urls')), 
        path('',home_page)
    ]
    ```

#### Dynamic Views and URL routing

- Not every permutation of a webpage should be known in advance. Django Views and URLs support a lot of dynamic and logic features to help with this.
- To a map a URL route as a variable to a View function:
  - The variable in the route should have syntax like `<var_name>`.
  - `var_name` will passed to the view function linked to this URL routing.
  - In `urls.py`

    ```py
    articles = {
        'sport':'Sports Page',
        'games':'Games Page'
    }

    def simple_view(request,topic):
        return HttpResponse(articles[topic])

    def sum_view(request,num1,num2):
        add = num1 + num2
        result = f'{num1} + {num2} = {add}'
        return HttpResponse(result)
    ```

  - In `views.py`:

    ```py
    urlpatterns = [
        # This will map any string in a route of `www.domain.com/first_app/<topic>` and pass it as an argument to
        # function `simple_view`
        path('<str:topic>',views.simple_view),
        # This will map any integers in a route of `www.domain.com/first_app/<num1>/<num2>` and pass them as
        # arguments to function `sum_view`
        path('<int:num1>/<int:num2>', views.sum_view),
    ]
    ```

#### Dealing with 404 PageNotFound

- It happens when a user tries to access a web page that doesn't exist.
- This is can be handled by using either `HttpResponseNotFound()` which helps in debugging or `Http404("")` as a generic error.
- We can create a custom 404 page or use Django's default one.
- Any of the above mentioned functions can be returned from the view as an exception.

#### Redirecting webpages

- Sometimes a client user will provide a path that we want to redirect to another webpage on our site.
- This can be accomplished in Django through the use of the `HttpResponseRedirect()` function.
- To facilitate referencing between URLs and pages, `name` argument in `path()` helps with this.
- To link a page to a specific name, in `urls.py`:

  ```py
  path('<str:topic>',views.simple_view, name='topic-name'),
  ```

- To send a page to a named routing URL, in `views.py`:

  ```py
  HttpResponseRedirect(reverse('topic-name',args=[topic]))
  ```
