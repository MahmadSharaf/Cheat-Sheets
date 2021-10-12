# Python Cheat sheet

- [Python Cheat sheet](#python-cheat-sheet)
  - [Module Importing](#module-importing)
    - [Using `import` statement](#using-import-statement)
    - [Using `reload` function vs `import`](#using-reload-function-vs-import)
    - [Using `from` statement vs `import`](#using-from-statement-vs-import)
    - [Using exec to Run Module Files](#using-exec-to-run-module-files)
  - [Data types](#data-types)
    - [Strings](#strings)
      - [Indexing](#indexing)
      - [Slicing](#slicing)
      - [String Mutability](#string-mutability)
      - [String Conversion Tools](#string-conversion-tools)
      - [String Formatting](#string-formatting)
      - [Advanced String Formatting](#advanced-string-formatting)
      - [Strings tips and tricks](#strings-tips-and-tricks)
      - [String References](#string-references)
    - [Lists](#lists)
      - [Mutability](#mutability)
        - [Assignment](#assignment)
      - [Lists Specific Operations](#lists-specific-operations)
      - [Lists Nesting](#lists-nesting)
      - [Comprehensions and Generators](#comprehensions-and-generators)
    - [Dictionaries](#dictionaries)
      - [Common dictionary literals and operations](#common-dictionary-literals-and-operations)
      - [Dictionary methods](#dictionary-methods)
      - [Dictionary comprehensions](#dictionary-comprehensions)
      - [Dictionary views](#dictionary-views)
      - [Dict Nesting](#dict-nesting)
      - [Dict Tricks](#dict-tricks)
      - [Iteration and Optimization](#iteration-and-optimization)
    - [Tuples](#tuples)
      - [Common tuple literals and operations](#common-tuple-literals-and-operations)
      - [Conversions, methods, and immutability](#conversions-methods-and-immutability)
      - [Tricks](#tricks)
    - [Namedtuples](#namedtuples)
      - [Common namedtuple literals and operations](#common-namedtuple-literals-and-operations)
      - [Namedtuple Conversion Operations](#namedtuple-conversion-operations)
      - [Namedtuples references](#namedtuples-references)
    - [Sets](#sets)
      - [Sets Operations](#sets-operations)
      - [Sets Comprehensions](#sets-comprehensions)
      - [Sets Tricks](#sets-tricks)
    - [Common operations/methods for data types](#common-operationsmethods-for-data-types)
  - [Dealing with files and folders](#dealing-with-files-and-folders)
    - [Binary Bytes Files](#binary-bytes-files)
  - [While loop](#while-loop)
  - [Tricks](#tricks-1)
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
  - [Data Structures](#data-structures)
    - [NumPy](#numpy)
      - [NumPy Modules](#numpy-modules)
    - [Pandas](#pandas)
      - [Input/Output](#inputoutput)
        - [Read and Write from CSV](#read-and-write-from-csv)
        - [Read and write from Excel](#read-and-write-from-excel)
        - [Read and Write to SQL Query or Database Table](#read-and-write-to-sql-query-or-database-table)
      - [Retrieving Information](#retrieving-information)
        - [Basic Information](#basic-information)
        - [Summary](#summary)
      - [Data Wrangling](#data-wrangling)
        - [Creating Data Frame](#creating-data-frame)
        - [Reshaping Data](#reshaping-data)
        - [Subset Observations (rows)](#subset-observations-rows)
        - [Subset Variables (Columns)](#subset-variables-columns)
        - [Subset row and column](#subset-row-and-column)
      - [Handling Missing Data](#handling-missing-data)
      - [Group Data](#group-data)
      - [Sort and Rank](#sort-and-rank)
      - [Applying functions](#applying-functions)
      - [Plotting](#plotting)
      - [Pandas Tips and Tricks](#pandas-tips-and-tricks)
      - [Logic in Python](#logic-in-python)
      - [Regular Expressions Examples](#regular-expressions-examples)
      - [Pandas References](#pandas-references)
    - [Matplotlib](#matplotlib)
      - [Create Plot](#create-plot)
      - [Plotting Routines](#plotting-routines)
      - [Customize Plot](#customize-plot)
      - [Save Plot](#save-plot)
      - [Show Plot](#show-plot)
      - [Close & Clear](#close--clear)
      - [Matplotlib references](#matplotlib-references)
    - [Seaborn](#seaborn)
      - [Import seaborn library](#import-seaborn-library)
      - [Basic Steps for creating plots with Seaborn](#basic-steps-for-creating-plots-with-seaborn)
        - [Step 1: Prepare the data](#step-1-prepare-the-data)
        - [Step 2: Figure Aesthetics](#step-2-figure-aesthetics)
        - [Step 3: Plotting](#step-3-plotting)
        - [Step 4: Further Customizations](#step-4-further-customizations)
        - [Step 5: Show, Save, Close](#step-5-show-save-close)
      - [Seaborn References](#seaborn-references)
    - [Resources](#resources)
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

## Module Importing

### Using `import` statement

- Imports working only once per module per session by default. Later imports will do nothing, even the module is changed.
  
  ```py
  # File 'script1' contains the below code
  print(2**100)
  print('Spam!'*10)
  ```
  
  ```cmd
  >>> import script1
  1267650600228229401496703205376
  Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
  >>> import script1
  >>> import script1
  ```

- This is by design; imports are too expensive operation to repeat more than once per file, per program run. As, imports must find files, compile them to byte code, and run the code.

### Using `reload` function vs `import`

```cmd
>>> import script1
1267650600228229401496703205376
Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
>>> import script1
>>> from importlib import reload

...Change script1.py in a text edit window to print 2 ** 16..

>>> reload(script1)
65536
Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
<module 'script1' from '.\\script1.py'>
```

### Using `from` statement vs `import`

- `from` statement in a sense defeats the namespace partitioning purpose of modules—because the from copies variables from one file to another, it can cause same-named variables in the importing file to be overwritten, and won’t warn you if it does. This essentially collapses namespaces together, at least in terms of the copied variables
  
  ```py
  # File 'threenames.py'
  a = 'dead'                      # Define three attributes
  b = 'parrot'                    # Exported to other files
  c = 'sketch'
  print(a, b, c)                  # Also used in this file (in 2.X: print a, b, c)
  ```
  
  ```cmd
  >>> from threenames import a,b
  >>> a
  'dead'
  >>> b
  'parrot'
  ```
  
  ```cmd
  >>> import threenames
  >>> threenames.a
  'dead'
  >>> threenames.c
  'sketch'
  ```

### Using exec to Run Module Files

- The exec(open('module.py').read()) built-in function call is another way to launch files from the interactive prompt without having to import and later reload. Each such exec runs the current version of the code read from a file, without requiring later reloads
  
  ```cmd
  >>> exec(open('script1.py').read())
  win32
  65536
  Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
  
  ...Change script1.py in a text edit window to print 2 ** 32...
  
  >>> exec(open('script1.py').read())
  win32
  4294967296
  Spam!Spam!Spam!Spam!Spam!Spam!Spam!Spam!
  ```

## Data types

### Strings

- Immutable (they cannot be changed).
- Sequences (Can be indexed and sliced).

```python
# Join: joins two strings together
result = '1234'.join("567")
===
result = '1234' + '567'
# result = "1234567"

# Methods
s = "apple"
s.startswith("a")
# True
s.endswith("e")
# True
s.isdigit()
# False
s.isspace()
# False
s.lower()
# 'apple'
s.upper()
# 'APPLE'
len(s)
# 5
"box" in "box of life"
# True
1 in [1,2,3]
# True
'abracadabra'.find('cad')
# 4
'badger badger badger mushroom'.count('bad')
# 3
```

#### Indexing

```py
s[0]
# 'a'
s[-1]
# 'e'
s[len(s)-1]
# 'e'
s[-2]
# 'p'
```

#### Slicing

```py
s[1:3]
# 'pp'
s[1:]
# 'pple'
s[:3]
# 'app'
s[:-1]
# 'appl'
```

- Slicing with step size

```py
s[1:3:2]
# 'p'
s[3:1:-2]
# 'l'
```

#### String Mutability

- Strings are Immutable. They can not be changed in place

```py
S = 'Sharaf'

S[0] = 'z'   # Immutable objects cannot be changed
# ...error text omitted...
# TypeError: 'str' object does not support item assignment
```

- Ways to change strings

```py
S = 'Sharaf'
'z' + S[1:]   # But we can run expressions to make new objects
# 'zpam'


L = list(S)    # Expand to a list: [...]
L

# ['s', 'h', 'a', 'r', 'a', 'f']

L[2] = 'e'  # Change it in place
''.join(L)  # Join with empty delimiter
# 'sheraf'

S.replace('a','e')
# 'Sheref'
```

- Or use `bytearray`, which is mutable and so may be changed in place. `bytearray` objects aren’t really text strings; they’re sequences of small, 8-bit integers. However, they support most of the same operations as normal strings and print as ASCII characters when displayed.

```py
B = bytearray(b'spam')  # A bytes/list hybrid (ahead)
B.extend(b'eggs')    # 'b' needed in 3.X, not 2.X
B  
# bytearray(b'spameggs')
B.decode()  # Translate to normal string
# 'spameggs'

B[1] = ord('c')
B.decode()
# 'scameggs'
```

#### String Conversion Tools

- The `int` function converts a string to a number.
- The `float` function converts a string to a float number.
- The `str` function converts a number to its string representation.
- The `repr` function converts an object to its string representation, but returns the object as a string of code that can be rerun to recreate the object.
- The `eval` function runs a string containing Python expression code.
- The `ord` function converts a character to ASCII or Unicode
- The `chr` function converts an ASCII number to the character.
- The `ascii` function same as repr(), return a string containing a printable representation of an object, but escape the non-ASCII characters in the string returned by repr()

```py
int("42"), str(42)
# (42, '42')

str('spam'), repr('spam')
# ('spam', "'spam'")
```

#### String Formatting

Credits to this, goes to "SShah" as an answer to [StackOverflow question](https://stackoverflow.com/questions/52155591/how-to-insert-string-into-a-string-as-a-variable)

There are 5 approaches for achieving this on python (Python 3):

1. Concatenation:

   You can do this using + for joining 2 strings, however you can only concatenate string type data, meaning non string type data needs to be converted to string using the str() function. For example:

   ```py
   print("The Enemy's health is " + str(EnemyHealth) + ". The Enemy is " + EnemyIs + ".")
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

   or multiplying the same string

   ```py
   print('='*10)
   # ==========
   ```

2. Taking advantage of Python 3's print() function which can take multiple parameter arguments:

   Here your `print()` statement similar to the concatenation statement above, except where ever I use + to concatenate you need to replace it with ,. The advantage of using this, is that different data types will be automatically converted to string, i.e. no longer needing the str() function. For example:

   ```py
   print("The Enemy's health is ", EnemyHealth, ". The Enemy is ", EnemyIs, ".")
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

3. `%` Operator:

   - Same syntax for `printf` function of c-programming language.
   - Add `%` and one of the types of below table next to it, ex: %d, inside a string. To be replaced with values, beside `%`, where stated after the string.
   - The values, if more than one, should be inside brackets and separated with a comma. Same as tuples.
   - Conversion Types:

      | Code| Meaning|
      | ------ | ------ |
      |d|Decimal (base-10 integer)|
      |i|Integer|
      |o|Octal integer (base 8)|
      |u|Same as d (obsolete: no longer unsigned)|
      |x|Hex integer (base 16)|
      |X|Same as x, but with uppercase letters|
      |e|Floating point with exponent, lowercase|
      |E|Same as e, but uses uppercase letters|
      |f|Floating-point decimal|
      |F|Same as f, but uses uppercase letters|
      |g|Floating-point e or f (defaults to 6 precision-point)|
      |G|Floating-point E or F (defaults to 6 precision-point)|
      |c|Character (int or str)|
      |r|Same as s, but uses repr, not str|
      |s|String (or any object’s str(X) string)|
      |%|Literal % (coded as %%)|

   ```py
   print("The Enemy's health is %d. The Enemy is %s." % (EnemyHealth, EnemyIs))
   # output = "The Enemy's health is 0. The Enemy is dead."
   ```

4. `format()` Method:

   - The `format()` method for python strings.
   - This is a built-in method for all strings in python, which allow you to easily replace the placeholder {} within python strings, with any variables.
   - Unlike modulo operator, this `format()` method doesn't require to express or convert different data types to string, as it would automatically do this.
   - **{[name][component][!conversion][:format_spec]}**
     - **[name]**: indicates which argument from the argument list is inserted into the Python format string in the given location.

        ```py
        print("The Enemy's health is {}. The Enemy is {}.".format(0, 'dead'))
        
        # OR
        
        print("The Enemy's health is {0}. The Enemy is {1}.".format(0, 'dead'))
        
        # OR
        
        print("The Enemy's health is {Health}. The Enemy is {Status}.".format(Health=0, Status='dead'))
        
        # output = "The Enemy's health is 0. The Enemy is dead."
        ```

     - **[component]**: is a string of zero or more “.name” or “[index]” references used to fetch attributes and indexed values of the argument, which may be omitted to use the whole argument value.

       - Access an element inside a list

         ```py
         a = ['foo', 'bar', 'baz']
         '{0[0]}, {0[2]}'.format(a)
         # 'foo, baz'
         ```

       - Access key-reference in dictionary

         ```py
         d = {'key1': 'foo', 'key2': 'bar'}
         
         '{0[key1]}'.format(d)
         # 'foo'

         '{my_dict[key2]}'.format(my_dict=d)
         # 'bar'
         ```

       - Access Object attributes

         ```py
         z = 3+5j

         'real = {0.real}, imag = {0.imag}'.format(z)
         # 'real = 3.0, imag = 5.0'
         ```

   - **[!conversion]**: used to convert string using three different built-in functions

      |Value|Meaning|
      |-----|-------|
      | !s  | Convert with str() |
      | !r  | Convert with repr()|
      | !a  | Convert with ascii()|

      ```py
      '{0!s}'.format(42)
      # '42'
      '{0!r}'.format(42)
      # '42'
      '{0!a}'.format(42)
      # '42'
      ```

   - `:<format_spec>` for advanced string control discussed in the next section. They represented as :[[fill]align][sign][#][0][width][group][.prec][type]

5. F-Strings

   - F-strings are introduced in python 3.6+, , to substitute variables within a string.
   - This method is similar to the the `.format()` method described above, and in my opinion is a better upgrade to the str.format() method.
   - To use this method, state `f` before the opening quote when defining a string and then, within the string use the format, {[variable name goes here]} for this to work.

   ```py
   print(f"The Enemy's health is {EnemyHealth}. The Enemy's tall avg  {EnemyAvg:.2f}.")
   # output = "The Enemy's health is 0. The Enemy's tall avg 181.21."
   ```

   - By using this method, the variable name is being instantiated directly within the curly brackets {}.
   - Limitations:
     - F-string expression can’t contain a backslash (`\`) character. You can get around this limitation by creating a temporary variable that contains the escape sequence you want to insert.
     - An expression in an f-string that is triple-quoted can’t contain comments

   For more [info](https://realpython.com/python-f-strings/#simple-syntax)

#### Advanced String Formatting

1. `%` Operator:
   - **%[(key name)][flags][width][.precision]conversion type %values**
    1. **%**: Required. The ‘%’ character, which marks the start of the specifier.
    2. **(key name)**: Optional. A key for indexing the dictionary used on the right side of the expression

         ```py
         '%(name)s' %{'name':'Sharaf'}
         # 'Sharaf'

         reply = """
         My name is %(name)s!
         My age is %(age)s
         """

         values = {'name': 'Sharaf', 'age': 30}
         print(reply % values) 
         # My is Sharaf!
         # My age is 30
         ```

    3. **flags**: Optional. Conversion flags, which affect the result of some conversion types.
       - `#`: The value conversion will use the “alternate form”

         ```py
         "%x" % 17
         # '11'
         "%#x" % 17
         # '0x11
         ```

       - `0`: The conversion will be zero padded for numeric values.

         ```py
         "%03d" % 1
         # '003'
         ```

       - `-`: The converted value is left adjusted (overrides the ‘0’ conversion if both are given).

         ```py
         "%-5d" % 1
         # '1    '
         ```

       - ` `: A blank should be left before a positive number (or empty string) produced by a signed conversion.

         ```py
         '%d' % 1
         # '1'
         '% d' % 1
         # ' 1'
         ```

       - `+`: A sign character ('+' or '-') will precede the conversion (overrides a “space” flag).

         ```py
         '%+d' % 1
         #'+1'
         '%+d' % -1
         #'-1'
         ```

    4. **width**: Optional. Minimum field width. If specified as an ‘*’ (asterisk), the actual width is read from the next element of the tuple in values, and the object to convert comes after the minimum field width and optional precision.

         ```py
         '%10d' %(150)
         # '       150'
         '%*d' %(10,150)
         # '       150'
         ```

    5. **precision**: Optional. Precision, given as a ‘.’ (dot) followed by the precision. If specified as ‘*’ (an asterisk), the actual width is read from the next element of the tuple in values, and the value to convert comes after the precision.

         ```py
         '%.10f' %(1.5)
         # '1.5000000000'
        '%.*f' %(10,1.5)
         # '1.5000000000'
         ```

         ```py
         # 1
         dict = {'Name':'Sharaf','Age':30}
         "My name is %(Name)s and I have %(Age)s years old" %(dict)
         # 'My name is Sharaf and I have 30 years old'

         # 2
         x = 123.456
         f'{x:010}'
         # '000123.456'
         f'{x:10}'
         # '   123.456'
         f'{x:+10}'
         # '  +123.456'
         ```

   [Reference](https://python-reference.readthedocs.io/en/latest/docs/str/formatting.html)

2. `format()` method:
   - **:[[fill]align][sign][#][0][width][group][.prec][type]**
   1. `:`: Separates the <format_spec> from the rest of the replacement field

   2. **align**: Specifies how to justify values that don’t occupy the entire field width
      - `<`: left-justified
      - `>`: right-justified
      - `^`: centered
      - `=`: (Numeric Only) When numeric output includes a sign, it appears at the left edge of the output field, and padding is placed in between the sign and the number.

         ```py
         '{0:+8d}'.format(123)
         # '    +123'
         '{0:=+8d}'.format(123)
         # '+    123'
         ```

   3. **fill**: Specifies how to pad values that don’t occupy the entire field width

         ```py
         '{0:->8s}'.format('foo')
         # '-----foo'
         '{0:#<8d}'.format(123)
         # '123#####'
         '{0:*^8s}'.format('foo')
         # '**foo***'
         ```

       - If you specify a value for `<fill>`, then you should also include a value for `<align>` as well.

   4. **sign**: Controls whether a leading sign is included for numeric values

      ```py
      '{0:+6d}'.format(123)
      # '  +123'
      '{0:+6d}'.format(-123)
      # '  -123'

      '{0:-6d}'.format(123)
      # '   123'
      '{0:-6d}'.format(-123)
      # '  -123'

      '{0:*> 6d}'.format(123)
      # '** 123'
      '{0:*>6d}'.format(123)
      # '***123'
      '{0:*> 6d}'.format(-123)
      # '**-123'
      ```

   5. **`#`**: The value conversion will use the “alternate form”

      ```py
      '{0:b}, {0:#b}'.format(16)
      # '10000, 0b10000'
      '{0:o}, {0:#o}'.format(16)
      # '20, 0o20'
      '{0:x}, {0:#x}'.format(16)
      # '10, 0x10'
      '{0:.0f}, {0:#.0f}'.format(123)
      # '123, 123.'
      '{0:.0e}, {0:#.0e}'.format(123)
      # '1e+02, 1.e+02'
      ```

   6. **`0`**: The conversion will be zero padded for numeric values instead of ASCII.

      ```py
      '{0:05d}'.format(123)
      # '00123'
      '{0:08.1f}'.format(12.3)
      # '000012.3'
      
      '{0:>06s}'.format('foo')
      # '000foo'

      '{0:*>05d}'.format(123)
      # '**123'
      ```

   7. **width**: Specifies the minimum width of the output

      ```py
      '{0:8s}'.format('foo')
      # 'foo     '
      '{0:8d}'.format(123)
      # '     123'

      '{1:{0}f}'.format(10, 123.456)
      # '123.456000'
      ```

   8. **group**: Specifies a grouping character for numeric output

      ```py
      '{0:,d}'.format(1234567)
      # '1,234,567'
      '{0:_b}'.format(0b111010100001)
      # '1110_1010_0001'
      ```

   9. **.prec**: Specifies the number of digits after the decimal point for floating-point presentation types, and the maximum output width for string presentations types

      ```py
      '{0:8.2f}'.format(1234.5678)
      # ' 1234.57'
      '{0:8.4f}'.format(1.23)
      # '  1.2300'

      '{:.4s}'.format('foobar')
      # 'foob'

      '{2:{0}.{1}f}'.format(10, 2, 123.456)
      # '    123.46'
      ```

   10. **type**: Specifies the presentation type, which is the type of conversion performed on the corresponding argument.

      - Differences between Modulo operator

         |Type| `.format()` Method | `%` Operator |
         | -- | -- | -- |
         | b  | Designates binary integer conversion | Not supported
         | i,u| Not supported | Designates integer conversion
         | c  | Designates character conversion, and the corresponding value must be an integer | Designates character conversion, but the corresponding value may be either an integer or a single-character string
         | g,G| Chooses between floating point or exponential output, but the rules governing the choice are slightly more complicated | Chooses between floating point or exponential output, depending on the magnitude of the exponent and the value specified for `<prec>`|
         |r, a| Not supported (though the functionality is provided by the !r and !a conversion components in the replacement field) | Designates conversion with repr() or ascii(), respectively
         | %  | Converts a numeric argument to a percentage | Inserts a literal '%' character into the output

3. F-string:
   - All the `<format_spec>` components that work with .format() also work with f-strings.

#### Strings tips and tricks

- Adding `r` before a string, treating it as a raw.
  
  ```py
  print(r'The n in "\n" will be printed not parsed as a new line')
  # The n in "\n" will be printed not skipped
  ```

- Built-in function `repr()`, converts objects to display strings.
  
  ```py
  repr('lion')
  # "'lion'"
  ```
#### String References

- [Real Python](https://realpython.com/python-formatted-output/)
- Python [format cookbook](https://mkaz.blog/code/python-string-format-cookbook/)

### Lists

- Mutable: changed in place.
- Index and slice Assignment
- Sequences: supports indexing, slicing, and concatenation.
- Store object references (not copies, unless asked explicitly)

#### Mutability

Mutable. That means you can change the items in a list after it has been created.

   ```python
   words = ["echidna", "dingo", "crocodile", "bunyip"]

   len(words)
   # 4

   words[0]
   # 'echidna'

   words[-1]
   # 'bunyip'

   words + [4, 5.4]
   # ["echidna", "dingo", "crocodile", "bunyip", 4, 5.4]

   words * 2
   # ["echidna", "dingo", "crocodile", "bunyip", "echidna", "dingo", "crocodile", "bunyip"]
   ```

##### Assignment

- Both index and slice assignments are in-place changes—they modify the subject list directly, rather than generating a new list object for the result.

1. Index Assignment

   ```py
   L = [1,2,3,4]
   L[1] = 1
   L
   # [1,1,3,4]
   ```

2. Slice Assignment

   ```py
   L[0:2]=[0,1,2] # Insertion/Replacement
   L
   # [0,1,2,3,4]

   L[1:1] = [0.5] # Insertion
   L
   # [0,0.5,1,2,3,4]

   L[1:2] = [] # Deletion
   L
   # [0,1,2,3,4]
   ```

- It can be though as a combination of two steps:
  - Deletion of the part specified on the left "`L[1:2]`"
  - Insertion of the items on the right "`[0,1,2]`" at the place where the old slice was deleted.
- This isn’t what really happens, but it can help clarify why the number of items inserted doesn’t have to match the number of items deleted.

#### Lists Specific Operations

- Growing:

   ```py
   words = ["echidna", "dingo", "crocodile", "bunyip"] 
   # Adds its argument as a single item to the end of the list.
   words.append("platypus")
   
   # Treats its argument as a sequence and adds each item in the sequence to the end of the list. In other words, it adds a sequence of items to a list.
   words.extend("abc")
   # ['echidna', 'dingo', 'crocodile', 'bunyip', 'platypus', 'a', 'b', 'c']

   # Adds each item of this list to the end of the words list
   words.extend(["kangaroo", "wallaby"])

   # Insert object before index.
   words.insert(1,'a')
   ```

- Searching:

   ```py
   # Return first index of value. Raises ValueError if the value is not present.
   words.index('a')
   # 1
   words.index('a',2)
   # 8
   words.count('a')
   # 2
   ```

- Sorting

   ```py

   # reverse the order of the list
   words.reverse()

   # Sort the list in ascending order
   words.sort()

   # The key argument gives a one-argument function that returns the value to be used in sorting
   words.sort(key=str.lower, reverse=True)
   ```

- Shrinking

   ```py
   words = ["echidna", "dingo", "crocodile", "bunyip"]
   # delete an item
   words.pop(2)
   # ["echidna", "dingo", "bunyip"]
   words.remove('echidna')
   # ["dingo", "bunyip"]

   del words[i]

   del words[i:j]

   words[i:j] = []

   words.clear()
   ```

#### Lists Nesting

```py
M = [[1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]]
```

#### Comprehensions and Generators

```py
col2 = [row[1] for row in M] # Collect the items in column 2
# [2, 5, 8]

[row[1] for row in M if row[1] % 2 == 0]  # Filter out odd items
# [2, 8]
```

```py
G = (sum(row) for row in M)   # Create a generator of row sums
next(G)  # iter(G) not required here
# 6
next(G)  # Run the iteration protocol next()
# 15
next(G)
# 24
```

```py
[ord(x) for x in 'spaam'] # List of character ordinals
# [115, 112, 97, 97, 109]
{ord(x) for x in 'spaam'} # Sets remove duplicates
# {112, 97, 115, 109}
{x: ord(x) for x in 'spaam'} # Dictionary keys are unique
# {'p': 112, 'a': 97, 's': 115, 'm': 109}
(ord(x) for x in 'spaam') # Generator of values
# <generator object <genexpr> at 0x000000000254DAB0>
```

### Dictionaries

- They are:
  - Accessed by key, not offset position.
    - They store objects by key instead of by relative position.
  - ~~Unordered~~ Ordered collections starting Python 3.7
  - Variable-length, heterogeneous, and arbitrarily nestable.
    - Can shrink and grow in place (without new copies being made).
    - Can contain any type of object
    - Can be nested into other dictionaries
  - Mutable that can change in place.
  - They are not sequences at all, but are instead known as mappings.
  - Tables of object references (hash tables)
    - Dictionaries are implemented as hash tables (data structures that support very fast retrieval), which start small and grow on demand.
  - They store object references (not copies, unless asked explicitly)
- They are not:
  - Sequences: because there’s no notion of ordering among their items, things like concatenation (an ordered joining) and slicing (extracting a contiguous section) simply don’t apply.

#### Common dictionary literals and operations

```py
# Empty dictionary
D = {}

# Two-item dictionary
D = {'name': 'Bob', 'age': 40}

# Nesting
E = {'cto': {'name': 'Bob', 'age': 40}}

# Alternative construction techniques:
## Keywords
D = dict(name='Bob', age=40)
## key/value pairs
D = dict([('name', 'Bob'), ('age', 40)])
## zipped key/value pairs
D = dict(zip(keyslist, valueslist))
## key lists
D = dict.fromkeys(['name', 'age'])

# Indexing by key
D['name']
E['cto']['age']

# Membership: key present test
'age' in D
```

#### Dictionary methods

```py
# Fetch all keys
D.keys()

# Fetch all values
D.values()

# Fetch all key+value tuples
D.items()

# copy (top-level)
D.copy()

# clear (remove all items)
D.clear()

# merge by keys
D.update(D2)
D |= D2 # Python 3.9

# concatenate two dicts and return a new dictionary
z = x | y          # NOTE: 3.9+ ONLY
z = {**x, **y}     # NOTE: 3.5+

# fetch by key, if absent default (or None)
D.get(key, default?)

# remove by key, if absent default (or error)
D.pop(key, default?)

# Insert key with a value of default. Return key value if present, else default
D.setdefault(key, default?)

# remove/return any (key, value) pair; etc.
D.popitem()

# Get dictionary length
len(D)

# Adding/Changing keys
D[key] = value

# Deleting entries by key
del D[key]
```

#### Dictionary comprehensions

```py
D = {x: x*2 for x in range(10)}
# {0: 0, 1: 2, 2: 4, 3: 6, 4: 8, 5: 10, 6: 12, 7: 14, 8: 16, 9: 18}
D = {x: x ** 2 for x in [1, 2, 3, 4]}
# {1: 1, 2: 4, 3: 9, 4: 16}
D = {k: v for (k, v) in zip(['a', 'b', 'c'], [1, 2, 3])}
# {'b': 2, 'c': 3, 'a': 1}
D = {c: c * 4 for c in 'SPAM'}
# {'S': 'SSSS', 'P': 'PPPP', 'A': 'AAAA', 'M': 'MMMM'}
```

#### Dictionary views

- `D.keys`, `D.values`, and `D.items`.

   ```py
   D = {'b': 2, 'c': 3, 'a': 1}

   K = D.keys()
   # dict_keys(['b', 'c', 'a'])
   V = D.values()
   # dict_values([2, 3, 1])
   D.items()
   dict_items([('b', 2), ('c', 3), ('a', 1)])
   ```

- They are:
  - Iterable,
  - Retain the original order of dictionary components,
  - and reflect future changes.

   ```py
   # Iterable
   for key in D: print(key)
   # b
   # c
   # a

   # reflect future changes
   del D['b']
   list(K)
   # ['c', 'a']
   ```

- They are not:
  - Lists
  - do not directly support operations like indexing or the list sort method,
  - and do not display their items as a normal list when printed

- `D.keys` return set-like object, and support set operations such as intersection and union.
- `D.values` are not set-like, since their items are not necessarily unique or immutable.
- `D.items` results are set-like, if their (key, value) pairs are unique and hashable (immutable).

```py
D = {'a': 1, 'b': 2, 'c': 3}

D.keys() & {'b'} # Intersect keys and set
# {'b'}
D.keys() & {'b': 1} # Intersect keys and dict
# {'b'}
D.keys() | {'b', 'c', 'd'} # # Union keys and set
# {'b', 'c', 'a', 'd'}

D = {'a': 1}

list(D.items()) # Items set-like if hashable
# [('a', 1)]
D.items() | D.keys() # Union view and view
# {('a', 1), 'a'}

D.items() | D # dict treated same as its keys
# {('a', 1), 'a'}

D.items() | {('c', 3), ('d', 4)} # Set of key/value pairs
# {('d', 4), ('a', 1), ('c', 3)}

dict(D.items() | {('c', 3), ('d', 4)}) # dict accepts iterable sets too
# {'c': 3, 'a': 1, 'd': 4}
```

#### Dict Nesting

```py
rec = {'name': {'first': 'Bob', 'last': 'Smith'},
           'jobs': ['dev', 'mgr'],
           'age':  40.5}

rec['name']   # 'name' is a nested dictionary
#{'last': 'Smith', 'first': 'Bob'}

rec['name']['last'] # Index the nested dictionary
#'Smith'

rec['jobs']   # 'jobs' is a nested list
#['dev', 'mgr']
rec['jobs'][-1]  # Index the nested list
#'mgr'

rec['jobs'].append('janitor')   # Expand Bob's job description in place
rec
#{'age': 40.5, 'jobs': ['dev', 'mgr', 'janitor'], 'name': {'last': 'Smith', 'first': 'Bob'}}
```

#### Dict Tricks

- Although Dictionaries aren't sequential, it can be `Print`ed in order with respect to keys

```py
D = {'a': 1, 'b': 2, 'c': 3}
# {'a': 1, 'c': 3, 'b': 2}

Ks = list(Ks)
Ks.sort()
for k in Ks: print(k, D[k])
# a 1
# b 2
# c 3

for key in sorted(D):
   print(key, D[key])
# a 1
# b 2
# c 3
```

- Search a dict by value instead of key

```py
table = {'1975': 'Holy Grail',
         '1979': 'Life of Brian',
         '1983': 'The Meaning of Life'}
[year for (year, title) in table.items() if title == 'Holy Grail']
# OR
[year for year in table if table[year] == 'Holy Grail']
# ['1975']
```

#### Iteration and Optimization

- In a nutshell, an object is *iterable* if it is either a physically stored sequence in memory, or an object that generates one item at a time in the context of an iteration operation—a sort of “virtual” sequence. More formally, both types of objects are considered *iterable* because they support the *iteration protocol* —they respond to the `iter` call with an object that advances in response to `next` calls and raises an exception when finished producing values.

### Tuples

- Immutable, like `strings` (can't changed in-place)
- Sequential, like `Lists`
- Ordered collections (main objects positions)
- Accessed by offset (indexing and slicing)
- Arrays of object references (store objects access points or references)
- Functionally, they’re used to represent fixed collections of items: the components of a specific calendar date, for instance.

#### Common tuple literals and operations

```py
# Empty tuple
T = ()

# A one-item tuple (not an expression)
T = (0,)

# A four-item tuple
T = (0, 'Ni', 1.2, 3)

# Another four-item tuple (same as prior line)
T = 0, 'Ni', 1.2, 3

# Nested tuples
T = ('Bob', ('dev', 'mgr'))

# Tuple of items in an iterable
T = tuple('spam')

# Index
T[i]

# index of index
T[i][j]

# slice
T[i:j]

# length
len(T)

# Concatenate
T1 + T2

# repeat
T * 3

# Iteration
for x in T: print(x)

# membership
'spam' in T
[x ** 2 for x in T]

# Search
T.index(value,[offset])

# Count
T.count(value)

# Named tuple extension type
namedtuple('Emp', ['name', 'jobs'])
```

#### Conversions, methods, and immutability

```py
# Conversion
L = list(T)
T = tuple(L)

# Sorting
L.sort()
T = tuple(L)
# OR
sorted(T)

```

#### Tricks

- Immutability applies only to the top level of the tuple itself, not its contents. A list inside a tuple, for instance, can be changed as usual
- Tuples can be used as dictionary keys
- Tuples can be unpacked using *

```py
{*range(4), 4, *(5, 6, 7)}
# {0, 1, 2, 3, 4, 5, 6, 7}
```

### Namedtuples

- A type of container like dictionaries called “namedtuple()” present in module, “collections“.
- They can be used similarly to struct or other common record types, except that they are immutable.
- Like dictionaries the1y contain keys that are hashed to a particular value. But on contrary, it supports both access from key value and iteration, the functionality that dictionaries lack.
- `namedtuples` should be used instead of `tuples` anywhere object notation will make the code more pythonic and more easily readable.

#### Common namedtuple literals and operations

```py
# Import from collections module
from collections import namedtuple 

# Declaring namedtuple()  
Student = namedtuple('Student',['name','age','DOB'])

# Adding values  
S = Student('Jack','19','2541997') 

# Access using index  
S[1]
# 19 
      
# Access using key   
S.name
# Jack

# Access using getattr
getattr(S,'DOB')
# 2541997

# _fields :- This function is used to return all the keynames of the namespace declared.
S._fields
('name', 'age', 'DOB')

# _replace() :- This function is used to change the values mapped with the passed keyname.
S._replace(name = 'Manjeet')
# Student(name='Manjeet', age='19', DOB='2541997')
```

#### Namedtuple Conversion Operations

```py
# Python code to demonstrate namedtuple() and
# _make(), _asdict() and "**" operator

# importing "collections" for namedtuple()
import collections

# Declaring namedtuple()
Student = collections.namedtuple('Student',['name','age','DOB'])

# Adding values
S = Student('Nandini','19','2541997')

# initializing iterable
li = ['Manjeet', '19', '411997' ]

# initializing dict
di = { 'name' : "Nikhil", 'age' : 19 , 'DOB' : '1391997' }

# using _make() to return namedtuple()
Student._make(li)
# Student(name='Manjeet', age='19', DOB='411997')

# using _asdict() to return an OrderedDict()
S._asdict()
# OrderedDict([('name', 'Nandini'), ('age', '19'), ('DOB', '2541997')]

# using ** operator to return namedtuple from dictionary
Student(**di)
# Student(name='Nikhil', age=19, DOB='1391997')
```

#### Namedtuples references

- [GeeksForGeeks](https://www.geeksforgeeks.org/namedtuple-in-python/)
- [StackOverflow](https://stackoverflow.com/questions/2970608/what-are-named-tuples-in-python)

### Sets

- Neither mappings nor sequences
- Unordered collections of unique and immutable objects.
  - Can be used to filter duplicates out of other collections, though items may be reordered in the process because sets are unordered in general.

```py
X = set('spam')  # Make a set out of a sequence in 2.X and 3.X
Y = {'h', 'a', 'm'} # Make a set with set literals in 3.X and 2.7
```

- Perform order-neutral equality tests by converting to a set before the test, because order doesn’t matter in a set.
  - Two sets are equal if and only if every element of each set is contained in the other, regardless of order.

```py
L1, L2 = [1, 3, 5, 2, 4], [2, 5, 3, 4, 1]
L1 == L2   # Order matters in sequences
# False
set(L1) == set(L2)  # Order-neutral equality
# True
sorted(L1) == sorted(L2)  # Similar but results ordered
# True
'spam' == 'asmp', set('spam') == set('asmp'), sorted('spam') == sorted('asmp')
# (False, True, True)
```

#### Sets Operations

- Support the usual mathematical set operations

```py
X = set('spam')
Y = {'h', 'a', 'm'}

X, Y # A tuple of two sets without parentheses
# ({'m', 'a', 'p', 's'}, {'m', 'a', 'h'})

X & Y   # Intersection
# {'m', 'a'}
X | Y   # Union
# {'m', 'h', 'a', 'p', 's'}
X - Y   # Difference
# {'p', 's'}
X > Y   # Superset
# False

X, Y # A tuple of two sets without parentheses
# ({'m', 'a', 'p', 's'}, {'m', 'a', 'h'})

X.intersection(Y)   # Intersection
# {'m', 'a'}
X.union(Y)   # Union
# {'m', 'h', 'a', 'p', 's'}
Y.issubset(X)   # Subset
# False
```

#### Sets Comprehensions

```py
# Set comprehensions in 3.X and 2.7
{n ** 2 for n in [1, 2, 3, 4]}  
#{16, 1, 4, 9}

>>> {x for x in 'spam'}                    # Same as: set('spam')
{'m', 's', 'p', 'a'}

# Set of collected expression results
{c * 4 for c in 'spam'}  
# {'pppp', 'aaaa', 'ssss', 'mmmm'}
{c * 4 for c in 'spamham'}
# {'pppp', 'aaaa', 'hhhh', 'ssss', 'mmmm'}

S = {c * 4 for c in 'spam'}
S | {'mmmm', 'xxxx'}
# {'pppp', 'xxxx', 'mmmm', 'aaaa', 'ssss'}
S & {'mmmm', 'xxxx'}
# {'mmmm'}
```

#### Sets Tricks

```py
S1 = {1, 2, 3, 4}

S1 - {1, 2, 3, 4}   # Empty sets print differently
# set()
type({})   # Because {} is an empty dictionary
# <class 'dict'>

S = set()  # Initialize an empty set
S.add(1.23)
S
# {1.23}
```

- Sets can only contain immutable (a.k.a. “hashable”) object types. Hence, lists and dictionaries cannot be embedded in sets, but tuples can.

```py
S
# {1.23}
S.add([1, 2, 3]) # Only immutable objects work in a set
# TypeError: unhashable type: 'list'
S.add({'a':1})
# TypeError: unhashable type: 'dict'
S.add((1, 2, 3))
S # No list or dict, but tuple OK
# {1.23, (1, 2, 3)}

S | {(4, 5, 6), (1, 2, 3)}   # Union: same as S.union(...)
# {1.23, (4, 5, 6), (1, 2, 3)}
(1, 2, 3) in S   # Membership: by complete values
# True
(1, 4, 3) in S
# False
```

- Sets themselves are mutable, and so cannot be nested in other sets directly. The `frozenset` built-in call works just like set but creates an immutable set that cannot change and thus can be embedded in other sets.

### Common operations/methods for data types

1. `sorted()`: Sorts collections
2. `len()`: Returns the length of a collection
3. `in` membership: test whether an item is in a collection
   1. Strings
   2. Dictionaries
   3. Lists

## Dealing with files and folders

```py
data = open('data.bin', 'rb').read()  # Open/read binary data file
data # 10 bytes, unaltered
# b'\x00\x00\x00\x07spam\x00\x08'
data[4:8]  # Slice bytes in the middle
# b'spam'
list(data) # A sequence of 8-bit bytes
# [0, 0, 0, 7, 115, 112, 97, 109, 0, 8]
struct.unpack('>i4sh', data) # Unpack into objects again
# (7, b'spam', 8
```

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

### Binary Bytes Files

- *binary files* represent content as a special bytes string and allow you to access file content unaltered.
- *binary files* are useful for processing media, accessing data created by C programs

```py
# Writing Binary bytes to a file
import struct
packed = struct.pack('>i4sh', 7, b'spam', 8)   # Create packed binary data
packed  # 10 bytes, not objects or text
# b'\x00\x00\x00\x07spam\x00\x08'

file = open('data.bin', 'wb')   # Open binary output file
file.write(packed)  # Write packed binary data
# 10
file.close()
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

## Data Structures

### NumPy

- It gives Arrays that a great data stucture objects, that makes working with numerical data easy and simple more than what it can be done in pure python.
- It is the foundation for the python data stack, and it is what makes python great for data analysis.

#### NumPy Modules

1. Random: it helps to simulate random events like coin flips.

   1. [randint(low = 0, high, size)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.randint.html?highlight=randint#numpy.random.randint): it generates a list of [size] numbers and each element value can be any value between [low] and [high-1].
   2. [choice(a, size, replace=True, p=None)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.choice.html?highlight=choice#numpy.random.choice): generates a random sample of size [size] from given 1-D array [a] and [p] is the probability of each value in [a]. [replace] is for bootstraping, as whether values could be chosen more than once or not.
   3. [binomial(n,p,size=None)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.binomial.html?highlight=binomial#numpy.random.binomial): Draw samples from a binomial distribution, Samples are drawn from a binomial distribution with specified parameters, n trials and p probability of success where n an integer >= 0 and p is in the interval [0,1]. (n may be input as a float, but it is truncated to an integer in use)
   4. seed
   5. gamma
   6. [normal(loc=0.0, scale=1.0, size=None)](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.random.normal.html): Draw random samples from a normal (Gaussian) distribution. [loc] is the center point, [scale] is the standard deviation, [size] is the number of sampling points.

   ```py
   import numpy as py
   
   np.random.randint(2, size=10)
   # [1,0,0,1,1,0,1,1,0,0]
   
   np.random.choice([0,1], size=10000, p=[0.8, 0.2]).mean()
   # 0.203199999999 which shows that the probility of 1 is 20%
   
   np.random.binomial(n=10, p=.5)
   # 5
   # the above is the same as the below
   (np.random.randint(2,size=10)==0).sum()
   # 5
   # The below will give the results of the above test 1000 times
   np.random.binomial(n=10, p=.5, size=1000)
   # result of flipping a coin 10 times, tested 1000 times.
   
   np.random.normal(70,std,10000)
   # returns a normal distribution of 10000 sample with center at 70 and has 2.5 wide spread.
   ```

[Python For Data Science NumPy Cheat Sheet](files/Python%20For%20Data%20Science%20NumPy%20Cheat%20Sheet.pdf)

### Pandas

- It gives Data Frames that are great data structures objects, that can manipulate and analyze data. It also includes some convenient methods for visualizing data that hook into matplotlib.
- [Compared to SQL](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_sql.html) and [Medium Article](https://medium.com/jbennetcodes/how-to-rewrite-your-sql-queries-in-pandas-and-more-149d341fc53e#e009)

#### Input/Output

##### Read and Write from CSV

- [read_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.htm)
- [to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html)

```py
# Read and write from CSV
pd.read_csv('file_name.csv',header=None,nrows=5)
df.to_csv('file_name.csv')

# `to_csv()` will store our index unless we tell it not to. To make it ignore the index, we have to provide the parameter `index=False`
df.to_csv('file_name_edited.csv', index=False)
```

##### Read and write from Excel

- read_excel
- to_excel

```py
# Read and write from Excel
pd.read_excel('file_name.xlsx')
df.to_excel('file_name.xlsx')

# Write to excel sheet with multiple sheets
with pd.ExcelWriter(path='file_name.xlsx') as writer:
        df1.to_excel(writer,sheet_name='df1')
        df2.to_excel(writer,sheet_name='df2')
        df3.to_excel(writer,sheet_name='df3')

# Read multiple sheets from excel file
xlsx = pd.ExcelFile('file_name.xlsx')
df = pd.read_excel(xlsx, 'Sheet1')
```

##### Read and Write to SQL Query or Database Table

```py
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')
pd.read_sql("SELECT * FROM my_table;", engine)
pd.read_sql_table('my_table',engine)
pd.read_sql_query("SELECT * FROM my_table;", engine)

# read_sql() is a convenience wrapper around read_sql_table() and read_sql_query()

pd.to_sql('my_DF', engine)
```

#### Retrieving Information

##### Basic Information

```py
# Get rows and columns counts
df.shape

# Describe index
df.index

# Describe Columns
df.columns

# This displays a concise summary of the dataframe,
# including the number of non-null values in each column
df.info()

# Number of non-NA values
df.count()

# This returns the datatypes of the columns
df.dtypes
```

##### Summary

- [idxmax](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.idxmax.html)

```py
# Sum of values
df.sum()

# Cummulative sum of values
df.cumsum()

# Min values
df.min()

# Max values
df.max()

# Min index value
df.idmin()

# Max index value
df.idmax()

# Finds the index of the row containing a column's maximum value!
df.colum_name.idxmax()

# Summary Statistics
df.describe()

# Mean of values
df.mean()

# Median of values
df.median()

# Variance of each object
df.var()

# Standard Deviation of each object
df.std()

# Count of Null values in each column
df.isna().sum()

# Count of Null values in each row
df.isna().sum(axis=1)

# List unique values in the df['name'] column
df.column_name.unique()

# This returns the number of unique values in each column
df.column_name.nunique()

# Return values at the given quantile over requested axis.
df.quantile(0.5)
```

#### Data Wrangling

##### Creating Data Frame

```py
# Specify values for each column
df = pd.DataFrame(
   {
      "a": [4,5,6],
      "b": [7,8,9],
      "c": [10,11,12]
   },
   index= [1,2,3])

# Specify values for each row
df = pd.DataFrame(
   [[4,7,10],
    [5,8,11],
    [6,9,12]],
   index = [1,2,3],
   column = ['a','b','c'])

# Specify DataFrame with a MultiIndex
df = pd.DataFrame(
   {
      "a": [4,5,6],
      "b": [7,8,9],
      "c": [10,11,12]
   },
   index= pd.MultiIndex.from_tuples(
      [('d',1),('d',2),('e',2)],
      names = ['n','v']))
```

##### Reshaping Data

- [df_new = df.copy() vs df_new = df](https://www.geeksforgeeks.org/python-difference-between-pandas-copy-and-copying-through-variables/)
- [to_datetime](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html) converts string to DateTime type
- [Merges()](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
- [cut()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html)

```py
# Gather columns into rows
pd.melt(df)

df_new = df.melt(id_vars = ['id','a_column'],
                  value_vars = ['col_1', 'col_2'],
                  var_name = 'var_col_name', value_name = 'val_col_name')

# Spread rows into columns
pd.pivot(columns='vars', values='val')

# Append rows of DataFrames
pd.concat([df1,df2])

# Append columns of DataFrames
pd.concat([df1,df2],axis=1)

# Combine dataframes
df3 = df1.append(df2, ignore_index=True)

# Merge dataframes
df_combined = df1.merge(df2, left_on='column_name_df1', right_on='column_name_df2', how='inner')

# Order rows by values of a column (low to high).
df.sort_values('col_name')

# Order rows by values of a column (low to high).
df.sort_values('col_name', ascending=False)

# Rename the columns of DataFrame
df.rename(columns = {'old_col_name':'new_col_name'})

# Rename all column labels to replace spaces with underscores and convert everything to lowercase. (Underscores can be much easier to work with in Python than spaces. For example, having spaces wouldn't allow you to use df.column_name instead of df['column_name'] to select columns or use query(). Being consistent with lowercase and underscores also helps make column names easy to remember.)
df.rename(columns=lambda x: x.strip().lower().replace(' ','_'), inplace=True)

# copying a DataFrame or Series
# Pandas .copy() method is used to create a copy of a Pandas object. Variables are also used to generate copy of an object but variables are just pointer to an object and any change in new data will also change the previous data.
df2 = df.copy()

# Converts string to datetime object. But CSV will read this column as strings next time the file reopened, unless the it parsed into the CSV file. But pandas to_datetime provides more options than that of CSV.
df['date_column'] = pd.to_datetime(df['date_column'])

# Use cut when you need to segment and sort data values into bins. This function is also useful for going from a continuous variable to a categorical variable. For example, cut could convert ages to groups of age ranges. Supports binning into an equal number of bins, or a pre-specified array of bins.
pd.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False, duplicates='raise', ordered=True)
```

##### Subset Observations (rows)

```py
# Extract rows that meet logical criteria
df[df.col_name > 7]

# Returns boolean column, which gives the duplicate TRUE value with escaping the first instance. All rows has to be the same to be identified as duplicate.
df.duplicated()

# Removes the duplicates (only consider columns) in the dataset and inplace parameter applies the change in the dataset.
df.drop_duplicates(inplace=True)

# Select first n rows
df.head(n)

# Select last n rows
df.tail(n)

# Randomly select fraction of rows
df.sample(frac=0.5)

# Randomly select n rows
df.sample(n=10)

# Select rows by position
df.iloc[10:20]

# Select and order top n entries.
df.nlargest(n, 'value')

# Select and order bottom n entries
df.nsmallest(n, 'value')
```

##### Subset Variables (Columns)

- [loc(), iloc()](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

```py
# Select multiple columns with specific names
df[['col1','col2','col3']]

# Select single column with specific name.
df['col']
df.col

# Select columns whose name matches regular expression regex.
df.filter(regex='regex')

# Select all columns between x2 and x4 (inclusive)
df.loc[:,'x2':'x4']

# Select columns in positions 1,2 and 5 (first column is 0)
df.iloc[:,[1,2,5]]
```

##### Subset row and column

- [loc(), iloc()](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

```py
# Select single value by row and column
## By Index/Position
df.iloc[[0],[0]]
df.iat[[0],[0]] # Get scalar/single value. It's a very fast iloc
## By Column/Label
df.loc[[0],['col_name']]
df.at[[0],['col_name']] # Get scalar/single value. It's a very fast loc

# Select rows meeting logical condition, and only in the specific columns
df.loc[df['a'] > 10, ['a','c']]

# Crosstab lets you select multiple columns and then see how many records, there are that overlap for different values of these columns.
pd.crosstab(df.col1,df.col2, aggFunc=sum, margins=True, normalize=True).plot(kind='bar')
```

#### Handling Missing Data

```py
# Drop values from rows
s.drop(['a','c'])

# Remove rows or columns by specifying label names and corresponding axis, or by specifying directly index or column names. When using a multi-index, labels on different levels can be removed by specifying the level.
df.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')

# Remove rows with NULL values
df.dropna()

# Remove columns with NULL values
df.dropna(axis=1)

# More dropna rules
df.dropna(how='all')
# specify the threshold equals 4, means that dropping the coulmn if it has 4 missing values or more.
df.dropna(thresh=4, axis=1)
df.dropna(subset=['Fruits'])

# Fills the missing values with value and if inplace is true it will replace the column with new data.
df['column_name'].fillna(value, inplace=True)

# Replace all null data with value
df.fillna(value)
# Method 'Pad' uses the previous record and use to impute the value. `limit` parameter limits the number of consecutive imputations
df.fillna(method = 'pad', limit=1)
# Method 'bfill' is the backfill technique, it fills the missing value with the value of the next one.
df.fillna(method = 'bfill')
# Method 'ffill' is the forward technique, it fills the missing value with the value of the previous one.
df.fillna(method = 'ffill')

# Substitute missing values using the existing one using interpolation technique
df.interpolate()
```

#### Group Data

- All of summary functions can be applied to a group
- [groupby](https://www.shanelynn.ie/summarising-aggregation-and-grouping-data-in-python-pandas/)

```py
# Return a GroupBy object, grouped by values in column 'col'
df.groupby(by='col')

# Return a GroupBy object, grouped by values in index level named 'ind'
df.groupby(level='ind')

# Aggregate group using function
agg(function)

# groupby and aggregate
df.groupby(['gender','major']).agg(
    total=('student_id', 'count'),
    to_females = ('student_id',lambda x: len(x)/df_females.shape[0]),
    to_males = ('student_id',lambda x : len(x)/df_males.shape[0]),
    admission_rate = ('admitted', 'mean'),
    )
```

#### Sort and Rank

- [CategoricalDtype](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.api.types.CategoricalDtype.html): to convert the data into an ordered type, the order of categories becomes innate to the feature, and we won't need to specify an "order" parameter each time it's required in a plot.

```py
# Sort by row or column index
df.sort_index(by='col_name')

# Sorts by the values along an axis
df.sort_values(by='Column lable')

# Sorts values by column1 in ascending order
df.sort_values(column1, ascending=True)

# Sort a series by its values
s.order()

# Assign ranks to entries
df.rank()

## CategoricalDtypes
# this method requires pandas v0.21 or later
level_order = ['Alpha', 'Beta', 'Gamma', 'Delta']
ordered_cat = pd.api.types.CategoricalDtype(ordered = True, categories = level_order)
df['cat_var'] = df['cat_var'].astype(ordered_cat)
# # use this method if you have pandas v0.20.3 or earlier
# df['cat_var'] = df['cat_var'].astype('category', ordered = True,
#                                      categories = level_order)
```

#### Applying functions

- [apply()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html)
- [applymap](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.applymap.html?highlight=applymap#pandas.DataFrame.applymap)

```py
f = lambda x: x*2
# Apply function
df.apply(f)

# Apply function element-wise
df.applymap(f)
```

#### Plotting

```py
# Plot Histogram for each column
df.plot.hist()

# hist() can be called on a Pandas series object as well
df.column_name.hist();

# plot() is a more general plotting function
df.column_name.plot(kind='hist');
df.plot(x='x-axis column_name', y='y-axis column_name', kind='scatter');
df.column_name.plot(kind='box');
df.column_name.plot(kind='pie');
# Scatter chart using pairs of points
df.plot.scatter(x='w', y='h')
# scatter_matrix() shows the relationships among numerical variables with scatter plots. It also returns a histogram for each variable.
pd.plotting.scatter_matrix(df, figsize=(15,15));
```

#### Pandas Tips and Tricks

```py
# Get information about a function
help(pd.Series.loc)

# convert to string and extract the integer using regular expressions
df['column_name'].str.extract('(\d+)').astype(int)

# get all rows that column_name has values contains (/)
df[df['column_name'].str.contains('/')]

# View the index number and label for each column
for i, v in enumerate(df.columns):
    print(i, v)

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

# make sure they're all identical like this
(df_08.columns == df_18.columns).all()

# Get dummy columns with 1,0 encoding for Linear Regression Model, it will return
pd.get_dummies(df['column_name'])
```

#### Logic in Python

- `<` : Less than
- `>` : Greater than
- `==`: Equals
- `<=`: Less than or equals
- `>=`: Greater than or equals
- `!=`: Not equal to
- `df.column.isna(values)` : Group membership
- `pd.isnull(obj)` : Is NaN
- `pd.notnull(obj)`: Is not Nan
- `&,|,~,^,df.any(),df.all()` : Logical and, or, not, xor, any, all

#### Regular Expressions Examples

- `'\.'` : Matches strings containg a period '.'
- `'Length$'` : Matches string ending with word 'Length'
- `'^Sepal'` : Matches string beginning with word 'Sepal'
- `'^x[1-5]$` : Matches strings beginning with 'x' and ending with 1,2,3,4,5
- `'^(?!Species$).*'` : Matches strings except the string 'Species'

#### Pandas References

[Python For Data Science Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)

### Matplotlib

- Matplotlib is a package for building visualizations from your data. It can make many kinds of simple plots with tiny amounts of codes, but it can take some code effort to  create a professional looking figures.
- Matplotlib is a Python 2D plotting library which produces publication-quality figures in a variety of hardcopy formats and interactive environments across platforms.
- [Magic words](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

#### Create Plot

- Import the library
  
  ```py
  import matplotlib.pyplot as plt
  
  # view the plots in the notebook
  %matplotlib inline
  ```

- Create figure
  
  ```py
  fig = plt.figure()
  fig2 = plt.figure(figsize=plt.figaspect(2.0))
  ```

- Axes: All plotting is done with respect to an Axes. In most cases, a subplot will fit your needs. A subplot is an axes on a grid system.
  
  ```py
  fig.add_axes()
  ax1 = fig.add_subplot(221) # row-col-num
  ax3 = fig.add_subplot(212)
  fig3, axes = plt.subplots(nrows=2,ncols=2)
  fig4, axes2 = plt.subplots(ncols=3)
  ```

#### Plotting Routines

- 1D Data
  
  ```py
  # Draw points with lines or markers connecting them
  lines = ax.plot(x,y
  
  # Draw unconnected points, scaled or colored
  ax.scatter(x,y)
  
  # Plot vertical rectangles (constant width)
  axes[0,0].bar([1,2,3],[3,4,5]
  
  # Plot horiontal rectangles (constant height)
  axes[1,0].barh([0.5,1,2.5],[0,1,2]
  
  # Draw a horizontal line across axes
  axes[1,1].axhline(0.45)
  
  # Draw a vertical line across axes
  axes[0,1].axvline(0.65)
  
  # Draw filled polygons
  ax.fill(x,y,color='blue')
  
  # Fill between y-values and 0
  ax.fill_between(x,y,color='yellow')
  ```

- Vector Fields
  
  ```py
  # Add an arrow to the axes
  axes[0,1].arrow(0,0,0.5,0.5)
  
  # Plot a 2D field of arrows
  axes[1,1].quiver(y,z)
  
  # Plot 2D vector fields
  axes[0,1].streamplot(X,Y,U,V)
  ```

- Data Distributions
  
  - [errorbar()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.errorbar.html)
  
  ```py
  # Plot a histogram
  ax1.hist(y)
  
  # Plot a Heat Map
  plt.hist2d(data = df, x = 'disc_var1', y = 'disc_var2', bins = [bins_x, bins_y])
  
  # Make a box-and-whisker plot
  ax3.boxplot(y)
  
  # Make a violin plot
  ax3.violinplot(z)
  
  # Make Line Plots. Plot y versus x as lines and/or markers with attached errorbars.
  plt.errorbar(data = df, x = 'num_var1', y = 'num_var2')
  ```

- 2D Data
  
  ```py
  # Colormapped or RGB arrays
  fig, ax = plt.subplots()
  im = ax.imshow(img, cmap='gist_earth', interpolation='nearest', vmin=-2,vmax=2)
  
  # Pseudocolor plot of 2D array
  axes2[0].pcolor(data2)
  
  # Pseudocolor plot of 2D array
  axes2[0].pcolormesh(data
  
  # Plot contours
  CS = plt.contour(Y,X,U
  
  # Plot filled contours
  axes2[2].contourf(data1)
  
  # Label a contour plot
  axes2[2]= ax.clabel(CS)
  ```

#### Customize Plot

- Colors, Color Bars & Color Maps
  
  ```py
  plt.plot(x, x, x, x**2, x, x**3)
  ax.plot(x, y, alpha = 0.4)
  ax.plot(x, y, c='k')
  fig.colorbar(im, orientation='horizontal')
  im = ax.imshow(img, cmap='seismic')
  ```

- Markers
  
  ```py
  fig, ax = plt.subplots()
  ax.scatter(x,y,marker=".")
  ax.plot(x,y,marker="o")
  ```

- Linestyles
  
  ```py
  plt.plot(x,y,linewidth=4.0)
  plt.plot(x,y,ls='solid')
  plt.plot(x,y,ls='--')
  plt.plot(x,y,'--',x**2,y**2,'-.')
  plt.setp(lines,color='r',linewidth=4.0)
  ```

- Text & Annotations
  
  ```py
  ax.text(1, -2.1, 'Example Graph', style='italic')
  ax.annotate("Sine",
              xy=(8, 0),
              xycoords='data',
              xytext=(10.5, 0),
              textcoords='data',
              arrowprops=dict(arrowstyle="->", connectionstyle="arc3"),)
  ```

- Mathtext
  
  ```py
  plt.title(r'$sigma_i=15$', fontsize=20)
  ```

- Limits, Legends & Layouts
  
  - Limits & Autoscaling

    ```py
    # Add padding to a plot
    ax.margins(x=0.0,y=0.1)
    
    # Set the aspect ratio of the plot to 1
    ax.axis('equal')
    
    # Set limits for x-and y-axis
    ax.set(xlim=[0,10.5],ylim=[-1.5,1.5])
    
    # Set limits for x-axis
    ax.set_xlim(0,10.5)
    
    # Scale the plot axis to one of Transformation {"linear", "log", "symlog", "logit", ...}
    ax.xscale('log')
    ```

  - Legends

    ```py
    # Set a title and x-and y-axis labels
    ax.set(title='An Example Axes', ylabel='Y-Axis', xlabel='X-Axis')
    
    # No overlapping plot elements
    ax.legend(loc='best')
    ```

  - Ticks

    ```py
    # Manually set x-ticks
    ax.xaxis.set(ticks=range(1,5),ticklabels=[3,100,-12,"foo"])
    
    # Make y-ticks longer and go in and out
    ax.tick_params(axis='y', direction='inout', length=10)
    
    # Rotate x-axis ticks
    plt.xticks(rotation = 45)
    ```

  - Subplot Spacing

    ```py
    # Adjust the spacing between subplots
    fig3.subplots_adjust(wspace=0.5, hspace=0.3, left=0.125, right=0.9, top=0.9, bottom=0.1)
    
    # Fit subplot(s) in to the figure area
    fig.tight_layout()
    ```

  - Axis Spines

    ```py
    # Make the top axis line for a plot invisible
    ax1.spines['top'].set_visible(False)
    
    # Move the bottom axis line outward
    ax1.spines['bottom'].set_position(('outward',10))
    ```

#### Save Plot

```py
#Save figures
plt.savefig('foo.png')

# Save transparent figures
plt.savefig('foo.png', transparent=True)
```

#### Show Plot

```py
plt.show()
```

#### Close & Clear

```py
# Clear an axis
plt.cla()

# Clear an entire figure
plt.clf()

# Close a window
plt.close()
```

#### Matplotlib references

- [Python For Data Science MatPlotLib Cheat Sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Matplotlib_Cheat_Sheet.pdf)
- [How to rotate axis lables in seaborn and matplotlib](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)

### Seaborn

- It is built on top of matplotlib, adds a number of functions to make common statistical visualizations easier to generate.
- [ScatterPlot Matrix](https://seaborn.pydata.org/examples/scatterplot_matrix.html)
- [countplot](https://seaborn.pydata.org/generated/seaborn.countplot.html): Draws a basic bar chart of frequencies for categorical variables. By default, each category is given a different color.
- [color_palette](https://seaborn.pydata.org/generated/seaborn.color_palette.html): returns a list of RGB tuples. Each tuple consists of three digits specifying the red, green, and blue channel values to specify a color. Calling this function without any parameters returns the current / default palette.

#### Import seaborn library

```py
import matplotlib.pyplot as plt
import seaborn as sb

# countplot Draws a bar chart for categorical variables. By default, each category is given a different color. we take the first color to be the color for all bars.
base_color = sb.color_palette()[0]
cat_order = df['col_name'].value_counts().index
sb.countplot(data = df, x = 'col_name', color = base_color, order = cat_order)
```

#### Basic Steps for creating plots with Seaborn

##### Step 1: Prepare the data

```py
# Seaborn offers built-in data sets
titanic = sb.load_dataset("titanic")
iris = sb.load_dataset("iris")
```

##### Step 2: Figure Aesthetics

- [subplot()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html)
- [figure()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html): The method requires one list as argument specifying the dimensions of the Axes, the first two elements of the list indicate the position of the lower-left hand corner of the Axes and the last two elements specifying the Axes width and height.

Python first creates a Figure object. And since the Figure doesn't start with any Axes to draw the plot onto, an Axes object is created inside the Figure. Finally, the plot is drawn within that Axes.

```py
# Create a figure object
fig = plt.figure()

# Create Axes object
ax = fig.add_axes([.125, .125, .775, .755])

# OR
# Create a figure and one subplot
fig, ax = plt.subplots(figsize=(5,6))

# Plot the chart
ax.hist(data = df, x = 'cat_var')
# OR
sb.countplot(data = df, x = 'cat_var', color = base_color, ax = ax)
```

- Seaborn styles:

```py
# (Re)set the seaborn default
sb.set()

# Set the matplotlib parameters
sb.set_style("whitegrid")

# Set the matplotlib parameters
sb.set_style("ticks", {"xtick.major.size":8,"ytick.major.size":8})

# Return a dict of params or use `with` to temporarily set the style
sb.axes_style("whitegrid")
```

- Context Functions

```py
# Set context to "talk"
sb.set_context("talk")

# Set context to "notebook", scale font elements and override param mapping
sb.set_context("notebook", t_scale=1.5, rc={"lines.linewidth":2.5})
```

- Color Palette

```py
# Define the color palette
sb.set_palette("husl",3)

# Use with `with` to temporarily set palette
sb.color_palette("husl")

# Set your own color palette
flatui = ["#9b59b6","#3498db","#95a5a6","#e74c3c","#34495e","#2ecc71"]
sb.set_palette(flatui)
```

##### Step 3: Plotting

- Axis Grids
- [FacetGrid](https://seaborn.pydata.org/generated/seaborn.FacetGrid.html)

```py
# Subplot grid for plotting conditional relationships
g = sb.FacetGrid(titanic, col="survived", row="gender")
g = g.map(plt.hist,"age")

# Draw a categorical plot onto a Facetgrid
sb.factorplot(x="pclass", y="survived", hue="gender", data=titanic)

# Plot data and regression model fits across a FacetGrid
sb.lmplot(x="sepal_width", y="sepal_length", hue="species", data=iris)

# Subplot grid for plotting pairwise relationships
h = sb.PairGrid(iris)
h = h.map(plt.scatter)

# Plot pairwise bivariate distributions
sb.pairplot(iris)

# Grid for bivariate plot with marginal univariate plots
i = sb.JointGrid(x="x", y="y", data=data)
i = i.plot(sb.regplot, sb.distplot)

# Plot bivariate distribution
sb.jointplot("sepal_length", "sepal_width", data=iris, kind='kde')
```

- Categorical Plots

1. Scatterplot

   ```py
   ## Scatterplot
   # Scatterplot with one categorical variable
   sb.stripplot(x="species", y="petal_length", data=iris)
   
   # Categorical scatterplot with non-overlapping points
   sb.swarmplot(x="species", y="petal_length", data=iris)
   ```

2. Bar Chart

   ```py
   # Show point estimates and confidence intervals with scatterplot glyphs
   sb.barplot(x="gender", y="survived", hue="class", data=titanic)
   ```

3. Count Plot

   ```py
   # Show count of observations
   sb.countplot(x="deck", data=titanic, palette="Greens_d")
   
   # Convert the column into an ordered categorical data type.
   # By default, pandas reads in string data as object types, and will plot the bars in the order in which the unique values were seen. By converting the data into an ordered type, the order of categories becomes innate to the feature, and we won't need to specify an "order" parameter each time it's required in a plot.
   level_order = ['Alpha', 'Beta', 'Gamma', 'Delta']
   ordered_cat = pd.api.types.CategoricalDtype(ordered = True,categories = level_order)
   # this method requires pandas v0.21 or later
   df['cat_var'] = df['cat_var'].astype(ordered_cat)
   
   # # use this method if you have pandas v0.20.3 or earlier
   # df['cat_var'] = df['cat_var'].astype('category', ordered = True,
   #                                      categories = level_order)
   
    base_color = sb.color_palette()[0]
    sb.countplot(data = df, x = 'cat_var', color = base_color)
   ```

4. Point Plot

   ```py
   # Show point estimates and confidence intervals as rectangular bars
   sb.pointplot(x="class", y="survived", hue="gender", data=titanic, palette={"male":"g", "female":"m"}, markers=["^","o"], linestyles=["-","--"])
   ```

5. Boxplot

   ```py
   # Boxplot
   sb.boxplot(x="alive", y="age", hue="adult_male", data=titanic)
   
   # Boxplot with wide-form data
   sb.boxplot(data=iris,orient="h")
   ```

6. Violinplot

   ```py
   # Violin plot
   sb.violinplot(x="age", y="gender", hue="survived", data=titanic)
   ```

- Regression Plots

```py
# Plot data and a linear regression model fit
sb.regplot(x="sepal_width", y="sepal_length", data=iris, ax=ax)
```

- Distribution Plots

```py
# Plot univariate distribution
plot = sb.distplot(df['col_name'], kde=False, color="b")
```

- Matrix Plots

```py
# Heatmap
sb.heatmap(uniform_data,vmin=0,vmax=1)
```

##### Step 4: Further Customizations

- Axisgrid Objects

```py
# Remove left spine
g.despine(left=True)

# Set the labels of the y-axis
g.set_ylabels("Survived")

# Set the tick labels for x
g.set_xticklabels(rotation=45)

# Set the axis labels
g.set_axis_labels("Survived", "gender")

# Set the limit and ticks of the x-and y-axis
h.set(xlim=(0,5), ylim=(0,5), xticks=[0,2.5,5], yticks=[0,2.5,5])
```

- Plot

```py
# Add plot title
plt.title("A Title")

# Adjust the label of the y-axis
plt.ylabel("Survived")

# Adjust the label of the x-axis
plt.xlabel("gender")

# Adjust the limits of the y-axis
plt.ylim(0,100)

# Adjust the limits of the x-axis
plt.xlim(0,10)

# Adjust a plot property
plt.setp(ax,yticks=[0,5])

# Adjust subplot params
plt.tight_layout()
```

##### Step 5: Show, Save, Close

- Show or Save Plot

```py
# Show the plot
plt.show()

# Save the plot as a figure
plt.savefig("foo.png")

# Save transparent figure
plt.savefig("foo.png", transparent=True)
```

- Close & Clear

```py
# Clear an axis
plt.cla()

# Clear an entire figure
plt.clf()

# Close a window
plt.close()
```

#### Seaborn References

- [DataCamp Cheat Sheet](https://www.datacamp.com/community/blog/seaborn-cheat-sheet-python)

### Resources

- [Python for data analysis](http://www.ruxizhang.com/uploads/4/4/0/2/44023465/python_for_data_analysis.pdf)
- [NumPy and Pandas by Udacity](https://classroom.udacity.com/courses/ud170)
- [How to rotate x-lables](https://kite.com/python/answers/how-to-rotate-date-ticks-using-matplotlib-in-python#:~:text=Use%20matplotlib.,specified%20amount%20of%20degrees%20degrees%20) and [here](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)

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
      1. `sklearn.preprocessing.LabelEncoder`

         ```py
         from sklearn.preprocessing import LabelEncoder
         
         loan_enc = LabelEncoder()
         y = group_enc.fit_transform(df['loan_approved'])
         ```

      2. `sklearn.preprocessing.OneHotEncoder`

         ```py
         from sklearn.preprocessing import OneHotEncoder
         
         df = pd.DataFrame({"Fruits":["Apple","Banana","Banana","Mango","Banana"]})
         num_type = group_enc.fit_transform(df['Fruits'])
         type_enc = OneHotEncoder()
         type_enc.fit(num_type.reshape(-1,1))
         ```

      3. Convert a collection of text documents to a matrix of token counts `sksklearn.feature_extraction.text.CountVectorizer`

         ```py
         from sklearn.feature_extraction.text import CountVectorizer
         
         count_vectorizer = CountVectorizer()
         x_train_count = count_vectorizer.fit_transform(data.text)
         
         count_vectorizer.vocabulary_
         ```

      4. Convert a collection of raw documents to a matrix of TF-IDF features. Equivalent to `:class:CountVectorizer` followed by `:class:TfidfTransformer`. `sklearn.feature_extraction.text.TfidfVectorizer`
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
