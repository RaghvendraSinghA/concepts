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

A class is a blueprint or template used to create objects.

For example, a `Car` class can define common properties and behaviors of cars.

```python
class Car:
    pass
```

The `pass` keyword is used as a placeholder when a class or function has no implementation yet.

---

## 1.2 What Is an Object?

An bject is an instance of a class.

```python
car1 = Car()
car2 = Car()
```

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

print(student1.name)    #op-> Ravi
print(student1.age)    #op-> 22
```

The first argument, `self`, refers to the object currently being initialized.

---

# 3. Instance Variables

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
print(student1.name)    #op-> Ravi
print(student2.name)    #op-> Amit
```



---

# 4. Instance Methods

An instance method operates on a particular object and receives `self` as its first parameter.

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

account = BankAccount(1000)
account.display_balance()    #op-> 1000
```

---

# 5. Class Variables

A class variable belongs to the class and is generally shared by all instances.

```python
class Employee:
    company = "ABC Technologies"

    def __init__(self, name):
        self.name = name

employee1 = Employee("Ravi")
employee2 = Employee("Amit")

# Accessing the class variable:

print(employee1.company) #op->ABC Technologies
print(employee2.company) #op->ABC Technologies
print(Employee.company). #op->ABC Technologies
```

---

# 6. Class Methods

A class method works with the class rather than a specific instance.

The `@classmethod` decorator is used to create a class method.

```python
class Employee:
    company = "ABC Technologies"

    @classmethod
    def change_company(cls, new_company):
        cls.company = new_company

    #These classmethods are shared to instance object too.

Employee.change_company("XYZ Technologies")

print(Employee.company) #op-> XYZ Technologies

```

The `cls` parameter refers to the current class.
`cls.variablenameofclass` inside classmethod to access class variables.

---

# 7. Static Methods

A static method does not automatically receive `self` or `cls`.

The `@staticmethod` decorator is used to create a static method.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b

result = Calculator.add(10, 20)    # op-> 30

print(result)
```

static methods cannot access `cls` of class but, they can directly access class variables.

```python

    @staticmethod
    def add(a, b):
        return ClassName.variablename

```

static methods cannot access `self` of instance but, they can access object variables
if u create an object and pass them to it.

```python

class Test():

    @staticmethod
    def print_name(obj):
        return obj.name

    def __init__(self, name):
        self.name

x = Test("Ravi")

print(Test.print_name(x))

```

Static methods are useful for utility functionality logically related to a class like helper function while classmethods are used for class logic like math class.
In static method you pass parameters, No self or cls.It calculate with logic and return.

---

# 8. Encapsulation

Encapsulation means combining data and methods inside a class and controlling how the data is accessed or modified.

Python uses naming conventions to indicate access levels.

## Public Attribute

```python
class Student:
    def __init__(self):
        self.name = "Ravi"

#The attribute can be accessed directly.

student = Student()

print(student.name) #op-> Ravi
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

print(student._name)    #op-> Ravi
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

# print(account.__balance)        #op-> error
```

Python internally changes the attribute name approximately to:

```python
account._BankAccount__balance

#This mechanism is called name mangling.

#But, you can access like this print(account._BankAccount__balance)   op-> no error
```

---

# 9. Getters and Setters

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

account = BankAccount(1000)

account.set_balance(2000)

print(account.get_balance()) #op->2000
```

---

# 10. The `@property` Decorator

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

account = BankAccount(1000)

print(account.balance)    #op-> 1000

account.balance = 2000

print(account.balance)    #op-> 2000
```

The code looks like normal attribute access, but the getter and setter methods execute internally.

---

# 11. Inheritance

Inheritance allows one class to acquire and reuse the properties and methods of another class.

The existing class is called:

* Parent class or Base class or Superclass

The new class is called the:

* Child class or Derived class or Subclass

Example:

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    pass

dog = Dog()

dog.eat()    #op-> Animal is eating    
```

---

# 12. Method Overriding

A child class can provide its own implementation of a parent method.

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    def speak(self):
        print("Dog barks")

dog = Dog()

dog.speak() #op-> Dog barks
```

The child class method overrides the parent class method.

---

# 13. The `super()` Function

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

print(dog.name)    #op->Rocky
print(dog.breed)    #op->Labrador
```

`super().__init__(name)` initializes the parent class portion of the object.

---

# 14. Types of Inheritance

## 14.1 Single Inheritance

One child inherits from one parent.

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

---

## 14.2 Multilevel Inheritance

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

## 14.3 Multiple Inheritance

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


child = Child()

child.father_method()
child.mother_method()
```

What if both have same method?
Then Father class method will be executed bcoz his order is first.

---

## 14.4 Hierarchical Inheritance

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

# 15. Polymorphism

Polymorphism means one interface with multiple forms of behavior.

Different objects can respond differently to the same method call.

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


#Output:
# Bark
# Meow
```
---

# 16. Duck Typing

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


---

# 17. Abstraction

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

# 18. Composition/Aggregation

Composition is an OOP concept where one object contains or uses another object.

For example, a `Car` has an `Engine`.

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self,):
        self.engine = Engine()

    def start(self):
        self.engine.start()

car = Car()

car.start()    #op->Engine started
```

Composition represents a **has-a relationship**.

```text
Car has an Engine
```

Inheritance generally represents an **is-a relationship**.

```text
Dog is an Animal
```

Dependency

Car USES-A Logger

It means it doesn't inherit or create object automatically.It asks for object in parameter while creating class object.

```python
class DependentClass():
    def __init__(self,other_class_dependency_object):
        other_class_dependency_object.fn_name()
        # we don't store it in self just use it temporarily.
    
```

---






