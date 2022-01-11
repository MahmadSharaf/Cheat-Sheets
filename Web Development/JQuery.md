# jQuery Cheat Sheet

## What jQuery is

- jQuery is an extremely popular JavaScript library meant to make a number of common javaScript tasks simpler ,via a consistent API across all browsers.

## Syntax

In order to use jQuery, you need to use jQuery Objects.

```js
function loadData() {

    var $body          = $('body');
    var $wikiElem      = $('#wikipedia-links');
    var $nytHeaderElem = $('#nytimes-header');
    var $nytElem       = $('#nytimes-articles');
    var $greeting      = $('#greeting');
}
```

- `var` initiates a new variable.
- `$` in the variable name, it is just a character that identify that this object is a jQuery object.
- `$` after the `=` to select an html object with jquery. Which is a pointer to a jquery object.
- `( )` inside the parenthesis, a string of the element that needs to be selected.

## methods

### 1. jQuery's [.ajax()](http://api.jquery.com/jquery.ajax/) method

### 2. jQuery's [.getJSON()](http://api.jquery.com/jquery.getjson/) method
