## Python for loops

[[B-Python-Basics Note-1]]
[[Lesson 8 - Introduction to Python While Loop]]
[[Lesson 9 - Introduction to Python While Loop]]

For loops in Python iterate over a sequence (such as a list, tuple, string, or range) and execute a block of code multiple times. They're beneficial for performing repetitive tasks efficiently and can handle numerical and non-numerical data. Python for loops are simple and flexible, making them a fundamental tool for [programming](https://www.simplilearn.com/tutorials/programming-tutorial/coding-for-beginners "programming").

### Flowchart of for loop Python

Start

   |

[Initialize Sequence]

   |

[First Item in Sequence] --> [Process Item] --> [Next Item in Sequence]

   |                                 |

   +-------------[Last Item?]--------+

                                 |

                                [End]

### Syntax

```
for item in sequence:
# Code block to be executed
```

### Example

```
numbers = [1, 2, 3, 4, 5]
for number in numbers:
print(number)
```

In this example, the loop iterates over each item in the numbers list and prints it to the console. The output will be:

> 1
> 
> 2
> 
> 3
> 
> 4
> 
> 5

#### Skyrocket Your Career: Earn Top Salaries!

Python Certification Course[ENROLL NOW](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCTABanner)

## How to Iterate Over a String With a Python for loop?

