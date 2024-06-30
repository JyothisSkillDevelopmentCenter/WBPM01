### Day 1: Python Programming Basics

#### Overview and Installation

**Introduction to Python:**
Python is a versatile, high-level programming language known for its readability and broad application spectrum. It is widely used in various domains, such as web development, data science, machine learning, automation, and more.

**Key Features of Python:**
- Easy to read and write.
- Supports multiple programming paradigms (procedural, object-oriented, functional).
- Extensive standard library.
- Large community and ecosystem of third-party packages.

**Installation Procedures:**
To ensure a smooth development experience, we'll use Anaconda, a distribution that simplifies package management and deployment. It includes Python and many other useful packages.

**Steps to Install Anaconda:**
1. **Download Anaconda:**
   - Go to the [Anaconda website](https://www.anaconda.com/products/individual).
   - Download the installer for your operating system (Windows, macOS, Linux).

2. **Install Anaconda:**
   - **Windows:**
     - Run the downloaded installer.
     - Follow the installation prompts, choosing default options unless you have specific requirements.
   - **macOS:**
     - Open the downloaded .pkg file.
     - Follow the installation prompts.
   - **Linux:**
     - Open a terminal.
     - Navigate to the directory where the installer is located.
     - Run the command: `bash Anaconda3-2023.11-Linux-x86_64.sh` (replace the filename with the version you downloaded).
     - Follow the installation prompts.

3. **Verify Installation:**
   - Open the Anaconda Navigator or a terminal.
   - Type `conda --version` to ensure Anaconda is installed correctly.

**Launching Jupyter Notebook:**
1. Open Anaconda Navigator.
2. Click on "Launch" under Jupyter Notebook.
3. A web browser will open with the Jupyter Notebook interface, where you can create and run notebooks.

#### Syntax and Variables

**Basic Syntax:**
Python's syntax is designed to be clean and easy to understand. Key points include:
- **Indentation:** Indentation is used to define the scope of loops, functions, classes, etc.
- **Comments:** Use `#` for single-line comments and triple quotes (`'''` or `"""`) for multi-line comments.
- **Case Sensitivity:** Python is case-sensitive (e.g., `Variable` and `variable` are different).

**Examples:**
```python
# This is a single-line comment

"""
This is a
multi-line comment
"""

x = 10  # Integer variable
name = "Alice"  # String variable
```

**Variables:**
Variables are used to store data. In Python, you don't need to declare the type of variable; it is inferred from the value assigned.

**Examples:**
```python
x = 5           # integer
y = "Hello"     # string
z = 3.14        # float
is_active = True  # boolean
```

**Data Types:**
- **Numbers:** Integers (`int`), floating-point numbers (`float`), complex numbers (`complex`).
- **Strings:** Immutable sequences of characters.
- **Lists:** Ordered, mutable collections of items.
- **Tuples:** Ordered, immutable collections of items.
- **Dictionaries:** Unordered collections of key-value pairs.
- **Sets:** Unordered collections of unique items.

**Examples:**
```python
num = 100          # Integer
pi = 3.14          # Float
text = "Python"    # String
items = [1, 2, 3]  # List
info = {"name": "Alice", "age": 25}  # Dictionary
unique_items = {1, 2, 3}  # Set
```

#### Operators and Data Types

**Arithmetic Operators:**
- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `//` (Floor Division)
- `%` (Modulus)
- `**` (Exponentiation)

**Examples:**
```python
a = 10
b = 3

print(a + b)  # 13
print(a - b)  # 7
print(a * b)  # 30
print(a / b)  # 3.333...
print(a // b)  # 3
print(a % b)  # 1
print(a ** b)  # 1000
```

**Comparison Operators:**
- `==` (Equal to)
- `!=` (Not equal to)
- `>` (Greater than)
- `<` (Less than)
- `>=` (Greater than or equal to)
- `<=` (Less than or equal to)

**Examples:**
```python
x = 10
y = 5

print(x == y)  # False
print(x != y)  # True
print(x > y)   # True
print(x < y)   # False
print(x >= y)  # True
print(x <= y)  # False
```

**Logical Operators:**
- `and`
- `or`
- `not`

**Examples:**
```python
x = True
y = False

print(x and y)  # False
print(x or y)   # True
print(not x)    # False
```

**Data Types:**
- **Numbers:** `int`, `float`, `complex`
- **Strings:** Immutable sequences of characters.
- **Lists:** Ordered, mutable collections.
- **Tuples:** Ordered, immutable collections.
- **Dictionaries:** Key-value pairs.
- **Sets:** Unordered collections of unique items.

**Examples:**
```python
num = 100          # Integer
pi = 3.14          # Float
text = "Hello"     # String
items = [1, 2, 3]  # List
point = (2, 3)     # Tuple
info = {"name": "Alice", "age": 25}  # Dictionary
unique_items = {1, 2, 3}  # Set
```

#### Conditional Statements: if, else, elif

Conditional statements are used to perform different actions based on different conditions.

**Syntax:**
```python
if condition1:
    # block of code
elif condition2:
    # block of code
else:
    # block of code
```

**Example:**
```python
x = 10

if x > 0:
    print("Positive")
elif x == 0:
    print("Zero")
else:
    print("Negative")
```

#### Practical Session

**Writing Simple Python Programs:**

1. **Check if a number is even or odd:**
```python
num = int(input("Enter a number: "))
if num % 2 == 0:
    print(f"{num} is even")
else:
    print(f"{num} is odd")
```

2. **Find the largest number in a list:**
```python
numbers = [10, 20, 30, 40, 50]
largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(f"The largest number is {largest}")
```

**Additional Sample Programs:**

3. **Calculate the factorial of a number:**
```python
num = int(input("Enter a number: "))
factorial = 1

for i in range(1, num + 1):
    factorial *= i

print(f"The factorial of {num} is {factorial}")
```

4. **Check if a string is a palindrome:**
```python
text = input("Enter a string: ")
if text == text[::-1]:
    print(f"{text} is a palindrome")
else:
    print(f"{text} is not a palindrome")
```

5. **Print the Fibonacci sequence up to n terms:**
```python
n = int(input("Enter the number of terms: "))
a, b = 0, 1
count = 0

if n <= 0:
    print("Please enter a positive integer")
elif n == 1:
    print(f"Fibonacci sequence up to {n} term: {a}")
else:
    print("Fibonacci sequence:")
    while count < n:
        print(a)
        nth = a + b
        a = b
        b = nth
        count += 1
```

6. **Sum of all elements in a list:**
```python
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)
print(f"The sum of all elements in the list is {total}")
```

### Assignment Questions

1. **Write a Python program to check if a number is even or odd.**
```python
num = int(input("Enter a number: "))
if num % 2 == 0:
    print(f"{num} is even")
else:
    print(f"{num} is odd")
```

2. **Create a list of numbers and write a program to find the largest number.**
```python
numbers = [10, 20, 30, 40, 50]
largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(f"The largest number is {largest}")
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 1: Python Programming Basics

## Overview and Installation
- **Introduction to Python**
- **Installation Procedures**

## Syntax and Variables
- **Basic Syntax**
- **Variables**
- **Data Types**

## Operators and Data
 Types
- **Arithmetic Operators**
- **Comparison Operators**
- **Logical Operators**

## Conditional Statements: if, else, elif
- **Syntax**
- **Example**

## Practical Session
- **Check if a number is even or odd**
- **Find the largest number in a list**
- **Calculate the factorial of a number**
- **Check if a string is a palindrome**
- **Print the Fibonacci sequence up to n terms**
- **Sum of all elements in a list**

## Assignments
1. Write a Python program to check if a number is even or odd.
2. Create a list of numbers and write a program to find the largest number.
```

In the code cells of the notebook, include the Python code provided above for each section.
