# Object-Oriented Programming (OOP) in Python

## Introduction

Object-Oriented Programming (OOP) is a programming paradigm that organizes programs around **objects** and **classes**. Instead of writing a program only as a collection of functions, OOP combines **data** and the **methods that operate on that data** into objects.

Python supports object-oriented programming and provides features such as:

* Classes and objects
* Instance variables
* Class variables
* Instance methods
* Class methods
* Static methods
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction

---

# 1. Classes and Objects

## 1.1 What Is a Class?

A **class** is a blueprint or template used to create objects.

For example, a `Car` class can define common properties and behaviors of cars.

```python
class Car:
    pass
```

The `pass` keyword is used as a placeholder when a class or function has no implementation yet.

---

## 1.2 What Is an Object?

An **object** is an instance of a class.

```python
class Car:
    pass


car1 = Car()
car2 = Car()
```

Here:

* `Car` is the class.
* `car1` is an object of `Car`.
* `car2` is another object of `Car`.

Each object is created independently.

---

# 2. The `__init__()` Method

The `__init__()` method is automatically called when an object is created. It is commonly used to initialize the attributes of an object.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Creating an object:

```python
student1 = Student("Ravi", 22)

print(student1.name)
print(student1.age)
```

Output:

```text
Ravi
22
```

When this statement runs:

```python
student1 = Student("Ravi", 22)
```

Python effectively creates an object and calls:

```python
__init__(student1, "Ravi", 22)
```

The first argument, `self`, refers to the object currently being initialized.

---

# 3. Understanding `self`

`self` represents the **current instance of a class**.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def introduce(self):
        print(f"My name is {self.name}")
```

Usage:

```python
student = Student("Ravi")

student.introduce()
```

Output:

```text
My name is Ravi
```

When calling:

```python
student.introduce()
```

Python internally passes the object:

```python
Student.introduce(student)
```

Therefore, `self` allows instance methods to access the data belonging to a particular object.

---

# 4. Instance Variables

Instance variables belong to individual objects.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

```python
student1 = Student("Ravi", 22)
student2 = Student("Amit", 24)
```

Each object has its own values.

```python
print(student1.name)
print(student2.name)
```

Output:

```text
Ravi
Amit
```

Changing one object's instance variable does not change another object's variable.

```python
student1.name = "Rahul"

print(student1.name)
print(student2.name)
```

Output:

```text
Rahul
Amit
```

---

# 5. Instance Methods

An instance method operates on a particular object and receives `self` as its first parameter.

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        self.balance -= amount

    def display_balance(self):
        print(self.balance)
```

Usage:

```python
account = BankAccount(1000)

account.deposit(500)
account.withdraw(200)
account.display_balance()
```

Output:

```text
1300
```

---

# 6. Class Variables

A class variable belongs to the class and is generally shared by all instances.

```python
class Employee:
    company = "ABC Technologies"

    def __init__(self, name):
        self.name = name
```

Creating objects:

```python
employee1 = Employee("Ravi")
employee2 = Employee("Amit")
```

Accessing the class variable:

```python
print(employee1.company)
print(employee2.company)
print(Employee.company)
```

Output:

```text
ABC Technologies
ABC Technologies
ABC Technologies
```

The variable `company` belongs to the `Employee` class.

---

# 7. Instance Variables vs Class Variables

| Instance Variable                      | Class Variable                    |
| -------------------------------------- | --------------------------------- |
| Belongs to an object                   | Belongs to the class              |
| Each object can have a different value | Usually shared by all objects     |
| Created using `self.variable`          | Created directly inside the class |
| Accessed through an object             | Can be accessed through the class |

Example:

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name
```

Here:

* `company` is a class variable.
* `name` is an instance variable.

---

# 8. Class Methods

A class method works with the class rather than a specific instance.

The `@classmethod` decorator is used to create a class method.

```python
class Employee:
    company = "ABC Technologies"

    @classmethod
    def change_company(cls, new_company):
        cls.company = new_company
```

Usage:

```python
Employee.change_company("XYZ Technologies")

print(Employee.company)
```

Output:

```text
XYZ Technologies
```

The `cls` parameter refers to the current class.

---

# 9. Static Methods

A static method does not automatically receive `self` or `cls`.

The `@staticmethod` decorator is used to create a static method.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b
```

