# JavaScript

- [JavaScript](#javascript)
  - [Basic Data types](#basic-data-types)
    - [Numbers](#numbers)
    - [String](#string)
    - [Other types](#other-types)
  - [Variables](#variables)
  - [Methods](#methods)

## Basic Data types

### Numbers

- Examples

    ```js
    >>> 10
    >>> 20.2
    >>> -13
    ```

- Operands

    ```js
    // Summation
    >>> 10 + 10
    20

    // Subtraction
    >>> 20-10
    10

    // Multiplication
    >>> 2*4
    8

    // Division
    >>> 8/2
    4

    // Exponents
    >>> 2 ** 4
    16

    // Modulo
    >>> 6%3
    0
    ```

### String

- Examples

    ```js
    >>> "Hello"
    >>> "10"
    ```

- Concatenation

    ```js
    >>> "Hello" + "World"
    "HelloWorld"
    ```

- Indexing

    ```js
    >>> "World"[3]
    l
    ```

- Attributes

    ```js
    // String length
    >>> "Hello".length
    5
    ```

- Escape characters

    ```js
    >>> "hello \n start a new line"
    "hello \
    start a new line"

    >>> "hello \t give me a tab"
    "hello  give me a tab"

    >>> "hello \"quotes\" "
    'hello "quotes" '
    ```

### Other types

- Boolean:
  - true
  - false
- undefined
- null

## Variables

- Variables in JavaScript doesn't need to be declared. (AKA. its type is identified).
- Variables can be defined, initialized and assigned.
- A variable is initialized with keyword `var`, and then the variable name. Variable initialization can end by an optional semicolon.

    ```js
    // Variable declaration
    >>> var bankAccount

    // Variable assignation
    >>> bankAccount = 100;
    100

    // Variable initialization
    >>> var deposit = 50

    // Variable recall
    >>> var total = bankAccount + deposit
    >>> total
    150
    ```

## Methods

- Basics

```js
// Show an alert pop up message on screen
>>> alert("This is an alert!")

// log an output to the browser's console
>>> console.log("Test Test")

// Show a prompt message to the user
>>> var age = prompt("Enter your age:")
```
