[[B-Python-Basics Note-1]]
[[Lesson 1 - Print & Strings]]
## Python Numbers

Python numbers are a fundamental data type for representing and manipulating numerical values. The three main forms of numbers in Python are integers, floating-point numbers, and complex numbers.

### 1. Int

Whole numbers without a fractional component are called integers. They could be zero, negative, or positive.

#### Example

‘x = 42’ and ‘y = -19’ are integers.

### 2. Float

A decimal point added to a real number makes it a floating-point number. To represent fractional values, they are employed.

#### Example

‘a = 3.14’ and ‘b = -0.001’ are floats.

### 3. Complex

The 'complex' type of number indicates that it contains both an imaginary and real component. The letters 'j' or 'J' represent the fictitious portion.

#### Example

‘z = 2 + 3j’, where ‘2’ is the real part and ‘3j’ is the imaginary part.

## Type Conversion in Python

Python type conversion facilitates operations between multiple kinds by enabling you to change the data type of a variable to another. Both built-in functions and arithmetic operations can be used to do this.

### 1. Using Arithmetic Operations

Arithmetic operations can implicitly convert types.

#### Example

dividing two integers results in a float: ‘result = 5 / 2’ yields ‘result’ as ‘2.5’.

### 2. Using built-in functions

Built-in functions for explicit type conversion are available in Python.

#### Example

```
‘int()’, ‘float()’, and ‘str()’ convert values to integers, floats, and strings, respectively. Converting a float to an integer can be done with ‘int(3.9)’, which results in ‘3’.
```

## Decimal Numbers in Python

Python's ability to handle decimal numbers enables exact arithmetic operations, which are particularly helpful in financial applications where precision is essential. Python's 'decimal' module helps prevent rounding errors related to floating-point integers and allows arbitrary precision arithmetic.

### 1. Precision

The 'decimal' module allows you to set the precision of decimal numbers, enabling exact representations and calculations.

#### Example

```
‘from decimal import Decimal, getcontext; getcontext().prec = 4; result = Decimal('1.12345') + Decimal('2.67890')’, which results in ‘result’ being ‘3.802’.
```

### 2. Rounding

The decimal module provides various rounding options to control how numbers are rounded. You can specify different rounding modes like ‘ROUND_UP’, ‘ROUND_DOWN’, ‘ROUND_HALF_UP’, etc.

#### Example

```
‘from decimal import Decimal, ROUND_HALF_UP, getcontext; getcontext().rounding = ROUND_HALF_UP; result = Decimal('2.675')’.quantize(Decimal('0.01')) rounds ‘2.675’ to ‘2.68’
```

### 3. Arithmetic Operations

The ‘decimal’ module supports all standard arithmetic operations with high precision

#### Example

```
‘from decimal import Decimal; a = Decimal('1.1'); b = Decimal('2.2'); result = a + b’ results in ‘result’ being ‘3.3’, maintaining precision without floating-point errors.
```

### 4. Context Management

The ‘decimal’ module allows managing arithmetic operations' context, such as precision and rounding, using the ‘decimal.Context’ class.

#### Example

```
‘from decimal import Decimal, Context; context = Context(prec=5); result = context.add(Decimal('1.23456'), Decimal('7.89012'))’ results in ‘result’ being ‘9.1247’.
```

## Best Practices

Working with numbers in Python efficiently and accurately requires following some best practices. Here are key recommendations for handling numbers in Python:

### 1. Choose the Right Data Type

Select the appropriate numerical type for your needs. Use integers ‘(int)’ for whole numbers, floating-point numbers ‘(float)’ for real numbers with decimals, and the ‘decimal’ module for high-precision arithmetic, especially in financial calculations. For complex numbers, use the ‘complex’ type.

#### Example

```
from decimal import Decimal# Using intcount = 10# Using floataverage = 7.5# Using Decimal for precise calculationsprice = Decimal('19.99')
```

### 2. Avoid Floating-Point Arithmetic for Precision-Critical Applications

Due to inherent limitations in floating-point arithmetic, consider using the ‘decimal module’ or ‘fractions.Fraction’ for applications requiring precise decimal representation and calculations.

#### Example

```
from decimal import Decimal# Using Decimal for precise financial calculationstotal = Decimal('10.99') + Decimal('20.01')
```

### 3. Be Mindful of Division Operations