Usage:

```python
result = Calculator.add(10, 20)

print(result)
```

Output:

```text
30
```

Static methods are useful for utility functionality logically related to a class.

---

# 10. Instance Methods vs Class Methods vs Static Methods

| Method Type     | First Parameter    | Works With                |
| --------------- | ------------------ | ------------------------- |
| Instance Method | `self`             | Object data               |
| Class Method    | `cls`              | Class data                |
| Static Method   | None automatically | Independent utility logic |

Example:

```python
class Example:
    class_variable = 100

    def instance_method(self):
        return self.class_variable

    @classmethod
    def class_method(cls):
        return cls.class_variable

    @staticmethod
    def static_method():
        return "Hello"
```

---

# 11. Encapsulation

Encapsulation means combining data and methods inside a class and controlling how the data is accessed or modified.

Python uses naming conventions to indicate access levels.

## Public Attribute

```python
class Student:
    def __init__(self):
        self.name = "Ravi"
```

The attribute can be accessed directly.

```python
student = Student()

print(student.name)
```

---

## Protected Convention

A single underscore indicates that an attribute is intended for internal use.

```python
class Student:
    def __init__(self):
        self._name = "Ravi"
```

The underscore is mainly a convention; Python does not strictly prevent access.

```python
student = Student()

print(student._name)
```

---

## Private Name Mangling

A double underscore triggers name mangling.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance
```

Direct access using the original name does not work normally:

```python
account = BankAccount(1000)

# print(account.__balance)
```

Python internally changes the attribute name approximately to:

```python
account._BankAccount__balance
```

This mechanism is called **name mangling**.

---

# 12. Getters and Setters

Getters and setters provide controlled access to attributes.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def set_balance(self, balance):
        if balance >= 0:
            self.__balance = balance
```

Usage:

```python
account = BankAccount(1000)

account.set_balance(2000)

print(account.get_balance())
```

---

# 13. The `@property` Decorator

Python provides a more natural way to create getters and setters using `@property`.

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, value):
        if value < 0:
            raise ValueError("Balance cannot be negative")

        self._balance = value
```

Usage:

```python
account = BankAccount(1000)

print(account.balance)

account.balance = 2000

print(account.balance)
```

The code looks like normal attribute access, but the getter and setter methods execute internally.

---

# 14. Inheritance

Inheritance allows one class to acquire and reuse the properties and methods of another class.

The existing class is called the:

* Parent class
* Base class
* Superclass

The new class is called the:

* Child class
* Derived class
* Subclass

Example:

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    pass
```

Since `Dog` inherits from `Animal`, it can use the `eat()` method.

```python
dog = Dog()

dog.eat()
```

Output:

```text
Animal is eating
```

---

# 15. Method Overriding

A child class can provide its own implementation of a parent method.

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

The child class method overrides the parent class method.

---

# 16. The `super()` Function

The `super()` function allows a child class to access methods or constructors from its parent class.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

Usage:

```python
dog = Dog("Rocky", "Labrador")

print(dog.name)
print(dog.breed)
```

Output:

```text
Rocky
Labrador
```

`super().__init__(name)` initializes the parent class portion of the object.

---

# 17. Types of Inheritance

## 17.1 Single Inheritance

One child inherits from one parent.

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

---

## 17.2 Multilevel Inheritance

A class inherits from another child class.

```python
class Animal:
    pass


class Mammal(Animal):
    pass


class Dog(Mammal):
    pass
```

---

## 17.3 Multiple Inheritance

A class inherits from more than one parent.

```python
class Father:
    def father_method(self):
        print("Father")


class Mother:
    def mother_method(self):
        print("Mother")


class Child(Father, Mother):
    pass
```

Usage:

```python
child = Child()

child.father_method()
child.mother_method()
```

---

## 17.4 Hierarchical Inheritance

Multiple child classes inherit from one parent.

```python
class Animal:
    pass


class Dog(Animal):
    pass


class Cat(Animal):
    pass
```

---

# 18. Polymorphism

Polymorphism means **one interface with multiple forms of behavior**.

Different objects can respond differently to the same method call.

```python
class Dog:
    def speak(self):
        return "Bark"


class Cat:
    def speak(self):
        return "Meow"
```

