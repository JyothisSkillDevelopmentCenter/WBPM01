### Day 3: OOPs Using Python

#### Classes and Objects: Introduction to classes and objects

**Object-Oriented Programming (OOP):**
OOP is a programming paradigm that uses objects and classes to organize code in a more modular and reusable way. 

**Classes and Objects:**
- **Class:** A blueprint for creating objects. It defines attributes and methods that the objects created from the class will have.
- **Object:** An instance of a class.

**Defining a Class:**
**Syntax:**
```python
class ClassName:
    def __init__(self, parameters):
        # Initialize attributes
        self.attribute = value
    
    def method(self):
        # Method definition
        pass
```
**Example:**
```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} is barking."

# Creating an object (instance) of the Dog class
my_dog = Dog("Buddy", 3)
print(my_dog.bark())  # Output: Buddy is barking.
```

**Attributes and Methods:**
- **Attributes:** Variables that belong to a class (also known as properties or fields).
- **Methods:** Functions that belong to a class.

**Example:**
```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} is starting."

# Creating an object of the Car class
my_car = Car("Toyota", "Camry", 2020)
print(my_car.start())  # Output: The 2020 Toyota Camry is starting.
```

#### Inheritance and Modules: Understanding inheritance, using modules

**Inheritance:**
Inheritance allows a class (child class) to inherit attributes and methods from another class (parent class). It promotes code reuse and establishes a hierarchical relationship between classes.

**Defining Inheritance:**
**Syntax:**
```python
class ParentClass:
    # Parent class definition

class ChildClass(ParentClass):
    # Child class definition
```
**Example:**
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound."

class Dog(Animal):
    def speak(self):
        return f"{self.name} barks."

# Creating an object of the Dog class
my_dog = Dog("Buddy")
print(my_dog.speak())  # Output: Buddy barks.
```

**Modules:**
Modules are files containing Python code (functions, classes, variables) that can be imported and used in other Python programs. Using modules helps organize code into separate files for better readability and maintainability.

**Creating and Using Modules:**
1. **Create a module:** Save the following code in a file named `mymodule.py`.
```python
def greet(name):
    return f"Hello, {name}!"
```

2. **Import and use the module:**
```python
import mymodule

print(mymodule.greet("Alice"))  # Output: Hello, Alice!
```

**Additional Sample Programs:**
1. **Class representing a bank account:**
```python
class BankAccount:
    def __init__(self, account_number, balance=0):
        self.account_number = account_number
        self.balance = balance
    
    def deposit(self, amount):
        self.balance += amount
        return self.balance
    
    def withdraw(self, amount):
        if amount > self.balance:
            return "Insufficient funds"
        self.balance -= amount
        return self.balance

# Creating an object of the BankAccount class
account = BankAccount("123456789")
account.deposit(1000)
print(account.withdraw(500))  # Output: 500
```

2. **Inheritance example with shapes:**
```python
class Shape:
    def __init__(self, color="Black"):
        self.color = color
    
    def area(self):
        pass
    
class Rectangle(Shape):
    def __init__(self, length, width, color="Black"):
        super().__init__(color)
        self.length = length
        self.width = width
    
    def area(self):
        return self.length * self.width

# Creating an object of the Rectangle class
rect = Rectangle(10, 5, "Blue")
print(f"Color: {rect.color}, Area: {rect.area()}")  # Output: Color: Blue, Area: 50
```

#### Practical Session

**Programs to Demonstrate OOP Concepts:**

1. **Class to represent a book:**
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    def description(self):
        return f"'{self.title}' by {self.author}, {self.pages} pages."

# Creating an object of the Book class
my_book = Book("1984", "George Orwell", 328)
print(my_book.description())  # Output: '1984' by George Orwell, 328 pages.
```

2. **Class hierarchy for vehicles:**
```python
class Vehicle:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} is starting."

class Car(Vehicle):
    def __init__(self, make, model, year, doors):
        super().__init__(make, model, year)
        self.doors = doors
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} with {self.doors} doors is starting."

# Creating an object of the Car class
my_car = Car("Honda", "Civic", 2021, 4)
print(my_car.start())  # Output: The 2021 Honda Civic with 4 doors is starting.
```

3. **Using a module to organize utility functions:**
```python
# Save this code in a file named 'utilities.py'
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# Main program
import utilities

print(utilities.add(5, 3))  # Output: 8
print(utilities.subtract(5, 3))  # Output: 2
```

### Assignment Questions

