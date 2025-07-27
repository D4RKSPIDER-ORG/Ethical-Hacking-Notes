[[B-Python-Basics Note-1]]
print method use to Display something i want so its basically like this. there is no need to use ''(single quotes)..i can use double quotes 

```
print('Hello World')
```

```
print("Hello World")
```

so both output's are same looks like this.

#### Hello world

so next is multiply. if i use command like this 

```
print("E" * 10)
```

this command do is give me 10 E s.

```
EEEEEEEEEE
```

Python can be used as a calculator to compute arithmetic operations like addition, subtraction, multiplication and division. Python can also be used for trigonometric calculations and statistical calculations.

### Arithmetic

Python can be used as a calculator to make simple arithmetic calculations.

Simple arithmetic calculations can be completed at the Python Prompt, also called the _Python REPL_. REPL stands for Read Evaluate Print Loop. The Python REPL shows three arrow symbols `>>>` followed by a blinking cursor. Programmers type commands at the `>>>` prompt then hit `[ENTER]` to see the results.

Commands typed into the Python REPL are _read_ by the interpreter, results of running the commands are _evaluated_, then _printed_ to the command window. After the output is printed, the `>>>` prompt appears on a new line. This process repeats over and over again in a continuous _loop_.

Try the following commands at the Python REPL:

Suppose the mass of a battery is 5 kg and the mass of the battery cables is 3 kg. What is the mass of the battery cable assembly?

`>>> 5 + 3 8`

Suppose one of the cables above is removed and it has a mass of 1.5 kg. What is the mass of the leftover assembly?

`>>> 8 - 1.5 6.5`

If the battery has a mass of 5000 g and a volume of 2500 cm3 What is the density of the battery? The formula for density is below, where D is density, m is mass and v is volume.

D=mv

In the problem above m=5000 and v=2500

Let's solve this with Python.

`>>> 5000 / 2500 2.0`

What is the total mass if we have 2 batteries, and each battery weighs 5 kg?

`>>> 5 * 2 10`

The length, width, and height of each battery is 3 cm. What is the area of the base of the battery? To complete this problem, use the double asterisk symbol `**` to raise a number to a power.

`>>> 3 ** 2 9`

What is the volume of the battery if each the length, width, and height of the battery are all 3 cm?

`>>> 3 ** 3 27`

Find the mass of the two batteries and two cables.

We can use Python to find the mass of the batteries and then use the answer, which Python saves as an underscore _ to use in our next operation. (The underscore `_` in Python is comparable to the `ans` variable in MATLAB)

`>>> 2 * 5  10 >>> _ + 1.5 + 1 12.5`

#### Section Summary

A summary of the arithmetic operations in Python is below:

|Operator|Description|Example|Result|
|---|---|---|---|
|`+`|addition|`2 + 3`|`5`|
|`-`|subtraction|`8 - 6`|`2`|
|`-`|negative number|`-4`|`-4`|
|`*`|multiplication|`5 * 2`|`10`|
|`/`|division|`6 / 3`|`2`|
|`**`|raises a number to a power|`10**2`|`100`|
|`_`|returns last saved value|`_ + 7`|`107`|

### Trigonometry: sine, cosine, and tangent

Trigonometry functions such as sine, cosine, and tangent can also be calculated using the Python REPL.

To use Python's trig functions, we need to introduce a new concept: _importing modules_.

In Python, there are many operations built into the language when the REPL starts. These include `+` , `-`, `*`, `/` like we saw in the previous section. However, not all functions will work right away when Python starts. Say we want to find the sine of an angle. Try the following:

`>>> sin(60) Traceback (most recent call last):   File "<stdin>", line 1, in <module> NameError: name 'sin' is not defined`

This error results because we have not told Python to include the `sin` function. The `sin` function is part of the _Python Standard Library_. The Python Standard Library comes with every Python installation and includes many functions, but not all of these functions are available to us when we start a new Python REPL session. To use Python's `sin` function, first import the `sin` function from the `math` _module_ which is part of the Python Standard Library.

Importing modules and functions is easy. Use the following syntax:

`from module import function`

To import the `sin()` function from the `math` module try:

`>>> from math import sin >>> sin(60) -0.3048106211022167`

