# Django web framework

- [Django](https://www.djangoproject.com/) is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

- [Django web framework](#django-web-framework)
  - [Installation](#installation)
    - [Install Django library](#install-django-library)
    - [Create a new project](#create-a-new-project)
    - [Create a new app](#create-a-new-app)
    - [Run the sever](#run-the-sever)
  - [Project structure](#project-structure)
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
  - [Models and Databases](#models-and-databases)
    - [Models and Fields](#models-and-fields)
      - [Django Model Key Concepts](#django-model-key-concepts)
      - [Updating a model](#updating-a-model)
      - [Validators](#validators)
    - [Migrations](#migrations)
    - [CRUD Interactions](#crud-interactions)
      - [Create](#create)
      - [Read](#read)
      - [Update](#update)
      - [Delete](#delete)
    - [Models and views](#models-and-views)
    - [Interactive shell](#interactive-shell)
  - [Admin](#admin)
  - [Forms](#forms)
    - [HTTP methods](#http-methods)
    - [CSRF](#csrf)
    - [Create a From class](#create-a-from-class)
    - [Connect Form class to a View](#connect-form-class-to-a-view)
    - [Connect the form view to the template](#connect-the-form-view-to-the-template)
    - [Form template rendering](#form-template-rendering)
      - [Form rendering options](#form-rendering-options)
      - [Rendering fields manually](#rendering-fields-manually)
      - [Looping over form's fields](#looping-over-forms-fields)
    - [Form styling](#form-styling)
    - [Form widgets](#form-widgets)
      - [Specifying a widget](#specifying-a-widget)
      - [Setting arguments for widgets](#setting-arguments-for-widgets)
    - [ModelForm Class](#modelform-class)
      - [Connect Model to Form](#connect-model-to-form)
    - [ModelForm customization](#modelform-customization)
    - [Register a model into Admin](#register-a-model-into-admin)
  - [Class Based Views](#class-based-views)
    - [Template view](#template-view)
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

### Connecting Views and URLs

- Connecting a View to a URL with `path()` function:
  - `route` argument is a string that contains the URL pattern. Django will scan the relevant `urlpatterns` list until it finds a matching string route.
  - `view` argument is a string that points to the `views.py` file which will be connected to the URL pattern found in `route`.
  - `kwargs` is an optional argument. It allows to pass in keyword arguments to the view.
  - `name` is an optional argument. It allows to name the URL for referencing elsewhere in the project.
- Create a Function Based View (FBV) or a Class Based View (CBV)
  - In `views.py` file under an App component:

    ```py
    from django.http import HttpResponse

    # Example for Function Based View:
    def simple_view(request):
      return HttpResponse("Simple View")

    # Example for Class Based View
    class SimpleView(TemplateView):
      template_name = 'classroom/home.html'
    ```

  - To connect this view to a URL routing, you need to add it as a `path` function to string `urlpatterns`.
  - Create (If not exists) `urls.py` file under the App folder:

    ```py
    from django.urls import path
    from . import views

    # '' is a route for the home page. But since this urls.py file under an app component,
    # the home page for the app. In other words, this is the routing for the webpages after being directed to www.domain.com/my_app/
    urlpatterns = [
        # FBV
        path('',views.simple_view)
        # CBV
        path('',views.SimpleView.as_view())
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
- This can be accomplished in Django through the use of the `HttpResponseRedirect()` function or `redirect().
- To facilitate referencing between URLs and pages, `name` argument in `path()` helps with this.
- To link a page to a specific name, in `urls.py`:

  ```py
  path('<str:topic>',views.simple_view, name='topic-name'),
  ```

- To send a page to a named routing URL, in `views.py`:

  ```py
  from django.http import HttpResponseRedirect
  HttpResponseRedirect(reverse('topic-name',args=[topic]))
  # OR
  from django.urls import reverse
  redirect(reverse('topic-name',args=[topic]))
  ```

## Templates and Views

### Where to create templates

- Now we might be able to get away with putting our templates directly in `myapp/templates` (rather than creating another `myapp` subdirectory), but it would actually be a bad idea. Django will choose the first template it finds whose name matches, and if you had a template with the same name in a different application, Django would be unable to distinguish between them. We need to be able to point Django at the right one, and the best way to ensure this is by namespacing them. That is, by putting those templates inside another directory named for the application itself.
- EX: `my_site/my_app/templates/my_app/index.html`

### Connecting Views and Templates

1. Update `settings.py` file using one of the below methods:
   1. Update `DIRS` in `TEMPLATES` variable as below with the templates folder path:

      ```py
      TEMPLATES = [
          {
              'DIRS': [BASE_DIR / 'templates'],
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
        # my_app/templates/my_app/example.html
        return render(request,'my_app/example.html')
      ```

3. Connect the view to the [URL routing](#connecting-views-and-urls).

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

  # Register the app namespace, to be used in URL name tags.
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

## Models and Databases

- Django is pretty agnostic to most major SQL engines with the use of its Django Models system, so switching to another SQL engine is more a matter of updating `settings.py` rather than rewriting the actual Python Django code.
- Run a migrate command to create the database, `python manage.py migrate`.
- [Django docs](https://docs.djangoproject.com/en/4.0/ref/settings/#databases)

  ```py
  # settings.py

  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': BASE_DIR / 'db.sqlite3',
      }
  }
  ```

- Models allow us to interact with a database with Python and Django. This includes the key interactions with a database - CRUD.
- Django Models are defined inside a Django app (or project) `models.py` file.
- The models class operates on a system which directly converts Python based code into SQL commands. This makes it much easier to work with the backend database.
- Creating a Model is similar to creating a new table in a database.
- Each database table has a name and then columns, where each column will have a specific data type, for example: character strings for names or integers for ages in years.

  ```py
  # Inside a model file
  from django.db import models

  class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30) 
  ```

  ```sql
  -- Automatically converted to SQL
  CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL
  );
  ```

### Models and Fields

#### Django Model Key Concepts

- Inherits from models class.
- Uses fields to define both data types and data constraints. For example,
  - You may want to require information, like a user’s email address, in which case you can add a `NOT NULL` constraint.
  - You may want to require unique entries, like a unique user email (no duplicate accounts) with a UNIQUE constraint.

  ```py
  # Inside a model file
  from django.db import models

  class Musician(models.Model):
    # Fields are chosen for data type. Like CharField, ForeignKey, DateField ...
    first_name = models.CharField(max_length=30)
    # Field arguments specify constraints. Like (max_length=30)
    last_name = models.CharField(max_length=30) 

  class Album(models.Model):
    # Django Models can also be connected through keys
    musician = models.ForeignKey(Musician,on_delete = models.CASCADE)
    name = models.CharField(max_length=100)
    releaseDate = models.DateField()
    rating = models.IntegerField()
  ```

#### Updating a model

- There may come a time when you need to create a new column or attribute for a model.
- You can easily update existing models by simply adding a new model class attribute and then migrating those changes.
- You should note that when adding new fields, the existing entries will need to have some default value inserted (even if it’s just null).
- In fact, when we attempt to run migrations without taking care of these issues, Django will specifically request us to make a decision.
- You’ll be given two options:
  - Choose a default value on the spot when making the migrations file.
  - Cancel the migration and create a default value within the model.
- It’s usually more robust to have the default live in the model, but each case is different.

#### Validators

- The `django.core.validators` module contains a collection of callable validators for use with model and form fields. They’re used internally but are available for use with your own fields, too. They can be used in addition to, or in lieu of custom field.clean() methods.
- Validators in Django documentations can be found in [Validators](https://docs.djangoproject.com/en/4.0/ref/validators/#built-in-validators) topic which lists all available validators. Or the supported validator for [field type](https://docs.djangoproject.com/en/4.0/ref/models/fields/).

  ```py
  from django.core.validators import MaxValueValidator,MinValueValidator

  class Patient(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30) 
    age = models.IntegerField(validators=[MinValueValidator(0),MaxValueValidator(120)]) 
    heartrate = models.IntegerField(default=60,validators=[MinValueValidator(1),MaxValueValidator(300)])

  ```

### Migrations

- In general, migrations is the act of connecting changes in your Django project or app to the database.
- This includes things like adding new models within an application, adding a new application, updating models with a new column/attribute, and more.
- There are 3 commands for migrations:
  - `python manage.py makemigrations my_app`:
    - This actually creates, but does not run, the set of instructions that will apply changes to the database.
    - The default applications in Django (e.g. Admin, Auth) already have their SQL `makemigrations` code ready, just not run yet.
    - The migrations files are created under `my_app/migrations/0001_initial.py`
  - `python manage.py migrate`:
    - Runs any existing migrations that created through the `makemigrations` command.
  - `python manage.py sqlmigrate my_app 0001`:
    - Used to check the SQL commands that will be executed by running `0001_initial.py` file.

### CRUD Interactions

- Each Model you create comes with a Manager that allows you to create a QuerySet which can then be used to retrieve entries from the database.
- [QuerySet is actually lazily](https://docs.djangoproject.com/en/4.0/topics/db/queries/#querysets-are-lazy) evaluated, meaning that it doesn’t hit the database until its explicitly asked to grab the information.

#### Create

- There are three ways to insert a new database entry:
  - Create an instance of the object class. Ex: `carl = Student(first_name="Carl",last_name="Smith")`. Then insert this object instance to DB by calling `.save()` method.
  - Use the built-in `.objects.create()` method to both create and save the new data entry in a single line.
  - Insert multiple entries at once by using `.objects.bulk_create()`

#### Read

- To [retrieve objects](https://docs.djangoproject.com/en/4.0/topics/db/queries/#retrieving-objects) from your database, construct a QuerySet via a Manager on your model class.
- A **QuerySet** represents a collection of objects from your database. It can have zero, one or many filters. Filters narrow down the query results based on the given parameters. In SQL terms, a QuerySet equates to a **SELECT** statement, and a filter is a limiting clause such as **WHERE** or **LIMIT**.
- [Retrieving all objects](https://docs.djangoproject.com/en/4.0/topics/db/queries/#retrieving-all-objects):
  - The simplest way to retrieve objects from a table is to get all of them. To do this, use the `all()` method on a Manager. `Entry.objects.all()`
- [Retrieving a single object with `get()`](https://docs.djangoproject.com/en/4.0/topics/db/queries/#retrieving-a-single-object-with-get):
  - If you know there is only one object that matches your query, you can use the get() method on a Manager which returns the object directly. `Entry.objects.get(pk=1)`
- [Retrieving specific objects with filters](https://docs.djangoproject.com/en/4.0/topics/db/queries/#retrieving-specific-objects-with-filters):
  - [Filtered QuerySets are unique](https://docs.djangoproject.com/en/4.0/topics/db/queries/#filtered-querysets-are-unique): Each time you refine a QuerySet, you get a brand-new QuerySet that is in no way bound to the previous QuerySet. Each refinement creates a separate and distinct QuerySet that can be stored, used and reused.
  - To create such a subset, you refine the initial QuerySet, adding filter conditions. The two most common ways to refine a QuerySet are:
    - `filter(**kwargs)`: Returns a new QuerySet containing objects that match the given lookup parameters. `Entry.objects.filter(pub_date__year=2006)`
    - `exclude(**kwargs)`: Returns a new QuerySet containing objects that do not match the given lookup parameters. `Entry.objects.exclude(pub_date__year=2006)`
  - The lookup parameters (****kwargs** in the above function definitions) should be in the format described in [Field lookups](https://docs.djangoproject.com/en/4.0/topics/db/queries/#field-lookups).
  - [Chaining filters](https://docs.djangoproject.com/en/4.0/topics/db/queries/#chaining-filters): The result of refining a QuerySet is itself a QuerySet, so it’s possible to chain refinements together.
  - [Complex lookups with Q objects](https://docs.djangoproject.com/en/4.0/topics/db/queries/#complex-lookups-with-q-objects):
    - Keyword argument queries – in filter(), etc. – are “AND”ed together. If you need to execute more complex queries (for example, queries with OR statements), you can use Q objects.
    - A Q object (django.db.models.Q) is an object used to encapsulate a collection of keyword arguments. These keyword arguments are specified as in “Field lookups” above.
    - Q objects can be combined using the & and | operators. When an operator is used on two Q objects, it yields a new Q object.
    - Each lookup function that takes keyword-arguments (e.g. filter(), exclude(), get()) can also be passed one or more Q objects as positional (not-named) arguments. If you provide multiple Q object arguments to a lookup function, the arguments will be “AND”ed together.

      ```py
      Poll.objects.get(
          Q(question__startswith='Who'),
          Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6)))
      ```

      ```sql
      -- SQL equivalent

      SELECT * from polls WHERE question LIKE 'Who%'
          AND (pub_date = '2005-05-02' OR pub_date = '2005-05-06')
      ```

- [Limiting QuerySets](https://docs.djangoproject.com/en/4.0/topics/db/queries/#limiting-querysets):
  - Use a subset of Python’s array-slicing syntax to limit your QuerySet to a certain number of results. This is the equivalent of SQL’s **LIMIT** and **OFFSET** clauses. `Entry.objects.all()[:5]`
  - Negative indexing (i.e. `Entry.objects.all()[-1]`) is not supported.

#### Update

- To update an existing record:
  1. Retrieve it.
  2. Do the changes to the object.
  3. Save this object.

  ```py
  # First, you need to retrieve it.
  John = Persons.objects.get(pk=1)

  # Second, do the changes to the object.
  John.first_name = 'Bond'

  # Finally, save this object.
  John.save()
  ```

#### Delete

- To delete an existing record:
  1. Retrieve it.
  2. Delete it.

  ```py
  # First, you need to retrieve it.
  John = Persons.objects.get(pk=1)

  # Finally, delete this object.
  John.delete()
  ```

### Models and views

- Typically, the model will contain the structure of the database. Like tables and attributes.
- While actual CRUD interactions will be applied in the Views.

    ```py
    def list_view(request):
    
      cars = Car.objects.all()
      context = {'cars': cars}
      
      return render(request, 'cars/list.html', context=context)
    ```

### Interactive shell

- If you want to run commands to the project, you can use the interactive shell
- `python manage.py shell` to run commands.

## Admin

- This is a feature meant to be used by the website manager, to have a graphical interface for interacting with data and users on the site.
- It is created automatically by Django
- It can be accessed by 'domain.com/admin'
- To create a Superuser `python manage.py createsuperuser`

## Forms

- It allows client users send information in their browser to the backend.
- The Django website can then Create/Read/Update/Delete information in the database based on the HTML forms.
- Django comes with a built-in Forms class which can be used with Django and Python to create forms and then send that form to the template through a simple Tag call `{{form}}`.
- This will be a huge productivity improvement and make our overall website code more readable.

### HTTP methods

- GET:
  - Requests data from a specified resource.
  - GET request can only request data, not modify or update anything.
  - GET request can be bookmarked
  - GET request saved in history
  - GET request can be cached
  - GET request has length limits
- POST:
  - Requests to send data to a server to create/update a resource.

### CSRF

- CSRF or Cross-Site Request Forgery is used to change the information that are meant to be sent originally by the form.
- This can be avoided:
  - By generating a random cryptographic token with every form during each session.
  - The server could then confirm if the token matches with the current session.
  - Since each session has a unique token, only the true original form would be accepted as authentic.
- Django creates these CSRF tokens automatically with a simple tag call `{% csrf_token %}`
- For [more information](https://docs.djangoproject.com/en/4.0/ref/csrf/)

### Create a From class

1. Create a file called `forms.py` under the App folder.
2. Import forms class from Django. `from django import forms`
3. Create a form class `class ViewForm(forms.Form)`
4. Inside the class, create a form attributes. The form attribute is a form field that connected to a widget. This widget renders the HTML form field related type.

```py
# forms.py
from django import forms

class ViewForm(forms.Form):
  first_name = forms.CharField(label='first_name', max_length=100)
  last_name  = forms.CharField(label='last_name', max_length=100)
  email      = forms.EmailField(label='Email')
```

### Connect Form class to a View

1. Import the form class in `views.py`. `from .forms import ViewForm`
2. Check if the request is a POST request (Form submission) or if not render an empty form.

```py
from django.shortcuts import redirect, render
from django.urls import reverse
from .forms import ReviewForm

def rental_review_view(request):
  # Check if the request is a POST request
  if request.method == 'POST':
    # create a form of Type ClassForm
    form = ReviewForm(request.POST)
    # Check if the form data is valid
    if form.is_valid():
      # Preview the form data as a dictionary like
      print(form.cleaned_data)
      return redirect(reverse('cars:thank_you'))
  else:
    # If not a POST then show an empty form
    form = ReviewForm
  return render(request,'cars/rental_review.html',context={'form': form})
```

### Connect the form view to the template

1. Create a Form HTML tag ``{{form}}. Form’s output does not include the surrounding `<form>` tags, or the form’s submit control.
2. Add csrf protection tag `{{ csrf_token }}`
3. Add the form tag `{{ form }}`
4. Add a submission button

```django
<form method="post">
    {% csrf_token %}
    {{form}}
    <input type="submit">
</form>
```

### Form template rendering

#### Form rendering options

- Wrap each form element with an HTML tag. For example, `{{form.as_p}}` wraps each element with a `<p></p>` tag; same applies to `{{form.as_table}}` will render them as table cells wrapped in `<tr>` tags. More info in [docs](https://docs.djangoproject.com/en/4.0/topics/forms/#form-rendering-options).

  ```django
  <form method="post">
      {% csrf_token %}
      {{form.as_p}}
      <input type="submit">
  </form>
  ```

#### Rendering fields manually

- It is possible to unpack each field manually. It allows for reordering.
- Each field is available as an attribute of the form using `{{ form.name_of_field }}`, its label as `{{ form.name_of_field.label_tag }}`.

  ```django
  <form method="post">
    {% csrf_token %}
    {{form.first_name.errors}}
    {{form.first_name.label_tag}}
    {{form.first_name}}
    <input type="submit">
  </form>
  ```

- More info in [docs](https://docs.djangoproject.com/en/4.0/topics/forms/#rendering-fields-manually).

#### Looping over form's fields

- It also possible to loop over all fields.
- More info in the [docs](https://docs.djangoproject.com/en/4.0/topics/forms/#looping-over-the-form-s-fields)

  ```django
  <form method="post">
      {% csrf_token %}
      {% for field in form %}
      <div class="mb-3">
          {{field.label_tag}}
          {{field}}
      </div>
      {% endfor %}
      <input type="submit">
  </form>
  ```

### Form styling

1. Link a static CSS file.
   1. Create `my_app/static/my_app/custom.css` file
   2. Load static directory in .html using `{% load static %}` tag.
   3. Link static CSS file connection using `{% static 'my_app/custom.css' %}` tag. `<link rel="stylesheet" href="{% static 'cars/custom.css' %}">`
   4. Run migrate to load new app in settings.py file

### Form widgets

- A widget is Django’s representation of an HTML input element. The widget handles the rendering of the HTML, and the extraction of data from a GET/POST dictionary that corresponds to the widget.
- [Django docs for widgets](https://docs.djangoproject.com/en/4.0/ref/forms/widgets/)

#### Specifying a widget

- Django will use a default widget that is appropriate to the type of data that is to be displayed. To find which widget is used on which field, see the documentation about [Built-in Field classes](https://docs.djangoproject.com/en/4.0/ref/forms/fields/#built-in-fields).
- However, it is possible to use a different widget for a field, you can use the widget argument on the field definition.

```py
from django import forms

class CommentForm(forms.Form):
    name = forms.CharField()
    url = forms.URLField()
    comment = forms.CharField(widget=forms.Textarea)
```

#### Setting arguments for widgets

- Many widgets have optional extra arguments; they can be set when defining the widget on the field. More information in the [documentation](https://docs.djangoproject.com/en/4.0/ref/forms/widgets/#setting-arguments-for-widgets).
- Django provides a representation of all the basic HTML widgets, plus some commonly used groups of widgets in the django.forms.widgets module, including the input of text, various checkboxes and selectors, uploading files, and handling of multi-valued input.

  ```py
  from django import forms
  name = forms.TextInput(attrs={'size': 10, 'title': 'Your name'})
  name.render('name', 'A name')
  ```
  
### ModelForm Class

- It automatically creates a Form with fields connected to each model field.
- Django [documentation](https://docs.djangoproject.com/en/4.0/topics/forms/modelforms/)

#### Connect Model to Form

1. Create a Model in `model.py`

    ```py
    # models.py
    from django.db import models

    class ReviewModel(models.Model):
      first_name = models.CharField(max_length=10)
      last_name  = models.CharField(max_length=10)
      star = models.IntegerField()
    ```

2. Register it in `admin.py`

    ```py
    # admin.py
    from django.contrib import admin
    from .models import ReviewModel

    admin.site.register(ReviewModel)
    ```

3. Import the Model into `forms.py` and create a form class of type `forms.ModelForm`.

    ```py
    # forms.py
    from django import forms
    from .models import ReviewModel

    class ReviewForm(forms.ModelForm):
      class Meta:
        model = ReviewModel
        fields = "__all__" # Pass all model fields as form fields
    ```

4. Save form submission using `.save()` in `views.py`

    ```py
    from django.shortcuts import redirect, render
    from django.urls import reverse
    from .forms import ReviewForm

    # Create your views here.
    def rental_review_view(request):
      if request.method == 'POST':
        form = ReviewForm(request.POST)
        if form.is_valid():
          print(form.cleaned_data)
          form.save()
          return redirect(reverse('cars:thank_you'))
      else:
        form = ReviewForm
      return render(request,'cars/rental_review.html',context={'form': form})
    ```

### ModelForm customization

- The from fields imported from the model can be customized in several ways.
- It is possible to add specific fields in the form.
- Override the field labels.
- Override validation error messages. Error messages keys can be found in form fields in [docs](https://docs.djangoproject.com/en/4.0/ref/forms/fields/#integerfield). For example, error messages keys for IntegerField are `required, invalid, max_value, min_value`

  ```py
  # models.py
  class ReviewForm(forms.ModelForm):
    class Meta:
      model = ReviewModel
      fields = ['first_name', 'last_name', 'star']
      labels = {
        'first_name': 'First Name',
        'last_name': 'Last Name',
        'star': 'Rating'
      }
      error_messages = {
        'star' : {
          'min_value':'Min value is 1',
          'max_value':'Max value is 5'
        }
      }
  ```

### Register a model into Admin

1. Using the default admin interface

    ```py
    # in my_app.admin.py file
    from django.contrib import admin
    from my_app.models import my_model

    # Register your models here.
    admin.site.register(my_model)
    ```

2. Using [modelAdmin](https://docs.djangoproject.com/en/4.0/ref/contrib/admin/#modeladmin-objects) class for more customization.

    ```py
    from django.contrib import admin

    class FlatPageAdmin(admin.ModelAdmin):
        fieldsets = (
            (None, {
                'fields': ('url', 'title', 'content', 'sites')
            }),
            ('Advanced options', {
                'classes': ('collapse',),
                'fields': ('registration_required', 'template_name'),
            }),
        )
    ```

## Class Based Views

- Writing web applications can be monotonous, because we repeat certain patterns again and again. Django tries to take away some of that monotony at the model and template layers, but web developers also experience this boredom at the view level.
- Django’s generic views were developed to ease that pain. They take certain common idioms and patterns found in view development and abstract them so that you can quickly write common views of data without having to write too much code.
- Django provides an entire View class system that is very powerful for quickly rendering commonly used views.
- Django CBVs (Class Based Views) come with many pre-built generic class views for common tasks, such as listing all the values for a particular model in a database (ListView) or creating a new instance of a model object (CreateView).

### Template view

- Compared to FBV
  - Create a class inherited from `TemplateView` class
  - Add the template relative path to variable `template_name`.

  ```py
  # Create your views here.
  def home_view(request):
    return render(request, 'classroom/home.html')

  class HomeView(TemplateView):
    template_name = 'classroom/home.html'
  ```

## Reference

- [Udemy - Django 4 and Python Full-Stack Developer Masterclass](https://www.udemy.com/course/django-and-python-full-stack-developer-masterclass)
