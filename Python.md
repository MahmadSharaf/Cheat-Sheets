# Python Cheat sheet

- [Python Cheat sheet](#python-cheat-sheet)
  - [Dealing with files and folders](#dealing-with-files-and-folders)
  - [Strings](#strings)
  - [Lists](#lists)
  - [While loop](#while-loop)
  - [Tricks](#tricks)
  - [Draw on screen using Turtle module](#draw-on-screen-using-turtle-module)
  - [Classes](#classes)
  - [HTTP servers](#http-servers)
  - [Python DB-API](#python-db-api)
  - [PostgreSQL ("psycopg2" module)](#postgresql-psycopg2-module)
  - [Bleach](#bleach)
  - [Conventions](#conventions)

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

    # This code will run when we run this module as a Python program,rather        than importing it.
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
       mesg = form.format("\n".join(memory))
       self.wfile.write(mesg.encode())
   ```

5. Requests library can do the following

   1. Make a Request
   2. Passing Parameters In URLs
   3. Response Content
   4. Binary Response Content
   5. JSON Response Content
   6. Response Status Codes
   7. Custom Headers
   8. Cookies
   9. and many [more](https://2.python-requests.org//en/master/user/quickstart/) ...

6. Concurrency

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

7. Cookies

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

## Conventions

1. [Google Style Guide for Python](https://google.github.io/styleguide/pyguide.html)
2. [pep8](http://pep8online.com/)