Success! Multiple modules can be imported at the same time. Say we want to use a bunch of different trig functions to solve the following problem.

An angle has a value of π/6 radians. What is the sine, cos, and tangent of the angle?

To solve this problem we need to import the `sin()`, `cos()`, and `tan()` functions. It is also useful to have the value of π, rather than having to write `3.14....` We can import all of these functions at the same time using the syntax:

`from module import function1, function2, function3`

Note the commas in between the function names.

Try:

`>>> from math import sin, cos, tan, pi >>> pi 3.141592653589793 >>> sin(pi/6) 0.49999999999999994 >>> cos(pi/6) 0.8660254037844387 >>> tan(pi/6) 0.5773502691896257`

#### Section Summary

The following trig functions are part of Python's **math** module:

|Trig function|Name|Description|Example|Result|
|---|---|---|---|---|
|`math.pi`|pi|mathematical constant π|`math.pi`|`3.14`|
|`math.sin()`|sine|sine of an angle in radians|`math.sin(4)`|`9.025`|
|`math.cos()`|cosine|cosine of an angle in radians|`cos(3.1)`|`400`|
|`math.tan()`|tangent|tangent of an angle in radians|`tan(100)`|`2.0`|
|`math.asin()`|arc sine|inverse sine, ouput in radians|`math.sin(4)`|`9.025`|
|`math.acos()`|arc cosine|inverse cosine, ouput in radians|`log(3.1)`|`400`|
|`math.atan()`|arc tangent|inverse tangent, ouput in radians|`atan(100)`|`2.0`|
|`math.radians()`|radians conversion|degrees to radians|`math.radians(90)`|`1.57`|
|`math.degrees()`|degree conversion|radians to degrees|`math.degrees(2)`|`114.59`|

### Exponents and Logarithms

Calculating exponents and logarithms with Python is easy. Note the exponent and logarithm functions are imported from the **math** module just like the trig functions were imported from the **math** module above.

The following exponents and logarithms functions can be imported from Python's math module:

- `log`
- `log10`
- `exp`
- `e`
- `pow(x,y)`
- `sqrt`

Let's try a couple of examples:

`>>> from math import log, log10, exp, e, pow, sqrt >>> log(3.0*e**3.4)         # note: natural log 4.4986122886681095`

A right triangle has side lengths 3 and 4. What is the length of the hypotenuse?

`>>> sqrt(3**2 + 4**2) 5.0` 

The power function `pow()` works like the `**` operator. `pow()` raises a number to a power.

`>>> 5**2 25`

  

`>>> pow(5,2) 25.0`

#### Section Summary

The following exponent and logarithm functions are part of Python's **math** module:

|Math function|Name|Description|Example|Result|
|---|---|---|---|---|
|`math.e`|Euler's number|mathematical constant e|`math.e`|`2.718`|
|`math.exp()`|exponent|e raised to a power|`math.exp(2.2)`|`9.025`|
|`math.log()`|natural logarithm|log base e|`math.log(3.1)`|`400`|
|`math.log10()`|base 10 logarithm|log base 10|`math.log10(100)`|`2.0`|
|`math.pow()`|power|raises a number to a power|`math.pow(2,3)`|`8.0`|
|`math.sqrt()`|square root|square root of a number|`math.sqrt(16)`|`4.0`|

### Statistics

To round out this section, we will look at a couple of statistics functions. These functions are part of the Python Standard Library, but not part of the **math** module. To access Python's statistics functions, we need to import them from the **statistics** module using the statement `from statistics import mean, median, mode, stdev`. Then the functions `mean`, `median`, `mode` and `stdev` (standard deviation) can be used.

`>>> from statistics import mean, median, mode, stdev  >>> test_scores = [60, 83, 83, 91, 100]  >>> mean(test_scores) 83.4  >>> median(test_scores) 83  >>> mode(test_scores) 83  >>> stdev(test_scores) 14.842506526863986` 

Alternatively, we can import the entire **statistics** module using the statement `import statistics`. Then to use the functions, we need to use the names `statistics.mean`, `statistics.median`, `statistics.mode`, and `statistics.stdev`. See below:

