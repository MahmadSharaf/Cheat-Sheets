# JavaScript

- [JavaScript](#javascript)
  - [Basic Data types](#basic-data-types)
    - [Numbers](#numbers)
    - [String](#string)
    - [Other types](#other-types)
  - [Variables](#variables)
  - [Methods](#methods)
  - [Comparison operators](#comparison-operators)
  - [Control flow](#control-flow)
    - [If condition](#if-condition)
  - [While loop](#while-loop)
  - [For loop](#for-loop)

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

## Comparison operators

```js
// Greater Than
>>> 3 > 2;
true
>>> 2 > 3;
false

// Less Than
>>> 1 < 2;
true

// Greater than or equal to
>>> 2 >= 2;
true

// Less than or equal to
>>> 1 <= 3;
true

// Equality
>>> 2 == 2;
true
>>> "username" == "username";
true

// Inequality
>>> 2 != 3;
true

// JS uses type coercion! This means it will try it's best to convert objects
// to similar data types to perform the comparison! A lot of times you don't
// actually want that!
>>> "2" == 2;
true

// Check equality of value and type
>>> 5 === 5;
true
>>> 5 === "5";
false

>>> true == 1;
true
>>> true === 1;
false

>>> false == 0;
true
>>> false === 0;
false

// Check for Inequality of value and type
>>> 5 !== "5";
true
>>> 5 !== 5;
false

// Weird behavior for null, undefined, and NaN values!

>>> null == undefined;
true

>>> NaN == NaN;
false
```

- Logical Operators
  - Logical Operators allow us to combine multiple comparison Operators!

```js

// AND is written with &&
// Need both conditions to be true to return true
>>> 1 === 1 && 2 ===2;
true

// OR is written with ||
// Need only one condition to be true to return true
>>> 1 === 2 || 1 ===1;
true

// NOT is written with !
// Basically a way of checking the opposite of a condition
>>> !(1===1);
false
// Can also stack these (not super common)
>>> !!(1===1);
true
```

## Control flow

### If condition

```js
if (temp > 80){
    console.log("Hot outside!")
} else if(temp <= 80 && temp >= 50){
    console.log('Nice outside!')
} else{
    console.log("Its really cold outside!")
}
```

## While loop

```js
while (condition){
    // Code executed here
    // while condition is true
}
```

## For loop

- There are three types of For loop
  - `for` - loops through a block of code a number of times.
  - `for/in` - loops through elements of an object sequence.
  - `for/of`

- `for` loop syntax

```js
for (statement 1; statement 2; statement 3) {
//     code block to be executed
}
// Statement 1 is executed before the loop (the code block) starts.
//
// Statement 2 defines the condition for running the loop (the code block).
//
// Statement 3 is executed each time after the loop (the code block) has been executed.

// Example 1
for (i = 0; i < 5; i=i+1) {
    console.log("Number is " + i );
}

// Example 2
var word = "ABCDEFGHIJK"
for (i = 0; i < word.length; i++) {
    console.log(word[i]);
}
```
