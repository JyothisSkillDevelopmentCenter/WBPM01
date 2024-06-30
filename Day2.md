### Day 2: Language Study Continues

#### Loops: while loop, for loop

**Loops:**
Loops allow you to execute a block of code repeatedly based on a condition or over a sequence.

**While Loop:**
The while loop executes a block of code as long as a specified condition is true.
**Syntax:**
```python
while condition:
    # block of code
```
**Example:**
```python
i = 1
while i <= 5:
    print(i)
    i += 1
```
In this example, the loop will print numbers from 1 to 5. The loop continues to execute as long as `i` is less than or equal to 5.

**Common Uses:**
- Repeating tasks until a condition changes.
- Creating infinite loops for continuously running tasks (with a break condition).

**For Loop:**
The for loop is used to iterate over a sequence (such as a list, tuple, dictionary, set, or string).
**Syntax:**
```python
for item in sequence:
    # block of code
```
**Example:**
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```
In this example, the loop will print each fruit in the list.

**Common Uses:**
- Iterating through items in a collection.
- Repeating a block of code a specific number of times using `range()`.

**Additional Sample Programs:**
1. **Sum of first n natural numbers using a while loop:**
```python
n = int(input("Enter a number: "))
sum = 0
i = 1

while i <= n:
    sum += i
    i += 1

print(f"The sum of the first {n} natural numbers is {sum}")
```

2. **Print each character of a string using a for loop:**
```python
text = "Python"
for char in text:
    print(char)
```

#### Functions and Lambda: Defining functions, lambda expressions

**Functions:**
Functions are blocks of code that perform a specific task. They help in organizing code, reusing code, and improving readability.

**Defining a Function:**
**Syntax:**
```python
def function_name(parameters):
    # block of code
    return value
```
**Example:**
```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))
```
In this example, the `greet` function takes a parameter `name` and returns a greeting message.

**Function Parameters:**
- **Positional Arguments:** Parameters passed in order.
- **Keyword Arguments:** Parameters passed by name.
- **Default Parameters:** Parameters with default values.

**Example:**
```python
def describe_pet(pet_name, animal_type="dog"):
    print(f"I have a {animal_type} named {pet_name}.")

describe_pet("Buddy")  # I have a dog named Buddy.
describe_pet("Whiskers", "cat")  # I have a cat named Whiskers.
```

**Lambda Expressions:**
Lambda expressions (or anonymous functions) are small, unnamed functions defined using the `lambda` keyword. They can have any number of arguments but only one expression.
**Syntax:**
```python
lambda arguments: expression
```
**Example:**
```python
add = lambda x, y: x + y
print(add(5, 3))
```
In this example, the `add` lambda function takes two arguments and returns their sum.

**Common Uses:**
- Quick, throwaway functions.
- Functions passed as arguments to higher-order functions (e.g., `map`, `filter`).

**Additional Sample Programs:**
1. **Function to calculate the area of a rectangle:**
```python
def area_of_rectangle(length, width):
    return length * width

length = float(input("Enter the length: "))
width = float(input("Enter the width: "))
print(f"The area of the rectangle is {area_of_rectangle(length, width)}")
```

2. **Lambda function to check if a number is even:**
```python
is_even = lambda x: x % 2 == 0
print(is_even(4))  # True
print(is_even(7))  # False
```

#### Arrays: Introduction to arrays and array operations

**Introduction to Arrays:**
In Python, arrays can be implemented using the `list` data type or using the `array` module for more advanced operations. Lists are more commonly used due to their simplicity.

**Examples:**
```python
# Using lists as arrays
numbers = [1, 2, 3, 4, 5]
print(numbers)

# Accessing elements
print(numbers[0])  # First element
print(numbers[-1])  # Last element

# Modifying elements
numbers[2] = 10
print(numbers)

# Array operations
numbers.append(6)
print(numbers)

numbers.remove(3)
print(numbers)
```

**Common Operations:**
- **Adding elements:** `append()`, `extend()`, `insert()`
- **Removing elements:** `remove()`, `pop()`, `clear()`
- **Sorting and reversing:** `sort()`, `reverse()`

**Additional Sample Programs:**
1. **Find the average of numbers in an array:**
```python
numbers = [10, 20, 30, 40, 50]
average = sum(numbers) / len(numbers)
print(f"The average of the numbers is {average}")
```

2. **Reverse the elements of an array:**
```python
numbers = [1, 2, 3, 4, 5]
numbers.reverse()
print(f"The reversed array is {numbers}")
```

#### Practical Session

**Writing Sample Programs to Implement Loops and Functions:**

1. **Print all even numbers up to a given number:**
```python
n = int(input("Enter a number: "))
for i in range(1, n + 1):
    if i % 2 == 0:
        print(i)
