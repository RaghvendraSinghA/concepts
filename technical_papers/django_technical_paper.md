# Django Technical Paper

## 1. Transactions

### What is the use of a transaction?

A transaction is a group of database operations treated as one unit.

Either all operations succeed, or the changes are rolled back if an error occurs.

Example:

    from django.db import transaction

    with transaction.atomic():
        Match.objects.create(...)
        Delivery.objects.create(...)

### Why atomic transactions?

Atomic transactions provide all-or-nothing behaviour.

For example, while importing IPL data:

    100 matches imported
    50 deliveries imported
    ERROR

Without a transaction, partial data may remain in the database.

With `transaction.atomic()`, the changes can be rolled back if the transaction fails.

---

# 2. Settings File

`settings.py` contains the configuration of a Django project.

Common settings include:

    SECRET_KEY
    DEBUG
    INSTALLED_APPS
    MIDDLEWARE
    DATABASES
    ROOT_URLCONF
    TEMPLATES
    WSGI_APPLICATION

## Secret Key

`SECRET_KEY` is a secret value used by Django for cryptographic signing.

It is used for things such as:

- Sessions
- Password reset tokens
- CSRF-related security
- Cryptographic signatures

It should not be exposed publicly or committed to a public repository.

## Default Django Apps

A new Django project usually contains:

    INSTALLED_APPS = [
        "django.contrib.admin",
        "django.contrib.auth",
        "django.contrib.contenttypes",
        "django.contrib.sessions",
        "django.contrib.messages",
        "django.contrib.staticfiles",
    ]

They provide:

- `admin` → Django admin site
- `auth` → users, groups and permissions
- `contenttypes` → tracks model types
- `sessions` → session management
- `messages` → temporary messages
- `staticfiles` → static file management

There are many other Django and third-party apps that can be added to a project.

---

# Middleware

Middleware is a layer that processes requests before they reach the view and responses before they reach the client.

    Request
       to
    Middleware
       to
    View
       to
    Middleware
       to
    Response

## Common Django Middleware

### SecurityMiddleware

Provides security-related protections such as security headers and HTTPS-related behavior.

### SessionMiddleware

Enables session support.

    request.session

### CommonMiddleware

Provides common HTTP functionality such as URL normalization.

### CsrfViewMiddleware

Protects against CSRF attacks.

### AuthenticationMiddleware

Adds the authenticated user to the request.

    request.user

### MessageMiddleware

Enables Django's temporary message framework.

### XFrameOptionsMiddleware

Helps protect against clickjacking by controlling whether pages can be loaded inside frames.

---

# Django Security

Django provides protections against several common web security problems.

## CSRF

**Cross-Site Request Forgery**

An attacker tries to make a user's browser send an unwanted request to a website where the user is authenticated.

Django uses a CSRF token for protection.

    <form method="POST">
        {% csrf_token %}
    </form>

## XSS

**Cross-Site Scripting**

An attacker attempts to inject malicious JavaScript into a webpage.

Django templates automatically escape many HTML characters:

    {{ username }}

This helps prevent malicious HTML/JavaScript from being interpreted as code.

## Clickjacking

Clickjacking tricks a user into clicking something different from what they think they are clicking.

Django's `XFrameOptionsMiddleware` helps protect against this by controlling whether a page can be embedded in an iframe.

## Other Security Concerns

Django also provides protections/features related to:

- SQL injection
- HTTPS
- Host header validation
- Secure cookies
- Password hashing

---

# WSGI

**WSGI = Web Server Gateway Interface**

WSGI is a standard interface between a Python web application and a web server.

Django provides a WSGI application in `wsgi.py`.

    application = get_wsgi_application()

Basic flow:

    Web Server
        to
       WSGI
        to
      Django
        to
       View

WSGI allows a web server to communicate with a Python web application.

---

# 3. Models File

`models.py` defines the structure of database data using Django model classes.

Example:

    class Match(models.Model):
        season = models.IntegerField()

Django uses models to create and interact with database tables.

---

# on_delete = CASCADE

`CASCADE` means:

> If the referenced parent object is deleted, related child objects are also deleted.

Example:

    class Delivery(models.Model):
        match = models.ForeignKey(
            Match,
            on_delete=models.CASCADE
        )

If a `Match` is deleted, its related `Delivery` objects are also deleted.

    Match
      ↓
    Deliveries
      ↓
    Deleted

---

# Django Model Fields

Fields define the type of data stored in a model.

Common fields include:

    CharField
    TextField
    IntegerField
    FloatField
    BooleanField
    DateField
    DateTimeField
    EmailField
    URLField
    DecimalField
    ForeignKey
    OneToOneField
    ManyToManyField

