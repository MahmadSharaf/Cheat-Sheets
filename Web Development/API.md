# API Cheatsheet

## What API is

* It stands for Application Programming Interface.
* It refers to any method of communication between two entities of code.
* APIs are a great way for controlling the exposure of code, allowing internal functionalities of an application to be used from the outside world without exposing all of the internal code.

## Web APIs

* They enable communication between several machines.
* Web APIs make it possible to invoke the execution of code on another machine via the internet.
* A machine can use multiple web APIs to create a new application, sometimes called a Mashup, providing users with a new experience that leverages existing applications.

### Web API Protocols

* A set of rules must be be in place in order for machines to speak the same language.

### OSI Model

* A common abstraction for conceptualizing this is with the open
systems interconnection or [OSI model](https://en.wikipedia.org/wiki/OSI_model).
* This model characterizes the communication functions of the computing system, without getting too caught up with the specifics of each different type of computer. This allows the model to focus on the interoperability of diverse communication systems with standard protocols.
* The model partitions a communications system into abstraction layers. The original version of the model defines seven layers (Application, Presentation, Session, Transport, Network, Data Link, and Physical). A layer serves the layer above it, and is served by the layer below it. A variety of protocols can exist within in each layer, but they all have to be able to receive and hand off data to the protocols in the adjacent layers.
* Once the message reaches the physical layer, it is transmitted as a stream of bits over a physical medium. Physical media are the wires, fiber optic cables or wireless signals that you use to connect to the Internet.
* Once the message reaches it's intended machine. It is now processed in reverse order such that the application sitting on the receiving computer gets the message the same way it was created by the sender.
* When it comes to developing web applications in API design, developers mainly focus on the application layer in the OSI model. Operating systems can handle the complexities of the lower levels for us in most cases.

#### Application Layer

* This layer responsible for setting all of the protocols in which applications exchange data.
* The most popular application level protocol is HTTP. HTTP functions via a series of requests and responses between clients and servers respectively.
* The original OSI model has the application layer sitting as the highest level set of protocols for communicating across the internet. But other protocols and technologies for sending and receiving information via APIs also exist.
* There are two layers above Application Layer (Web Service and Message Formatting)

#### Web Service Layer

* It refers to the protocols that can sit on top of the application layer and can determine the format in which APIs are sent and received.
* One of the most popular protocols at this level is the Simple Object Access Protocol (SOAP).
* SOAP uses the extensible markup language (XML) to transmit sets of information in the form of objects. SOAP most commonly sits atop the HTTP application protocol, but can also function with SMTP (Simple Mail Transfer Protocol).
* REST (Representational State Transfer) is an alternative to SOAP. REST is more of a set of styles and guidelines than a protocol, since it leverages the features of HTTP in order to transmit information. HTTP verbs such as GET, POST, PUT and DELETE handles the management a set of resources.
* While SOAP is still used in some contexts, RESTful APIs currently dominate the API landscape. It is the best practice for API development.

#### Message Formatting Layer

* It contains the languages that formats the sets of information between machines. These protocols focus mainly on the data structures that contain the information we want to communicate like the protocols in the other layers.
* There are several implementations already out there, the most two common formats are XML and JSON.
* XML stands for extensible markup language. It looks very similar to HTML and is readable by humans and machines.
* JSON stands for JavaScript Object Notation. It was designed to resemble JavaScript code, and has attribute value pairs, making it very easy to read for human eye.

### SOAP vs REST

* SOAP was originally developed by Microsoft in 1998.
* For SOAP, it is obliged to use XML for data structures, but can choose HTTP or another underlying application-level protocol.
* REST is more of a description than a development project. The acronym first appeared in a dissertation by Roy Thomas Fielding in 2000.
* REST uses HTTP verbs in order to access and manipulate resources, but can use any type if messaging protocol to structure the data it sends. In order for an application to be truly RESTful, it must adhere to a set of constraints Fielding defined in his dissertation.
* REST is more popular

### XML vs JSON

* XML was developed in 1997. It uses identifying tags similar to HTML and provides a rigid way of structuring data.
* JSON was developed in 2001. It is derived from the JavaScript language. Similar to HTML, it is easily human readable, but can condensed with less characters to be very lightweight.
* JSON is more popular.

### REST Constraints

It applies a few [constraints](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) to clarify communication and resource management.

1. The separation of clients and servers.
   * A client is defined as a machine requesting a resource where the server is the machine that responds with the requested resource.
   * A machine can function as a client and as a server, but for the duration of an HTTP request and response cycle, it must assume the role as either the requester of the information or the holder of that information.
2. Stateless
   * A stateful architecture remembers a client's activity between requests. A login session in websites that remembers the activity throughout the duration of time on the website.
   * A truly RESTful architecture, however, is not allowed to retain information about the state of another machine during the communication process.
   * Each request from a client to a server must be treated as though it was the first request the server has ever seen from that client. A server should not remember its clients and readjust its state accordingly. The server may only give back up to date state about its state to the client and allow for modifications, if it is authorized to do so.
3. Cacheable
   * Response messages from the server to the client are explicitly labeled as cacheable or non-cacheable. This way, responses can me cached by the client if the information on the server hasn’t changed since the last request.
4. Uniform Interface
   * RESTful architectures must have a uniform interface between all clients and servers. For example, a server must not require a different way of accessing data if a client has a Windows laptop verses an iPhone or a Unix server.
   * Gaining access to these end points is the same for any machine trying to access this information.
5. Layered System
   * A layered system means that a client can have access to endpoint that relies on other endpoints without having to understand all of the underlying implementations.
   * If client A wants to communicate with server B and that server goes out to Google or some other database in order to generate a response, client A should not have to some other database in order to generate a response, client A should not have to accommodate for any other technologies besides accessing server B's endpoint.
   * Layering allows very complicated tasks to be completed without having to understand all of the underlying complexities that are required to generate the response.
6. Code on Demand (optional)
   * Code on Demand is an optional constraint for RESTful applications, but it opens a possibility for code like JavaScript, for example, from the server to be sent off to the client for execution.
