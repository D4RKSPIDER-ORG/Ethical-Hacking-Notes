## What Are Python loops?

[[B-Python-Basics Note-1]]
[[Lesson 7 - Python For Loops - Comprehensive Guide]]
[[Lesson 8 - Introduction to Python While Loop]]
[[Lesson 9 - Introduction to Python While Loop]]
A loop is an instruction that repeats multiple times as long as some condition is met.

**Flowchart:**

![flowchart.](https://www.simplilearn.com/ice9/free_resources_article_thumb/flowchart.JPG)

Fig: Flowchart of Python loop

### Significance of indentation

Indentation is significant in Python. It is used to define a block of code; without indentation, the program will show an error.

## Type of Loops

There are mainly two types of loops. Let’s discuss them one by one.

### 1. For Loop

A [**for** loop](https://www.simplilearn.com/tutorials/python-tutorial/python-for-loop "for Loop") in Python is used to iterate over a sequence (list, tuple, set, dictionary, and string).

**Flowchart:**

![for-loop](https://www.simplilearn.com/ice9/free_resources_article_thumb/for-loop.JPG)

Fig: Flowchart of a for loop

**Syntax:** for iterating_var in sequence:  

   statement(s) 

**Example:**

**![for-loop-ex.](https://www.simplilearn.com/ice9/free_resources_article_thumb/for-loop-ex.JPG)**

Fig: for loop example

The preceding code executes as follows: The variable **i** is a placeholder for every item in your iterable object. The loop iterates as many times as the number of elements and prints the elements serially.

### **2. While Loop**

The while loop is used to execute a set of statements as long as a condition is true.

**Flowchart:**

![whileloop](https://www.simplilearn.com/ice9/free_resources_article_thumb/whileloop.JPG)

Fig: While loop flowchart

**Syntax:** while expression:  

    statements  

**Example:**

 ![while-loop](https://www.simplilearn.com/ice9/free_resources_article_thumb/while-loop.JPG)

Fig: While loop

The preceding code executes as follows: We assign the value to variable x as 1. Until the value of x is less than 3, the loop continues and prints the numbers. 

#### Automation Test Engineer Master's Program

To learn about the automation of web applications[Explore Course](https://www.simplilearn.com/automation-testing-masters-program-certification-training-course?source=GhPreviewCTAText)

![Automation Test Engineer Master's Program](https://www.simplilearn.com/ice9/banners/free_resources_banners/lead_banners/Vector_Automation_test_engineer.png)

### **3. Nested Loop**

If a loop exists inside the body of another loop, it is called a nested loop.

**Example:**

**![nested-loop](https://www.simplilearn.com/ice9/free_resources_article_thumb/nested-loop.JPG)**

Fig: Nested loop

The preceding code executes as follows: The program first encounters the outer loop, performing its first iteration. This first iteration triggers the inner, nested loop, which then runs to completion. Then the program returns to the top of the outer loop, completing the second iteration and again triggers the nested loop. The nested loop runs to completion, and the program returns to the top of the outer loop until the sequence is complete.

## Conditional Statements in Python

Decision-making statements are used to execute the statements only when a particular condition is fulfilled.

**Flowchart:**

![conditional-statement](https://www.simplilearn.com/ice9/free_resources_article_thumb/conditional-statement.JPG)

Fig: Conditional statement flowchart

There are three main types of conditional statements. They are:

**1. If statement:** The if statement is used to test a specific condition. If the condition is true, a block of code is executed.

**Syntax:** if expression:

  statement(s)

**Flowchart:**

![flowchart-if](https://www.simplilearn.com/ice9/free_resources_article_thumb/flowchart-if.JPG)

Fig: flowchart of if statement in Python loop

**Example:**

![if](https://www.simplilearn.com/ice9/free_resources_article_thumb/if.JPG)

Fig: if statement in Python loop

**2. Else statement:** The else statement is executed when the expression in the if condition is false.

**Flowchart:**

![else-flow](https://www.simplilearn.com/ice9/free_resources_article_thumb/else-flow.JPG)

Fig: else flowchart in Python loop

**Example:**

![/else-state](https://www.simplilearn.com/ice9/free_resources_article_thumb/else-state.JPG)

Fig: else statement  
  

**3. Elif statement**: The **elif** statement in Python enables you to check multiple conditions and execute specific blocks of statements if the previous conditions were false.

**Example:**

![elif-stat.](https://www.simplilearn.com/ice9/free_resources_article_thumb/elif-stat.JPG)

Fig: elif statement in Python

## Practice Exercises

It’s time to test our understanding with these practice exercises. We will suggest trying to solve the questions on your own.

**Question 1:** Write a program to check if the given number is prime or not.

**Program:**

![sol-1.](https://www.simplilearn.com/ice9/free_resources_article_thumb/sol-1.JPG)

Fig: Solution 1

The preceding code executes as follows: You assign value to a variable number. If the number entered is greater than 1, you check for factors of that number. If a factor is found, it is not a prime number. Otherwise, the given number is a prime number.

**Question 2:** Write a program to print the numbers from 1 to 10. Exit the loop if the number becomes equal to 6.

**Program:**

![](https://www.simplilearn.com/ice9/free_resources_article_thumb/sol-2.JPG)

Fig: Solution 2

The preceding code executes as follows: Until the value of myNum does not become equal to myVar, the while loop iterates. As soon as the value becomes equal, the loop breaks.