Example:

    class Match(models.Model):
        season = models.IntegerField()
        team1 = models.CharField(max_length=100)
        date = models.DateField()

---

# Validators

Validators check whether a value satisfies a condition.

Example:

    from django.core.validators import MinValueValidator

    age = models.IntegerField(
        validators=[MinValueValidator(18)]
    )

Common validators include:

    MinValueValidator
    MaxValueValidator
    MinLengthValidator
    MaxLengthValidator
    RegexValidator
    EmailValidator
    URLValidator

---

# Python Module vs Class

## Module

A Python module is usually a `.py` file containing Python code.

Example:

    models.py

It can contain classes, functions and variables.

## Class

A class is a blueprint for creating objects.

    class Match:
        pass

Therefore:

    models.py → module
    Match     → class

A module can contain multiple classes.

---

# 4. Django ORM

ORM stands for **Object Relational Mapper**.

It allows us to interact with the database using Python instead of writing SQL directly.

Example:

    Match.objects.all()

Instead of directly writing:

    SELECT * FROM match;

---

# Using ORM in Django Shell

Start the Django shell:

    python manage.py shell

Then:

    from ipl_app.models import Match

    matches = Match.objects.all()

    for match in matches:
        print(match.season)

---

# Turning ORM into SQL

In Django Shell:

    query = Match.objects.filter(season=2015)

    print(query.query)

This displays the SQL generated by Django.

---

# Aggregations

Aggregation calculates a summary value from multiple database rows.

Common aggregation functions:

    Count
    Sum
    Avg
    Min
    Max

Example:

    from django.db.models import Count

    Match.objects.aggregate(
        total=Count("id")
    )

Result:

    {"total": 756}

`aggregate()` usually produces an overall summary value.

---

# Annotations

`annotate()` adds a calculated value to each object or group in a QuerySet.

Example:

    from django.db.models import Count

    Match.objects.values("season").annotate(
        matches=Count("id")
    )

Result:

    2008 → 58
    2009 → 57
    2010 → 60

Simple difference:

    aggregate() → overall summary
    annotate()  → calculated value for each object/group

---

# Migration File

A migration file contains instructions for changing the database structure based on model changes.

Example model:

    class Match(models.Model):
        season = models.IntegerField()

Create migrations:

    python manage.py makemigrations

Apply migrations:

    python manage.py migrate

Flow:

    models.py
        to
    makemigrations
        to
    migration file
        to
    migrate
        to
    database

Migration files allow Django to track and apply database schema changes.

---

# SQL Transactions

A SQL transaction is a group of database operations treated as one unit.

Example:

    BEGIN;

    UPDATE accounts
    SET balance = balance - 100
    WHERE id = 1;

    UPDATE accounts
    SET balance = balance + 100
    WHERE id = 2;

    COMMIT;

If something goes wrong:

    ROLLBACK;

`COMMIT` saves the transaction and `ROLLBACK` undoes its changes.

---

# Atomic Transactions

Atomic means all or nothing.

    All operations succeed
            then
          COMMIT

    Something fails
            then
         ROLLBACK

In Django:

    from django.db import transaction

    with transaction.atomic():
        Match.objects.create(...)
        Delivery.objects.create(...)

The operations inside `atomic()` are treated as one transaction.

---


# References

- Django Security:
  https://docs.djangoproject.com/en/4.0/topics/security/

- Django Settings:
  https://docs.djangoproject.com/en/4.0/topics/settings/

- Django Middleware:
  https://docs.djangoproject.com/en/4.0/topics/http/middleware/

- Django CSRF Protection:
  https://docs.djangoproject.com/en/4.0/ref/csrf/

- Django Model Fields:
  https://docs.djangoproject.com/en/4.0/ref/models/fields/

- Django Validators:
  https://docs.djangoproject.com/en/4.0/ref/validators/

- Django Models:
  https://docs.djangoproject.com/en/4.0/topics/db/models/

- Django ORM:
  https://docs.djangoproject.com/en/4.0/topics/db/queries/

- Django Aggregation:
  https://docs.djangoproject.com/en/4.0/topics/db/aggregation/

- Django Transactions:
  https://docs.djangoproject.com/en/4.0/topics/db/transactions/

- Django Migrations:
  https://docs.djangoproject.com/en/4.0/topics/migrations/

- Django Management Commands:
  https://docs.djangoproject.com/en/4.0/howto/custom-management-commands/

- Django WSGI:
  https://docs.djangoproject.com/en/4.0/howto/deployment/wsgi/

- WSGI:
  https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface
