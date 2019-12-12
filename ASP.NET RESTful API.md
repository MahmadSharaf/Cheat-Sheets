# RESTFUL API
* It's how we build APIs, and JSON is what we get back from APIs.
* RESTFUL API is not just an API with HTTP services and return JSON.
* REST "REpresentational State Transfer" is intended to evoke an image of how a well-designed web applicaton behaves.
* REST is not a standard, it's an architectural style.

## REST is defined by six constraints:
### 1-Client-server 'fundamental':
* It enforces client-server architecture.
* Client is not concerned how data is stored.
* Server is not concerned how user interface is implemented.

### 2-Statelessness: 
* The necessary state to handle every request is contained in the request itself.

### 3-Cacheable:
* Each response message must explicitly state if it can be cached or not.

### 4-Layered System:
* A REST-based solution can be compromised of multiple architectural layers. These layers can be removed, 
added, modified, but no layer can directly access a layer that's beyond the next one.

### 5-Code on Demand 'optional':
* Server can extend client functionality.

### 6-Uniform Interface:
* API and consumers share one single technical interface.

#### a. Identification of resources: 
* It states that individual resources are identified in requests
using URIs and those resources are conceptually seperate from its representation.

#### b. Manipulation of resources through representations
* Representation + metadata should be sufficient to modify or delete the resource.

#### c. Self-Descriptive message:
* Each message must include enough info to describe how to process the message.

#### d. HATEOAS "Hypermedia As The Engine Of Application State".
* Hypermedia is a generalization of hyperytext (links) it includes other types like video, music, pictures,..etc
* Drives how to consume and use the API. It tells the consumer what it can do with the API. Can I update this resource? Can I delete it? How I create it? and Where can I find it?
* Allows for a self-documenting API.

##### A system is only considered RESTful when it adheres to all constraints.

## The Richardson Maturity Model:
* It's developed by lenorad Richardson.
* It shows how to go from a simple API to a RESTful API

### It has 4 levels:

#### Level 0 (The swamp of POX):
* HTTP protocol is used for remote interaction, the rest if the protocol isn't used as it should be 

#### Level 1(Resources)
* Each resource is mapped to a URI
* On level 0, there was only 1 URI but level 1 has multiple URIs
* Reduces complexity by using multiple endpoints instead of one endpoint.

#### Level 2 (verbs):
* Correct HTTP verbs are used
* Correct status codes are used 

#### Level 3 (hypermedia controls):
* The API supports Hypermedia as the engine of the App state (HATEOS)
* Introduces discoverability.

##### Roy-fielding states that level 3 is a pre-conditioned RESTful API.


## The Model-View-Controller Pattern
* It's Architectural pattern for implementing user interfaces.
* Encourages loose coupling and sepreation of concerns that allow then better testability of the app and the ability to use part of it.
* Not a full application architecture, It's used in the app layer.

### Model:
* Handles the logic for our application data, It can contain code to retreive or store data.

### View:
* Represents the parts of the application that handle displaying of data (JSON)

### Controller:
* Handles the interaction between the view and the model, including user input.