You can treat the [string](https://www.simplilearn.com/tutorials/python-tutorial/python-strings) as a sequence of characters to iterate over a string with for loops in Python. Each iteration of the loop will process one character from the string. Here's an example to illustrate this:

```
text = "Hello, World!"
for char in text:
print(char)
```

#### Explanation

- Initialization: The string text is initialized with "Hello, World!".
- Iteration: The for loop iterates over each character in the string.
- Processing: The current character (char) is printed during each iteration.

#### Output

In this example, the loop iterates over each character in the string text and prints it. The output will be:

> H
> 
> e
> 
> l
> 
> l
> 
> o
> 
> ,
> 
> W
> 
> o
> 
> r
> 
> l
> 
> d
> 
> !

## Break Statement in Python for loop

The [break statement in Python](https://www.simplilearn.com/tutorials/python-tutorial/break-in-python) for loop terminates the loop prematurely when a specific condition is met. Once the break statement is executed, the loop stops iterating, and the program control moves to the following statement after the loop.

### Example

```
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for number in numbers:    
if number == 5:        
break    
print(number)
print("Loop terminated when number reached:", number)
```

#### Explanation

- Initialization: The list numbers are initialized with values from 1 to 10.
- Iteration: The for loop iterates over each number in the list.
- Condition: The loop checks if the current number equals 5 during each iteration.
- Break: The break statement is executed when the number 5 is encountered, terminating the loop.
- Output: The loop stops, and the program prints the numbers from 1 to 4, followed by a message indicating that the loop was terminated when the number reached 5.

#### Output

> 1
> 
> 2
> 
> 3
> 
> 4

Loop terminated when the number reached: 5

## Continue Statement in Python for loop

The continue statement in a Python for loop skips the current iteration and moves to the next iteration. When the continue statement is executed, the loop doesn't terminate but jumps to the next iteration, bypassing any code that follows it within the [Python loop](https://www.simplilearn.com/tutorials/python-tutorial/python-loops).

#### Unleash Your Career as a Full Stack Developer!

Full Stack Developer - MERN Stack[EXPLORE COURSE](https://www.simplilearn.com/full-stack-developer-course-mern-certification-training?source=GhPreviewCTABanner)

### Example

```
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for number in numbers:    
if number % 2 == 0:        
continue    
print(number)
print("Loop skipped even numbers")
```

#### Explanation

- Initialization: The list numbers are initialized with values from 1 to 10.
- Iteration: The for loop iterates over each number in the list.
- Condition: During each iteration, the loop checks if the current number is even (i.e., if number % 2 == 0).
- Continue: If the number is even, the continue statement is executed, causing the loop to skip the current iteration and move to the next number.
- Processing: If the number is odd, it is printed to the console.

#### Output

> 1
> 
> 3
> 
> 5
> 
> 7
> 
> 9

Loop skipped even numbers

## The Range() Function in Python for loop

The [range() function](https://www.simplilearn.com/tutorials/python-tutorial/range-in-python) in Python for loop generates a sequence of numbers. It is often used to iterate over a specific set of values in for loops in python. The range() function can take one, two, or three arguments: start, stop, and step.

### Example

```
for i in range(1, 10, 2):
print(i)
```

#### Explanation

- Initialization: The range() function is called with three arguments: start = 1, stop = 10, and step = 2.
- Iteration: The for loop iterates over the sequence generated by range(1, 10, 2).
- Processing: During each iteration, the current value of i is printed.

#### Output

> 1
> 
> 3
> 
> 5
> 
> 7
> 
> 9

In this example, the range() function generates the sequence [1, 3, 5, 7, 9]. The Python for loop then iterates over this sequence, printing each value. The loop starts at 1 and increments by 2 each time, stopping before it reaches 10.

#### Dive Deep into Core Python Concepts

Python Certification Course[ENROLL NOW](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCTABanner)

## Python for loop Enumerate

The [enumerate function](https://www.simplilearn.com/tutorials/python-tutorial/enumerate-in-python) in Python is used with a for loop to iterate over a list (or other iterable) and have access to both the index and the item at that index during each iteration. This can be very useful when you need to know the position of items in a list as you process them.

### Example

```
# Sample list
fruits = ["apple", "banana", "cherry", "date"]
# Using enumerate in a for loop
for index, fruit in enumerate(fruits):
print(f"Index {index}: {fruit}")
```

#### Explanation

In this example, enumerate(fruits) returns pairs of an index and an item from the list of the fruits. The for loop then iterates over these pairs, unpacking them into the variable's index and fruit. The print statement outputs the index and the corresponding fruit for each iteration.

#### Output

> Index 0: apple
> 
> Index 1: banana
> 
> Index 2: cherry
> 
> Index 3: date

## Else in for loop Python

The [else](https://www.simplilearn.com/tutorials/python-tutorial/python-if-else-statement "else") block after a for loop in Python is executed when it usually completes (i.e., it is not terminated by a break statement). This can be useful when distinguishing between a loop that completed all iterations and one that exited early.

### Example

```
# Sample list
numbers = [1, 2, 3, 4, 5]
# Using else in a for loop
for number in numbers:    
if number % 7 == 0:        
print(f"Found a multiple of 7: {number}")        
break
else:    
print("No multiples of 7 found in the list")
```

#### Explanation

In this example, the Python for loop iterates over the numbers list, looking for a number that is a multiple of 7. If it finds such a number, it prints a message and breaks out of the loop. The other block is executed if the loop completes all iterations without finding a multiple of 7.

#### Output

Since there are no multiples of 7 in the numbers list, the output will be:

No multiples of 7 found in the list.

#### Master Web Scraping, Django & More!

Python Certification Course[ENROLL NOW](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCTABanner)

## Nested Loops in for loop Python

Nested loops are loops within loops. In Python, you can nest any loop inside another loop.

### Example

```
# Outer loop for rows
for i in range(1, 6):    
# Inner loop for columns    
for j in range(1, 6):        
print(f"{i * j:2}", end=" ")    
print()  # Newline after each row
```

#### Explanation

In this example, the outer loop iterates over the range from 1 to 5, representing the rows of the multiplication table. The inner loop also iterates over the range from 1 to 5, representing the columns. The product of the current row and column indices (i * j) is printed, with a space (end=" ") to separate the numbers on the same row. After each inner loop completes, a new line is printed to move to the next row.

#### Output

The output of this code will be:

> 1  2  3  4  5 
> 
>  2  4  6  8 10 
> 
>  3  6  9 12 15 
> 
>  4  8 12 16 20 
> 
>  5 10 15 20 25 

## Pass Statement in Python for loop

The [pass statement](https://www.simplilearn.com/tutorials/python-tutorial/pass-in-python) in for loop Python is a null operation; it does nothing when executed. It's used as a placeholder for code that has yet to be written or to create minimalistic function bodies that do nothing.

### Example

```
# Example of pass statement in a function
def placeholder_function():    
pass
# Example of pass statement in a loop
for i in range(5):    
if i % 2 == 0:        
pass  # Placeholder for future code    
else:        
print(f"Odd number: {i}")
```

#### Explanation

In this example:

- placeholder_function is defined but does nothing because of the pass statement.
- In the for loop, the pass statement is used as a placeholder for future code in the if block that checks if i is an even number. For odd numbers, it prints the number.

#### Output

> Odd number: 1
> 
> Odd number: 3
> 
> Odd number: 5

## For loops in Python with Dictionary

In Python, you can use a for loop to iterate over the keys and values of a dictionary. The items method of a [dictionary](https://www.simplilearn.com/dictionary-in-python-article "dictionary") returns a view object that displays a list of a dictionary's key-value tuple pairs, which can be used in a for loop.

### Example

```
# Sample dictionary
student_grades = {    
"Alice": 85,    
"Bob": 90,    
"Charlie": 78,    
"Diana": 92}
# Using a for loop to iterate over dictionary items
for student, grade in student_grades.items():    
print(f"{student}: {grade}")
```

#### Explanation

In this example, student_grades.items() returns pairs of keys (student names) and values (grades). The for loop iterates over these pairs, unpacking them into the variables student and grade. The print statement outputs the student's name and their grade for each iteration.

#### Output

> Alice: 85
> 
> Bob: 90
> 
> Charlie: 78
> 
> Diana: 92

## Python for loop with Tuple

You can use a Python for loop to iterate over a list of tuples. During each iteration, you can unpack the tuple into individual variables.

### Example 

```
# List of tuples
students = [("Alice", 90), ("Bob", 85), ("Charlie", 92), ("David", 88)]
# Using a for loop to iterate over the list of tuples
for name, grade in students:    
print(f"{name} scored {grade}")
```

#### Explanation

In this example, students is a list of tuples, each containing a student's name and grade. The for loop iterates over each tuple in the list, unpacking it into the variables' names and grades. The print statement then outputs the student's name and corresponding grade for each iteration.

#### Output

> Alice scored 90
> 
> Bob scored 85
> 
> Charlie scored 92
> 
> David scored 88

#### Skyrocket Your Career: Earn Top Salaries!

Python Certification Course[ENROLL NOW](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCTABanner)

## For loop Python with Zip()

The zip function in Python allows you to iterate over multiple iterables (like lists, tuples, etc.) in parallel, combining their elements into tuples. This can be very useful when processing multiple sequences in tandem.

### Example

```
# Sample lists
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

# Using zip in a for loop
for name, age in zip(names, ages):
    print(f"{name} is {age} years old.")
```

#### Explanation

In this example, zip(names, ages) pairs up elements from the names and ages lists, creating tuples. The for loop then iterates over these [tuples](https://www.simplilearn.com/tutorials/python-tutorial/python-tuples), unpacking them into the variable's name and age. The print statement outputs the name and corresponding age for each iteration.

#### Output

> Alice is 25 years old.
> 
> Bob is 30 years old.
> 
> Charlie is 35 years old.

## Conclusion

In this tutorial, we've explored Python's powerful and versatile `for` loop, learning how to use it effectively with functions like `enumerate` and `zip` to iterate over lists and other iterables. By mastering these techniques, you can write more efficient and readable code, making your [programming skills](https://www.simplilearn.com/essential-programmer-skills-article) more manageable.

Consider enrolling in our [Python Certification Course](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCoursepages "Python Certification Course") to enhance your Python skills further and dive deeper into advanced topics. It is designed to provide you with a solid foundation in Python programming, with expert-led sessions and hands-on projects to reinforce your learning.

## FAQs

### 1. How to start for loop from 1 in Python?

To start a for loop from 1 in Python, use the range() function like this:

```
for i in range(1, n):    
# code block
```

Here, n is the endpoint, and the loop will start at 1 and continue until n-1.

### 2. What is the range function in Python for loop?

The range() function generates a sequence of numbers, which can be used to iterate over in a for loop. It accepts up to three arguments: start, stop, and step, and returns an immutable sequence of numbers from the start (inclusive) to stop (exclusive).

### 3. What is I in for loop?

I in a for loop is a loop variable that takes on each value in the sequence or is iterable during each iteration. It's commonly used as a counter or to reference elements in a sequence.

### 4. What is the formula of loop?

There isn't a fixed "formula" for loops, but loops typically follow the structure:

```
for variable in iterable:    
# code block
```

The loop executes the code block for each item in the iterable (like a list, range, etc.).

### 5. How to create a list in Python?

A list in Python can be created by placing comma-separated values inside square brackets. For example:

```
my_list = [1, 2, 3, 4, 5]
```

Lists can contain elements of different data types, including numbers, strings, and other lists.

## About the Author