```python
animals = [Dog(), Cat()]

for animal in animals:
    print(animal.speak())
```

Output:

```text
Bark
Meow
```

The same method name, `speak()`, produces different behavior.

---

# 19. Duck Typing

Python supports duck typing.

The idea is:

> If an object behaves like the required object, Python can use it.

Example:

```python
class Dog:
    def speak(self):
        print("Bark")


class Cat:
    def speak(self):
        print("Meow")


def make_sound(animal):
    animal.speak()
```

Both objects work:

```python
make_sound(Dog())
make_sound(Cat())
```

The function does not need to know the exact class of the object. It only requires the object to have a `speak()` method.

---

# 20. Abstraction

Abstraction means exposing only essential behavior while hiding unnecessary implementation details.

Python provides the `abc` module for creating abstract base classes.

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self):
        pass
```

A child class must implement the abstract method.

```python
class CreditCardPayment(Payment):

    def pay(self):
        print("Payment completed")
```

Usage:

```python
payment = CreditCardPayment()

payment.pay()
```

Output:

```text
Payment completed
```

The abstract `Payment` class defines what subclasses must do without specifying the complete implementation.

---

# 21. Composition

Composition is an OOP concept where one object contains or uses another object.

For example, a `Car` has an `Engine`.

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
```

Usage:

```python
car = Car()

car.start()
```

Output:

```text
Engine started
```

Composition represents a **has-a relationship**.

```text
Car has an Engine
```

Inheritance generally represents an **is-a relationship**.

```text
Dog is an Animal
```

---

# 22. Complete OOP Example

The following example combines several OOP concepts.

```python
class BankAccount:
    bank_name = "Python Bank"

    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")

        self._balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")

        if amount > self._balance:
            raise ValueError("Insufficient balance")

        self._balance -= amount

    def display_info(self):
        print(f"Account holder: {self.account_holder}")
        print(f"Balance: {self._balance}")


class SavingsAccount(BankAccount):
    def __init__(self, account_holder, balance=0, interest_rate=0.05):
        super().__init__(account_holder, balance)
        self.interest_rate = interest_rate

    def add_interest(self):
        interest = self._balance * self.interest_rate
        self._balance += interest
```

Usage:

```python
account = SavingsAccount("Ravi", 1000)

account.deposit(500)
account.withdraw(200)
account.add_interest()

account.display_info()
```

This example demonstrates:

* Class creation
* Objects
* Constructors
* Instance variables
* Class variables
* Instance methods
* Encapsulation
* Properties
* Inheritance
* Method reuse through `super()`

---

# 23. Four Main Principles of OOP

| Principle         | Meaning                                                   |
| ----------------- | --------------------------------------------------------- |
| **Encapsulation** | Combining data and methods and controlling access to data |
| **Inheritance**   | Creating new classes based on existing classes            |
| **Polymorphism**  | The same interface producing different behavior           |
| **Abstraction**   | Hiding unnecessary implementation details                 |

---

# 24. OOP Cheatsheet

## Creating a Class

```python
class MyClass:
    pass
```

## Creating an Object

```python
obj = MyClass()
```

## Constructor

```python
def __init__(self):
    pass
```

## Instance Variable

```python
self.name = "Ravi"
```

## Class Variable

```python
class MyClass:
    value = 10
```

## Instance Method

```python
def display(self):
    pass
```

## Class Method

```python
@classmethod
def method(cls):
    pass
```

## Static Method

```python
@staticmethod
def method():
    pass
```

## Inheritance

```python
class Child(Parent):
    pass
```

## Parent Constructor

```python
super().__init__()
```

## Property

```python
@property
def value(self):
    return self._value
```

## Abstract Class

```python
from abc import ABC, abstractmethod


class MyClass(ABC):

    @abstractmethod
    def method(self):
        pass
```

---

# Conclusion

Object-Oriented Programming is an important approach for designing structured and maintainable Python applications. Classes provide blueprints for objects, while objects combine state and behavior.

Python's OOP features include instance and class variables, different types of methods, encapsulation, inheritance, polymorphism, abstraction, and composition. Understanding these concepts helps developers build reusable, modular, and scalable software.

The four fundamental principles—**encapsulation, inheritance, polymorphism, and abstraction**—form the foundation of object-oriented programming and are widely used in real-world Python applications.
