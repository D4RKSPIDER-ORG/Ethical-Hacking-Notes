## Break Statement in While Loop

[[B-Python-Basics Note-1]]
[[Lesson 7 - Python For Loops - Comprehensive Guide]]
[[Lesson 9 - Introduction to Python While Loop]]
The Python break statement is used to exit from the loop immediately after a particular condition is met.

Example:

Here's an example of using a while loop with a break statement to find the first even number in a sequence:

```
# Initialize a variable to store the current number
num = 1

# Iterate through numbers until we find the first even number
while True:
    if num % 2 == 0:
        print("First even number found:", num)
        break  # Exit the loop if an even number is found
    num += 1
```

In this example:

- We start with `num` initialized to 1.
- The `while True:` statement creates an infinite loop.
- Inside the loop, we check if `num` is divisible by 2 without a remainder (i.e., if it's even). If it is, we print a message indicating that the first even number is found, and then we `break` out of the loop.
- If `num` is not even, we increment it by 1 and continue the loop until an even number is found.

## Continue Statement in While Loop

The function of the continue statement is to skip the current iteration of a loop and continue with the next one.

Example:

Here's an example of using a while loop with a continue statement to skip printing odd numbers in a sequence:

```
# Initialize a variable to store the current number
num = 1

# Iterate through numbers and print only even numbers
while num <= 10:
    if num % 2 != 0:
        num += 1
        continue  # Skip the rest of the loop and move to the next iteration if num is odd
    print(num)
    num += 1
```

In this example:

- We start with `num` initialized to 1.
- The `while num <= 10:` statement sets the condition for the loop to execute until `num` reaches 10.
- Inside the loop, we check if `num` is odd by using the condition `num % 2 != 0`. If it is odd, we `continue`, skipping the rest of the loop body and moving to the next iteration.
- If `num` is even, we print its value and then increment `num`.
- This loop prints only the even numbers between 1 and 10, skipping the odd numbers.

## While Loop With Else

Python allows an else clause at the end of a while loop. The else part is executed if the loop terminates naturally.

Example:

Here's an example of a while loop with an else block that prints a message if the loop completes without encountering a break statement:

```
# Initialize a variable
count = 0

# Iterate through numbers
while count < 5:
    print("Inside the loop:", count)
    count += 1
else:
    print("Loop completed without encountering a break statement.")
```

In this example:

- We start with `count` initialized to 0.
- The `while count < 5:` statement sets the condition for the loop to execute until `count` reaches 5.
- Inside the loop, it prints the current value of `count` and then increments it by 1.
- After the loop completes all iterations, the `else` block is executed, printing a message indicating that the loop completed without encountering a `break` statement.
- Since there are no `break` statements in this loop, the `else` block will always execute after the loop completes its iterations.

#### Become a Full Stack Developer in Just 6 Months!

Full Stack Java Developer[Explore Program](https://www.simplilearn.com/java-full-stack-developer-certification?source=GhPreviewCTABanner)

## Python While Loop Exercise

We would suggest attempting the following question on your own before you refer to the solutions.

Question: Write a program to add all the numbers less than 10 using while loop.

Solution:

```
# Initialize variables
total = 0
num = 1

# Iterate through numbers less than 10 and add them to the total
while num < 10:
    total += num
    num += 1

# Print the total sum
print("The sum of all numbers less than 10:", total)
```

## Ending a While Loop in Python

In Python, you can end a `while` loop using the `break` statement. The `break` statement immediately terminates the innermost enclosing loop. Here's an example:

```
count = 0
while True:
    print(count)
    count += 1
    if count >= 5:
        break  # End the loop if count is greater than or equal to 5
```

In this example, the loop will continue indefinitely (`while True:` creates an infinite loop) until the `count` variable becomes greater than or equal to 5. Once `count` reaches 5 or more, the `break` statement is executed, terminating the loop.

> Learn data operations in Python, strings, conditional statements, error handling, and the commonly used Python web framework Django. Check out Simplilearn's [Python Training course](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCTAText "Python Training course").

## Learn Python and Take Your Career to the Next Level

Understanding Python loops is one of the many steps toward mastering this exciting and versatile programming language. As big data and business intelligence become more broadly adopted across all industries, mastering Python could open doors in your professional career. Simplilearn’s [Python Training Course](https://www.simplilearn.com/mobile-and-software-development/python-development-training "Python Training Course") is a great introduction to this dynamic programming language.

## FAQs

### 1. What is a do-while loop in Python with an example?

Python doesn't have a built-in do-while loop like some other programming languages do. However, you can achieve similar behavior using a while loop with an initial condition and then checking the condition again at the end of the loop. Here's an example:

```
# Example of a do-while loop in Python
count = 0
while True:
 print(count)
 count += 1
 if count >= 5:
 break
```

In this example, the loop will execute at least once, and then the condition if count >= 5 acts as the exit condition, similar to the condition typically checked at the start of a do-while loop in other languages.

### 2. What is called a while loop?

A while loop is a control flow statement that allows code to be executed repeatedly based on a given condition. The loop continues to execute the block of code as long as the condition remains true. Once the condition becomes false, the loop terminates. Here's a general syntax:

```
while condition:
# Code block to execute
```

### 3. What is the difference between while and for loop?

- - while loop: A while loop repeats a block of code as long as a specified condition is true. It is useful when you don't know in advance how many times the loop will iterate.
    - for loop: A for loop iterates over a sequence (such as a list, tuple, string, etc.) or other iterable objects. It executes the block of code for each item in the sequence. It's typically used when you know the number of iterations or when you need to iterate over a collection of elements.

### 4. How to restart a while loop in Python?

You can restart a while loop by using the continue statement. When the continue statement is encountered within a loop, the current iteration of the loop is terminated, and the next iteration begins. Here's a simple example:

```
count = 0
while count < 5:
 count += 1
 if count == 3:
 continue # Restart the loop when count is 3
 print(count)
```

In this example, when `count` becomes 3, the `continue` statement is executed, skipping the rest of the loop's code for that iteration and restarting the loop with the next iteration.