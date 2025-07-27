![[Pasted image 20250720221507.png]]
[[B-Python-Basics Note-1]]

[[]]

this is Flow chart
# start/end

* using to start and end the program..
# input/output

* using to input information.
* and get information as output.

# process/calculation

* process that running to make output we expect


A flowchart that describes this program is is shown.

![Flowchart of a program that includes input, output and a calculation](https://problemsolvingwithpython.com/08-If-Else-Try-Except/images/flow_chart_calculation_program.png)

The Python code that corresponds to this flow chart is:

`# start num = input("Enter a number: ") num = float(num) num_plus_2 = num + 2 print(num_plus_2) # end`

The description of another program is below:

> The program starts. Next the program asks a user for a number. If the number is greater than zero, the program prints "Greater than 0", then the program ends.

A flow chart that describes this program is shown.

![Flow chart of a program that contains user input and a selection structure](https://problemsolvingwithpython.com/08-If-Else-Try-Except/images/flow_chart_simple_user_input_program.png)

The Python code that corresponds to this flow chart is:

`# start num = input("Enter a number: ") num = float(num) if num>0:     print("Greater than 0") # end`

The description of a more complex program is below:

> The program starts. Next, the program asks a user for a number. If the number is greater than zero, the program prints "Greater than 0". If the number is less than zero, the program prints "Less than 0". Then the program prints "Done" and the program ends.

A flowchart that describes this program is below:

![Flowchart of a program that contains user input and two if-statements](https://problemsolvingwithpython.com/08-If-Else-Try-Except/images/flow_chart_more_complex_user_input_program.png)

The Python code that corresponds to this flow chart is:

`# start num = input('Enter a number: ') num = float(num) if num>0:     print('num greater than zero') if num<0:     print('num less than zero') print('Done') # end`