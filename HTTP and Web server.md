# HTTP & web server Cheat sheet

## Getting Started

1. Git version control
2. Python
3. NMap: You'll also need to install `ncat`, which is part of the Nmap network testing toolkit. We'll be using `ncat` to investigate how web servers and browsers talk to each other.

## Web server

An HTTP transaction always involves a client and a server. You're using an HTTP client right now — your web browser. Your browser sends HTTP requests to web servers, and servers send responses back to your browser. Displaying a simple web page can involve dozens of requests — for the HTML page itself, for images or other media, and for additional data that the page needs.

HTTP was originally created to serve hypertext documents, but today is used for much more. As a user of the web, you're using HTTP all the time.

### Running a web server from python

Open up a terminal; `cd` to a directory that has some files in it — maybe a directory containing some text files, HTML files, or images — then run `python3 -m http.server 8000` in your terminal.

When you start up the demo server, it will print a message telling you that it's serving HTTP. Leave it running, and leave the terminal open. Now try accessing <http://localhost:8000/> from your browser.

### What's a server anyway

A server is just a program that accepts connections from other programs on the network.

When you start a server program, it waits for clients to connect to it. Then when a connection comes in, the server runs a piece of code — like calling a function — to handle each incoming connection. A connection in this sense is like a phone call: it's a channel through which the client and server can talk to each other. Web clients send requests over these connections, and servers send responses back.

## URI

- A web address is also called a URI for Uniform Resource Identifier.
- the term URL or Uniform Resource Locator. These are pretty close to the same thing; specifically, a URL is a URI for a resource on the network.
- URIs are made out of several different parts, each of which has its own syntax. Many of these parts are optional, which is why URIs for different services look so different from one another.
- Here is an example of a URI: <https://en.wikipedia.org/wiki/Fish>  
  This URI has three visible parts, separated by a little bit of punctuation:

  - `https` is the scheme
  - `en.wikipedia.org` is the hostname
  - and `/wiki/Fish` is the path

