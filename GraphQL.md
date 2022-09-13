# GraphQL cheat sheet

- [GraphQL cheat sheet](#graphql-cheat-sheet)
  - [What GraphQL is](#what-graphql-is)
  - [Schema](#schema)
    - [Query](#query)
    - [Mutation](#mutation)
    - [Subscription](#subscription)
  - [Architecture](#architecture)

## What GraphQL is

- GraphQL is a new API standard that provides a more efficient, powerful and flexible alternative to REST
- At its core, GraphQL enables declarative data fetching where a client can specify exactly what data it needs from an API.
- GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.
- GraphQL minimizes the amount of data that needs to be transferred over the network and thus majorly improves applications operating under these conditions.

## Schema

- GraphQL has its own type system that's used to define the schema of an API.
- The syntax for writing schemas is called the Schema Definition Language, or short SDL.
- In the below example, there are two types "Person" and "Post".

    ```graphql
    type Person {
        name: String! 
        age: Int!
    }

    type Post {
        title: String!
    }
    ```

  - "Person" has two fields "name" and "age" of types "string" and "int", the exclamation mark "!" means that the field is required.
  - "Post" has one field "title" of type "string" and is required.
  - These two types can get related together as below:

    ```graphql
    type Person {
        name: String! 
        age: Int!
        posts: [Post!]!
    }

    type Post {
        title: String!
        author: Person!
    }
    ```

  - Person has a new field "posts" of type "list of Type Post". And Post has a new field "author" of type "Person".
  - This created many to one relationship.
- The schema is one of the most important concepts when working with a GraphQL API.
- It specifies the capabilities of the API and defines how clients can fetch and update data.
- Each schema will have some root types that define the entry points for the API. These root types are, the Query, the Mutation, and the Subscription types.

### Query

- Requesting data is not coupled to the API endpoint, instead GraphQL has a single endpoint and the request payload determines the shape of the data received from the server.
- In a GraphQL query each field can have zero or more arguments if that is specified in the GraphQL schema.
- In the below example, it shows the schema for querying Person type. It starts with "type Query" to state that it is a Query object. Then the root field name of the query "allPersons" followed by the Type that will be sent, which in our case a list of Person Type.

```graphql
type Query {
    allPersons(last: Int): [Person!]!
}
```

- For example, the following request payload contains a root field "allPersons" followed by the query payload.

```graphql
allPersons(last:2) {
    name
    posts{
        title
    }
}
```

- This payload will return the name of the last two Persons and the title of their Posts.

### Mutation

- It is way of changing to the data in the server.
- There are three types of mutations:
  - creating new data
  - updating existing data
  - deleting existing data
- Mutations generally follow the same syntactical structure as queries but they always need to start with a mutation keyword.
- In the below example, it shows the schema for mutating Person type. It starts with "type Mutation" to state that it is a Mutation object. Then the root field name of the mutation "createPerson" followed by the arguments of the Type "(name: String!, age: String!)" and the Type itself "Person!".

```graphql
type Mutation {
    createPerson(name: String!, age: String!): Person!
}
```

- For example, it is possible to create a new person as below. It contains a root field "createPerson" which has the values of the record, followed by the payload. This payload is considered a query to the server. This helps to have a "mutation" and query in a single request to the server.

```graphql
mutation {
    createPerson(name: "Sharaf", age: 32) {
        id
    }
}
```

### Subscription

- It is used to create a steady connection between the server and the client.
- It is used to update the client with any new events occurred on the server side.
- It has the same syntactical structure as queries but they always need to start with a "subscription" keyword.
- In the below example, it shows the schema for subscription type. It starts with "type Subscription" to state that it is a Subscription object. Then the root field name of the subscription "newPerson" followed by the arguments of the Type "{name, age}".

```graphql
type subscription {
    newPerson: Person!
}
```

- In the below example, the client subscribes on the server to get informed about new users being created.

```graphql
subscription {
    newPerson {
        name
        age
    }
}
```

## Architecture

- GraphQL, as a concept, is just a specification. This means that GraphQL is, in fact, not more than a long document that describes in detail how a GraphQL server has to behave, meaning what kinds of requests it should accept and what the response format for these requests has to look like. The specification for GraphQL can be found [here](http://spec.graphql.org/).
- GraphQL to be used in a project, it has to be built from scratch. It can be built in any programming language with the help of any of the available reference implementations for it.
- GraphQL is actually transport-layer agnostic. This means it can potentially be used with any available network protocol. So, it is definitely possible to implement a GraphQL server based on TCP, WebSockets, or any other transport.
- GraphQL also doesn't care about the database or the format that is used to store the data.
- There are three common architectural use cases for GraphQL:
  1. GraphQL server with a connected database
     - It is the most common for greenfield projects.
     - Uses a single web server that implements the GraphQL.
     - The server resolves queries and constructs response with data that it fetches from the database.
  2. GraphQL server to integrate with existing or legacy systems.
     - It can be used to unify existing systems and hide their complexity of data fetching logic behind a GraphQL API. This way, new client applications can be developed that simply talk to the GraphQL server to fetch the data they need. The server is then responsible to make sure it fetches the data from the existing systems and packages it up in the GraphQL response format.
     - The server doesn't care about what the data sources are (databases, web services ,3rd party APIs, ..)
  3. A hybrid approach with a connected database and integration of existing systems.
     - In this architecture, when a query is received by the server, the server will resolve it and either retrieve the required data from the connected database or from the integrated APIs.
- The key to understanding how GraphQL is able to cope with all these different environments is the concept of a resolver function.
  - GraphQL queries/mutations consist of set of fields
  - Its server has one resolver function per field
  - The purpose of each resolver is to retrieve the data to its corresponding field