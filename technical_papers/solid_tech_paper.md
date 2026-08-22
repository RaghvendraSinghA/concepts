# SOLID Principles in Python

## Introduction

SOLID is a collection of five object-oriented design principles that help developers create software that is easier to understand, maintain, test, extend and modify.

SOLID stands for:

- S —> Single Responsibility Principle (SRP)
- O —> Open/Closed Principle (OCP)
- L —> Liskov Substitution Principle (LSP)
- I —> Interface Segregation Principle (ISP)
- D —> Dependency Inversion Principle (DIP)

These principles are guidelines for designing classes and modules. They are not strict rules that must always be followed in every situation.Sometimes we do trade-offs when necessary.

---

# 1. Single Responsibility Principle (SRP)
    A class should have one responsibility and therefore, one primary reason to change.

A class should focus on one job.

For example if  `User` class have all these things:

- Stores user information
- Validates user data
- Saves users to a database
- Sends emails

then, it has multiple responsibilities and bad design according to SRP.

---

## Bad Example

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def validate(self):
        return "@" in self.email

    def save_to_database(self):
        print(f"Saving {self.name} to database")

    def send_email(self):
        print(f"Sending email to {self.email}")
```

This class has several reasons to change:

* Validation rules may change.
* Database implementation may change.
* Email functionality may change.
* User data structure may change.

Therefore, it violates SRP.

---

## Better Design

Separate the responsibilities.

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email
```

Validation:

```python
class UserValidator:
    def validate(self, user):
        return "@" in user.email
```

Database storage:

```python
class UserRepository:
    def save(self, user):
        print(f"Saving {user.name} to database")
```

Email functionality:

```python
class EmailService:
    def send_welcome_email(self, user):
        print(f"Sending welcome email to {user.email}")
```

---

# 2. Open/Closed Principle (OCP)
    Software entities should be open for extension but closed for modification.

    This means that we should try to add new behaviour by extending existing code 
    rather than repeatedly modifying existing code.

---

## This is Bad Example

Suppose we calculate the area of different shapes.

```python
class AreaCalculator:
    def calculate(self, shape):
        if shape["type"] == "rectangle":
            return shape["width"] * shape["height"]

        if shape["type"] == "circle":
            return 3.14 * shape["radius"] ** 2
```

Now imagine adding a triangle.

We must modify `AreaCalculator`.

```python
if shape["type"] == "triangle":
    return 0.5 * shape["base"] * shape["height"]
```

Every new shape requires modifying existing code.

This increases the risk of introducing bugs.

---

## Better Design

Create a common abstraction.

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def area(self):
        pass
```

Create individual shapes.

```python
class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height
```

```python
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2
```

The calculator does not need to know the concrete shape.

```python
class AreaCalculator:
    def calculate(self, shape):
        return shape.area()
```


Now we can add a new shape without changing `AreaCalculator`.

```python
class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height
```

---

# 3. Liskov Substitution Principle (LSP)
    
    Objects of a subclass should be usable in place of objects of their parent class without breaking the program.

If `Child` inherits from `Parent`, code expecting a `Parent` should also work correctly with a `Child`.Child object should be able to replace parent object if required.

---

## Bad Example

Consider birds.

```python
class Bird:
    def fly(self):
        print("Flying")
```

A sparrow can fly.

```python
class Sparrow(Bird):
    pass
```

But a penguin cannot fly.

```python
class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly")
```

Now consider:

```python
def make_bird_fly(bird):
    bird.fly()
```

This works for:

```python
make_bird_fly(Sparrow())
```

But fails for:

```python
make_bird_fly(Penguin())
```

`Penguin` cannot correctly replace `Bird` in code that expects every bird to fly.

Therefore, this design violates LSP.

---

## Better Design

Do not place behavior in a parent class unless every child can support it.

```python
class Bird:
    def eat(self):
        print("Eating")
```

Create a separate abstraction for flying birds.

```python
class FlyingBird(Bird):
    def fly(self):
        print("Flying")
```

Now create the subclasses.

```python
class Sparrow(FlyingBird):
    pass


class Penguin(Bird):
    pass
```

Usage:

```python
sparrow = Sparrow()
penguin = Penguin()

