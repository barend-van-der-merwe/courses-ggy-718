[[Training Schedule]]
## Session 1
### Why use python in Geomorphology?
1. Geocomputation is the application of a computational paradigm to geographical problems ([[Openshaw2014]]).

### Creating and using virtual environments.
#### What are virtual environments
1. Python has been around for a long time and because of this, different versions of packages may interfere or prevent other packages of performing as intended.
2. Virtual environments were developed to mitigate this.
3. Each of your Python projects should have its own conda environment ([[Vaughan2023]])
	1. Alternatively, you can create virtual environments for types of tasks such as data analysis, computer vision, artificial intelligence etc. This is the approach I follow.
4. You can think of conda environments as separate Python installations ([[Vaughan2023]]).
5. Conda environments let you use any version of any package you want, including Python, without the risk of compatibility conflicts ([[Vaughan2023]]). 
6. You can share your environments with others, making it possible for them to perfectly reproduce your projects ([[Vaughan2023]]).
7. These environments are directories in your computer’s directory tree ([[Vaughan2023]]).
8. It’s best to install all the packages that you’re going to need for a project at the same time, if possible, to avoid dependency conflicts ([[Vaughan2023]]).
9. Conda downloads packages into a package cache, and each environment links to the appropriate packages in this cache ([[Vaughan2023]]).
	1. This package cache is in the pkgs directory of your Anaconda distribution and saves space in storage ([[Vaughan2023]]).
10. The command `conda info --envs` can be used to find the location of the different virtual environments ([[Vaughan2023]]).

#### Creating a virtual environment
1. The base environment is created by default when you install Anaconda, and it includes a Python installation and core system libraries and dependencies of conda ([[Vaughan2023]]).
	1. Avoid installing additional packages into your base environment ([[Vaughan2023]]).
2. The command `conda create --name ENVNAME python=3.X` (where ENVNAME is the name of the virtual environment, and 3.X is the python version that should run in that environment) can be used to create a virtual environment (adapted from [[Vaughan2023]]).

---
**EXAMPLE**: Create a virtual environment named "data_analysis" that uses python 3.9.

```
conda create --name data_analysis python=3.9
```
---
#### Accessing a virtual environment
1. The command `conda activate ENVNAME` is used to access virtual environments while `conda deactivate`  is used to exit the current virtual environment and return to the base environment (adapted from [[Vaughan2023]]).

---
**EXAMPLE**: Access the environment you created in the previous step. Afterwards, leave tge environment and return to the base environment.
```
conda activate data_analysis
conda deactivate
```

---
### Installing packages inside virtual environments
1. Search online for the command to install a package.
2. For example, to install the pandas library, the following command needs to be entered into the terminal: `conda install anaconda::pandas`. You will then be provided with a series of prompts after which the package will be installed.

### The Python IDLE
1. Although there are many IDEs (Integrated Development Environments) available for python, we will be using the IDLE which comes with Python.
2. To open the IDLE, the following command needs to be typed inside the terminal: `python -m idlelib`. 
3. Within the IDLE, programs code can either be executed line by line (similar to the terminal) or a separate file containing more intricate code can be run.
4. The image below is an example of an IDLE with the terminal interface on the left and a blank file on the right.
![](images/idle.png)

---
### Introduction to programming concepts: variables, data types, operators, expressions.
#### The Zen of Python
```
>>> import this
The Zen of Python, by Tim Peters
 
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

#### Variables
1. Data is stored within the computer at specific locations of the system's memory. Each of these locations have an address (e.g. 0x7ffcc1a8a350).
2. All the data you will be using when carrying out data analysis will be stored in one or more addresses in memory.
3. To access a specific piece of information, you need to inform Python where in your system's memory the piece of information you are working with is stored. However, given the example of a memory address given above, this will be a cumbersome process. Therefore, variables were developed in order to make this easier.
4. Variables are names that are used to designate specific memory locations (the computer will create the actual memory address internally) ([[Forouzan2014]]).
5. In python, there are a couple of rules when creating variable names ([[Matthes2023]]):
	1. Variable names can only contain letters, numbers, and underscores.
	2. They can start with a letter or an underscore, but they cannot start with a number.
	3. Spaces are not allowed in variable names.
	4. Avoid using Python keywords (e.g. `print`) as variable names.
	5. Variable names should be short but descriptive.

---
**EXAMPLE** Here we create two variables (`var1` and `var2`) and obtain their memory addresses using the `hex()` and `id()` functions.
```
>>> var1 = 15
>>> var2 = "GGY 718"
>>> hex(id(var1))
'0x7ffcc1a8a350'
>>> hex(id(var2))
'0x1286bb30ef0'
```

---
#### Data types
1. The type of variable can be determined using the `type()` function.
2. Strings
	1. A string is a series of characters ([[Matthes2023]]).
	2. Anything inside single or double quotes is considered a string ([[Matthes2023]]), e.g. `"GGY 718`.
3. Numbers
	1. Integers
		1. An integer is a whole number without a fractional part ([[Forouzan2014]]).
	2. Floats
		1. Any number that contains a fractional part (i.e. a decimal) is considered a float ([[Matthes2023]]).
4. Boolean
	1. A boolean value is a value that can only take one of two forms: true and false
	2. Note that boolean values do not have quotation marks.

---
 **EXAMPLE** Determine the type of data for each of the following: "Geomorphology", 42, 42.0, True, and "True"
```
>>> type("Geomorphology")
<class 'str'>
>>> type(42)
<class 'int'>
>>> type(42.0)
<class 'float'>
>>> type(True)
<class 'bool'>
>>> type("True")
<class 'str'>
```
---

