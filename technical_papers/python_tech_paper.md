# Python Technical Paper and Cheatsheet

## Introduction

Python is a high-level, interpreted programming language known for its simple syntax, readability, and extensive ecosystem. It supports multiple programming paradigms, including procedural programming, object-oriented programming, and functional programming.

This paper provides a practical overview and cheatsheet covering commonly used Python concepts:

1. Array methods
2. String methods
3. Objects and Object-Oriented Programming
4. Decorators
5. Virtual environments
6. The `pip` package manager
7. PEP 8 coding standards

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

For most applications, Python lists are the standard choice.

---

## 1.2 Common List Methods

### `append()`

Adds one item to the end of a list.

```python
numbers = [1, 2, 3]

numbers.append(4)

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

### `extend()`

Adds multiple elements from an iterable.

```python
numbers = [1, 2, 3]

numbers.extend([4, 5, 6])

print(numbers)
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

---

### `insert()`

Inserts an item at a specified index.

```python
numbers = [1, 2, 4]

numbers.insert(2, 3)

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

### `remove()`

Removes the first matching value.

```python
numbers = [1, 2, 3, 2]

numbers.remove(2)

print(numbers)
```

Output:

```text
[1, 3, 2]
```

If the value does not exist, Python raises a `ValueError`.

---

### `pop()`

Removes and returns an element.

```python
numbers = [10, 20, 30]

value = numbers.pop()

print(value)
print(numbers)
```

Output:

```text
30
[10, 20]
```

An index can also be specified:

```python
numbers.pop(0)
```

---

### `clear()`

Removes all elements.

```python
numbers = [1, 2, 3]

numbers.clear()

print(numbers)
```

Output:

```text
[]
```

---

### `index()`

Returns the index of the first matching element.

```python
numbers = [10, 20, 30]

print(numbers.index(20))
```

Output:

```text
1
```

---

### `count()`

Counts how many times an element occurs.

```python
numbers = [1, 2, 2, 3, 2]

print(numbers.count(2))
```

Output:

```text
3
```

---

### `sort()`

Sorts the original list.

```python
numbers = [4, 1, 3, 2]

numbers.sort()

print(numbers)
```

Output:are

```text
[1, 2, 3, 4]
```

Descending order:

```python
numbers.sort(reverse=True)
```

Custom sorting:

```python
words = ["banana", "kiwi", "apple"]

words.sort(key=len)

print(words)
```

---

### `reverse()`

Reverses the original list.

```python
numbers = [1, 2, 3]

numbers.reverse()

print(numbers)
```

Output:

```text
[3, 2, 1]
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
numbers[1:4]
```

Output:

```text
[20, 30, 40]
```

Reverse a list:

```python
numbers[::-1]
```

---

# 2. String Methods

## 2.1 Strings in Python

A string is a sequence of Unicode characters.

```python
name = "Python"
```

Strings are **immutable**, meaning their characters cannot be modified directly.

```python
name = "Python"

# name[0] = "J"  # TypeError
```

---

## 2.2 Case Conversion Methods

### `upper()`

```python
text = "python"

print(text.upper())
```

Output:

```text
PYTHON
```

### `lower()`

```python
text = "PYTHON"

print(text.lower())
```

Output:

```text
python
```

### `title()`

```python
text = "hello world"

print(text.title())
```

Output:

```text
Hello World
```

### `capitalize()`

```python
text = "python programming"

print(text.capitalize())
```

Output:

```text
Python programming
```

### `swapcase()`

```python
text = "PyThOn"

print(text.swapcase())
```

Output:

```text
pYtHoN
```

---

## 2.3 Removing Whitespace

### `strip()`

Removes whitespace from both ends.

```python
text = "  Python  "

print(text.strip())
```

### `lstrip()`

Removes whitespace from the left.

```python
text.lstrip()
```

### `rstrip()`

Removes whitespace from the right.

```python
text.rstrip()
```

---

## 2.4 Searching Methods

### `find()`

Returns the first index of a substring. Returns `-1` if not found.

```python
text = "Hello Python"

print(text.find("Python"))
```

### `index()`

Similar to `find()`, but raises a `ValueError` if the substring does not exist.

```python
text.index("Python")
```

### `count()`

Counts occurrences.

```python
text = "banana"

print(text.count("a"))
```

### `startswith()`

```python
text = "Python"

print(text.startswith("Py"))
```

### `endswith()`

```python
print(text.endswith("on"))
```

---

## 2.5 Replacing and Splitting

### `replace()`

```python
text = "I like Java"

new_text = text.replace("Java", "Python")

print(new_text)
```

### `split()`

Converts a string into a list.

```python
text = "apple,banana,mango"

fruits = text.split(",")

print(fruits)
```

Output:

```text
['apple', 'banana', 'mango']
```

### `join()`

Combines iterable elements into a string.

```python
fruits = ["apple", "banana", "mango"]

result = ", ".join(fruits)

print(result)
```

Output:

```text
apple, banana, mango
```

---

## 2.6 String Validation Methods

| Method      | Purpose                                          |
| ----------- | ------------------------------------------------ |
| `isalpha()` | Checks whether all characters are alphabetic     |
| `isdigit()` | Checks whether all characters are digits         |
| `isalnum()` | Checks whether characters are letters or numbers |
| `isspace()` | Checks whether characters are whitespace         |
| `islower()` | Checks whether characters are lowercase          |
| `isupper()` | Checks whether characters are uppercase          |

Example:

```python
value = "123"

print(value.isdigit())
```

Output:

```text
True
```

---

# 3. Objects and Object-Oriented Programming

## 3.1 What Is Object-Oriented Programming?

Object-Oriented Programming, commonly called **OOP**, is a programming paradigm that organizes code using **objects** and **classes**.

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
```

