## Variables

[[B-Python-Basics Note-1]]
[[Lesson 1 - Print & Strings]]

Variables are assigned in Python using the `=` equals sign also called the _assignment operator_. The statement:

`a = 2`

Assigns the integer `2` to the variable `a`.

`>>> a = 2 >>> a 2`

Note the assignment operator `=`(equals), is different from the logical comparison operator `==` (equivalent to).

```>>> a == 2 True```

Variable names in Python must conform to the following rules:

- variable names must start with a letter
- variable names can only contain letters, numbers, and the underscore character `_`
- variable names can not contain spaces
- variable names can not include punctuation
- variable names are not enclosed in quotes or brackets The following code lines show valid variable names:

`constant = 4  new_variable = 'var'  my2rules = ['rule1','rule2']  SQUARES = 4`

The following code lines show invalid variable names:

`a constant = 4  3newVariables = [1, 2, 3]  &sum = 4 + 4`

Let's solve the problem below at the Python REPL using variables.

#### Problem

The Arrhenius relationship states:

n=nve−Qv/(RT)

In a system where nv=2.0×10−3, Qv=5, R=3.18, and T=293, calculate n.

#### Solution

Use variables to assign a value to each one of the constants in the problem and calculate n.

`>>> nv = 2.0e-3 >>> Qv = 5 >>> R = 3.18 >>> T = 293 >>> from math import exp >>> n = nv*exp(-1*Qv/(R*T)) >>> n 0.0019892961379660424`

so its like this 
