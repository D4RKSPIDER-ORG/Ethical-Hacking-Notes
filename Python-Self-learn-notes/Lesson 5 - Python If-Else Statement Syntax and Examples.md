[[B-Python-Basics Note-1]]
[[Lesson 1 - Print & Strings]]
Decision making is an essential concept in any programming language and is required when you want to execute code when a specific condition is satisfied. In this blog, you will learn about the famous if-else statement in Python. We’ll be using [Jupyter Notebook](https://www.simplilearn.com/tutorials/python-tutorial/jupyter-notebook "Jupyter Notebook") to demonstrate the code.

There are multiple forms of if-else statements. Let’s explore them one by one.

## If Statement

It uses the if keyword, followed by the condition.

### Syntax:

if condition:

#statement to execute if the condition is true

Below is the entire workflow of how if statements work:

![test-expression](https://www.simplilearn.com/ice9/free_resources_article_thumb/test-expression.JPG)

First, the test expression is checked. If the expression is true, the body of the if the statement is executed. If it is false, the statement present after the if statement is executed. In either case, any line of code present outside if the statement is evaluated by default.

To understand this better, we’ll use an example:

a=20

if a>50:

    print("This is the if body")

print("This is outside the if block")

Since 20 is not greater than 50, the statement present inside the if block will not execute. Instead, the statement present outside the if block is executed.

![if-block.](https://www.simplilearn.com/ice9/free_resources_article_thumb/if-block.JPG)

In the code below, both the print statements will be executed since a is greater than 50.

![outside-if](https://www.simplilearn.com/ice9/free_resources_article_thumb/outside-if.JPG)

So far, we could specify the statements that will be executed if a condition is true. Now, if you want to evaluate statements that determine whether a condition is actual and if a separate set of statements is false, you can use the if-else conditional statement.

#### Basics to Advanced - Learn It All!

Full Stack Java Developer Masters Program[Explore Program](https://www.simplilearn.com/java-full-stack-developer-certification?source=GhPreviewCTABanner)

![Basics to Advanced - Learn It All!](https://www.simplilearn.com/ice9/banners/free_resources_banners/lead_banners/Full_Stack_Java_Developer.png)

## If-Else Statement

The if-else statement is used to execute both the true part and the false part of a given condition. If the condition is true, the if block code is executed and if the condition is false, the else block code is executed.

### Syntax:

if(condition):

#Executes this block if the condition is true

else:

#Executes this block if the condition is false

You should note here that Python uses indentation in both the blocks to define the scope of the code. Other [programming languages](https://www.simplilearn.com/best-programming-languages-start-learning-today-article "programming languages") often use curly brackets for this purpose.

Below is the entire workflow of how the if-else statement works.

![false](https://www.simplilearn.com/ice9/free_resources_article_thumb/false.JPG)

First, the test expression is checked. If it is true, the statements present in the body of the if block will execute. Next, the statements present below the if block is executed. In case the test expression has false results, the statements present in the else body are executed, and then the statements below the if-else are executed.

![ifblock-even](https://www.simplilearn.com/ice9/free_resources_article_thumb/ifblock-even.JPG)

The following is an example that better illustrates how if-else works:

![ifblock-odd.](https://www.simplilearn.com/ice9/free_resources_article_thumb/ifblock-odd.JPG)

Since the value of “i” is divisible by two, the if statement is executed.

Since the value of “i” is not divisible by two, the else statement is executed.

Let us now look at what a nested IF statement is and how it works.

## Nested IF Statement

When an if a statement is present inside another if statement, it is called a nested IF statement. This situation occurs when you have to filter a variable multiple times.

### Syntax:

if (condition1):

    #Executes if condition1 is true

    if (condition2):

        #Executes if condition2 is true

    #Condition2 ends here

#Condition1 ends here

In nested IF statements, you should always take care of the indentation to define the scope of each statement. You can have as many levels of nesting as required, but it makes the program less optimized, and as a result, can be more complex to read and understand. Therefore, you should always try to minimize the use of nested IF statements.

The workflow below demonstrates how nested IF statements work:

![test-expression-1](https://s3.amazonaws.com/static2.simplilearn.com/ice9/free_resources_article_thumb/test-expression-1.JPG)

The following is another example that shows how nested IF works: We have a number, and we’re going to check if the number is greater or less than 25. If the number is less than 25, we’ll check if it is an odd number or an even number. If the number is greater than 25, we will print that the number is greater than 25.

![c-evenodd](https://www.simplilearn.com/ice9/free_resources_article_thumb/c-evenodd.JPG)

So far, with IF and if-else, we have only seen a binary approach. Suppose we have a problem that has multiple conditions. In this scenario, the if-elif-else statement comes to the rescue.

## If-Elif-Else Statement

It checks the if statement condition. If that is false, the elif statement is evaluated. In case the elif condition is false, the else statement is evaluated.

### Syntax:

if (condition):

    statement

elif (condition):

    statement

.

.

else:

    Statement

Below is a flowchart that shows how the if-elif-else ladder works. The Test Expression1 is checked. If that proves true, the body of if is evaluated. If it is false, then the control moves to the proceeding Test Expression2. If it’s true, the body of elif1 is executed. If it’s false, the test expression3 is checked. If true, the body of elif2 is executed. If it is false, the body of else is evaluated. Any statement below in if-elif is then checked.

![test-expression-123](https://www.simplilearn.com/ice9/free_resources_article_thumb/test-expression-123.JPG)

The program below uses the if-elif-else ladder to check if a letter is a vowel or a consonant.

![var](https://www.simplilearn.com/ice9/free_resources_article_thumb/var.JPG)

Now that we have looked at the basics of if, else, elif and nested IF, let’s do some exercises.

## What Happens When the ‘If Condition’ Does Not Meet?

If the conditional statement is true, the code block included within the if statement is executed. But, if the condition is not met, the code inside the curly brackets is skipped, and the next if statement will be executed. It shows an error because it does not match the specified if condition. 

## When ‘Else Condition’ Does Not Work?

It is sometimes impossible to get desired output using the 'else condition'. This is because of a logical error that occurs in the program. This often occurs when a program has more than two statements or conditions. If you get an issue with the else, it's because you directed the operator that the ';' marks the conclusion of your if statement; hence, when it discovers the 'else' a few steps later, it starts to report.

## What Does for Else and While Else Mean in Python?

Python provides handy features such as for-else and while-else. The else block may be used immediately following the for and while loop. If a [break statement](https://www.simplilearn.com/tutorials/python-tutorial/break-in-python "break statement") does not end the loop, the else block will be performed.

The syntax for for-else Python is:

for i in range(n) :

         #code

else :

         #code 

The syntax for while-else Python is:

while condition :

        #code

else:

        #code

## What Does == Mean in Python?

The equality of the two objects is compared using the '= =' operator. In Python, one equal mark '=' allocates a value to a variable, while two equal marks '==' check if two expressions give the same value. In general, you're comparing the worth of two items. If you want to assess if two objects share similar characteristics and don't bother where they're kept in memory, this is all you require.

#### Basics to Advanced - Learn It All!

Full Stack Java Developer Masters Program[Explore Program](https://www.simplilearn.com/java-full-stack-developer-certification?source=GhPreviewCTABanner)

![Basics to Advanced - Learn It All!](https://www.simplilearn.com/ice9/banners/free_resources_banners/lead_banners/Full_Stack_Java_Developer.png)

## ShortHand If

A shorthand statement is an executable statement constructed so concisely that it only contains one line of code. For example, Python offers various shorthand statements, allowing us to compose our code more condensed and space-efficiently.

## ShortHand If … else

Shorthand is an excellent approach to building small if-else statements when you have only one line to execute. Python provides programmers with many syntactic options for writing the same code. For example, you can create an if-else statement in one code line using a shorthand if-else feature. 

The format for shorthand, if else, is:

statement1 if condition else statement2

## Python Operators

[Operators](https://www.simplilearn.com/tutorials/python-tutorial/operators-in-python "Operators") are generally utilized for carrying out functions on values and attributes. These are common symbols used in logical and mathematical processes. For example, arithmetic operators can carry out fundamental mathematical operations. For comparing two values, relational operators are used, and results are true or false depending on the criteria. Boolean or logical operators are: AND, OR and NOT. Bitwise operators are operators for binary numbers. 

### AND

AND is a logical operator in Python. The operator returns TRUE if both the values are actual, that is, both on the left and right sides.

### OR

The operator returns, OR if any of the values is true, it can be the right or left side. 

### NOT

The operator returns true when both sides of the values are false.

Below is an example of logical operators:

p = true

s = false

print( (‘p and s is’, x and y) )

print( (‘p or s is’, x or y) )

print( (‘not p is’, not x) )

#### Output:

(p and s is, False)

(p or s is', True)

('not p is', False)

## The Pass Statement

The pass statement in Python programming is a null statement that can be utilized as a blank for future code. For example, assume you have an unimplemented loop or function you intend to build. You can utilize the pass statement in such circumstances. However, there is a difference between a pass statement and a comment; the interpreter cannot ignore a pass statement, while a comment can be ignored.

## Switch Case Statement in Python

Switch case is not in-built into Python, but you can implement them using various other methods. For example, switching execution control can be performed using a control statement. In addition, Python has developed structural pattern matching, a switch case feature. Using match and case keywords, you can put this feature into practice. You can use match and case keywords as both variable and function names. A switch statement compares the values of variables to the values mentioned in case statements. A case statement is often a multiway branch statement.

## Lambda if Else in Python 

Although a [lambda](https://www.simplilearn.com/tutorials/python-tutorial/lambda-in-python "lambda") function might have many parameters, it only has one expression. An evaluation and return are made for this single expression. Therefore, lambda functions may be used as functional objects. The lambda function will return a value for each data that is given. When the condition, in this case, is true, the if block is returned; when it is false, the else block is returned.

The format for the lambda if-else function is:

lambda <arguments> : <statement1> if <condition> else <statement2>