Understand the difference between true division (‘/’) and floor division (‘//’). Use floor division when you need an integer result without the fractional part.

#### Example

```
# True divisionresult = 5 / 2  # result is 2.5# Floor divisionresult = 5 // 2  # result is 2
```

### 4. Use Built-in Functions for Type Conversion

Convert between numerical types using built-in functions like ‘int()’, ‘float()’, and ‘complex()’ to ensure clarity and avoid unexpected results.

#### Example

```
# Converting float to intnum = 7.8whole_num = int(num)  # whole_num is 7
```

### 5. Leverage Math and NumPy Libraries

For complex mathematical operations, utilize the ‘math’ module for standard mathematical functions and the ‘NumPy’ library for advanced numerical operations, array manipulations, and linear algebra.

#### Example

```
import mathimport numpy as np# Using math modulesquare_root = math.sqrt(16)  # square_root is 4.0# Using NumPy for array operationsarray = np.array([1, 2, 3])array_sum = np.sum(array)  # array_sum is 6
```

### 6. Handle Exceptions

Use try-except blocks to handle potential exceptions, such as division by zero or invalid type conversions, ensuring your program is robust and error-tolerant.

#### Example

```
try:    result = 10 / 0except ZeroDivisionError:    print("Cannot divide by zero")
```

### 7. Document Your Code

Document your numerical operations, especially when using type conversions and high-precision calculations, to make your code easier to understand and maintain.

#### Example

```
# Adding two Decimal numbers for precise calculationfrom decimal import Decimalsubtotal = Decimal('10.99')tax = Decimal('2.01')total = subtotal + tax  # total is Decimal('13.00')
```

## Conclusion

Comprehending Python numbers, encompassing floats, complex numbers, and integers, is essential for efficient programming and accurate numerical calculations. Whole numbers work best with integers, decimal points are handled by floats, and operations involving real and imaginary components can be supported by complex numbers. Calculations are guaranteed to be accurate and efficient when using the 'decimal' module for high-precision arithmetic and libraries like 'math' and 'NumPy' for complex mathematical functions. You can improve Python programming by adhering to best practices and using the right type of conversions and error handling. To create dependable and robust apps, you must grasp fundamental numerical ideas, regardless of your experience level with [Python Training](https://www.simplilearn.com/mobile-and-software-development/python-development-training?source=GhPreviewCoursepages "Python Training").

## FAQs

### 1. How to Add Two Numbers in Python?

To add two numbers in Python, you simply use the ‘+’ operator. First, assign the numbers to variables, then apply the ‘+’ operator between these variables. 

For example, if you have two numbers, ‘a’ and ‘b’, you can add them by writing ‘result = a + b’. Here’s a step-by-step illustration: if ‘a = 5’ and ‘b = 10’, then ‘result = a + b’ would set result to ‘15’. This operation works with various numerical data types, including integers and floats. Additionally, you can directly add two numbers without assigning them to variables, like ‘result = 5 + 10’, which also yields result as ‘15’. This basic arithmetic operation is fundamental in Python and is widely used in various applications, from simple calculations to complex mathematical computations.

### 2. How to Swap Two Numbers in Python?

To swap two numbers in Python, you can use a simple and elegant technique that doesn't require a temporary variable. This method utilizes Python's multiple assignment feature. Suppose you have two variables, ‘a’ and ‘b’, with values ‘5’ and ‘10’, respectively. You can swap their values by writing ‘a, b = b, a’. After this statement, a will hold the value ‘10’ and ‘b’ will hold the value ‘5’. This approach takes advantage of Python's ability to simultaneously unpack and pack values in a single line, making the swap operation concise and efficient. For instance, given ‘a = 5’ and ‘b = 10’, executing ‘a, b = b’, a effectively swaps the values, resulting in a being ‘10’ and ‘b’ being ‘5’. This technique is simple and widely used due to its readability and efficiency in Python programming.

### 3. How to Print Numbers in Python?

To print numbers in Python, you can use the built-in ‘print()’ function, which outputs the specified value to the console. You can directly print numerical values or variables holding numbers. For example, to print the number 10, you simply write ‘print(10)’. If you have a variable ‘num’ assigned the value 20, you can print it by writing ‘print(num)’. The ‘print()’ function can also handle multiple numbers at once, separated by commas, which prints them with a space in between. For instance, ‘print(5, 15, 25)’ will output ‘5 15 25’. Additionally, you can use formatted strings (f-strings) for more complex output, allowing you to include numbers within text. For example, ‘a = 10’ and ‘b = 20’, ‘print(f"The values are {a} and {b}")’ will output ‘The values are 10 and 20’. This flexibility makes the ‘print()’ function an essential tool for displaying numbers and other information in Python.