sparrow.fly()
penguin.eat()
```

---

# 4. Interface Segregation Principle (ISP)
    A client should not be forced to depend on methods it does not use.

    Instead of creating one large interface, create smaller and focused interfaces.

    Python does not have interfaces in the same way as Java. However, we can represent interfaces using abstract base classes.

---

## Bad Example

```python
from abc import ABC, abstractmethod


class Worker(ABC):

    @abstractmethod
    def work(self):
        pass

    @abstractmethod
    def eat(self):
        pass
```

A human worker can implement both methods.

```python
class HumanWorker(Worker):

    def work(self):
        print("Working")

    def eat(self):
        print("Eating")
```

But a robot may not need `eat()`.

```python
class RobotWorker(Worker):

    def work(self):
        print("Working")

    def eat(self):
        raise NotImplementedError("Robot does not eat")
```

The robot is forced to implement an irrelevant method.

This violates ISP.

---

## Better Design

Split the large interface into smaller interfaces.

```python
class Workable(ABC):

    @abstractmethod
    def work(self):
        pass
```

```python
class Eatable(ABC):

    @abstractmethod
    def eat(self):
        pass
```

Now a human can implement both.

```python
class HumanWorker(Workable, Eatable):

    def work(self):
        print("Working")

    def eat(self):
        print("Eating")
```

A robot only implements what it needs.

```python
class RobotWorker(Workable):

    def work(self):
        print("Working")
```

---

# 5. Dependency Inversion Principle (DIP)
    High-level modules should not depend directly on low-level modules. Both should
    depend on abstractions.
    Also, abstraction should not depend on details. Details should depend on abstractions.
    
    -abstraction means how things should be done.
    -details means code implementation or logic of doing that thing.
    

---

Let's say we have a user registration system.

The high-level business logic:

```text
UserService
```

The low-level database implementation:

```text
PostgreSQLDatabase
```

A direct dependency might look like:

```text
UserService
     ↓
PostgreSQLDatabase
```

This means the business logic directly depends on a specific database.

---

## Bad Example

```python
class PostgreSQLDatabase:
    def save(self, user):
        print(f"Saving {user} to PostgreSQL")
```

```python
class UserService:
    def __init__(self):
        self.database = PostgreSQLDatabase()

    def create_user(self, user):
        self.database.save(user)
```

Usage:

```python
service = UserService()

service.create_user("Ravi")
```

The problem is that `UserService` is tightly coupled to `PostgreSQLDatabase`.

If we want to change to MongoDB:

```text
UserService
     ↓
PostgreSQLDatabase
```

must become:

```text
UserService
     ↓
MongoDBDatabase
```

We must modify the high-level business class.

---

## Better Design: Depend on an Abstraction

Create an abstraction.

```python
from abc import ABC, abstractmethod


class UserRepository(ABC):

    @abstractmethod
    def save(self, user):
        pass
```

Create the PostgreSQL implementation.

```python
class PostgreSQLDatabase(UserRepository):

    def save(self, user):
        print(f"Saving {user} to PostgreSQL")
```

Create a MongoDB implementation.

```python
class MongoDBDatabase(UserRepository):

    def save(self, user):
        print(f"Saving {user} to MongoDB")
```

Now the high-level module depends on the abstraction.

```python
class UserService:
    def __init__(self, repository):
        self.repository = repository

    def create_user(self, user):
        self.repository.save(user)
```

Usage with PostgreSQL:

```python
postgres_repository = PostgreSQLDatabase()

service = UserService(postgres_repository)

service.create_user("Ravi")
```

Usage with MongoDB:

```python
mongo_repository = MongoDBDatabase()

service = UserService(mongo_repository)

service.create_user("Ravi")
```

The `UserService` does not need to change.

---

## Dependency Injection

The previous example uses dependency injection.

Instead of creating the dependency internally:

```python
class UserService:
    def __init__(self):
        self.repository = PostgreSQLDatabase()
```

The dependency is provided from outside:

```python
class UserService:
    def __init__(self, repository):
        self.repository = repository
```

This makes the dependency replaceable.
Like we can use either mongoDB object or PostgreSQLDatabase object without any erorr and it is cleaner.



# References :

- Codewitharyan (https://codewitharyan.com/tech-blogs/solid-principles)
- Medium (https://medium.com/@danaprata/the-l-in-solid-principles-6d55cf101cdb)
- GeeksForGeeks (https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/)



