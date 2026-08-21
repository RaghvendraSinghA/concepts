# Python Technical Paper

## Introduction

Python is a high-level, interpreted programming language known for its simple syntax and readability. It supports multiple programming paradigms, including procedural programming, object-oriented programming, and functional programming.

This paper provides a practical overview and cheatsheet covering commonly used Python concepts:

1. Array methods
2. String methods
3. Objects and Object-Oriented Programming
4. Decorators
5. Virtual environments
6. The `pip` package manager
7. PEP 8 coding standards
8. References

---

# 1. Array Methods

## 1.1 What Is an Array in Python?

Python does not have a built-in array type equivalent to arrays in languages such as Java or C for general-purpose programming. In everyday Python programming, a **list** is commonly used as a dynamic array.

```python
numbers = [10, 20, 30, 40]
```

Python also provides the `array` module and libraries such as NumPy for specialized numerical arrays.

```python
from array import array

numbers = array('i', [10, 20, 30])
```
    'i' means the array stores signed integers, you cannot store string
        or another object in it.
---

## 1.2 Common List Methods

### `append()`

Adds one item to the end of a list.

```python
numbers = [1, 2, 3]
numbers.append(4)

print(numbers) #op-> [1, 2, 3, 4]
```

### `extend()`

Adds multiple elements from an iterable.

```python
numbers = [1, 2, 3]
numbers.extend([4, 5, 6])

print(numbers) #op-> [1, 2, 3, 4, 5, 6]
```

### `insert()`

Inserts an item at a specified index.

```python
numbers = [1, 2, 4]
numbers.insert(2, 3)

print(numbers) #op-> [1, 2, 3, 4]
```

---

### `remove()`

Removes the first matching value.

```python
numbers = [1, 2, 3, 2]
numbers.remove(2)

print(numbers)    #op->[1, 3, 2]
```

If the value does not exist, Python raises a `ValueError`.

---

### `pop()`

Removes and returns an element.

```python
numbers = [10, 20, 30]

value = numbers.pop()

print(value)    #op->30
print(numbers)    #op->[10, 20]
```

An index can also be also used:

```python
numbers.pop(0)
```

---

### `clear()`

Removes all elements.

```python
numbers = [1, 2, 3]
numbers.clear()

print(numbers) #op->[]
```


---

### `index()`

Returns the index of the first matching element.

```python
numbers = [10, 20, 30]
print(numbers.index(20)) #op->1
```

---

### `count()`

Counts how many times an element occurs.

```python
numbers = [1, 2, 2, 3, 2]

print(numbers.count(2))    #op->3
```

---

### `sort()`

Sorts the original list.

```python
numbers = [4, 1, 3, 2]
numbers.sort()

print(numbers)    #op->[1, 2, 3, 4]
```

Descending order:

```python
numbers.sort(reverse=True)

#it doesn't return new array.
```

Custom sorting:

```python
words = ["banana", "kiwi", "apple"]
words.sort(key=len)

print(words)    #op->['kiwi', 'apple', 'banana']
```

---

### `reverse()`

Reverses the original list.

```python
numbers = [1, 2, 3]

numbers.reverse()
print(numbers)    op-->[3, 2, 1]
```
---

### `copy()`

Creates a shallow copy of a list.

```python
numbers = [1, 2, 3]
new_numbers = numbers.copy()
```

---

## 1.3 List Slicing

Python lists support slicing.

```python
numbers = [10, 20, 30, 40, 50]
```

Syntax:

```python
list[start:stop:step]
```

Examples:

```python
numbers[1:4] #op->20, 30, 40]
```
---

# 2. String Methods
A string is a sequence of Unicode characters.

```python
name = "Python"
```
Strings are immutable, meaning their characters cannot be modified directly.

```python
name = "Python"
# name[0] = "J"  # TypeError
```

---

## 2.2 Case Conversion Methods

### `upper()`

```python
text = "python"

print(text.upper()) #op->PYTHON
```

### `lower()`

```python
text = "PYTHON"

print(text.lower()) #op->python
```

---

## 2.3 Removing Whitespace

### `strip()`

Removes whitespace from both ends.

```python
text = "  Python  "

print(text.strip()) #op-> Python
```

---

## 2.4 Searching Methods

### `find()`

Returns the first index of a substring. Returns `-1` if not found.

```python
text = "Hello Python"

print(text.find("Python")) #op->6
```

### `index()`

Similar to `find()`, but raises a `ValueError` if the substring does not exist.

```python
text.index("Python") #op->6
```

### `startswith()`

```python
text = "Python"

print(text.startswith("Py")) #op-> True
```

### `endswith()`

```python
print(text.endswith("on"))    #op->True
```

---

## 2.5 Replacing and Splitting

### `replace()`

```python
text = "I like Java"
new_text = text.replace("Java", "Python")

print(new_text) #op->"I like Python"
```