`>>> import statistics  >>> test_scores = [60, 83, 83, 91, 100 ]  >>> statistics.mean(test_scores) 83.4  >>> statistics.median(test_scores) 83  >>> statistics.mode(test_scores) 83  >>> statistics.stdev(test_scores) 14.842506526863986` 

#### Section Summary

The following functions are part of Python's **statistics** module. These functions need to be imported from the `statistics` module before they are used.

|Statistics function|Name|Description|Example|Result|
|---|---|---|---|---|
|`mean()`|mean|mean or average|`mean([1,4,5,5])`|`3.75`|
|`median()`|median|middle value|`median([1,4,5,5])`|`4.5`|
|`mode()`|mode|most often|`mode([1,4,5,5])`|`5`|
|`stdev()`|standard deviation|spread of data|`stdev([1,4,5,5])`|`1.892`|
|`variance()`|variance|variance of data|`variance([1,4,5,5])`|`3.583`|


# FROM SIMPLILEARN

Python is a high-level, interpreted [programming language](https://www.simplilearn.com/best-programming-languages-start-learning-today-article "programming language") developed in the late 1980s that has enjoyed tremendous growth over the last few years. While it can be used for many different applications, its resurgence in popularity has been driven by the surge in [data science](https://www.simplilearn.com/tutorials/data-science-tutorial/what-is-data-science) and [business intelligence](https://www.simplilearn.com/what-is-business-intelligence-article).

In this article, we will learn about one of Python programming's fundamental data types: Python strings, including an overview of how to work with them, Python string methods, and more. So, let’s get started.

## What is a Python String?

 Python string is a data type used to represent a sequence of characters. These characters can include letters, numbers, symbols, and whitespace. In Python, strings are immutable, meaning that once a string is created, its content cannot be changed. This immutability feature ensures that strings are consistent and secure throughout the program execution.

Strings in Python are enclosed within either single quotes (' '), double quotes (" "), or triple quotes (''' ''' or """ """). Each type of quote can be used interchangeably, allowing flexibility in how strings are defined, particularly when a string itself contains quotes. For example:

```
# Single quotes
single_quote_string = 'Hello, World!'

# Double quotes
double_quote_string = "Hello, World!"

# Triple quotes for multi-line strings or strings containing both single and double quotes
triple_quote_string = '''Hello,
World!'''
```

## How to Create a String in Python?

Creating strings in Python is straightforward, and the language offers multiple ways to define them, catering to different use cases such as single-line, multi-line, and strings containing quotes. Below are detailed explanations and examples of how to create strings in Python.

### Basic String Creation

#### Single Quotes

You can create a string using single quotes (' '):

```
single_quote_string = 'Hello, World!'
```

#### Double Quotes

Alternatively, double quotes (" ") can also be used to create strings:

```
double_quote_string = "Hello, World!"
```

Both single and double quotes work the same way in Python and can be used interchangeably. The choice between them often depends on the presence of quotes within the string itself.

#### Triple Quotes

Triple quotes (''' ''' or """ """) are used to create multi-line strings or strings that span several lines:

```
# Using triple single quotes
triple_single_quote_string = '''This is a multi-line
string that spans
several lines.'''

# Using triple double quotes
triple_double_quote_string = """This is another way
to create a multi-line string."""
```

Triple quotes are particularly useful for documentation strings (docstrings) and when the string itself contains both single and double quotes.

## Creating Strings with Embedded Quotes

When a string contains quotes, using a different type of quote to enclose the string can make it easier to include quotes inside the string without needing escape characters:

```
# String with double quotes inside
string_with_double_quotes = 'She said, "Hello!"'

# String with single quotes inside
string_with_single_quotes = "It's a beautiful day!"
If you need to include both single and double quotes inside a string, you can use escape characters (\) or triple quotes:
# Using escape characters
escaped_string = 'She said, "It\'s a beautiful day!"'

# Using triple quotes
triple_quote_string = """She said, "It's a beautiful day!" """
```

## Using Escape Characters

Escape characters allow you to include special characters in strings, such as newline:

```
(\n), tab (\t), backslash (\\), and quotes (\' or \"):
# Newline and tab
special_char_string = "Hello,\n\tWorld!"

# Backslash and quotes
escaped_quotes_string = "She said, \"It\'s a beautiful day!\""
```

## Raw Strings

Raw strings treat backslashes as literal characters and are created by prefixing the string with an r or R. This is particularly useful for regular expressions and file paths:

```
# Regular string with escape sequences
regular_string = "C:\\Users\\Name"

# Raw string
raw_string = r"C:\Users\Name"
```

## String Concatenation

String concatenation combines two or more strings into one. You can concatenate strings using the + operator:

```
str1 = "Hello"
str2 = "World"
concatenated = str1 + ", " + str2 + "!"  # 'Hello, World!'
Alternatively, you can use the join method for concatenation, especially when dealing with lists of strings:
words = ["Hello", "World"]
joined_string = " ".join(words)  # 'Hello World'
```

## Multi-line Strings

In addition to using triple quotes for multi-line strings, you can use the backslash (\) to continue a string onto the next line without including a newline character:

```
multi_line_string = "This is a long string that is " \
                    "split across multiple lines " \
                    "for better readability."
```

## String Formatting

Python offers several ways to create formatted strings that include variables and expressions within them:

### Percent (%) Formatting

This is an older method for string formatting:

```
name = "Alice"
age = 30
formatted_string = "Name: %s, Age: %d" % (name, age)  # 'Name: Alice, Age: 30'
str.format() Method
```

This method provides more control and readability:

```
name = "Alice"
age = 30
formatted_string = "Name: {}, Age: {}".format(name, age)  # 'Name: Alice, Age: 30'
```

### f-strings (Formatted String Literals)

Introduced in Python 3.6, f-strings are a concise and readable way to format strings:

```
name = "Alice"
age = 30
formatted_string = f"Name: {name}, Age: {age}"  # 'Name: Alice, Age: 30'
```

## Accessing Characters in a String

Accessing individual characters in a Python string is straightforward thanks to Python’s support for indexing and slicing. Since strings are sequences of characters, each character in a string has a specific position, starting from 0 for the first character.

### Indexing

Indexing allows you to access a specific character in a string by its position. Python uses zero-based indexing, so the first character is at index 0, the second at index 1, and so on. Negative indexing is also supported, where -1 refers to the last character, -2 to the second last, and so forth.

Here’s how you can use indexing to access characters:

```
string = "Hello, World!"

# Accessing characters with positive indices
first_character = string[0] # 'H'
second_character = string[1] # 'e'

# Accessing characters with negative indices
last_character = string[-1] # '!'
second_last_character = string[-2] # 'd'
```

### Out-of-Range Indices

Attempting to access a character using an index that is out of the range of the string will result in an IndexError. It's important to ensure that the index you are accessing is within the valid range of the string’s length.

```
string = "Hello"
# Accessing out-of-range index
try:
 invalid_character = string[10] # IndexError
except IndexError:
 print("Index out of range")
```

### Slicing

Slicing allows you to access a substring by specifying a range of indices. The syntax for slicing is string[start:stop], where start is the beginning index (inclusive) and stop is the ending index (exclusive).

Here’s how slicing works:

```
 "Hello, World!"

# Slicing with start and stop indices
substring = string[0:5] # 'Hello'

# Omitting start index (defaults to 0)
substring_from_start = string[:5] # 'Hello'

# Omitting stop index (defaults to end of string)
substring_to_end = string[7:] # 'World!'

# Using negative indices for slicing
substring_negative = string[-6:-1] # 'World'
```

### Step in Slicing

The slicing syntax also supports an optional step parameter, which specifies the interval between indices to include in the slice. The syntax is:

```
string[start:stop:step].
string = "Hello, World!"

# Slicing with a step
every_second_character = string[::2] # 'Hlo ol!'

# Reversing a string using slicing with a negative step
reversed_string = string[::-1] # '!dlroW ,olleH'
```

### Using Loops to Access Characters

You can also access characters in a string using loops, which can be useful for iterating over each character in the string.

```
string = "Hello"

# Using a for loop to access each character
for char in string:
 print(char)
Alternatively, you can use a while loop along with indexing:
string = "Hello"
index = 0

# Using a while loop to access each character
while index < len(string):
 print(string[index])
 index += 1
```

## String Slicing

String slicing in Python is a powerful feature that allows you to access a substring or a portion of a string by specifying a range of indices. This capability makes it easy to extract and manipulate parts of strings without having to write complex loops or manually handle individual characters.

### Basic Slicing

The basic syntax for slicing is

```
string[start:stop]
```

where:

- ```
    start​
    ```
    
     is the index at which the slice begins (inclusive).
- ```
    stop​
    ```
    
     is the index at which the slice ends (exclusive).

Here are some examples to illustrate basic slicing:

```
string = "Hello, World!"

# Slicing from index 0 to 5 (characters 0 through 4)
substring = string[0:5]  # 'Hello'

# Slicing from index 7 to 12 (characters 7 through 11)
substring = string[7:12]  # 'World'
```

### Omitting Indices

You can omit the start or stop index to slice from the beginning of the string or to the end of the string, respectively:

```
string = "Hello, World!"

# Omitting the start index (default is 0)
substring_from_start = string[:5]  # 'Hello'

# Omitting the stop index (default is the end of the string)
substring_to_end = string[7:]  # 'World!'

# Omitting both start and stop (returns the entire string)
entire_string = string[:]  # 'Hello, World!'
```

### Negative Indices

Negative indices can be used to slice from the end of the string. For example, -1 refers to the last character, -2 to the second last, and so on:

```
string = "Hello, World!"

# Slicing with negative indices
substring_negative = string[-6:-1]  # 'World'
```

### Step in Slicing

The slicing syntax also supports an optional step parameter, which specifies the interval between indices in the slice. The syntax is

```
string[start:stop:step]:
```

```
string = "Hello, World!"

# Slicing with a step of 2 (every second character)
every_second_character = string[::2]  # 'Hlo ol!'

# Slicing with a negative step (reverses the string)
reversed_string = string[::-1]  # '!dlroW ,olleH'
```

## Concatenating Strings

Concatenating strings in Python involves combining two or more strings into a single string. This operation is common in various programming tasks, such as generating output, constructing messages, or building data structures. Python provides multiple approaches to concatenate strings, each offering flexibility and convenience for different scenarios.

### Using the + Operator

The simplest way to concatenate strings in Python is by using the + operator. You can directly concatenate two strings or combine strings with other data types:

```
str1 = "Hello"
str2 = "World"

# Concatenating two strings
concatenated = str1 + ", " + str2 + "!"  # 'Hello, World!'

# Combining strings with other data types
result = "The answer is: " + str(42)  # 'The answer is: 42'
```

In Python, string length refers to the number of characters present in a string. This includes letters, numbers, symbols, and whitespace characters. Knowing the length of a string is a fundamental aspect of text processing and is crucial for a variety of programming tasks.

### Measuring String Length

To measure the length of a string in Python, the built-in `len()` function is used. This function takes a string as its argument and returns the number of characters in that string.

#### Example:

```
my_string = "Hello, World!"
length = len(my_string)
print(length)  # Output: 13
```

In this example, '`len(my_string)` returns 13 because the string "Hello, World!" contains 13 characters, including the comma and space.

### Handling Multibyte Characters

Python 3 handles strings as sequences of Unicode characters, which means it counts characters rather than bytes. This is particularly useful for dealing with text in different languages that may include multibyte characters.

#### Example:

```
my_string = "你好"
length = len(my_string)
print(length)  # Output: 2
```

Here, `len(my_string)` returns 2 because there are two Chinese characters, even though each character might be represented by multiple bytes internally.

### String Length and Whitespace

Whitespace characters such as spaces, tabs (`\t`), and newlines (`\n`) are included in the string length.

#### Example:

```
my_string = "Hello\nWorld"
length = len(my_string)
print(length)  # Output: 11
```

## String Methods

String methods in Python provide a wide range of functionalities for manipulating and working with strings. These methods allow you to perform operations such as converting cases, searching for substrings, replacing text, splitting strings, and much more. Understanding and leveraging these methods can greatly simplify string manipulation tasks and make your code more concise and readable.

### Commonly Used String Methods

#### str.lower() and str.upper()

These methods return a new string with all characters converted to lowercase or uppercase, respectively.

```
string = "Hello, World!"
lowercase = string.lower()  # 'hello, world!'
uppercase = string.upper()  # 'HELLO, WORLD!'
str.strip()
The strip() method removes leading and trailing whitespace (spaces, tabs, and newlines) from a string.
string = "   Hello, World!   "
stripped = string.strip()  # 'Hello, World!'
```

#### str.replace(old, new)

The replace() method replaces all occurrences of a specified substring (old) with another substring (new) in a string.

string = "Hello, World!"

new_string = string.replace("World", "Python")  # 'Hello, Python!'

#### str.split(separator)

The split() method splits a string into a list of substrings based on a specified separator. By default, it splits on whitespace.

string = "Hello, World!"

split = string.split(",")  # ['Hello', ' World!']

#### str.join(iterable)

The join() method concatenates the elements of an iterable (such as a list) into a single string, using the string as a separator.

words = ["Hello", "World"]

joined_string = " ".join(words)  # 'Hello World'

#### str.find(substring) and str.index(substring)

These methods search for the first occurrence of a substring within a string and return its index. The find() method returns -1 if the substring is not found, while index() raises a

```
ValueError
```

string = "Hello, World!"

index = string.find("World")  # 7

### Chaining String Methods

String methods can be chained together to perform multiple operations sequentially, which can lead to more concise and readable code:

```
string = "   Hello, World!   "
processed_string = string.strip().lower().replace("world", "Python")
# 'hello, python!'
```

## String Formatting

String formatting in Python refers to the process of creating formatted strings by embedding variables, expressions, or other strings within a template string. This allows you to construct dynamic strings that incorporate data or values in a structured and readable manner. Python offers several approaches to string formatting, each with its own syntax and features.

### Using % Operator

The % operator is an older method for string formatting, where placeholders in the template string are replaced by values provided in a tuple or dictionary:

```
name = "Alice"
age = 30
formatted_string = "Name: %s, Age: %d" % (name, age)  # 'Name: Alice, Age: 30'
```

### Using str.format()

The str.format() method provides more flexibility and readability for string formatting. It allows you to specify placeholders and insert values in a template string using curly braces {}:

```
name = "Alice"
age = 30
formatted_string = "Name: {}, Age: {}".format(name, age)  # 'Name: Alice, Age: 30'
```

### Using f-strings (Formatted String Literals)

Introduced in Python 3.6, f-strings offer a concise and intuitive way to format strings by directly embedding expressions and variables within the string:

```
name = "Alice"
age = 30
formatted_string = f"Name: {name}, Age: {age}"  # 'Name: Alice, Age: 30'
```

F-strings provide a more readable and efficient alternative to % formatting and str.format(), especially when working with complex expressions or multiple variables.

## Iterating through a string

Iterating through a string in Python allows you to access each character in the string one by one. This can be done using a loop construct such as a for loop or a while loop:

### Using a for Loop

```
string = "Hello"
for char in string:
    print(char)
```

### Using a while Loop with Indexing

```
string = "Hello"
index = 0
while index < len(string):
    print(string[index])
    index += 1
```

Iterating through a string is useful for performing operations on each character, such as counting occurrences, checking for specific patterns, or transforming the characters.

## How to Compare Strings in Python?

Comparing strings in Python involves evaluating whether two strings are equal, or if one string comes before or after another in lexicographic (dictionary) order. Python provides several methods for comparing strings:

### Using Comparison Operators

You can use standard comparison operators (==, !=, <, >, <=, >=) to compare strings:

```
str1 = "apple"
str2 = "banana"
result = str1 == str2  # False
result = str1 < str2   # True (since 'apple' comes before 'banana' in dictionary order)
```

### Using str.compare()

The compare() method compares two strings and returns:

- 0 if the strings are equal.
- -1 if the first string is lexicographically less than the second.

1 if the first string is lexicographically greater than the second.

## String Example Problems

### Example 1: Counting Substrings

```
text = "Hello, Hello, World!"
substring = "Hello"
count = text.count(substring)  # 2
```

### Example 2: Palindrome Check

```
def is_palindrome(s):
    return s == s[::-1]

string = "radar"
result = is_palindrome(string)  # True
```

### Example 3: Word Reversal

```
sentence = "Hello, World!"
words = sentence.split()
reversed_sentence = " ".join(word[::-1] for word in words)
# 'olleH, dlroW!'
```