1. Scheme

   - The first part of a URI is the scheme, which tells the client how to go about accessing the resource.
   - `File` URIs tell the client to access a file on the local filesystem. `HTTP` and `HTTPS` URIs point to resources served by a web server.
   - `HTTP` and `HTTPS` URIs look almost the same. The difference is that when a client goes to access a resource with an HTTPS URI, it will use an encrypted connection to do it.
   - There are many other URI schemes out there, though. You can take a look at the [official list!](http://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml)

2. Hostname

   - This tells the client which server to connect to.
   - not every URI has a hostname. For instance, a `mailto` URI just has an email address: `mailto:spam@example.net` is a well-formed `mailto` URI. This also reveals a bit more about the punctuation in URIs: the `:` goes after the scheme, but the `//` goes before the hostname. `Mailto` links don't have a hostname part, so they don't have a `//`.
   - A hostname in a URI can also be an IP address: for instance, if you put <http://216.58.194.174/> in your browser, you'll end up at Google.
   - The Internet tells computers apart by their IP addresses; every piece of network traffic on the Internet is labeled with the IP addresses of the sending and receiving computers.
   - In order to connect to a web server such as `www.udacity.com`, a client needs to translate the hostname into an IP address. Your operating system's network configuration uses the Domain Name Service (DNS) — a set of servers maintained by Internet Service Providers (ISPs) and other network users — to look up hostnames and get back IP addresses.

3. Path

   - Identifies a particular resource on a server. The path tells the server which resource the client is looking for.
   - URI paths don't necessarily equate to specific filenames. For instance, if you do a Google search, you'll see a URI path such as `/search?q=ponies`. This doesn't mean that there's literally a file on a server at Google with a filename of `search?q=ponies`. The server interprets the path to figure out what resource to send. In the case of a search query, it sends back a search result page that maybe never existed before.
   - The path written with just a single slash is also called the root.

4. Ports:

   - The port in URI `http://localhost:8000/` is `8000`.
   - Most web addresses doesn't have a port number in them because the client usually figures out the port number number from the URI scheme. `HTTP` URIs imply a port number of `80`, whereas `HTTPS` URIs imply a port number of `443`
   - All of the network traffic that computers send and receive is split up into messages called packets. Each packet has the IP addresses of the computer that sent it, and the computer that receives it. It also has the port number for the sender and recipient. IP addresses distinguish computers; port numbers distinguish _programs_ on those computers.

5. Other URI parts
   - There are many other parts that can occur in a URI. Consider the difference between these two Wikipedia URIs:  
     <https://en.wikipedia.org/wiki/Oxygen>  
     <https://en.wikipedia.org/wiki/Oxygen#Discovery>  
     If you follow these links in your browser, it will fetch the same page from Wikipedia's web server. But the second one displays the page scrolled to the section about the discovery of oxygen. The part of the URI after the `#` sign is called a `fragment`. The browser doesn't even send it to the web server. It lets a link point to a specific named part of a resource; in HTML pages it links to an element by `id`.
   - In contrast, consider this Google Search URI:
     <https://www.google.com/search?q=fish>  
     The `?q=fish` is a query part of the URI. This does get sent to the server.
   - For way more detail: <https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#Generic_syntax>

## HTTP Requests/Responses

### HTTP Request Message

- HTTP message consists of a message header, and an optional message body. These two entities are separated by space.
- In HTTP request, the first line of the header is called the request line.
- The request line contains the HTTP verb, the URI (Uniform Resource Identifer), and the HTTP version number.
- After the request line, there is the optional request headers. These are the parameters that can be used to describe specific properties about a request.
- Request headers appear in name value pairs. Multiple values can be separated by commas.
- A blank line separates the header and the body of an HTTP request.
- In the body, Any other information can be added about the request that needs to be sent to the server.

   ```txt
   GET puppies.html HTTP/1.1
   Host: www.puppyshelter.com
   Accept: image/gif, image/jpeg, */*
   Accept-language: en-us
   Accept-Encoding: gzip, deflate
   User-Agent: Mozilla/4.0
   Content-Length: 35

   puppyId=12345&name=Fido+Simpson
   ```

### Request Verbs

#### 1. GET for receiving resources

"`"GET /readme.png HTTP/1.1" 200`

- The word `GET` is the method or HTTP verb being used
- `GET` is the verb that clients use when they want a server to send a resource, such as a web page or image.
- `/readme.png` is the path of the resource being requested. Notice that the client does not send the whole URI of the resource here. It doesn't say `https://localhost:8000/readme.png`. It just sends the path.
- `HTTP/1.1` is the protocol of the request. Over the years, there have been several changes to the way HTTP works. Clients have to tell servers which dialect of HTTP they're speaking. `HTTP/1.1` is the most common version today.
- When a browser submits a form via `GET`, it puts all of the form fields into the URI that it sends to the server. These are sent as a query, in the request path — just like search engines do.
- `GET` methods are good for search forms and other actions that are intended to look something up or ask the server for a copy of some resource. But `GET` is not recommended for actions that are intended to alter or create a resource.

#### 2. POST for creating resources

- `POST` requests are not idempotent.  
  An action is idempotent if doing it twice (or more) produces the same result as doing it once.
- It is used in a form that adds an item to a shopping cart on an e-commerce site, or posts a new message on a comments board.
- `POST` is for actions that are intended to alter or create a resource.
- When a browser submits a form as a POST request, it doesn't encode the form data in the URI path, the way it does with a `GET` request. Instead, it sends the form data in the request body, underneath the headers. The request also includes Content-Type and Content-Length headers.
- By the way, the names of HTTP headers are case-insensitive. So there's no difference between writing Content-Length or content-length

#### 3. PUT for creating resources

- The HTTP `PUT` method can be used for creating a new resources.
- The client sends the URI path that it wants to create, and a piece of data in the request body.
- A server should respond to a `PUT` request with a `201 Created` status code, if the `PUT` action completed successfully.
- After a successful `PUT`, a `GET` request to the same URI should return the newly created resource.
- `PUT` can be used for actions such as uploading a file to a web site. However, it's not the most common way to do file uploads. `PUT` has to be done in application code (e.g. JavaScript), whereas with `POST` method it's possible to do uploads with just `HTML` on the client side.

#### 4. DELETE for deleting resources

- The destructive counterpart to `PUT` is `DELETE`, for removing a resource from the server.
- After a `DELETE` has happened successfully, further `GET` requests for that resource will yield `404 Not Found` … unless, of course, a new resource is later created with the same name!

#### 5. PATCH for making changes

- The `PATCH` method is a relatively new addition to `HTTP`. It expresses the idea of patching a resource, or changing it in some well-defined way.
- However, just as `HTTP` doesn't specify what format a resource has to be in, it also doesn't specify in what format a patch can be in: how it should represent the changes that are intended to be applied. That's up to the application to decide. An application could send diffs over `HTTP` `PATCH` requests, for instance.
- One standardized format for PATCH requests is the JSON Patch format, which expresses changes to a piece of JSON data. A different one is JSON Merge Patch.

#### 6. HEAD

Works just like `GET`, except the server doesn't return any content — just headers.

#### 7. OPTIONS

Can be used to find out what features the server supports.

#### 8. TRACE

Echoes back what the server received from the client — but is often disabled for security reasons

#### Important TIP

HTTP can't prevent a service from using methods to mean something different from what they're intended to mean, but this can have some surprising effects. For instance, you could create a service that used a GET request to delete content. However, web clients don't expect GET requests to have side-effects like that. In one famous case from 2006, an organization put up a web site where "edit" and "delete" actions happened through GET requests, and the result was that [the next search-engine web crawler to come along deleted the whole site](http://thedailywtf.com/articles/The_Spider_of_Doom).

### HTTP Response Message

- When the server receives an HTTP request, it returns a response message to the client.
- This response can contain the information requested or an error message there was one.
- HTTP message consists of a message header, and an optional message body. These two entities are separated by space.
- In HTTP response, the first line of the header is called the status line.
- The status line contains the HTTP version, status code, and a reason phrase that explains the status code in English.
- After the status line, there is the optional response headers. These are the parameters that can be used to describe specific properties about a response.
- Response headers appear in name value pairs. Multiple values can be separated by commas.
- A blank line separates the header and the body of an HTTP response.
- The response body contains the data that the client requested.

   ```txt
   HTTP/1.1 200 OK
   Date: Fri, 04 Sep 2015 01:11:12 GMT
   Server: Apache/1.3.29 (Win32)
   Last-Modified: Sat, 07 Feb 2014
   ETag: "0-23-4024c3a5:
   ContentType: text/html
   ContentLength: 35
   Connection: KeepAlive
   KeepAlive: timeout-15, max = 100

   <h1>Welcome to my home page!</h1>
   ```

### Response Status codes

- **1xx — Informational** The request is in progress or there's another step to take.
- **2xx — Success!** The request succeeded. The server is sending the data the client asked for.
- **3xx — Redirection**. The server is telling the client a different URI it should redirect to. The headers will usually contain a Location header with the updated URI. Different codes tell the client whether a redirect is permanent or temporary.
- **4xx — Client error**. The server didn't understand the client's request, or can't or won't fill it. Different codes tell the client whether it was a bad URI, a permissions problem, or another sort of error.
- **5xx — Server error**. Something went wrong on the server side

You can find out much more about HTTP status codes in this [Wikipedia article](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) or [in the specification for HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).

### Headers

- Headers are a sort of metadata for the response. They aren't displayed by browsers or other clients; instead, they tell the client various information about the response.
- Many, many features of the Web are implemented using headers. For instance, cookies are a Web feature that lets servers store data on the browser, for instance to keep a user logged in. To set a cookie, the server sends the Set-Cookie header. The browser will then send the cookie data back in a Cookie header on subsequent requests.

1. content-type

   - A `Content-type` header indicates the kind of data that the server is sending.
   - It includes a general category of content as well as the specific format.

2. Content-Length
   - Tells the client how long (in bytes) the response body will be.
   - Browsers use this so they can fetch multiple pieces of data (such as images on a web page) without having to reconnect to the server.

## Servers and handlers

Web servers using `http.server` are made of two parts: the `HTTPServer` class, and a request handler class. The first part, the `HTTPServer` class, is built in to the module and is the same for every web service. It knows how to listen on a port and accept HTTP requests from clients. Whenever it receives a request, it hands that request off to the second part — a **request handler** — which is different for every web service.

Here's what your Python code will need to do in order to run a web service:

1. Import http.server, or at least the pieces of it that you need.
2. Create a subclass of `http.server.BaseHTTPRequestHandler`. This is your handler class.
3. Define a method on the handler class for each **HTTP verb** you want to handle.
   1. The method for GET requests has to be called `do_GET`.
   2. Inside the method, call built-in methods of the handler class to read the HTTP request and write the response.
4. Create an instance of `http.server.HTTPServer`, giving it your handler class and server information — particularly, the port number.
5. Call the `HTTPServer` instance's `serve_forever` method.

Once you call the HTTPServer instance's `serve_forever` method, the server does that — it runs forever, until stopped. Just as in the last lesson, if you have a Python server running and you want to stop it, type Ctrl-C into the terminal where it's running. (You may need to type it two or three times.)

## Queries and quoting

### Unpacking query parameters

When you take a look at a URI for a major web service, you'll often see several query parameters, which are a sort of variable assignment that occurs after a `?` in the URI.  
The query part of the URI is the part after the `?` mark. Conventionally, query parameters are written as `key=value` and separated by `&` signs.

There is a Python library called `urllib.parse` that knows how to unpack query parameters and other parts of an HTTP URL. (The library doesn't work on all URIs, only on some URLs). In the [documentation](https://docs.python.org/3/library/urllib.parse.html) check out the `urlparse` and `parse_qs` functions specifically.

### URL quoting

HTTP URLs aren't allowed to contain spaces or certain other characters. So if you want to send these characters in an HTTP request, they have to be translated into a "URL-safe" or "URL-quoted" format.

**"Quoting"** in this sense doesn't have to do with quotation marks, the kind you find around Python strings. It means translating a string into a form that doesn't have any special characters in it, but in a way that can be reversed (unquoted) later. It's sometimes also referred to as **URL-encoding**

One of the features of the URL-quoted format is that spaces are sometimes translated into plus signs. Other special characters are translated into hexadecimal codes that begin with the percent sign.

Take a look at the [documentation](https://docs.python.org/3/library/urllib.parse.html#url-quoting) for `urllib.parse.quote` and related functions.

## Design pattern

### Post-Redirect-Get

- There's a very common design pattern for interactive HTTP applications and APIs, called the PRG or Post-Redirect-Get pattern. A client POSTs to a server to create or update a resource; on success, the server replies not with a 200 OK but with a 303 redirect. The redirect causes the client to GET the created or updated resource.
- One big advantage of Post-Redirect-Get is that as a user, every page you actually see is the result of a GET request, which means you can bookmark it, reload it, and so forth — without ever accidentally resubmitting a form.

## Concurrency

Being able to handle two ongoing tasks at the same time is called **concurrency**, and the basic `http.server.HTTPServer` doesn't have it. It's pretty straightforward to plug concurrency support into an **HTTPServer**, though.

## Specialized Web Servers

### Static content and more

- The Web was originally designed to serve documents, not to deliver applications.
- Specialized web server programs — like **Apache**, **Nginx**, or **IIS** — can serve static content from disk storage very quickly and efficiently. They can also provide access control, allowing only authenticated users to download particular static content

### Routing and load balancing

- Some web applications have several different server components, each running as a separate process. One thing a specialized web server can do is dispatch requests to the particular backend servers that need to handle each request. There are a lot of names for this, including request routing and reverse proxying.
- Some web applications need to do a lot of work on the server side for each request, and need many servers to handle the load. Splitting requests up among several servers is called _load balancing_.
- _Load balancing_ also helps handle conditions where one server becomes unavailable, allowing other servers to pick up the slack. A reverse proxy can _health check_ the backend servers, only sending requests to the ones that are currently up and running. This also makes it possible to do updates to the backend servers without having an outage.

### Concurrent users

- Handling a large number of network connections at once turns out to be complicated — even more so than plugging concurrency support into your Python web service.
- As you may have noticed in your own use of the web, it takes time for a server to respond to a request. The server has to receive and parse the request, come up with the data that it needs to respond, and transmit the response back to the client. The network itself is not instantaneous; it takes time for data to travel from the client to the server.
- In addition, a browser is totally allowed to open up multiple connections to the same server, for instance to request resources such as images, or to perform API queries.
- All of this means that if a server is handling many requests per second, there will be many requests in progress at once — literally, at any instant in time. We sometimes refer to these as in-flight requests, meaning that the request has "taken off" from the client, but the response has not "landed" again back at the client. A web service can't just handle one request at a time and then go on to the next one; it has to be able to handle many at once.

### Caching

- It is a temporary storage for resources that are likely to be reused like complicated processing or calculation, to avoid recalculating same process and to avoid re-sending large object if it doesn't have to.
- Web systems can perform caching in a number of places — but all of them are under control of the server that serves up a particular resource. That server can set HTTP headers indicating that a particular resource is not intended to change quickly, and can safely be cached.
- There are a few places that caching usually can happen. Every user's browser maintains a browser cache of cacheable resources — such as images from recently-viewed web pages. The browser can also be configured to pass requests through a web proxy, which can perform caching on behalf of many users. Finally, a web site can use a reverse proxy to cache results so they don't need to be recomputed by a slower application server or database.
- All HTTP caching is supposed to be governed by cache control headers set by the server. You can read a lot more about them in [this article](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching) by Google engineer Ilya Grigorik.

### Capacity

- Why serve static requests out of cache (or a static web server) rather than out of your application server? Python code is totally capable of sending images or video via HTTP, after all. The reason is that — all else being equal — handling a request faster provides a better user experience, but also makes it possible for your service to support more requests.
- If your web service becomes popular, you don't want it to bog down under the strain of more traffic. So it helps to handle different kinds of request with software that can perform that function quickly and efficiently.

### HTTPS

- When a browser and a server speak HTTPS, they're just speaking HTTP, but over an encrypted connection. The encryption follows a standard protocol called Transport Layer Security, or TLS for short. TLS provides some important guarantees for web security:
  - It keeps the connection **private** by encrypting everything sent over it. Only the server and browser should be able to read what's being sent.
  - It lets the browser **authenticate** the server. For instance, when a user accesses <https://www.udacity.com/,> they can be sure that the response they're seeing is really from Udacity's servers and not from an impostor.
  - It helps protect the **integrity** of the data sent over that connection — checking that it has not been (accidentally or deliberately) modified or replaced.
- TLS is also very often referred to by the older name SSL (Secure Sockets Layer). Technically, SSL is an older version of the encryption protocol.

### Cookies

- Cookies are a way that a server can ask a browser to retain a piece of information, and send it back to the server when the browser makes subsequent requests. Every cookie has a name and a value, much like a variable in your code; it also has rules that specify when the cookie should be sent back.

#### Uses

- If the server sends each client a unique cookie value, it can use these to tell clients apart.
- Cookies are used by analytics and advertising systems to track user activity from site to site.
- Cookies are also sometimes used to store user preferences for a site.

#### How cookies happen

- The first time the client makes a request to the server, the server sends back the response with a Set-Cookie header.
- This header contains three things: a cookie name, a value, and some attributes.
- Every subsequent time the browser makes a request to the server, it will send that cookie back to the server. The server can update cookies, or ask the browser to expire them.

#### What are the pieces of data in the cookie

- The cookie's **name** and **content**, are also called its key and value. The value of the cookie is where the "real data" of the cookie goes — for instance, a unique token representing a logged-in user's session.
- Domain and Path, describe the scope of the cookie. By default, the domain of a cookie is the hostname from the URI of the response that set the cookie. But a server can also set a cookie on a broader domain, within limits.
- **Secure** and **HttpOnly**, and they are boolean flags (true or false values). The internal names are a little bit misleading. If the Secure flag is set, then the cookie will only be sent over HTTPS (encrypted) connections, not plain HTTP. If the HttpOnly flag is set, then the cookie will not be accessible to JavaScript code running on the page.
- The **creation time** is just the time of the response that set the cookie. The **expiration time** is when the server wants the browser to stop saving the cookie. There are two different ways a server can set this: it can set an Expires field with a specific date and time, or a Max-Age field with a number of seconds. If no expiration field is set, then a cookie is expired when the browser closes.

### TLS/SSL

- The server-side configuration for TLS includes two important pieces of data: a private key and a public certificate. The private key is secret; it's held on the server and never leaves there. The certificate is sent to every browser that connects to that server via TLS. These two pieces of data are mathematically related to each other in a way that makes the encryption of TLS possible.
- The server's certificate is issued by an organization called a certificate authority (CA). The certificate authority's job is to make sure that the server really is who it says it is.
- The role of a certificate authority is kind of like getting a document notarized. A notary public checks your ID and witnesses you sign a document, and puts their stamp on it to indicate that they did so.

#### How does TLS assure privacy

- The data in the TLS certificate and the server's private key are mathematically related to each other through a system called public-key cryptography. The important part is that the two endpoints (the browser and server) can securely agree on a shared secret which allows them to scramble the data sent between them so that only the other endpoint — and not any eavesdropper — can unscramble it.

#### How does TLS assure authentication

- A server certificate indicates that an encryption key belongs to a particular organization responsible for that service. It's the job of a certificate authority to make sure that they don't issue a cert to someone other than the company who actually runs that domain.
- But the cert also contains metadata that says what DNS domain the certificate is good for. When the browser connects to a particular server, if the TLS domain metadata doesn't match the DNS domain, the browser will reject the certificate and put up a big scary warning to tell the user that something fishy is going on.

#### How does TLS assure integrity

- Every request and response sent over a TLS connection is sent with a message authentication code (MAC) that the other end of the connection can verify to make sure that the message hasn't been altered or damaged in transit.

## Deploy to an online host

### Deploy to Heroku

1. Sign up for a free [Heroku](https://signup.heroku.com/dc) account.
2. Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) and authenticate
3. From the command line, use `heroku login` to authenticate to Heroku.
   - It will prompt you for your username and password; use the ones that you just set up when you created your account. This command will save your authentication information in a hidden file (.netrc) so you will not need to ender your password again on the same computer.
4. Create configuration files  
   There are a few configuration files that Heroku requires for deployment, to tell its servers how to run your application.
   1. `runtime.txt` tells Heroku what version of Python you want to run. [Check the currently supported runtimes in the Heroku documentation](https://devcenter.heroku.com/articles/python-runtimes); this will change over time!
   2. `requirements.txt` is used by Heroku (through pip) to install dependencies of your application that aren't in the Python standard library.
   3. `Procfile` is used by Heroku to specify the command line for running your application. It can support running multiple servers, but in this case we're only going to run a web server. [Check the Heroku documentation about process types for more details](https://devcenter.heroku.com/articles/procfile).
5. Listen on a configurable port.

   - Heroku runs many users' processes on the same computer, and multiple processes can't (normally) listen on the same port. So Heroku needs to be able to tell your server what port to listen on.
   - The way it does this is through an _environment variable_ — a configuration variable that is passed to your server from the program that starts it, usually the shell. Python code can access environment variables in the `os.environ` dictionary. The names of environment variables are usually capitalized; and the environment variable we need here is called, unsurprisingly, `PORT`.
   - The port your server listens on is configured when it creates the `HTTPServer` instance, near the bottom of the server code. We can make it work with or without the PORT environment variable, like so:

     ```python
     if __name__ == '__main__':
      port = int(os.environ.get('PORT', 8000))   # Use PORT if it's there.
      server_address = ('', port)
      httpd = http.server.HTTPServer(server_address, Shortener)
      httpd.serve_forever()
     ```

6. Create and push your app
   - Before you can put your service on the web, you have to give it a name. You can call it whatever you want, as long as the name is not already taken by another user! Your app's name will appear in the URI of your deployed service. For instance, if you name your app silly-pony, it will appear on the web at <https://silly-pony.herokuapp.com/.>
   - Use `heroku create your-app-name` to tell Heroku about your app and give it a name. Again, you can choose any name you like, but it will have to be unique — the service will tell you if you're choosing a name that someone else has already claimed.
   - Finally, use `git push heroku master` to deploy your app!

## Authentication vs Authorization

### Authentication

- It is the process of saying "you are who you say you are".
- It is used to create a unique username and password to grant access to the website.
- Websites can verified by a trusted certificate authority. The browser can tell so that this website is the real one.

#### Securing your website by the following aspects

1. Requiring a **strong passwords** from the users, prevents the hacker from simply guessing the password.
2. Use **strong encryption** by adding a mathematical algorithms to make information virtually impossible to be decrypted.
3. Ensure **secure communication** between client and server to make sure you private information doesn't become public at any point along communication.
4. Securing **password storage** in an encrypted database; such that no one can get access to the user passwords.
5. Implement **Password recovery** in which if the user forget their password, there will be a way to create a new one quickly and securely.
6. Implement **2-factor authentication** that requires the password and an extra key to gain access to a private data.
7. Include protection against "**man-in-the-middle**" attacks, to make sure no malicious system interfering with the data being transmitted or pretending to be a trusted website. `Anti-forgery state token` can be used in this case.

- All these security features are important, some need to be implemented on server side and some on client side and others on both.
  - Requiring users for strong password can be implemented in different ways, it can be checked in the JS but the attacker may mimic the HTTP request sent from the browser, and implementing them on the server can prevent the users to create weak passwords but will not figure out until the server responds, so best practice is to implement on both server and client side.
  - Secure password storage can be implemented on server side.
  - Protection against man-in-the-middle attacks has to be implemented on both sides since sensitive information can be acquired from both sides.
  - Notes:
    - [App for Checking password security](https://howsecureismypassword.net/)
    - [Password Storage - Hashing vs. Encrypting](http://www.darkreading.com/safely-storing-user-passwords-hashing-vs-encrypting/a/d-id/1269374)
    - [Man-in-the-Middle Attacks](http://en.wikipedia.org/wiki/Man-in-the-middle_attack)

### Authorization

- It is the process of checking whether the user has the privilege to access certain locations or do specific actions.

### Third Party Auth Providers

- It is by using the user account at the third party like Facebook or Gmail

#### Pros

1. Outsource Auth handling to OAuth providers. You don't need to think how to keep and store users passwords.
2. Easer to register users
3. Less passwords for users to remember

#### Neutral

1. Users need to have a 3rd party account.
2. Users don't trust your site to gain access to their info from their third party account. So, it is better to keep authorization scope minimal.
3. Limited/restricted internet access.
4. Different auth requirements. The need for creating a 2-factor passwords for users.

### OAuth2 Playground

- Google has created a website where developers can test making API calls.
- How to use:
  - Visit <https://developers.google.com/oauthplayground/>
  - At the right hand side, there is a panel which has the options for the google products that can be used to make API calls using OAuth.
  - For example to get the users name, email, age, gender and pic:
    1. Select Google OAuth2 API v2 and then select `https://www.googleapis.com/auth/userinfo.profile` and `https://www.googleapis.com/auth/userinfo.email` , and finally click `Authorize APIs`
    2. Exchange authorization code for tokens
    3. Click on `List possible operations`, then choose `V2 userinfo` under `Google OAuth2 API v2`, and finally click send request.

## Handful Resources

1. [Mozilla Developer Network's HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP) index page contains a variety of tutorial and reference materials on every aspect of HTTP.
2. The standards documents for HTTP/1.1 start at [RFC 7230](https://tools.ietf.org/html/rfc7230). The language of Internet standards tends to be a little difficult, but these are the official description of how it's supposed to work.
3. The standards documents for HTTP/2 are at <https://http2.github.io/.>
4. If you already run your own web site, [Let's Encrypt](https://letsencrypt.org/) is a great site to learn about HTTPS in a hands-on way, by creating your own HTTPS certificates and installing them on your site.
5. [HTTP Spy](https://chrome.google.com/webstore/detail/http-spy/agnoocojkneiphkobpcfoaenhpjnmifb?hl=en) is a neat little Chrome extension that will show you the headers and request information for every request your browser makes.