Usage:

```python
account = BankAccount(1000)

account.deposit(500)

account.display_balance()
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

print(employee1.company)
print(employee2.company)
```

---

## 3.5 Encapsulation

Encapsulation means bundling data and behavior together and controlling access to implementation details.

Python uses naming conventions for non-public attributes.

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance
```

A double underscore triggers name mangling:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance
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

dog.speak()
```

Output:

```text
Dog barks
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

## 3.9 OOP Principles Summary

| Principle     | Description                           |
| ------------- | ------------------------------------- |
| Encapsulation | Bundles data and methods together     |
| Inheritance   | Allows classes to reuse functionality |
| Polymorphism  | Same interface, different behavior    |
| Abstraction   | Hides implementation details          |

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
* Performance measurement
* Caching
* Input validation
* Retry mechanisms
* Framework functionality

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

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
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
* Better reproducibility
* Reduced conflicts between projects
* Cleaner development environments

A recommended practice is to create a virtual environment for each Python project.

---

# 6. pip Package Manager

## 6.1 What Is pip?

`pip` is Python's package installer and package manager. It is used to install, upgrade, uninstall, and manage Python packages.

Example:

```bash
pip install matplotlib
```

On some systems:

```bash
pip3 install matplotlib
```

A more reliable approach is:

```bash
python3 -m pip install matplotlib
```

This ensures that `pip` belongs to the Python interpreter being used.

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

## 6.4 Upgrading a Package

```bash
python3 -m pip install --upgrade requests
```

---

## 6.5 Uninstalling a Package

```bash
python3 -m pip uninstall requests
```

---

## 6.6 Viewing Installed Packages

```bash
python3 -m pip list
```

---

## 6.7 Viewing Package Information

```bash
python3 -m pip show matplotlib
```

---

## 6.8 Checking Outdated Packages

```bash
python3 -m pip list --outdated
```

---

## 6.9 Creating a Requirements File

A project can store its dependencies in a `requirements.txt` file.

```bash
python3 -m pip freeze > requirements.txt
```

Example:

```text
matplotlib==3.10.0
numpy==2.2.0
pandas==2.2.3
```

---

## 6.10 Installing Dependencies from a File

```bash
python3 -m pip install -r requirements.txt
```

This makes it easier for another developer to reproduce the same project environment.

---

# 7. PEP 8 Standards Summary

## 7.1 What Is PEP 8?

PEP stands for **Python Enhancement Proposal**.

PEP 8 is Python's official style guide for writing readable and consistent Python code. Its purpose is to improve code readability and maintainability.

PEP 8 is primarily a style guide rather than a set of rules enforced by the Python interpreter.

---

## 7.2 Indentation

Use four spaces for each indentation level.

Correct:

```python
if age >= 18:
    print("Adult")
```

Avoid mixing tabs and spaces.

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

Recommended organization:

1. Standard library imports
2. Related third-party imports
3. Local application imports

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

Comments should explain **why** something is done when the code itself does not make the reason obvious.

```python
# Retry because the external API occasionally times out.
response = fetch_data()
```

Avoid comments that merely repeat obvious code.

```python
# Add 1 to count
count += 1
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

# Python Cheatsheet Summary

## List / Array Methods

```python
items.append(value)
items.extend(iterable)
items.insert(index, value)
items.remove(value)
items.pop()
items.pop(index)
items.clear()
items.index(value)
items.count(value)
items.sort()
items.sort(reverse=True)
items.reverse()
items.copy()
```

---

## String Methods

```python
text.upper()
text.lower()
text.title()
text.capitalize()
text.swapcase()

text.strip()
text.lstrip()
text.rstrip()

text.find(value)
text.index(value)
text.count(value)

text.replace(old, new)
text.split(separator)
separator.join(iterable)

text.startswith(value)
text.endswith(value)

text.isalpha()
text.isdigit()
text.isalnum()
text.isspace()
```

---

## OOP

```python
class Student:
    class_variable = "value"

    def __init__(self, name):
        self.name = name

    def instance_method(self):
        return self.name

    @classmethod
    def class_method(cls):
        return cls.class_variable

    @staticmethod
    def static_method():
        return "Static method"
```

---

## Decorator

```python
from functools import wraps


def decorator(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result

    return wrapper
```

Usage:

```python
@decorator
def my_function():
    pass
```

---

## Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
deactivate
```

---

## pip

```bash
python3 -m pip install package_name
python3 -m pip uninstall package_name
python3 -m pip list
python3 -m pip show package_name
python3 -m pip install --upgrade package_name
python3 -m pip freeze > requirements.txt
python3 -m pip install -r requirements.txt
```

---

## PEP 8

```text
Variables/functions: snake_case
Classes: PascalCase
Constants: UPPER_CASE
Indentation: 4 spaces
Imports: At the top of the file
Whitespace: Use around operators
Commas: Follow with a space
Comments: Explain why, not obvious code
Docstrings: Document public APIs where useful
Line length: Keep lines reasonably short
```

# Conclusion

Python's simplicity does not mean that its ecosystem and language features are simplistic. Lists and strings provide powerful built-in operations for data manipulation, while object-oriented programming helps organize complex applications through classes, objects, inheritance, encapsulation, polymorphism, and abstraction. Decorators enable reusable behavior around functions and methods.

Virtual environments and `pip` are essential tools for managing project dependencies and avoiding conflicts between applications. Finally, following PEP 8 helps developers write code that is consistent, readable, and easier to maintain.

Together, these concepts form an important foundation for writing professional Python applications.
