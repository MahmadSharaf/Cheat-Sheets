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
  - [Templates and Views](#templates-and-views)
    - [Where to create templates](#where-to-create-templates)
    - [Connecting Views and Templates](#connecting-views-and-templates)
    - [Pass variables from Views to Templates](#pass-variables-from-views-to-templates)
    - [Apply functions directly on templates using Filters](#apply-functions-directly-on-templates-using-filters)
    - [Apply logic directly on the template using Tags](#apply-logic-directly-on-the-template-using-tags)
    - [Reversing namespaced URLs](#reversing-namespaced-urls)
    - [Template inheritance](#template-inheritance)
    - [Customizing error views](#customizing-error-views)
    - [Use static files](#use-static-files)
  - [Reference](#reference)

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

## Views, Routing and URLs

- A list of view routes is defined in a list variable called `urlpatterns`.

### Connecting Views and URLs

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

### Dynamic Views and URL routing

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
        # This will map any string in a route of `www.domain.com/my_app/<topic>` and pass it as an argument to
        # function `simple_view`
        path('<str:topic>',views.simple_view),
        # This will map any integers in a route of `www.domain.com/my_app/<num1>/<num2>` and pass them as
        # arguments to function `sum_view`
        path('<int:num1>/<int:num2>', views.sum_view),
    ]
    ```

### Dealing with 404 PageNotFound

- It happens when a user tries to access a web page that doesn't exist.
- This is can be handled by using either `HttpResponseNotFound()` which helps in debugging or `Http404("")` as a generic error.
- We can create a custom 404 page or use Django's default one.
- Any of the above mentioned functions can be returned from the view as an exception.

### Redirecting webpages

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

## Templates and Views

### Where to create templates

- Now we might be able to get away with putting our templates directly in `myapp/templates` (rather than creating another `myapp` subdirectory), but it would actually be a bad idea. Django will choose the first template it finds whose name matches, and if you had a template with the same name in a different application, Django would be unable to distinguish between them. We need to be able to point Django at the right one, and the best way to ensure this is by namespacing them. That is, by putting those templates inside another directory named for the application itself.
- EX: `my_site/my_app/templates/my_app/index.django`

### Connecting Views and Templates

1. Update `settings.py` file using one of the below methods:
   1. Update `DIRS` in `TEMPLATES` variable as below with the templates folder path:

      ```py
      TEMPLATES = [
          {
              'DIRS': [os.path.join(BASE_DIR, 'templates')],
              'APP_DIRS': True,
          },
      ]
      ```

   2. Update `INSTALLED_APPS` variable with the APP class `MyAppConfig` path, which under `apps.py` in the App folder.

      ```py
      INSTALLED_APPS = [
        'my_app.apps.MyAppConfig',
        ...
        ]
      ```

2. Create a function in the `views.py` file that points to the template file using `render` function.
   - `render` function
     - `HttpRequest` argument: The request object.
     - `template_name` argument: The template relative path.
     - `context` argument: It passes kwargs as a dictionary to the template.

      ```py
      def simple_view(request):
        # my_app/templates/my_app/example.django
        return render(request,'my_app/example.django')
      ```

3. Connect the view to the URL routing.

    ```py
    urlpatterns = [
        path('',views.simple_view)
    ]
    ```

### Pass variables from Views to Templates

- Variables can be passed using argument `context` in `render` function.

  ```py
  def simple_view(request):

    my_var = {
      'key': 'value',
      'list': [1,2,3],
      'nested_dict': {'inside_key':'inside_value'}
    }
    
    return render(request,'my_app/template',my_var)
  ```

- To access the variables from the template.

  ```django
  <h2> {{key}} </h2>
  <h2> {{list.0}} </h2>
  <h2> {{nested_dict.inside_key}} </h2>
  <h2> {# This how to write a comment in Jinja #} </h2>

  value
  1
  inside_value
  ```

### Apply functions directly on templates using Filters

- Filters are built-in modifiers in Django templating that allow you to quickly apply a change to a variable on the template side, rather than in Python script.
- Filters are often similar to a Python method.
- An example of the [full list](https://docs.djangoproject.com/en/4.0/ref/templates/builtins/#built-in-filter-reference)

  ```py
  >> {{ first_name | capfirst }}
  Rosalind
  >> {{ first_name | upper }}
  ROSALIND
  ```

### Apply logic directly on the template using Tags

- Django Tags are able to provide further logic at the template in the rendering process.
- This includes a lot of functionalities, such as for loops, if-else statements, and linking to URLs.
- An example of the [full list](https://docs.djangoproject.com/en/4.0/ref/templates/builtins/#built-in-tag-reference):
  
  ```django
  <ul>
    {% for item in some_list  %}

      {% comment %} Spacing between operands and operators is essential {% endcomment %}
      {% if item == 2 %}
        <p>if statement triggered</p>
      {% endif %}
      
      <li>{{item}}</li>
      
    {% endfor %}
  </ul>
  ```

### Reversing namespaced URLs

- If you want to refer to a URL path, within your project, in a template, you can use `{% url %}` tag.
- Also, this can be achieved with the help of `name` argument in `path()` function.
- If there are templates with same name, it is required to differentiate between them. Register the app namespace in its `urls.py` file.

  ```py
  # my_app/urls.py

  # Register the app namespace
  app_name = 'my_app'

  urlpatterns = [
      path('', views.example_view, name='example_view'),
      path('variable', views.variable_view, name='variable_view'),
  ]
  ```

  ```django
  <h2><a href="{% url 'my_app:variable' %}">Click here</a></h2>
  ```

### Template inheritance

- To avoid repetitive components in templates, you can create a base template that contains the common components and inherit from it using `{%block%}` tag.
- A base template can be created in the project directory `my_site/templates/base.html`. Remember to register this base.html in your settings.py file as mentioned in [Connecting Views and Templates](#connecting-views-and-templates)

  ```django
  <h1>I am above the block in the project base.html file.</h1>
  {%block content%}

  {%endblock%}

  <h1>I am below the block in the project base.html file.</h1>
  ```
  
- Any other templates within the Apps can inherit as below.

  ```django
  {% extends "base.html" %}

  {%block content%}
  <h1>This is the h1 tag inside my_app/home.html</h1>

  {%endblock content%}
  ```

### Customizing error views

- The default error views in Django should suffice for most web applications, but can easily be overridden if you need any custom behavior. Specify the handlers as seen below in your URLconf (setting them anywhere else will have no effect).
- There are two options:
  1. Create a template with the same name of the error in the templates under project main directory. Django will load this template automatically without any additional configuration.

      ```django
      <!-- my_site/templates/404.html -->

      <h1>CUSTOM 404 page</h1>
      ```

  2. Create a template with a different name than the error. For example if you want to create a template file with name `error_404.html` instead of `404.html`, you would need to create a view variable, and add a handler in `urls.py` in the project folder. [Full list of handlers in Django documentation](https://docs.djangoproject.com/en/4.0/topics/http/views/#customizing-error-views)

      ```py
      # my_site/urls.py

      # Handlers expects the full path of the view variable name. 
      handler404 = 'my_site.views.my_custom_page_not_found_view'
      ```

      ```py
      # my_site/views.py

      def my_custom_page_not_found_view(request,exception):
    
        return render(request, 'error_404.html',status=404)
      ```

### Use static files

- Most projects will have static files, such as images, JS, or CSS.
- Django can serve these static files through the use of Tags, instead of having to refer to a full file path.
- This is similar to the `{% url %}` tag, but using a `{% static %}` tag.
- To do this:
  - Make sure that `settings.py` file is configured properly.
    - `'django.contrib.staticfiles'` is an item of `INSTALLED_APPS` list.
    - `STATIC_URL` variable is set to the location of static folder. By default, `STATIC_URL = 'static/'`
  - It is recommended to create a sub-directory in Static folder for organization purposes. For example, `'static/CSS'`, `'static/IMG'`, ...
  - Refer to it using `{% static %}` tag, as below.

    ```django
    <img src="{% static 'IMG/my_app/image.jpg' %}">
    ```

## Reference

- [Udemy - Django 4 and Python Full-Stack Developer Masterclass](https://www.udemy.com/course/django-and-python-full-stack-developer-masterclass)
