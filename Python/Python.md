# Python Cheat sheet

- [Python Cheat sheet](#python-cheat-sheet)
  - [While loop](#while-loop)
  - [Tricks](#tricks)
  - [Desktop App using Tkinter](#desktop-app-using-tkinter)
  - [Draw on screen using Turtle module](#draw-on-screen-using-turtle-module)
  - [Classes](#classes)
  - [HTTP servers](#http-servers)
  - [Python DB-API](#python-db-api)
  - [PostgreSQL ("psycopg2" module)](#postgresql-psycopg2-module)
  - [Bleach](#bleach)
  - [CRUD operations with SQLAlchemy](#crud-operations-with-sqlalchemy)
    - [First: database setup](#first-database-setup)
    - [Second: CRUD operation](#second-crud-operation)
  - [Web Frameworks](#web-frameworks)
    - [Flask](#flask)
      - [Third Party Auth](#third-party-auth)
    - [Streamlit](#streamlit)
      - [Getting Started](#getting-started)
      - [Syntax](#syntax)
  - [Machine Learning](#machine-learning)
    - [StatsModels](#statsmodels)
    - [Scikit learn](#scikit-learn)
    - [YellowBrick](#yellowbrick)
    - [MLxtend](#mlxtend)
    - [Apache MXNet](#apache-mxnet)
    - [OpenCV](#opencv)
  - [Conventions](#conventions)
  - [Speed Up Performance](#speed-up-performance)
    - [Speed up execution time](#speed-up-execution-time)
      - [Compare time](#compare-time)
      - [Speed up techniques](#speed-up-techniques)
    - [Speed up references](#speed-up-references)
  - [Tips and Tricks](#tips-and-tricks)
    - [Shared References and In-Place Changes](#shared-references-and-in-place-changes)
    - [Creating a Slide Deck with Jupyter](#creating-a-slide-deck-with-jupyter)
  - [Handful resources](#handful-resources)

## While loop

```python
n = 10
while n > 0:
    print(n)
    n -= 1
    time.sleep(1)
print("Blastoff!")
```

## Tricks

1. Augmented assignment

   ```python
   # The effect of n = n + 1 and n += 1 is the same. The latter is called an augmented assignment statement, because it's an assignment statement but it augments the existing value rather than replacing it.
   
   # So augmented assignment is not only shorter, but also can catch some errors that otherwise might creep into the code.
   n += 1
   n -= 1
   n *= 1
   n /= 1
   ```

2. Comprehension function:

   - The below line code has for loop and if condition in the same line

     ```python
     ''.join(i for i in name if not i.isdigit())
     ```

3. Change data type

   ```python
   import numpy as np
   # convert string to int
   int("123")
   
   # convert int to string
   str(123)
   
   # convert list to array
   arr = np.array([0,1,2])
   
   # convert array to list
   lst = list(arr)
   ```

## Desktop App using Tkinter

1. Import the library

   ```py
   import tkinter as tk
   ```

2. Create a window

   ```py
   # Define a window
   window = tk.Tk()
   
   # Define window title
   window.title("My first GUI")
   
   # Define window size
   window.geometry("300x200")
   ```

3. Widgets

   - The basic syntax of widget is:

   ```py
   # parent is the window variable
   tk.Widget_name(parent,options)
   ```

   1. Entry
      Entry fields are used to get some inputs.

      ```py
      tk.Entry(parent,width=25)
      ```

   2. Button:
      Buttons are used to make some events.

      ```py
      tk.Button(parent, text="Click Here")
      ```

   3. Checkbutton:
      It is used to check some conditions and terms.

      ```py
      tk.Checkbutton(parent,text="Remember me",variable=tk.IntVar())
      ```

   4. Label
      It is used to display some text or image

      ```py
      tk.Label(text="Hello world",, font=("Times new roman", 20))
      ```

   5. OptionMenu
      It is used to select an option from a drop-down menu.

      ```py
      tk.OptionMenu(parent,tk.IntVar(),"Age","15+","25+","40+")
      ```

   6. Scrollbar
      It is used to scroll the app.

      ```py
      tk.Scrollbar(parent,orient=tk.VERTICAL)
      ```

   7. Radiobutton
      It is used to provide multiple options in which the only one of them can be selected.

      ```py
      tk.Radiobutton(parent,text="Male",variable=tk.IntVar(),value=5)
      ```

   8. Text
      It is used to add text and print them on the GUI.

      ```py
      tk.Text(parent,height=20,width=10)
      ```

   - There are some more widgets available like the list box, progress bar, scale, spinbox, etc. You can learn more about widgets [here](http://tkdocs.com/tutorials/widgets.html).
4. `pack` and `grid`

   - We can arrange the widgets using the `pack()` method instead of the `grid()`. The problem with `pack()` is that it packs things as close as possible. You can’t even give space or change the rows and columns, or change the order of widgets. That is why `pack()` is not often used, instead, `grid()` is used mostly.

     ```py
     widget_name.grid(column=col_pos,row=row_pos)
     ```

5. Bind Function

   - It is used to bound a function with a button after an event is fired.

   ```py
   # We use window as the first argument of the Button method, to connect the button to our window.
   button_name = tk.Button(window, text = "some text")
   button_name.grid(column=1,row=0)
   
   # An function to be called after the trigger is fired
   def fn():
      print("Event Triggered")
   
   # Bound it to the window of the app using the bind method.
   # The first parameter is the event. <Button-1> is the left click short key of the mouse.
   # The second parameter is the name of the event function.
   button_name.bind("<Button-1>",fn)
   ```

6. Connecting Entries with Buttons

   - We can connect a button with entries using the keyword command and assigning it a function name.

   ```py
   button = tk.Button(text="click",command=function_name)
   ```

   - Also, we can get the value from the entry using `get()` method.

     ```py
     name_entry.get()
     ```

7. Load the app

   - This function is like `main()` in C. It is used to start the app

     ```py
     window.mainloop()
     ```

## Draw on screen using Turtle module

```python
import Turtle

# Initialize a turtle object
sharaflex = turtle.Turtle()

# Change its color
sharaflex.color("purple")

# Movements
sharaflex.forward(100)
sharaflex.right(90)
sharaflex.backward(100)
sharaflex.left(90)

# Draw a circle
sharaflex.circle(100)

# Current coordination
sharaflex.xcor()
sharaflex.ycor()

# Change object shape
sharaflex.shape("turtle")

# Stop drawing
sharaflex.penup()

# Continue drawing
sharaflex.pendown()

# Increase drawing line width
sharaflex.width(5)

# Increase drawing speed
sharaflex.speed(6)
sharaflex.speed(0) # Max speed

# Hide turtle
sharaflex.hideturtle()

# Initiate the screen object to manipulate it
window = turtle.Screen()

# change screen background
window.bgcolor("red")

# Close the screen after clicking
window.exitonclick()

# Finish Drawing
turtle.done()
```

## Classes

1. Creating classes in a separate file

   ```python
   # Create a class
   class Movie():
       # class documentation
       """This class provides a way to store movie related information"""
       #Class variables
       VALID_RATINGS = ['G', 'PG', 'PG-13', 'R']
       # Define Constructor (Initialization function) that runs whenever an    instance is created
       # self is the instance object name
       def __init__(self, movie_title, movie_storyline, poster_image,  trailer_youtube):
   
           #define Instance variables
           self.title = movie_title
           self.storyline = movie_storyline
           self.poster_image_url = poster_image
           self.trailer_youtube_url = trailer_youtube
       # Define Instance methods
       def show_trailer(self):
           webbrowser.open(self.trailer_youtube_url)
   
   # Create an inheritance class
   class Stats(Movie):
       def __init__(self, movie_title, movie_storyline, poster_image,  trailer_youtube,cast,budget):
           Movie.__init__(self, movie_title, movie_storyline, poster_image,    trailer_youtube)
           self.cast = cast
           self.budget = budget
   
   # Note that parent method can be overridden by creating the method in the child class
   
   # Predefined class variables:
   __doc__ # documentation for the class
   __name__
   __module__
   ```

2. Import the class file and use it

   ```python
   import media
   # create an instance of the inheritance(child) class
   toy_story = media.Stats(
       "Toy_story",
       "A cowboy doll is profoundly threatened and jealous when a new  spaceman figure supplants him as top toy in a boy's room.",
       "https://www.imdb.com/title/tt0114709/?ref_=ttpl_pl_tt",
       "https://www.imdb.com/video/imdb/vi2052129305?playlistId=tt0114709& ref_=tt_ov_vi",
       "42","45M")
   # calling a method from the parent class
   toy_story.show_trailer()
   # Note that parent method can be overridden by creating the method in the child class
   ```

## HTTP servers

1. Send request

   ```python
   # 1. Import http.server, or at least the pieces of it that you need.
   from http.server import HTTPServer, BaseHTTPRequestHandler
   
   # 2. Create a subclass of `http.server.BaseHTTPRequestHandler`. This is your handler class.
   class HelloHandler(BaseHTTPRequestHandler):
   # 3. Define a method on the handler class for each **HTTP verb** you want to handle.
   def do_GET(self):
   # Inside the method, call built-in methods of the handler class to read the HTTP request and write the response.
   
       # First, send a 200 OK response.
       self.send_response(200)
   
       # Then send headers.
       self.send_header('Content-type', 'text/plain; charset=utf-8')
       self.end_headers()
   
       # Now, write the response body.
       paths = self.path # This instance returns the request path
       # The name wfile stands for writeable file.
       # self.wfile represents the connection from the server to the client; and it is write-only; hence the name
       # to send a string over the HTTP connection, you have to encode the string into a bytes object.
       self.wfile.write(path[1,:].encode())
   
    # This code will run when we run this module as a Python program,rather than importing it.
    if __name__ == '__main__':
    server_address = ('', 8000)  # Serve on all addresses, port 8000.
    # 4. Create an instance of `http.server.HTTPServer`, giving it your handler class and server information — particularly, the port number.
    httpd = HTTPServer(server_address, HelloHandler)
    # 5. Call the `HTTPServer` instance's `serve_forever` method.
    httpd.serve_forever()
   ```

2. Parse query string

   ```python
   from urllib.parse import urlparse, parse_qs
   address = 'https://www.google.com/search?q=gray+squirrel&tbm=isch'
   parts = urlparse(address)
   print(parts)
   #ParseResult(scheme='https', netloc='www.google.com', path='/search',    params='', query='q=gray+squirrel&tbm=isch', fragment='')
   print(parts.query)
   #q=gray+squirrel&tbm=isch
   query = parse_qs(parts.query)
   query
   #{'q': ['gray squirrel'], 'tbm': ['isch']}
   ```

3. Redirect to the root

   ```python
   # Send a 303 back to the root page
       self.send_response(303)  # redirect via GET
       self.send_header('Location', '/')
       self.end_headers()
   ```

4. Send an HTML form

   ```python
   form = '''<!DOCTYPE html>
   <title>Message Board</title>
   <form method="POST">
   <textarea name="message"></textarea>
   <br>
   <button type="submit">Post it!</button>
   </form>
   <pre>
   {}
   </pre>
   '''
   
   class MessageHandler(BaseHTTPRequestHandler):
       def do_GET(self):
       # First, send a 200 OK response.
       self.send_response(200)
   
       # Then send headers.
       self.send_header('Content-type', 'text/html; charset=utf-8')
       self.end_headers()
   
       # Send the form with the messages in it.
       msg = form.format("\n".join(memory))
       self.wfile.write(msg.encode())
   ```

5. Read data out of a form:

   1. Using urllib module:

      ```py
      from http.server import BaseHTTPRequestHandler, HTTPServer
      from urllib.parse import parse_qs
      
      def form(title, button):
           return f'''
            <form
            method='POST'
            enctype='multipart/form-data'
            <h2>{title}</h2>
            <br>
            <input name="message" type="text">
            <input type="submit" value="{button}">
            </form>
            '''
      
       class WebServerHandler(BaseHTTPRequestHandler):
      
           def do_GET(self):
                if self.path.endswith("/restaurants/new"):
                    form("Add new restaurant","Add")
      
           def do_POST(self):
               if self.path.endswith("/restaurants/new"):
                   length = int(self.headers.get('Content-length'0))
                   body = self.rfile.read(length).decode()
                   params = parse_qs(body)
                   messagecontent = params["message"][0]
      ```

   2. Using cgi library:

      ```py
      from http.server import BaseHTTPRequestHandler, HTTPServer
      import cgi
      
      def form(title, button):
           return f'''
            <form
            method='POST'
            enctype='multipart/form-data'
            <h2>{title}</h2>
            <br>
            <input name="message" type="text">
            <input type="submit" value="{button}">
            </form>
            '''
      
       class WebServerHandler(BaseHTTPRequestHandler):
      
           def do_GET(self):
                if self.path.endswith("/restaurants/new"):
                    form("Add new restaurant","Add")
      
           def do_POST(self):
               if self.path.endswith("/restaurants/new"):
                    # ? Method 1:
                    ctype, pdict = cgi.parse_header(self.headers.get('content-type'))
                    pdict['boundary'] = bytes(pdict['boundary'], "utf-8")
                    content_len = int(self.headers.get('Content-length'))
                    pdict['CONTENT-LENGTH'] = content_len
                    if ctype == 'multipart/form-data':
                        fields = cgi.parse_multipart(self.rfile, pdict)
                    message = fields.get('message')
                    messagecontent = message[0]
      
                    # ? Method 2:
                    form = cgi.FieldStorage(fp=self.rfile, headers=self.headers, environ={'REQUEST_METHOD': 'POST', 'CONTENT_TYPE': self.headers['Content-Type'], })
                    messagecontent = form['message'].value
      ```

6. Requests library can do the following

   1. Make a Request
   2. Passing Parameters In URLs
   3. Response Content
   4. Binary Response Content
   5. JSON Response Content
   6. Response Status Codes
   7. Custom Headers
   8. Cookies
   9. and many [more](https://2.python-requests.org//en/master/user/quickstart/) ...
7. Concurrency

   ```python
   import threading
   from socketserver import ThreadingMixIn
   
   class ThreadHTTPServer(ThreadingMixIn, http.server.HTTPServer):
       "This is an HTTPServer that supports thread-based concurrency."
   
   if __name__ == '__main__':
   port = int(os.environ.get('PORT', 8000))
   server_address = ('', port)
   httpd = ThreadHTTPServer(server_address, Shortener)
   httpd.serve_forever()
   ```

8. Cookies

   To set a cookie from a Python HTTP server, all you need to do is set the `Set-Cookie` header on an HTTP response. Similarly, to read a cookie in an incoming request, you read the `Cookie` header. However, the format of these headers is a little bit tricky; I don't recommend formatting them by hand. Python's `http.cookies` module provides handy utilities for doing so.

   To create a cookie on a Python server, use the SimpleCookie class. This class is based on a dictionary, but has some special behavior once you create a key within it:

   ```python
   from http.cookies import SimpleCookie, CookieError
   
   out_cookie = SimpleCookie()
   out_cookie["bearname"] = "Smokey Bear"
   out_cookie["bearname"]["max-age"] = 600
   out_cookie["bearname"]["httponly"] = True
   ```

   Then you can send the cookie as a header from your request handler:

   ```python
   self.send_header("Set-Cookie", out_cookie["bearname"].OutputString())
   ```

   To read incoming cookies, create a SimpleCookie from the Cookie header:

   ```python
   in_cookie = SimpleCookie(self.headers["Cookie"])
   in_data = in_cookie["bearname"].value
   ```

   Be aware that a request might not have a cookie on it, in which case accessing the `Cookie` header will raise a `KeyError` exception; or the cookie might not be valid, in which case the `SimpleCookie` constructor will raise `http.cookies.CookieError`

   **Important safety tip**: Even though browsers make it difficult for users to modify cookies, it's possible for a user to modify a cookie value. Higher-level web toolkits, such as Flask (in Python) or Rails (in Ruby) will cryptographically sign your cookies so that they won't be accepted if they are modified. Quite often, high-security web applications use a cookie just to store a session ID, which is a key to a server-side database containing user information.

   For a lot more information on cookie handling in Python, see the documentation for the [http.cookies module](https://docs.python.org/3/library/http.cookies.html).

## Python DB-API

For a full reference to the Python DB-API, see [the specification](https://www.python.org/dev/peps/pep-0249/) and the documentation for specific database modules, such as [sqlite3](https://docs.python.org/2/library/sqlite3.html) and [psycopg2](http://initd.org/psycopg/docs/).

- `module.connect(…)`
  Connect to a database. The arguments to connect differ from module to module; see the documentation for details. connect returns a Connection object or raises an exception.
  
  For the methods below, note that you don't literally call (for instance) Connection.cursor() in your code. You make a Connection object, save it in a variable (maybe called db) and then call db.cursor().
- `Connection.cursor()`
  Makes a Cursor object from a connection. Cursors are used to send SQL statements to the database and fetch results.
- `Connection.commit()`
  Commits changes made in the current connection. You must call commit before closing the connection if you want changes (such as inserts, updates, or deletes) to be saved. Uncommitted changes will be visible from your currect connection, but not from others.
- `Connection.rollback()`
  Rolls back (undoes) changes made in the current connection. You must roll back if you get an exception if you want to continue using the same connection.
- `Connection.close()`
  Closes the connection. Connections are always implicitly closed when your program exits, but it's a good idea to close them manually especially if your code might run in a loop.
- `Cursor.execute(statement)`
  `Cursor.execute(statement, tuple)`
  Execute an SQL statement on the database. If you want to substitute variables into the SQL statement, use the second form — see the documentation for details.
  
  If your statement doesn't make sense (like if it asks for a column that isn't there), or if it asks the database to do something it can't do (like delete a row of a table that is referenced by other tables' rows) you will get an exception.
- `Cursor.fetchall()`
  Fetch all the results from the current statement.
- `Cursor.fetchone()`
  Fetch just one result. Returns a tuple, or None if there are no results.

## PostgreSQL ("psycopg2" [module](http://initd.org/psycopg/docs/usage.html))

- Install Psycopg2

```cmd
pip install psycopg2
```

- Import psycopg2

```python
import psycopg2
```

- Connect to an existing database
  - The function `connect()` creates a new database session and returns a new connection instance.
  - The class `connection` encapsulates a database session. It allows to:
    - Create new `cursor` instances using the `cursor()` method to execute database commands and queries,
    - Terminate transactions using the methods `commit()` or `rollback()`.

```python
conn = psycopg2.connect("dbname=test user=postgres")
```

- Open a `cursor` to perform database operations:
  - The class `cursor` allows interaction with the database:
    - send commands to the database using methods such as `execute()` and `executemany()`,
    - retrieve data from the database by iteration or using methods such as `fetchone()`, `fetchmany()`, `fetchall()`.

```python
cur = conn.cursor()
```

- Execute a command: this creates a new table

```python
cur.execute("CREATE TABLE test (id serial PRIMARY KEY, num integer, data varchar);")
```

- Pass data to fill a query placeholders and let Psycopg perform the correct conversion ([**no more SQL injections**!](https://bobby-tables.com))

**Warning:**
**_Never, never, NEVER use Python string concatenation (+) or string parameters interpolation (%) to pass variables to a SQL query string. Not even at gunpoint._**

```python
cur.execute("INSERT INTO test (num, data) VALUES (%s, %s)", (100, "abc'def"))
#OR for inserting from variable "content"
cur.execute("INSERT INTO posts VALUES (%s)", (content,))
```

- Query the database and obtain data as Python objects

```python
cur.execute("SELECT * FROM test;")

cur.fetchone()
#(1, 100, "abc'def")
```

- Make the changes to the database persistent

```python
conn.commit()
```

- Close communication with the database

```python
cur.close()
conn.close()
```

- TIPs
  
  - How to use placeholders

    1. For variables:

       ```py
       c.execute("UPDATE posts SET content = (%s) WHERE content LIKE (%s)",
              (friendly, "%" + inappropriate + "%"))
       ```

    2. For Table names

       ```py
       from psycopg2 import sql
       
       c.execute(
       sql.SQL("""
           WITH A AS (SELECT x,y FROM {schema}.{table1}),
                B AS (SELECT x,y FROM {schema}.{table2})
           SELECT count(*) FROM A JOIN B ON A.x = B.x and  A.y = B.y
           """
           ).format(
               table1=sql.Identifier("abc"),
               table2=sql.Identifier("bcd"),
               schema=sql.Identifier("public")
               )
       )
       ```

## [Bleach](https://bleach.readthedocs.io/en/latest/)

- Bleach is an allowed-list-based HTML sanitizing library that escapes or strips markup and attributes.
- Bleach is intended for sanitizing text from untrusted sources. If you find yourself jumping through hoops to allow your site administrators to do lots of things, you’re probably outside the use cases. Either trust those users, or don’t.
- Installing Bleach

```cmd
pip install bleach
```

- Basic use

```py
import bleach

bleach.clean('an <script>evil()</script> example')
# u'an <script>evil()</script> example'

bleach.linkify('an http://example.com url')
# u'an <a href="http://example.com" rel="nofollow">http://example.com</a> url'
```

## CRUD operations with SQLAlchemy

### First: database setup

Create a python script that creates/connects to the database

1. Import all modules needed

   1. `sys`: provides a number of functions and variables that can be used to manipulate different parts in runtime environment.
   2. `from sqlalchemy import Column, ForeignKey, Integer, String`: Can be used in mapping
   3. `from sqlalchemy.ext.declarative import declarative_base`: Will be used in configuration and class code
   4. `from sqlalchemy.orm import relationship`: in order to create foreign key relationship
   5. `from sqlalchemy import create_engine`: will be used in configuration code

   ```py
   import sys
   from sqlalchemy import Column, ForeignKey, Integer, String
   from sqlalchemy.ext.declarative import declarative_base
   from sqlalchemy.orm import relationship
   from sqlalchemy import create_engine
   ```

2. Create instance of declarative base

   To create classes inherited from this class in order to make SQLAlchemy know that these classes are special and corresponds to tables in our DB

   ```py
   Base = declarative_base()
   ```

3. Classes: create an inherited class for each table
4. Mapper: Define the column names and attributes.

   ```py
   class Restaurant(Base):
   # Table respresentation with syntax: __tablename__ = 'some_table'
   __tablename__ = 'restaurant'
   #! Mapper
   name = Column(String(80), nullable=False)
   id = Column(Integer, primary_key=True)
   ```

5. Create/Connect the database and add tables and columns

   ```py
   # An instance of the engine that points to the type of the DB
   engine = create_engine('sqlite:///restaurantmenu.db')
   # This goes into the DB and will add the classes and  tables into the DB
   Base.metadata.create_all(engine)
   ```

### Second: CRUD operation

Create a file for CRUD operation

1. Import modules

   ```py
   from sqlalchemy import create_engine
   from sqlalchemy.orm import sessionmaker
   from database_setup import Base, Restaurant, MenuItem
   ```

2. Let the program now which database engine to communicate with

   ```py
   engine = create_engine('sqlite:///restaurantmenu.db')
   ```

3. Bind the engine to the metadata of the `Base class` so that the `declarative` can be accessed through a `DBSession` instance

   ```py
   Base.metadata.bind = engine
   ```

4. Create a `DBSession()`

   A `DBSession()` instance establishes all conversations with the database and represents a "staging zone" for all the objects loaded into the database session object. Any change made against the objects in the session won't be persisted into the database until you call session.commit (). If you're not happy about the changes, you can revert all of them back to the last commit by calling session.rollback()

   ```py
   DBSession = sessionmaker(bind=engine)
   ```

5. SQLAlchemy needs a session to execute any of CRUD operations.

   The session is staging zone and all data will not be persisted in the DB until session.commit()

   ```py
   session = DBSession()
   ```

6. Do CRUD operations

   1. CREATE: Add an entry

      ```py
      # 1. Create an instance
      myFirstRestaurant = Restaurant(name="Pizza Palace")
      # 2. Add it to the session
      session.add(myFirstRestaurant)
      # 3. Commit to apply the changes
      session.commit()
      ```

   2. [READ](http://docs.sqlalchemy.org/en/rel_0_9/orm/query.html): Find some information of our database using SQLAlchemy

      ```py
      # Use 'session.query' to fetch the data in the session
      firstRestaurant = session.query(Restaurant).first()
      allRestaurants = session.query(Restaurant).all()
      # You can use for loop to get the values
      for restaurant in allRestaurants:
          print(restaurant.name)
      ```

   3. UPDATE: Change the values of some records

      ```py
      # 1. Find the entry
      #todo use filter_by to query by specific value in column
      veggieBurgers = session.query(MenuItem).filter_by(name =        'Veggie Burger')
      #todo use for loop to print items in the list
      for veggieBurger in veggieBurgers:
          print(veggieBurger.id)
          print(veggieBurger.price)
          print(veggieBurger.restaurant.name)
          print("\n")
      #todo OR you can filter by specific id and return one       object
      urbanVeggieBurger = session.query(MenuItem).filter_by       (id=1).one()
      print(urbanVeggieBurger.price)
      # 2. Reset the values
      urbanVeggieBurger.price = "$2.50"
      # 3. Add to session
      session.add(urbanVeggieBurger)
      # 4. Session commit
      session.commit()
      ```

   4. DELETE: remove an entry from the DB

      ```py
      # 1. Find the entry
      spinach = session.query(MenuItem).filter_by(name='Spinach       Ice Cream').one()
      print(spinach.restaurant.name)
      # 2. Delete this entry
      session.delete(spinach)
      # 3. commit this action
      session.commit()
      ```

## Web Frameworks

### Flask

1. Routing:

   - Create an instance of flask class.
   - The name of the running application as an argument, anytime this application is run, a special variable called `__name__` gets defined.

     ```py
     from flask import Flask, render_template, request, redirect, url_for, flash, jsonify
     
     app = Flask(__name__)
     ```

   - This flask decorator wraps our function inside `app.route` function, so either of the below routes were sent from the browser, the `HelloWorld()` gets executed. In a brief, `app.route` will execute the function below it when the browser visit it.

     ```py
     @app.route('/')
     @app.route('/restaurants')
     def showRestaurants():
         restaurants = CRUD.read_restaurants()
         return render_template('restaurants.html', restaurants=restaurants)
     ```

   - You can take a variable from the GET request and map to the decorater function

     ```py
     @app.route('/restaurants/<int:restaurant_id>/menu/<int:menu_id>/JSON')
     def menuItemJSON(restaurant_id, menu_id):
        menuItem = session.query(MenuItem).filter_by(id=menu_id).one()
        return jsonify(MenuItem=menuItem.serialize)
     ```

2. Templates

   - Flask has a template engine to store the HTML code which is used to render templates. The HTML must be in a folder named templates inside the project folder.
   - It uses a method called `render_template("Template_name.html",Template_Variable=Keyword)` that helps in HTML Escaping.
   - HTML Escaping terminology is when HTML files retrieve data from python code or database.

     ```py
     @app.route('/')
     @app.route('/restaurants')
     def showRestaurants():
         restaurants = CRUD.read_restaurants()
         return render_template('restaurants.html', restaurants=restaurants)
     ```

     ```html
     </div>
         {% for i in restaurants %}
         <div>
             <a href="{{url_for('RestaurantMenu', restaurant_id = i.id) }}">{{i.name}}</a>
         </div>
         {% endfor %}
     </div>
     ```

3. URL Building with `url_for()`:

   - It helps in create and execute URLs that you need to create links for other pages.
   - `url_for('FunctionName',URL_Function=Value)` is one of many Flask helper functions.

     ```html
     <a href="{{url_for('RestaurantMenu', restaurant_id = i.id) }}"></a>
     ```

4. Request and Redirects:

   - Flask deals in default with `GET` requests only. `methods` argument must state the methods in the request.
   - To retreive data from `POST`Request, request should be used as `request.form['name']`
   - To redirect to a URL, `redirect()` can be used and also can be used with `url_for()`.

     ```py
     # todo: Create New Restaurant
     @app.route('/restaurants/new', methods=['GET', 'POST'])
     def newRestaurant():
        if request.method == 'POST':
            CRUD.create_restaurant(request.form['name'])
            return redirect(url_for('showRestaurants'))
        else:
            return render_template('newrestaurant.html')
     ```

5. Flash messages:

   - It prompts a message to the user after a certain action has taken place and disappears the second time the page is requested.

     ```py
     from flask import flash
     # todo: Create new menu item
     @app.route('/restaurants/<int:restaurant_id>/new', methods=['GET', 'POST'])
     def newMenuItem(restaurant_id):
         if request.method == 'POST':
             CRUD.create_menuitem(request.form['name'], restaurant_id)
             flash("new menu item created!")
             return redirect(url_for('showMenu', restaurant_id=restaurant_id))
         else:
             return render_template('newmenuitem.html', restaurant_id=restaurant_id)
     ```

     ```html
     <div class="flash">
       {% with messages = get_flashed_messages() %} {% if messages %}
     
       <ul>
         {% for message in messages %}
         <li><strong> {{ message }} </strong></li>
         {% endfor %}
       </ul>
       {% endif %} {% endwith %}
     </div>
     ```

6. Secret Key:

   - Flask uses this to create sessions for users, this should be a very secure password.

     ```py
     if __name__ == '__main__':
     # Create a session for the user
     app.secret_key = 'super_secret_key'
     app.debug = True
     app.run(host='0.0.0.0', port=5000)
     ```

7. Static Files: JS, media and CSS files

   - Flask will look for CSS, JS and mediafiles if they are in folder named 'static'
   - Access it html file like below

   ```html
   <link rel=stylesheet type=text/css href="{{ url_for('static',
   filename='styles.css') }}">
   ```

8. JSONify

   - It can converts dictionaries into JSON objects that can be then sent to the client.
   - The JSONify function in flask returns reponse object that already has the appropriate content type Header for use with JSON responses.

     ```py
     import jsonify
     
     @app.route('/restaurants/<int:restaurant_id>/menu/<int:menu_id>/JSON')
     def menuItemJSON(restaurant_id, menu_id):
        menuItem = CRUD.read_menuitem(menu_id)
        return jsonify(MenuItem=menuItem.serialize)
     ```

#### Third Party Auth

1. [Google login with flash](https://realpython.com/flask-google-login/#why-use-google-login-for-your-users)

### [Streamlit](https://www.streamlit.io/)

- Streamlit’s open-source app framework is the easiest way for data scientists and machine learning engineers to create beautiful, performant apps in only a few hours!  All in pure Python. All for free.
- It supports live coding

#### Getting Started

- Install it with `pip install streamlit`
- Import it in the project script `import streamlit as st`
- You can run the server by typing in the terminal `streamlit run app.py`

#### Syntax

- Write a title for the web page by `st.title("")`
- Write a markdown text by `st.markdown("")`

## Machine Learning

### StatsModels

1. Linear Regression:

   1. First you need to add an intercept column to the dataset as statsmodels doesn't add it at its own.
   2. Then provide y and x variables to [OLS model](http://www.statsmodels.org/dev/regression.html)
   3. Fit the model
   4. Interpret the linear Model results with summary(). It shows the intercept and the slope, p-values, R-squared values.

   ```py
   import statsmodels.api as sm
   
   # Add intercept column to the dataset
   df['intercept'] = 1
   # Here providing OLS method for x and y variables.
   # OLS stands for Ordinary Least Squares. It used for Linear Regression
   # sm.OLS(y, list(x-variables))
   lm = sm.OLS(df['price'],df[['intercept','area']])
   # Logit is used for Logistc Regression
   lm = sm.Logit(df['price'],df[['intercept','area']])
   # Fit the model with fit()
   results = lm.fit()
   # Show results summary
   results.summary()
   ```

### Scikit learn

1. Installation

   ```py
   import sklearn
   ```

2. Preprocessing

   1. Imputation:

      - `sklearn.preprocessing.imputer`

        ```py
        from sklearn.preprocessing import Imputer
        import numpy as np
        
        arr = np.array([[5,3,2,2],[3,None,1,9],[5,2,7,None]])
        
        imputer = Imputer(strategy = 'mean')
        imp = imputer.fit(arr)
        imputer.transform(arr)
        
        # array([[5,3,2,2],
        #        [3,2.5,1,9],
        #        [5,2,7,5.5]])
        ```

      - `sklearn.impute.MICEImpute` (v0.20)

   2. Encoding:
      1. [Label Encoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html?highlight=labelencoder#sklearn.preprocessing.LabelEncoder)
         - `sklearn.preprocessing.LabelEncoder`
         - Encode target labels with value between 0 and n_classes-1.

            ```py
            from sklearn.preprocessing import LabelEncoder
            
            loan_enc = LabelEncoder()
            y = group_enc.fit_transform(df['loan_approved'])
            ```

      2. [One Hot Encoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html?highlight=onehotencoder#sklearn.preprocessing.OneHotEncoder)
         - `sklearn.preprocessing.OneHotEncoder`
         - Encode categorical features as a one-hot numeric array

            ```py
            from sklearn.preprocessing import OneHotEncoder
            
            df = pd.DataFrame({"Fruits":["Apple","Banana","Banana","Mango","Banana"]})
            num_type = group_enc.fit_transform(df['Fruits'])
            type_enc = OneHotEncoder()
            type_enc.fit(num_type.reshape(-1,1))
            ```

      3. [Count Vectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer)
         - `sklearn.feature_extraction.text.CountVectorizer`
         - It tokenizes the string (separates the string into individual words) and gives an integer ID to each token.
         - It counts the occurrence of each of those tokens.

            ```py
            from sklearn.feature_extraction.text import CountVectorizer
            
            count_vectorizer = CountVectorizer()
            x_train_count = count_vectorizer.fit_transform(data.text)
            
            count_vectorizer.vocabulary_
            ```

           - The CountVectorizer method automatically converts all tokenized words to their lower case form so that it does not treat words like 'He' and 'he' differently. It does this using the `lowercase` parameter which is by default set to `True`.

           - It also ignores all punctuation so that words followed by a punctuation mark (for example: 'hello!') are not treated differently than the same words not prefixed or suffixed by a punctuation mark (for example: 'hello'). It does this using the `token_pattern` parameter which has a default regular expression which selects tokens of 2 or more alphanumeric characters.

           - The third parameter to take note of is the `stop_words` parameter. Stop words refer to the most commonly used words in a language. They include words like 'am', 'an', 'and', 'the', etc. By setting this parameter value to `english`, CountVectorizer will automatically ignore all words (from our input text) that are found in the built in list of English stop words in scikit-learn. This is extremely helpful as stop words can skew our calculations when we are trying to find certain key words that are indicative of spam.

      4. [Tfidf Vectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html?highlight=tfidfvectorizer#sklearn.feature_extraction.text.TfidfVectorizer)
         - `sklearn.feature_extraction.text.TfidfVectorizer`
         - It converts a collection of raw documents to a matrix of TF-IDF features. Equivalent to `:class:CountVectorizer` followed by `:class:TfidfTransformer`.

3. Splitting the data

   ```py
   from sklearn.model_selection import train_test_split
   
   # random_state is used to randomize the data
   
   X_train, X_test, y_train, y_test =
   train_test_split(X, y,test_size=0.2, random_state=0)
   ```

4. Cross validation

   ```py
   from sklearn.model_selection import cross_val_score
   
   # model: the model you want to evaluate
   # X, y: dataset
   # cv: the corresponding ground truth target labels or values. By default, cross_val_score does threefold cross-validation.
   cv_scores = cross_val_score(model, X, y, cv = 3)
   print('Cross-validation scores (3-fold):', cv_scores)
   print('Mean cross-validation score (3-fold): {:.3f}'.format(np.mean(cv_scores)))
   ```

5. Models

   1. Supervised:
      1. Regression:
         1. Linear Regression `sklearn.linear_model .LinearRegression`
         2. Lasso Regression `sklearn.linear_model .Lasso`
         3. Ridge Regression `sklearn.linear_model .Ridge`
         4. Stochastic Gradient Descent Regression `sklearn.linear_model .SGDRegressor`
      2. Classification:
         1. Logistic Regression `sklearn.linear_model .LogisticRegression`
         2. Naive Bayes `sklearn.naive_bayes.GaussianNB`
         3. Support Vector Machine `sklearn.svm.SVC`
         4. K-Nearest Neighbor `sklearn.neighbors.KNeighborsClassifier`
         5. Decision Tree `sklearn.tree.DecisionTreeClassifier`
         6. Random Forest `sklearn.ensemble.RandomForestClassifier`
   2. Unsupervised:
      1. Clustering
         1. K-Means `sklearn.cluster.KMeans`

   ```py
   # Create Estimator
   model = model_fn()
   # Fit the training data
   model.fit(x_train, y_train)
   # Pedict the test data
   y_pred = model.predict(x_test)
   ```

6. Model Evaluation

   1. Regression:

      - R2 Score

        ```py
        # R2 Score
        from sklearn.metrics import r2_score
        score = r2_score(y_test, y_pred)
        # or using the built-in function
        model.score(x_test, y_test)
        ```

   2. Classification:

      - Confusion Matrix `sklearn.metrics.confusion_matrix`
      - Accuracy `sklearn.metrics.accuracy_score`
      - Precision `sklearn.metrics.precision_score`
      - Recall `sklearn.metrics.recall_score`
   3. Clustering

      - Silhouette score `sklearn.metrics.silhouette_score`
      - Homogeneity score `sklearn.metrics.homogeneity_score`
      - Completeness Score `sklearn.metrics.completeness_score`
      - V measure `sklearn.metrics.v_measure_score`
      - Adjusted Random Score `sklearn.metrics.adjusted_rand_score`
      - Adjusted Mutual Information Score `sklearn.metrics.adjusted_mutual_info_score`
7. Feature Engineering

   - Mean/Variance Standardization

     ```py
     from sklearn.preprocessing import StandardScalar
     
     scale = StandardScalar()
     arr = np.array([[5,3,2,2],[2,3,1,9],[5,2,7,6]],dtype=float)
     print(scale.fit_transform(arr))
     print(scale.scale_)
     ```

   - MinMax Scaler

     ```py
     from sklearn.preprocessing import MinMaxScaler
     scaler = MinMaxScaler()
     scaler.fit(x_train)   # compute the min and max feature   values for each feature in this training dataset.
     X_trained_scaled = scaler.transform(X_train)
     X_test_scaled = scaler.transform(X_test)
     clf = Ridge().fit(X_train_scaled, y_train)
     r2_score = clf.score(X_test_scaled, y_test)
     # or more efficiently fit and transform in one step
     X_train_scaled = scaler.fit_transform(X_train)
     ```

   - Polynomial features

     ```py
     from sklearn.linear_model import LinearRegression
      from sklearn.linear_model import Ridge
      from sklearn.preprocessing import PolynomialFeatures
     
      X_train, X_test, y_train, y_test =  train_test_split(x, y, random_state = 0)
     
      linreg = LinearRegression().fit(X_train, y_train)
     
      poly = PolynomialFeatures(degree=2)
      X_poly = poly.fit_transform(x)
     
      X_train, X_test, y_train, y_test =  train_test_split(X_poly,y, random_state = 0)
     
      linreg = LinearRegression().fit(X_train, y_train)
     ```

   - Feature Selection

     - Filtering methods

       ```py
       # Select the best K features
       from sklearn.feature_selection import SelectKBest
       
       # Statistical technique to create a univariate linear regression that calculates the correlation between each regressor and target
       from sklearn.feature_selection import f_regression
       
       select_univariate = SelectKBest(f_regression, k=5).fit(features, target)
       
       # Get the mask for the best K=5 features
       feature_mask = select_univariate.get_support()
       # Get the best 5 features
       features.columns[feature_mask]
       # Get the cscore of each feature (Higher is better)
       select_univariate.scores_
       ```

     - Wrapping methods

       1. Recursive Feature Elimnation: Selects features by recursively considering smaller subsets of features by pruning the least important feature at each step.

          ```py
          from sklearn.linear_model import LinearRegression
          # Recursive Feature Elimnation
          from sklearn.feature_selection import RFE
          
          linear_regression = LinearRegression()
          
          rfe = RFE(estimator = linear_regression, # The estimator that will be used to train the model on different set of features
          n_features_to_select = 5, # Select the most 5 relevant features
          step = 1)
          
          # Fit the data
          rfe.fit(features,target)
          
          # Get the 5 most relevant features
          rfe_features = features.columns[rfe.support_]
          
          # View rankings of all the features. The selected features are assigned a rank of 1
          pd.DataFrame({'FeatureName': features.columns, 
            'Rank': rfe.ranking_}).sort_values(by='Rank')
          ```

     - Embedded methods

       1. Regularization techniques

          ```py
          from sklearn.linear_model import  Lasso
          
          lasso = Lasso(alpha=1.0) # strength of Regularization, 1 is the strogest effect
          
          lasso.fit(features, target)
          
          # lasso.coef_ shows the regularization coefficient of each feature
          
          lasso_coef = pd.DataFrame({'Feature': features.columns, 
                         'LassoCoef': lasso.coef_}).sort_values(by = 'LassoCoef',
                                                                ascending =False)
          
          lasso_coef['LassoCoef'] = abs(lasso_coef['LassoCoef'])
          
          lasso_coef.sort_values(by='LassoCoef', ascending=False)
          ```

8. Hyperparameter tuning:

- Grid Search
  
  ```py
  from sklean.datasets import make_classification
  from sklearn import svm
  from sklearn.model_selection import GridSearchCV
  
  plt.figure(4)
  X2, Y2 = make_classification(n_features = 5, n_redundant = 0, n_informative = 2)
  
  parameters = {'kernel':('linear','rbf'), 'C':[1,5,10,15], 'degree':[2,3,4,5]}
  svc = svm.SVC()
  clf = GridSearchCV(svc, parameters)
  clf.fit(X2, Y2)
  
  clf.best_params_
  
  # {'C': 5, 'degree':2, 'kernel':'rbf'}
  ```

### YellowBrick

[Yellowbrick](https://www.scikit-yb.org/en/latest/) is suite of visual analysis and diagnostic tools for machine learning.

1. Installation

   ```py
   pip install yellowbrick
   ```

2. Feature Correlation

   - Pearson Correlation

     ```py
     from yellowbrick.target import FeatureCorrelation
     
     visualizer = FeatureCorrelation(labels = feature_names, method='pearson')
     
     visualizer.fit(features, target)
     
     visualizer.poof()
     ```

   - Mutual Information: Mutual information between features and the dependent variable.

     ```py
     visualizer = FeatureCorrelation(method='mutual_info-regression',
                                   feature_names=feature_names, sort=True)
     
     visualizer.fit(features, target)
     visualizer.poof()
     ```

### MLxtend

[Mlxtend](https://github.com/rasbt/mlxtend) (machine learning extensions) is a Python library of useful tools for the day-to-day data science tasks.

1. Installation

   ```cmd
   pip install mlxtend
   ```

2. Feature Engineering

   - Feature Selection
     - Wrapping methods

       1. Backward feature selection: In backward elimination, we start with all the features and removes the least significant feature at each iteration which improves the performance of the model. We repeat this until no improvement is observed on removal of features.
       2. Forward feature selection: Forward selection is an iterative method in which we start with having no feature in the model. In each iteration, we keep adding the feature which best improves our model till an addition of a new variable does not improve the performance of the model.

          ```py
          from mlxtend.feature_selection import SequentialFeatureSelector
          from sklearn.linear_model import LinearRegression
          
          feature_selector = SequentialFeatureSelector(LinearRegression(), # Estimator
                                           k_features=5, # Best relevant features to chosen
                                           forward=False, # Backward or Forward
                                           scoring='neg_mean_squared_error', # Higher value indicates a better model.
                                           cv=4)
          
          feature_filtered = feature_selector.fit(features, target)
          
          # The name of the features
          backward_features = list(feature_filtered.k_feature_names_)
          ```

### Apache MXNet

1. Installation:
   1. MXNet:

      1. Basic: a version of MXNet that will use the CPU for computation.

         ```py
         pip install mxnet
         ```

      2. CPU Optimized: for an Intel CPU, a version of MXNet that uses Intel's Math kernel Library. All of the CPU cores will be used with this version for potential boost and performance.

         1. Install Intel MKL for windows [here](https://software.intel.com/content/www/us/en/develop/tools/math-kernel-library/choose-download/windows.html)
         2. Install MXNet MKL version

            ```py
            pip install mxnet-mkl
            ```

      3. GPU Optimized: If you have an Nvidia GPU, you can use the CUDA optimized version of MXNet. Make sure that CUDA is installed beforehand and find its version to make sure that you get the corresponding version of MXNet.

         1. Check if the [GPU supports CUDA](https://developer.nvidia.com/cuda-gpus)
         2. Check if CUDA installed `nvcc --version`. If yes, jump to step 5
         3. Install the [CUDA toolkit](https://developer.nvidia.com/cuda-downloads?)
         4. Install cuDNN on Windows 10 which is compatible with CUDA version.

            1. Download [cuDNN](https://developer.nvidia.com/cudnn)
            2. Extract the downloaded files
            3. Copy the 3 folders and the text file to the location where NVIDIA GPU Computing Toolkit is located. ex: `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2`
            4. Add path on environmental variables for

               - `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\bin`
               - `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\libnvvp`
            5. Install MXNet [related version](https://mxnet.apache.org/versions/1.7/get_started?platform=windows&language=python&processor=gpu&environ=pip&) library

               ```cmd
               pip install mxnet-cu102
               
               # OR
               
               pip install mxnet-cu102 -f https://dist.mxnet.io/python
               ```

            - Reference:
              - [Medium Article](https://medium.com/analytics-vidhya/cuda-toolkit-on-windows-10-20244437e036)
              - [Python 3 Microsoft Visual C++ 14.0 is required](https://www.scivision.dev/python-windows-visual-c-14-required/)
      4. Combine both CPU and GPU optimized versions

         ```cmd
         pip install mxnet-cu101mkl
         
         # OR
         
         pip install mxnet-cu102mkl==1.6.0 -f https://dist.mxnet.io/python
         ```

   2. GluonCV:

      1. Stable

         ```py
         pip install gluoncv
         ```

      2. Nightly

         ```py
         pip install gluoncv --pre
         ```

### OpenCV

1. Installation:
   1. Packages for standard desktop environments (Windows, macOS, almost any GNU/Linux distribution):
      1. Main modules package: `pip install opencv-python`
      2. Full package (contains both main modules and contrib/extra modules): `pip install opencv-contrib-python` (check contrib/extra modules listing from [OpenCV documentation](https://docs.opencv.org/master/))
   2. Packages for server (headless) environments (such as Docker, cloud environments etc.), no GUI library dependencies
      1. Headless main modules package: `pip install opencv-python-headless`
      2. Headless full package (contains both main modules and contrib/extra modules): `pip install opencv-contrib-python-headless` (check contrib/extra modules listing from [OpenCV documentation](https://docs.opencv.org/master/))
   3. GPU Optimized: If you have an Nvidia GPU, you can use the CUDA optimized version of OpenCV. Make sure that CUDA is installed beforehand and find its version to make sure that you get the corresponding version of OpenCV.
      1. Check if the [GPU supports CUDA](https://developer.nvidia.com/cuda-gpus)
      2. Install Visual Studio with C Desktop Development
      3. [Download](https://cmake.org/download/) and Install CMake
      4. Check if CUDA installed `nvcc --version`. If yes, jump to step 5
      5. Install the [CUDA toolkit](https://developer.nvidia.com/cuda-downloads?)
      6. Install cuDNN on Windows 10 which is compatible with CUDA version.
         1. Download [cuDNN](https://developer.nvidia.com/cudnn)
         2. Extract the downloaded files
         3. Copy the 3 folders and the text file to the location where NVIDIA GPU Computing Toolkit is located. ex: `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.x`
         4. Add path on environmental variables for
            - `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\bin`
            - `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\libnvvp`
      7. Download [OpenCV](https://opencv.org/releases/) Sources and [Contrib](https://github.com/opencv/opencv_contrib/releases) files. But the two folders in the same folder and extract one separately.
      8. Build OpenCV
         1. Open CMake GUI
         2. Choose OpenCV source folder
         3. Choose where the BUILD will be placed
         4. Unmark GROUPED check
         5. Configure to WIN x64
         6. For Virtual Environment, add its path in CMake > Environment > Path
         7. Build
         8. Check the logs in CMake, and look for "OpenCV modules:". If "python3" exists beside "Unavailable", then numpy library needs to be updated.
            1. Click on File and Delete Cache
            2. Update numpy `pip install --upgrade numpy`
         9. Mark below Libraries:
            1. `WITH_CUDA`
            2. `OPENCV_DNN_CUDA`
            3. `ENABLE_FAST_MATH`
            4. `BUILD_opencv_world`
            5. `BUILD_opencv_python3`
            6. `OPENCV_EXTRA_MODULES_PATH` :opencv_contrib-4.5.2\modules
         10. Click on 'Configure' Button.
             1. After the configurations are finished, check the logs for 'CUDA' and 'cuDNN' are detected.
         11. Search for below libraries:
             1. Enable `CUDA_FAST_MATH`
             2. Search for `CUDA_ARCH_BIN`, and edit the value to include only the [CUDA version](https://en.wikipedia.org/wiki/CUDA) that supports the GPU. For example, Nvidia RTX 3060 Ti supports CUDA version 8.6
             3. Change Installation folder if needed `CMAKE_INSTALL_PREFIX`
             4. Remove Debug from `CMAKE_CONFIGURATION_TYPES`
         12. Click on `Configure` Button.
         13. Click on `Generate` Button.
         14. Once finished, close CMake
         15. Open CMD, and run command `cmake --build "C:\OpenCV_Build\build" --target INSTALL --config Release`
2. Import the package: `import cv2`

- Reference
  - [pypi](https://pypi.org/project/opencv-python/)
  - [YouTube video](https://www.youtube.com/watch?v=YsmhKar8oOc)
  - [cv-tricks](https://cv-tricks.com/how-to/installation-of-opencv-4-1-0-in-windows-10-from-source/)

## Conventions

1. [Google Style Guide for Python](https://google.github.io/styleguide/pyguide.html)
2. [pep8](http://pep8online.com/)

## Speed Up Performance

Performance may refer to many different factors in a solution (e.g. execution time, CPU usage, memory usage, etc.)

### Speed up execution time

The improvement in the execution time of a new solution can be computed as simply as making a division. That is, we’ll be dividing the execution time of the old (or non-optimized) solution by the new (or optimized) solution: Told / Tnew. This metric is commonly referred to as speedup.

#### Compare time

```py
import time

def compute_speedup(slow_func, opt_func, func_name, tp=None):
  x = range(int(1e5))
  if tp: x = list(map(tp, x))  slow_start = time.time()
  slow_func(x)
  slow_end = time.time()
  slow_time = slow_end - slow_start  opt_start = time.time()
  opt_func(x)
  opt_end = time.time()
  opt_time = opt_end - opt_start  speedup = slow_time/opt_time
  print('{} speedup: {}'.format(func_name, speedup))
```

In order to obtain significant results, we’ll be using a relatively large array (100.000 elements), and pass it to both functions as an argument. We’ll then compute the execution time using the time module and finally deliver the obtained speedup.

Note that we are also passing an optional argument that would allow us to change the type of our list elements.

#### Speed up techniques

1. Avoid concatenating strings with the + operator

   Python’s strings were created to be immutable, and therefore cannot be modified. That means that every time we use the + operator, Python is actually creating a new string based on both substrings and returning the new string.

   ```py
   def slow_join(x):
      s = ''
      for n in x:
         s += n
   ```

   a cheaper solution using join(), such as in the following example:

   ```py
   def opt_join(x):
      s = ''.join(x)
   ```

   This solution takes the array of substrings and joins them with the empty string separator. Let’s check our performance improvement:

   ```py
   compute_speedup(slow_join, opt_join, 'join', tp=str)
   ```

   I’m getting a speedup factor of 7,25!
2. Use the map function

   ```py
   def slow_map(x):
      l = (str(n) for n in x)
      for n in l:
         pass
   ```

   ```py
   def opt_map(x):
      l = map(str, x)
      for n in l:
         pass
   ```

   ```py
   compute_speedup(slow_map, opt_map, 'map')
   ```

   I’m obtaining a speedup of 1,55.
3. Avoid reevaluating functions

   ```py
   y = []
   for n in x:
      y.append(n)
      y.append(n**2)
      y.append(n**3)
   
   # OR
   
   def slow_loop(x):
   y = []
   for n in x:
      y.append(n)
   ```

   ```py
   def opt_loop(x):
   y = []
   append = y.append
   for n in x:
      append(n)
   ```

   ```py
   compute_speedup(slow_loop, opt_loop, 'loop')
   ```

   I’m obtaining a speedup of 2,07!

### Speed up references

- [Medium Article](https://towardsdatascience.com/3-techniques-to-make-your-python-code-faster-193ffab5eb36)

## Tips and Tricks

### Shared References and In-Place Changes

- There are objects and operations that perform in-place object changes—Python’s mutable types, including `lists`, `dictionaries`, and `sets`. For instance, an assignment to an offset in a `list` actually changes the `list` object itself in place, rather than generating a brand-new `list` object.

```py
L1 = [2, 3, 4]
L2 = L1
L1[0] = 1
L2[0]

>> 1
```

### Creating a Slide Deck with Jupyter

- Jupyter notebooks include a tool, [nbconvert](https://nbconvert.readthedocs.io/en/latest/), that can export notebooks in an HTML slides format.
  - To start, you need to categorize the type of slide element that each cell will correspond with. From the menu bar, select **View > Cell Toolbar > Slideshow**. You'll see a drop down appear in the upper right hand corner of each cell, from which you can assign slide element types.
  - Set Slide Types:

    - For cells that you want readers to see, you'll choose the *Slide*, *Sub-Slide*, or *Fragment* types.
    - *Slides* will form the main flow of the presentation, while *sub-slides* are children of slides in the main flow. *Fragments* are attached to preceding *slides* or *sub-slides*, and allow for gradual reveals of information on the same slide.
      - Example presentation found on the [reveal.js](https://revealjs.com/) homepage (the library that is behind the nbconvert slide functionality).
    - Cells that you don't want users to see should be in the Skip or Notes types. Skip-type cells will never show up in a slide flow, while Notes cells can only be seen by the presenter in a speaker notes window.
  - In addition to setting slide types, make sure that all of your code cells have been run and produce the output that you want to show. `nbconvert` will only export elements of the notebook as-is, and won't run the notebook cells as is. It is recommended that you use the Kernel > Restart & Run All menu option to do a clean run-through of all of your cells as a final preparatory action.
  - Once your notebook has been prepared, save it and shut down your notebook server.

    - On the command line, you can render the notebook as slides using the following expression as a base.
    - `jupyter nbconvert presentation.ipynb --to slides`
  - By default, code cell inputs and outputs are both rendered in the slides. To hide the code in your presentation, you can specify a template file using the --template option. The template file available at [this link](https://s3.amazonaws.com/video.udacity-data.com/topher/2018/March/5abe98f3_output-toggle/output-toggle.tpl), will hide code cells from nbconvert.
  - In order to serve the slides, you would need to install a local copy of reveal.js ([Installation documentation](https://github.com/hakimel/reveal.js#installation)), make sure that your HTML slides point to the library correctly (using the --reveal-prefix option), and then start a local http server (e.g., via python -m http.server).

    - Alternatively, you can add the --post serve option to your expression to make use of a public, online version of reveal.js, start up a server, and immediately open a tab in your web browser with the slide deck ready to navigate.
  - If you're at home with HTML, css, and web engine templating, then you have a lot of potential room for customizing your slide deck work. Otherwise, you can just use an expression like the following to get a basic slide deck up and running.

    ```cmd
    jupyter nbconvert presentation.ipynb --to slides --template output-toggle.tpl
    --post serve
    ```

## Handful resources

1. This [article](http://simeonfranklin.com/blog/2012/jul/1/python-decorators-in-12-steps/) discuss:
   1. Decorators
   2. Functions
   3. Scope
   4. Variable resolution rules
   5. Variable lifetime
   6. Function arguments and parameters
   7. Nested functions
   8. Closures
   9. \*args and \*\*kwargs
2. [Virtual Environments](https://realpython.com/python-virtual-environments-a-primer/#why-the-need-for-virtual-environments)
   1. Using Virtual Env:
      1. Install Virtual Env `pip install virtualenv`
      2. Create a new virtual environment in the directory `python3 -m venv {VirEnv Name}`
      3. Use the environment `source {VirEnv Name}/Scripts/activate`
      4. Deactivate Environment `deactivate`
   2. Using Virtual Wrapper (recommended):
      1. Install Virtual Env `pip install virtualenv`
      2. Install Virtual Wrapper:
         1. For Bash (recommended):
            1. Install: `pip install virtualenvwrapper`
            2. Add virtualenvwrapper.sh path in the Bash profile `source {path/to/Python}/Scripts/virtualenvwrapper.sh`
         2. For Windows PowerShell: `pip install virtualenvwrapper-win`
      3. Reload the startup
      4. Create a new environment `mkvirtualenv {VirEnv Name}`
      5. Deactivate current environment `deactivate`
      6. Use an enviroment `workon {VirEnv Name}`
      7. Remove an environment `rmvirtualenv {VirEnv Name}`
      8. List all available environments `workon`
      9. Resources:
         1. [Medium Article](https://medium.com/the-andela-way/configuring-python-environment-with-virtualenvwrapper-8745c2895745)
         2. [Virtual Wrapper Docs](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)
3. [Jupyter Notebook](http://jupyter.org)
   1. How to install Jupyter without anaconda
      1. `python -m pip install --upgrade pip`
      2. `python -m pip install notebook`
      3. Restart VS Code
      4. Pick the Python environment you did the pip install in
   2. To download all the files/folders in Jupyter notebook.
      1. Run this line in a jupyter cell `!tar czf myfiles.tar.gz *`
      2. Click on Juypter Logo at the most top left corner.
      3. Scroll to find your just created file "myfiles.tar.gz" and check it.
      4. Scroll to the top of the page and click on Download