```

2. **Calculate the sum of squares of first n natural numbers using a function:**
```python
def sum_of_squares(n):
    sum = 0
    for i in range(1, n + 1):
        sum += i ** 2
    return sum

n = int(input("Enter a number: "))
print(f"The sum of squares of the first {n} natural numbers is {sum_of_squares(n)}")
```

3. **Lambda function to find the maximum of three numbers:**
```python
max_of_three = lambda x, y, z: max(x, y, z)
print(max_of_three(3, 5, 1))  # 5
print(max_of_three(10, 7, 9))  # 10
```

### Assignment Questions

1. **Write a Python function to calculate the factorial of a number.**
```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

num = int(input("Enter a number: "))
print(f"The factorial of {num} is {factorial(num)}")
```

2. **Create a program to demonstrate the use of lambda functions.**
```python
# Lambda function to calculate the square of a number
square = lambda x: x ** 2
print(square(4))  # 16

# Lambda function to concatenate two strings
concat = lambda s1, s2: s1 + s2
print(concat("Hello, ", "World!"))  # Hello, World!
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 2: Language Study Continues

## Loops: while loop, for loop
### While Loop
- **Syntax:**
```python
while condition:
    # block of code
```
- **Example:**
```python
i = 1
while i <= 5:
    print(i)
    i += 1
```
- **Common Uses:**
  - Repeating tasks until a condition changes.
  - Creating infinite loops for continuously running tasks (with a break condition).

### For Loop
- **Syntax:**
```python
for item in sequence:
    # block of code
```
- **Example:**
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```
- **Common Uses:**
  - Iterating through items in a collection.
  - Repeating a block of code a specific number of times using `range()`.

## Functions and Lambda: Defining functions, lambda expressions
### Defining a Function
- **Syntax:**
```python
def function_name(parameters):
    # block of code
    return value
```
- **Example:**
```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))
```
- **Function Parameters:**
  - **Positional Arguments:** Parameters passed in order.
  - **Keyword Arguments:** Parameters passed by name.
  - **Default Parameters:** Parameters with default values.

### Lambda Expressions
- **Syntax:**
```python
lambda arguments: expression
```
- **Example:**
```python
add = lambda x, y: x + y
print(add(5, 3))
```
- **Common Uses:**
  - Quick, throwaway functions.
  - Functions passed as arguments to higher-order functions (e.g., `map`, `filter`).

## Arrays: Introduction to arrays and array operations
### Introduction to Arrays

- **Examples:**
```python
# Using lists as arrays
numbers = [1, 2, 3, 4, 5]
print(numbers)

# Accessing elements
print(numbers[0])  # First element
print(numbers[-1])  # Last element

# Modifying elements
numbers[2] = 10
print(numbers)

# Array operations
numbers.append(6)
print(numbers)

numbers.remove(3)
print(numbers)
```
- **Common Operations:**
  - **Adding elements:** `append()`, `extend()`, `insert()`
  - **Removing elements:** `remove()`, `pop()`, `clear()`
  - **Sorting and reversing:** `sort()`, `reverse()`

## Practical Session
- **Print all even numbers up to a given number:**
```python
n = int(input("Enter a number: "))
for i in range(1, n + 1):
    if i % 2 == 0:
        print(i)
```
- **Calculate the sum of squares of first n natural numbers using a function:**
```python
def sum_of_squares(n):
    sum = 0
    for i in range(1, n + 1):
        sum += i ** 2
    return sum

n = int(input("Enter a number: "))
print(f"The sum of squares of the first {n} natural numbers is {sum_of_squares(n)}")
```
- **Lambda function to find the maximum of three numbers:**
```python
max_of_three = lambda x, y, z: max(x, y, z)
print(max_of_three(3, 5, 1))  # 5
print(max_of_three(10, 7, 9))  # 10
```

## Assignments
1. Write a Python function to calculate the factorial of a number.
```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

num = int(input("Enter a number: "))
print(f"The factorial of {num} is {factorial(num)}")
```

2. Create a program to demonstrate the use of lambda functions.
```python
# Lambda function to calculate the square of a number
square = lambda x: x ** 2
print(square(4))  # 16

# Lambda function to concatenate two strings
concat = lambda s1, s2: s1 + s2
print(concat("Hello, ", "World!"))  # Hello, World!
```
```

In the code cells of the notebook, include the Python code provided above for each section.
