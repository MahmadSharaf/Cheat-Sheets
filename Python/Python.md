# Python Cheat sheet

- [Python Cheat sheet](#python-cheat-sheet)
  - [Dealing with files and folders](#dealing-with-files-and-folders)
  - [Strings](#strings)
    - [String with variables inside](#string-with-variables-inside)
    - [String formatting](#string-formatting)
  - [Lists](#lists)
  - [While loop](#while-loop)
  - [Tricks](#tricks)
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
  - [Data Structures](#data-structures)
    - [NumPy](#numpy)
    - [Pandas](#pandas)
      - [Pandas methods and functions](#pandas-methods-and-functions)
    - [Matplotlib](#matplotlib)
    - [Resources](#resources)
  - [Conventions](#conventions)
  - [Handful resources](#handful-resources)

## Dealing with files and folders

```py
import os

# Get the current working directory
os.getcwd()

# Change the working directory
os.chdir(file_path)

# Rename file names
os.rename(current_filename,new_filename)
```

```py
# Open a file, read it and close it
f = open("file_path", w+)
# "w" letter indicates write and will create a file if it does not exist in library
# Plus sign indicates both read and write.
# The available option beside "w" are, "r" for read, and "a" for append
f.write("string")
f.close()
```

## Strings

```python
# strings are immutable (they cannot be changed).

# Join: joins two strings together
result = '1234'.join("567")
===
result = '1234' + '567'
# result = "1234567"

# Methods
s = "apple"
s.startswith("a")
s.endswith("e")
s.isdigit()
s.isspace()
s.lower()
"box" in "box of life"
1 in [1,2,3]
'abracadabra'.find('cad')
'badger badger badger mushroom'.count('bad')
```

### String with variables inside

Credits to this, goes to "SShah" as an answer to [StackOverflow question](https://stackoverflow.com/questions/52155591/how-to-insert-string-into-a-string-as-a-variable)

There are 5 approaches for achieving this on python (Python 3):

1. Concatenation:

   You can do this using + for joining 2 strings, however you can only concatenate string type data, meaning non string type data needs to be converted to string using the str() function. For example:

   ```py
   print("The Enemy's health is " + str(EnemyHealth) + ". The Enemy is " + EnemyIs + ".")
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

2. Taking advantage of Python 3's print() function which can take multiple parameter arguments:

   Here your `print()` statement similar to the concatenation statement above, except where ever I use + to concatenate you need to replace it with ,. The advantage of using this, is that different data types will be automatically converted to string, i.e. no longer needing the str() function. For example:

   ```py
   print("The Enemy's health is ", EnemyHealth, ". The Enemy is ", EnemyIs, ".")
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

3. Using your string replacement approach

   The reason your code doesn't work, is because %d means you will replace it with an integer and therefore to make your code work, for the string stored on the variable EnemyIs needs to be replaced with %s which is used to state that it will be replaced with a string. Therefore to solve your problem you need to do:

   ```py
   print("The Enemy's health is %d. The Enemy is %s." % (EnemyHealth, EnemyIs))
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

4. The format() method for python strings (This is the best approach to use)

   This is a built in method for all strings in python, which allow you to easily replace the placeholder {} within python strings, with any variables. Unlike solution number 3 above, this format() method doesn't require you to express or convert different data types to string, as it would automatically do this for you. For example, to make your print statement work you can do:

   ```py
   print("The Enemy's health is {}. The Enemy is {}.".format(EnemyHealth, EnemyIs))

   # OR

   print("The Enemy's health is {0}. The Enemy is {1}.".format(EnemyHealth, EnemyIs))

   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

5. F-Strings

   As of python 3.6+, you can now also use f-strings, to substitute variables within a string. This method is similar to the the .format() method described above, and in my opinion is a better upgrade to the str.format() method. To use this method all you have to do is state f before your opening quote when defining a string and then, within the string use the format, {[variable name goes here]} for this to work. For example, to make your print statement work, using this method, you can do:

   ```py
   print(f"The Enemy's health is {EnemyHealth}. The Enemy is {EnemyIs}.")
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

   using this method, the variable name is being instantiated directly within the curly brackets {}.

   For more [info](https://realpython.com/python-f-strings/#simple-syntax)

### String formatting

Python [format cookbook](https://mkaz.blog/code/python-string-format-cookbook/)

## Lists

```python
# Mutable. That means you can change the items in a list after it has been created.

words = ["echidna", "dingo", "crocodile", "bunyip"]

# Adds its argument as a single item to the end of the list. It only ever adds one item to a list.
words.append("platypus")

# Treats its argument as a sequence and adds each item in the sequence to the end of the list. In other words, it adds a sequence of items to a list.
words.extend("abc")
# ['echidna', 'dingo', 'crocodile', 'bunyip', 'platypus', 'a', 'b', 'c']

# Adds each item of this list to the end of the words list
words.extend(["kangaroo", "wallaby"])

# reverse the order of the list
words.reverse()

# Sort the list in ascending order
words.sort()
```

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
# u'an &lt;script&gt;evil()&lt;/script&gt; example'

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

## Data Structures

### NumPy

- It gives Arrays that a great data stucture objects, that makes working with numerical data easy and simple more than what it can be done in pure python.
- It is the foundation for the python data stack, and it is what makes python great for data analysis.

[Python For Data Science NumPy Cheat Sheet](files/Python%20For%20Data%20Science%20NumPy%20Cheat%20Sheet.pdf)

### Pandas

- It gives Data Frames that are great data structures objects, that can manipulate and analyze data.

#### Pandas methods and functions

- [Compared to SQL](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_sql.html) and [Medium Article](https://medium.com/jbennetcodes/how-to-rewrite-your-sql-queries-in-pandas-and-more-149d341fc53e#e009)
- [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [loc(), iloc()](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)
- to_csv()
- [df_new = df.copy() vs df_new = df](https://www.geeksforgeeks.org/python-difference-between-pandas-copy-and-copying-through-variables/)
- [apply()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html)
- [Merges()](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
- [idxmax](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.idxmax.html)



```py
import pandas as pd
# Import a CSV file into a Pandas Data Frame variable.
# sep: specifies the separtor.
# header: specifies the column labels.
# names: specifies a header column.
# index_col: can specify one or more of your columns to be the index of the dataframe.
labels = ['id', 'name', 'attendance', 'hw', 'test1', 'project1', 'test2', 'project2', 'final']
df = pd.read_csv('file_name.csv', sep=',', header=None, names=labels, index_col=['Name', 'ID'])
# save the dataframe with file_name_edited data into a csv file.
# `to_csv()` will store our index unless we tell it not to. To make it ignore the index, we have to provide the parameter `index=False`
df.to_csv('file_name_edited.csv', index=False)
# head() is a useful function you can call on your dataframe to display the first few rows.
df.head()
# last two rows.
df.tail(2)
# this returns useful descriptive statistics for each column of data.
# such as count, mean, std, min, 25%, 50%, 75%,and max.
df.describe()
# this returns a tuple of the dimensions of the dataframe
df.shape
# this displays a concise summary of the dataframe,
# including the number of non-null values in each column
df.info()
# this returns the datatypes of the columns
df.dtypes
# returns the count of data frame
df.count(axis='rows')
# value_count aggreagates counts for each unique value in column
df.column_name.value_counts()
# List unique values in the df['name'] column
df.column_name.unique()
# this returns the number of unique values in each column
df.column_name.nunique()
# Return values at the given quantile over requested axis.
df.quantile(0.5)
# Fills the missing values with value and if inplace is true it will replace the column with new data.
df['column_name'].fillna(value, inplace=True)
# Count of Null values in each column
df_08.isna().sum()
# returns boolean column, which gives the duplicate TRUE value with escaping the first instance. All rows has to be the same to be identified as duplicate.
df.duplicated()
# removes the duplicates in the dataset and inplace parameter applies the change in the dataset.
df.drop_duplicates(inplace=True)
# Converts string to datetime object. But CSV will read this column as strings next time the file reopened, unless the it parsed into the CSV file. But pandas to_datetime provides more options than that of CSV.
df['date_column'] = pd.to_datetime(df['date_column'])
# View the index number and label for each column
for i, v in enumerate(df.columns):
    print(i, v)
# We can select data using loc and iloc. loc uses labels of rows or columns to select data, while iloc uses the index numbers.
# select all the columns from 'id' to the last column
df_means = df.loc[:,'id':]
# repeat the step above using index numbers
df_means = df.iloc[:,:12]
# remove "_mean" from column names
new_labels = []
for col in df.columns:
    if '_mean' in col:
        new_labels.append(col[:-5])  # exclude last 6 characters
    else:
        new_labels.append(col)
# datatypes of columns
for i, v in enumerate(df.iloc[0,:]):
    print(df.columns[i],':', type(v))
# Remove rows or columns by specifying label names and corresponding axis, or by specifying directly index or column names. When using a multi-index, labels on different levels can be removed by specifying the level.
df.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')
# Rename all column labels to replace spaces with underscores and convert everything to lowercase. (Underscores can be much easier to work with in Python than spaces. For example, having spaces wouldn't allow you to use df.column_name instead of df['column_name'] to select columns or use query(). Being consistent with lowercase and underscores also helps make column names easy to remember.)
df.rename(columns=lambda x: x.strip().lower().replace(' ','_'), inplace=True)
# make sure they're all identical like this
(df_08.columns == df_18.columns).all()
# Remove missing values
df.dropna()
# convert to string and extract the integer using regular expressions
df['column_name'].str.extract('(\d+)').astype(int)
# get all rows that column_name has values contains (/)
df[df['column_name'].str.contains('/')]
# copying a DataFrame or Series
# Pandas .copy() method is used to create a copy of a Pandas object. Variables are also used to generate copy of an object but variables are just pointer to an object and any change in new data will also change the previous data.
df.copy()
# Applies a user function to a DataFrame
df1[column_name].apply(lambda x: x.split("/")[0])
# combine dataframes
df3 = df1.append(df2, ignore_index=True)
# Merge dataframes
df_combined = df1.merge(df2, left_on='column_name_df1', right_on='column_name_df2', how='inner')
# idxmax function that finds the index of the row containing a column's maximum value!
df.colum_name.idxmax()
```

[Python For Data Science Cheat Sheet](Files/Python%20For%20Data%20Science%20Pandas%20Cheat%20Sheet.pdf)

### Matplotlib

- It is a package for builiding visualizations from your data. It can make many kinds of simple plots with tiny amounts of codes, but also create a professional looking figures.
- [Magic words](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

```py
import pandas as pd
import matplotlib.pyplot as plt
# view the plots in the notebook
%matplotlib inline
# Plot Title
plt.title("Number of Unique Models Using Alternative Fuels")
# plot x-axis Label
plt.xlabel("Year")
# plot y-axis label
plt.ylabel("Number of Unique Models");
# plot bar graph
plt.bar(["2008", "2018"], [alt_08, alt_18])
# hist(): plots a histogram graph to the Data Set. Figsize: resizes the figures
df.hist(figsize=(8,8));
# hist() can be called on a Pandas series object as well
df.column_name.hist();
# plot() is a more general plotting function
df.column_name.plot(kind='hist');
df.plot(x='x-axis column_name', y='y-axis column_name', kind='scatter');
df.column_name.plot(kind='box');
df.column_name.plot(kind='pie');
# scatter_matrix() shows the relationships among numerical variables with scatter plots. It also returns a histogram for each variable.
pd.plotting.scatter_matrix(df, figsize=(15,15));
# line Chart
plot(t, s)
# Shows x labels for each xth frequent
plt.xticks(np.arange(min(x), max(x)+1, 1.0))
```

- [Python For Data Science MatPlotLib Cheat Sheet](Files/Python%20For%20Data%20Science%20MatPlotLib%20Cheat%20Sheet.pdf)
- [How to rotate axis lables in seaborn and matplotlib](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)

### Resources

- [Python for data analysis](http://www.ruxizhang.com/uploads/4/4/0/2/44023465/python_for_data_analysis.pdf)
- [NumPy and Pandas by Udacity](https://classroom.udacity.com/courses/ud170)
- [How to rotate x-lables](https://kite.com/python/answers/how-to-rotate-date-ticks-using-matplotlib-in-python#:~:text=Use%20matplotlib.,specified%20amount%20of%20degrees%20degrees%20) and [here](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)

## Conventions

1. [Google Style Guide for Python](https://google.github.io/styleguide/pyguide.html)
2. [pep8](http://pep8online.com/)

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
      2. Install Virtual Wrapper `pip install virtualenvwrapper` or for Windows `pip install virtualenvwrapper-win`
      3. Add virtualenvwrapper.sh path in the Bash profile `source {path/to/Python}/Scripts/virtualenvwrapper.sh`
      4. Reload the startup
      5. Create a new environment `mkvirtualenv {VirEnv Name}`
      6. Deactivate current environment `deactivate`
      7. Use an enviroment `workon {VirEnv Name}`
      8. Remove an environment `rmvirtualenv {VirEnv Name}`
      9. List all available environments `workon`
      10. [Medium Article](https://medium.com/the-andela-way/configuring-python-environment-with-virtualenvwrapper-8745c2895745)
3. How to install Jupyter without anaconda
   1. `python -m pip install --upgrade pip`
   2. `python -m pip install notebook`
   3. Restart VS Code
   4. Pick the Python environment you did the pip install in
   For more information see <http://jupyter.org/install>