### `split()`

Converts a string into a list.

```python
text = "apple,banana,mango"
fruits = text.split(",") #op->['apple', 'banana', 'mango']

print(fruits)
```

### `join()`

Combines iterable elements into a string.

```python
fruits = ["apple", "banana", "mango"]
result = ", ".join(fruits)

print(result) #op->apple, banana, mango
```

---



Example:

```python
value = "123"

print(value.isdigit()) #op->True

Checks if string all characters are integer.
```

---
# 3. Object-Oriented Programming

## 3.1 What Is Object-Oriented Programming?

Object-Oriented Programming, commonly called OOP, is a programming paradigm that organizes code using objects and Classes

A class acts as a blueprint.

An object is an instance of a class.

```python
class Car:
    pass


car1 = Car()
car2 = Car()
```

`Car` is a class, while `car1` and `car2` are objects.

---

## 3.2 Class and Object

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student = Student("Ravi", 22)

print(student.name)
print(student.age)
```

### Explanation

The `__init__` method is a constructor-like initializer that runs when an object is created.

```python
self.name = name
```

`self` refers to the current object.

---

## 3.3 Instance Methods

Instance methods operate on object data.

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def display_balance(self):
        print(self.balance)

account = BankAccount(1000)

account.deposit(500)

account.display_balance()    #op-> 1500
```

---

## 3.4 Class Variables

Class variables belong to the class and are shared by its instances unless shadowed.

```python
class Employee:
    company = "ABC Technologies"

    def __init__(self, name):
        self.name = name


employee1 = Employee("Ravi")
employee2 = Employee("Amit")

print(employee1.company)        #op-> ABC Technologies
print(employee2.company)        #op-> ABC Technologies
```

---

## 3.5 Encapsulation

Encapsulation means bundling data and behaviour together and controlling access to implementation details.

Python uses naming conventions for non-public attributes.

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance        # _ -> means protected, no error can access.
```

A double underscore triggers name mangling:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance       # __ -> means private, error on access.
                                       #. but, with mangling we can access it.
```

However, Python does not enforce traditional private access in the same way as some other languages.

---

## 3.6 Inheritance

Inheritance allows one class to reuse and extend another class.

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    def speak(self):
        print("Dog barks")
```

Usage:

```python
dog = Dog()

dog.speak()       #op-> Dog barks
```

A child class can access parent functionality using `super()`.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

---

## 3.7 Polymorphism

Polymorphism allows different objects to respond to the same method call differently.

```python
class Dog:
    def speak(self):
        return "Bark"


class Cat:
    def speak(self):
        return "Meow"


animals = [Dog(), Cat()]

for animal in animals:
    print(animal.speak())
```

Output:

```text
Bark
Meow
```

---

## 3.8 Abstraction

Abstraction means exposing essential behavior while hiding unnecessary implementation details.
Abstract classes have contracts which child class have to fill if they want to inherit from that abstract class.

Python can use the `abc` module.

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self):
        pass


class CreditCardPayment(Payment):

    def pay(self):
        print("Payment completed")
```

---

# 4. Decorators

## 4.1 What Is a Decorator?

A decorator is a function that modifies or extends the behavior of another function without directly changing that function's source code.

Python functions are first-class objects. They can be:

* Assigned to variables
* Passed as arguments
* Returned from other functions

Example:

```python
def greet():
    return "Hello"


message = greet

print(message())
```

---

## 4.2 Basic Decorator

```python
def decorator_function(original_function):

    def wrapper():
        print("Before function execution")

        original_function()

        print("After function execution")

    return wrapper
```

Applying the decorator:

```python
@decorator_function
def greet():
    print("Hello")
```

Calling the function:

```python
greet()
```

Output:

```text
Before function execution
Hello
After function execution
```

The syntax:

```python
@decorator_function
def greet():
    pass
```

is equivalent to:

```python
greet = decorator_function(greet)
```

---

## 4.3 Decorators with Arguments

```python
def decorator_function(original_function):

    def wrapper(*args, **kwargs):
        print("Before execution")

        result = original_function(*args, **kwargs)

        print("After execution")

        return result

    return wrapper
```

Usage:

```python
@decorator_function
def add(a, b):
    return a + b


print(add(10, 20))
```

Using `*args` and `**kwargs` makes the decorator work with functions having different argument signatures.

---

## 4.4 Preserving Function Metadata

A decorator can replace metadata such as the original function's name. The `functools.wraps` decorator preserves this metadata.

```python
from functools import wraps


def decorator_function(original_function):

    @wraps(original_function)
    def wrapper(*args, **kwargs):
        return original_function(*args, **kwargs)

    return wrapper
```

---

## 4.5 Common Uses of Decorators

Decorators are commonly used for:

* Logging
* Authentication and authorization

Examples in Python include:

```python
@property
@staticmethod
@classmethod
```

---

# 5. Virtual Environments

## 5.1 What Is a Virtual Environment?

A virtual environment is an isolated Python environment containing its own installed packages and dependencies.

Consider two projects:

* Project A requires `Django 4`
* Project B requires `Django 5`

Installing packages globally can create dependency conflicts. Virtual environments solve this problem by isolating project dependencies.

---

## 5.2 Creating a Virtual Environment

Python provides the built-in `venv` module.

```bash
python3 -m venv .venv
```

This creates a virtual environment named `.venv`.

A typical project structure might be:

```text
project/
│
├── .venv/
├── main.py
└── requirements.txt
```

---

## 5.3 Activating the Environment

### macOS and Linux

```bash
source .venv/bin/activate
```

### Windows Command Prompt

```cmd
.venv\Scripts\activate
```

After activation, the terminal usually displays the environment name.

```text
(.venv) user@computer project %
```

---

## 5.4 Deactivating the Environment

```bash
deactivate
```

---

## 5.5 Why Use Virtual Environments?

Virtual environments provide:

* Dependency isolation
* Project-specific package versions
* Cleaner development environments

---

# 6. pip Package Manager

## 6.1 What Is pip?

`pip` is Python's package installer and package manager. It is used to install, upgrade, uninstall, and manage Python packages.

Example:

```bash
pip install matplotlib
```


---

## 6.2 Installing a Package

```bash
python3 -m pip install requests
```

---

## 6.3 Installing a Specific Version

```bash
python3 -m pip install requests==2.31.0
```

---

## 6.4 Uninstalling a Package

```bash
python3 -m pip uninstall requests
```

---

## 6.5 Viewing Installed Packages

```bash
python3 -m pip list
```
---


## 6.6 Creating a Requirements File

A project can store its dependencies in a `requirements.txt` file.

```bash
python3 -m pip freeze > requirements.txt
```
---

## 6.7 Installing Dependencies from a File

```bash
python3 -m pip install -r requirements.txt
```

---

# 7. PEP 8 Standards Summary

## 7.1 What Is PEP 8?

PEP stands for **Python Enhancement Proposal**.

PEP 8 is Python's official style guide for writing readable and consistent Python code. Its purpose is to improve code readability and maintainability.

---

## 7.2 Indentation

Use four spaces for each indentation level.

Correct:

```python
if age >= 18:
    print("Adult")
```

---

## 7.3 Maximum Line Length

Traditional PEP 8 guidance recommends keeping lines around 79 characters or fewer.

Long expressions can be broken across multiple lines.

```python
result = (
    first_value
    + second_value
    + third_value
)
```

---

## 7.4 Blank Lines

Use blank lines to separate top-level functions and classes.

```python
class User:
    pass


def create_user():
    pass
```

Top-level definitions are generally separated clearly, while related methods inside a class have tighter spacing.

---

## 7.5 Naming Conventions

### Variables and Functions

Use `snake_case`.

```python
student_name = "Ravi"


def calculate_total():
    pass
```

---

### Classes

Use `PascalCase`.

```python
class BankAccount:
    pass
```

---

### Constants

Use uppercase letters with underscores.

```python
MAX_USERS = 100
DATABASE_URL = "localhost"
```

---

### Private/Internal Attributes

Use a leading underscore for non-public implementation details.

```python
self._balance
```

Double leading underscores invoke name mangling:

```python
self.__balance
```

---

## 7.6 Imports

Imports should normally be placed at the top of a module.

Example:

```python
import os
from pathlib import Path

import matplotlib.pyplot as plt
import numpy as np

from data import load_data
```

---

## 7.7 Whitespace Around Operators

Use spaces around most binary operators.

Correct:

```python
total = price + tax
```

Avoid:

```python
total=price+tax
```

---

## 7.8 Spaces After Commas

Correct:

```python
numbers = [1, 2, 3, 4]
```

Avoid:

```python
numbers = [1,2,3,4]
```

---

## 7.9 Function Definitions

Use descriptive names and appropriate spacing.

```python
def calculate_average(numbers):
    return sum(numbers) / len(numbers)
```

---

## 7.10 Comments

Comments should explain why something is done when the code itself does not make the reason obvious.

```python
# Retry because the external API occasionally times out.
response = fetch_data()
```

---

## 7.11 Documentation Strings

Use docstrings to document modules, classes, and public functions when appropriate.

```python
def calculate_square(number):
    """Return the square of a number."""
    return number ** 2
```

---


# 8. References:
- Python full course (https://youtube.com/playlist?list=PLsyeobzWxl7poL9JTVyndKe62ieoN-MZ3&si=r3B9DBf4ZqrKTXhz)

- W3School (https://www.w3schools.com/python/)
- python.org (https://docs.python.org/3/tutorial/index.html)