1. **Create a class to represent a student with attributes name, age, and grade. Include methods to display student details.**
```python
class Student:
    def __init__(self, name, age, grade):
        self.name = name
        self.age = age
        self.grade = grade
    
    def display_details(self):
        return f"Student Name: {self.name}, Age: {self.age}, Grade: {self.grade}"

# Creating an object of the Student class
student = Student("John Doe", 20, "A")
print(student.display_details())  # Output: Student Name: John Doe, Age: 20, Grade: A
```

2. **Write a Python program to demonstrate inheritance by creating a base class and derived class.**
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display_info(self):
        return f"Name: {self.name}, Age: {self.age}"

class Employee(Person):
    def __init__(self, name, age, employee_id):
        super().__init__(name, age)
        self.employee_id = employee_id
    
    def display_info(self):
        return f"Name: {self.name}, Age: {self.age}, Employee ID: {self.employee_id}"

# Creating an object of the Employee class
employee = Employee("Jane Doe", 30, "E123")
print(employee.display_info())  # Output: Name: Jane Doe, Age: 30, Employee ID: E123
```

### IPython Notebook Example

Create a new Jupyter Notebook and include the following content:

```markdown
# Day 3: OOPs Using Python

## Classes and Objects: Introduction to classes and objects
### Defining a Class
- **Syntax:**
```python
class ClassName:
    def __init__(self, parameters):
        # Initialize attributes
        self.attribute = value
    
    def method(self):
        # Method definition
        pass
```
- **Example:**
```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} is barking."

# Creating an object (instance) of the Dog class
my_dog = Dog("Buddy", 3)
print(my_dog.bark())  # Output: Buddy is barking.
```
### Attributes and Methods
- **Example:**
```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} is starting."

# Creating an object of the Car class
my_car = Car("Toyota", "Camry", 2020)
print(my_car.start())  # Output: The 2020 Toyota Camry is starting.
```

## Inheritance and Modules: Understanding inheritance, using modules
### Defining Inheritance
- **Syntax:**
```python
class ParentClass:
    # Parent class definition

class ChildClass(ParentClass):
    # Child class definition
```
- **Example:**
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound."

class Dog(Animal):
    def speak(self):
        return f"{self.name} barks."

# Creating an object of the Dog class
my_dog = Dog("Buddy")
print(my_dog.speak())  # Output: Buddy barks.
```

### Modules
- **Creating and Using Modules:**
1. **Create a module:** Save the following code in a file named `mymodule.py`.
```python
def greet(name):
    return f"Hello, {name}!"
```

2. **Import and use the module:**
```python
import mymodule

print(mymodule.greet("Alice"))  # Output: Hello, Alice!
```

## Practical Session
- **Class to represent a book:**
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    def description(self):
        return f"'{self.title}' by {self.author}, {self.pages} pages."

# Creating an object of the Book class
my_book = Book("1984", "George Orwell", 328)
print(my_book.description())  # Output: '1984' by George Orwell, 328 pages.
```

- **Class hierarchy for vehicles:**
```python
class Vehicle:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} is starting."

class Car(Vehicle):
    def __init__(self, make, model, year, doors):
        super().__init__(make, model, year)
        self.doors = doors
    
    def start(self):
        return f"The {self.year} {self.make} {self.model} with {self.doors} doors is starting."

# Creating an object of the Car class
my_car = Car("Honda", "Civic", 2021, 4)
print(my_car.start())  # Output: The 2021 Honda Civic with 4 doors is starting.
```

- **Using a module to organize utility functions:**
```python
# Save this code in a file named 'utilities.py'
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# Main program
import utilities

print(utilities.add(5, 3))  # Output: 8
print(utilities.subtract(5, 3))  # Output: 2
```

## Assignments
1. Create a class to represent a student with attributes name, age, and grade. Include methods to display student details.
```python
class Student:
    def __init__(self, name, age, grade):
        self.name = name
        self.age = age
        self.grade = grade
    
    def display_details(self):
        return f"Student Name: {self.name}, Age: {self.age}, Grade: {self.grade}"

# Creating an object of the Student class
student = Student("John Doe", 20, "A")
print(student.display_details())  # Output: Student Name: John Doe, Age: 20, Grade: A
```

2. Write a Python program to demonstrate inheritance by creating a base class and derived class.
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def display_info(self):
        return f"Name: {self.name}, Age: {self.age}"

class Employee(Person):
    def __init__(self, name, age, employee_id):
        super().__init__(name, age)
        self.employee_id = employee_id
    
    def display_info(self):
        return f"Name: {self.name}, Age: {self.age}, Employee ID: {self.employee_id}"

# Creating an object of the Employee class
employee = Employee("Jane Doe", 30, "E123")
print(employee.display_info())  # Output: Name: Jane Doe, Age: 30, Employee ID: E123
```
```

In the code cells of the notebook, include the Python code provided above for each section.