#### Operators
1. An operator is a language-specific token that requires an action to be taken ([[Forouzan2014]]). 
2. Operators are used to either carry out mathematical operations or to express relationships between one or more variables.
3. The are often used as part of the conditional statements in loops.

| Operator | Category | Description                         |
| -------- | -------- | ----------------------------------- |
| `+`      | Math     | Addition                            |
| `-`      | Math     | Subtraction                         |
| `*`      | Math     | Multiplication                      |
| `/`      | Math     | Division                            |
| `//`     | Math     | Division (floor integer)            |
| `%`      | Math     | Modulus (remainder)                 |
| `**`     | Math     | Exponent                            |
| `=`      |          | Assignment                          |
| `==`     | Logic    | Equality                            |
| `!=`     | Logic    | Not equal to                        |
| `>`      | Logic    | Greater than                        |
| `<`      | Logic    | Lesser than                         |
| `>=`     | Logic    | Greater or equal than               |
| `<=`     | Logic    | Less or equal than                  |
| `is`     | Logic    | Object identity                     |
| `is not` | Logic    | Negated object identity             |
| `and`    | Logic    | Used to combine multiple conditions |
| `or`     | Logic    | Used to combine multiple conditions |

---
**Example** 
```
>>> 5 + 2        # addition
7
>>> 5 - 2        # subtraction
3
>>> 5 * 2        # multiplication
10
>>> 5 / 2        # division
2.5
>>> 5 // 2       # division (floor integer)
2
>>> 5 ** 2       # exponent
25
>>> 1 == 1       # equality
True
>>> 1 == 2       # equality
False
>>> 1 != 2       # not equal to
True
>>> 2 > 1        # greater than
True
>>> 2 < 1        # less than
False
>>> 6 >= 2       # greater or equal to
True
>>> 6 <= 2       # less or equal to
False
>>> 5 is 2       # object identity
False
>>> 5 is 5       # object identity
True
>>> 5 is not 2   # negated object identity
True
>>> 5 is not 5   # negated object identity
False
```
---
#### Expressions
1. Formally, an expression is any sequence of operands and operators that reduce to a single value ([[Forouzan2014]]). For example, the expression `6 * 8 - 6` reduces to a value of `42` which is returned as the output.
---
### Basic syntax: control flow (if-else statements, loops), functions (simple examples).
#### Functions and methods
1. Functions are named blocks of code that are designed to do one specific job ([[Matthes2023]]).
2. In order to use a function within your code, it must be called ([[Matthes2023]]).
3. Methods are actions that a particular data type can perform ([[Vaughan2023]]).

---
**Example**
```
>>> random_numbers = [51,48,85,65,41]  #create a list of random numbers
>>> sum(random_numbers)                #use the sum function to add the numbers
290
>>> random_numbers.sort()              #use the sort method to sort the numbers
>>> random_numbers
[41, 48, 51, 65, 85]
```

---
#### Conditional functions
1. As the term implies, conditional functions are functions that only run when a certain conditions, or set of conditions, are met.
2. A condition is a statement that either evaluates to a `True` or `False` ([[Speight2020]]).
3. The `if` statement is used to evaluate a condition ([[Matthes2023]]).
4. Note that the `if` statement only determines whether a given expression is `True` or `False`. If the expression is `True`, then the code following the `if` statement will be executed. When the `if` statement returns a `False`, then the code following the `if` statement will not be executed. In the example below, the `if` statement first determine whether the integer 2 is equivalent to itself. Since this statement is true, the code following the `if` statement (namely the `print()` function) is executed and the text appears on the screen. In the second example, the `if` statement evaluates whether the integer 3 is equivalent to the integer 2. Since this is not the case, the code following the `if` statement is not evaluated and therefore no output is produced.  
---
**Example**
```
>>> if 2 == 2:
	print("The two numbers are equal")

The two numbers are equal
>>> if 3 == 2:
	print("The two numbers are equal")

>>>
```
---
#### elif statements
1. It is more common to use the `if` statement along with an `elif` statement (this is a shorthand for "else if").
2. The `if else` statement can be considered as an alternative to the first `if` statement. In other words, if the `if` statement evaluates to `False`, then python will skip the code following the `if` statement and go to the `elif` statement and evaluate it as being either `True` or `False`.
3. Multiple `elif` statements can be used to provide any number of alternative options.
4. The `else` statement can also be used to execute code that does not meet any of the conditions in the previous statement(s).
---
**Example**
```
if 2==3:
    print(True)
elif 2!=3:
    print(False)

False
```
---
#### Multiple conditions
1. In some cases, it may be required that more than one condition be met before a code executes.
2. In these cases, the `and` and `or` operator are used. The `and` operator tells the `if` function that both of the conditions need to be met before the code can execute while the `or` operator indicates that any one of the conditions can be met for the `if` statement to evaluate as `True`.
---
**Example**
```
if (10%2 == 0 and 10 >= 5):
    print("Ten is an even number and is larger than five")
else:
    print("Ten is not an even nmber and is not larger than 5")
Ten is an even number and is larger than five
```
---
#### Loops


---
## Session 2

### Introduction to data structures: lists, tuples, dictionaries
#### Lists

#### Tuples

#### Dictionaries

---
### Working with files: reading and writing data
#### Reading data


#### Writing data

---
### Introduction to libraries: NumPy, Pandas, SciPy, Matplotlib
#### NumPy


#### Pandas


#### SciPy



#### Matplotlib

---
### Assignment 1