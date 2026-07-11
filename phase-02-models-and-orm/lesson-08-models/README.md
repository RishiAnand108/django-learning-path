# Lesson 08 – Django Models

## 📖 Overview

In the previous phase, we learned how to create a Django project, configure settings, create apps, define URLs, and render templates.

However, our application could not store any information permanently. Every time the server restarted, any hardcoded data remained the same.

This is where **Models** come into the picture.

A Django Model represents the structure of your data. It tells Django what information should be stored in the database and how different pieces of data are related.

In this lesson, we'll learn how to create models, understand how Django converts them into database tables, and build our first model.

---

# 🎯 Learning Objectives

After completing this lesson, you will be able to:

- Understand what a Django Model is.
- Understand why databases are required.
- Create your first Django Model.
- Understand how Django maps models to database tables.
- Learn the role of `models.Model`.
- Create database tables using migrations.
- Store and retrieve data using the Django ORM.
- Build a simple Student model.

---

# 🤔 Why Do We Need Models?

Imagine you're building a **Student Management System**.

You need to store:

- Student Name
- Roll Number
- Email
- Age
- Course

Where should this information be stored?

If you hardcode it inside Python,

```python
students = [
    {"name": "Rahul", "age": 20},
    {"name": "Priya", "age": 21},
]
```

the data disappears whenever the application changes or grows.

Instead, we store this information inside a **database**.

But writing SQL queries manually every time would be repetitive.

Django solves this using **Models**.

---

# 📚 What is a Model?

A Model is a Python class that represents a table inside the database.

Each Model becomes a table.

Each object becomes a row.

Each attribute becomes a column.

Example

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()
```

This creates a table similar to

| id | name | age |
|----|------|-----|
| 1 | Rahul | 20 |
| 2 | Priya | 21 |

---

# 🌍 Real World Analogy

Imagine a school register.

The register contains information like:

| Roll No | Name | Class | Phone |

Every student occupies one row.

Each column stores one type of information.

A Django Model works exactly the same way.

The model defines the columns.

The database stores the rows.

---

# 🏗️ How Django Models Work

```
Developer

↓

Model

↓

Migration

↓

Database Table

↓

Data Stored
```

Whenever we create or modify a model,

Django generates migrations.

Those migrations create or update the corresponding database tables.

---

# 🧠 Behind the Scenes

When Django sees

```python
class Student(models.Model):
```

it understands that

> "This is not just a Python class.
> This class represents a database table."

Every attribute inside the class becomes a column in the database.

Example

```python
name = models.CharField(max_length=100)
```

becomes

```
name VARCHAR(100)
```

inside SQLite or PostgreSQL.

---

# 💻 Code Implementation

## Step 1

Open

```
students/models.py
```

---

## Step 2

Import models

```python
from django.db import models
```

---

## Step 3

Create your first model

```python
from django.db import models

class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    email = models.EmailField()

    course = models.CharField(max_length=50)
```

---

## Understanding the Code

```python
class Student(models.Model):
```

Creates a database table called

```
student
```

---

```python
name = models.CharField(max_length=100)
```

Creates a column

```
name
```

that stores text.

---

```python
age = models.IntegerField()
```

Stores numbers.

---

```python
email = models.EmailField()
```

Stores valid email addresses.

---

```python
course = models.CharField(max_length=50)
```

Stores the course name.

---

# Running Migrations

Whenever a model changes,

run

```bash
python manage.py makemigrations
```

Output

```
Migrations for 'students':

0001_initial.py
```

Now apply it

```bash
python manage.py migrate
```

Now Django creates the table inside the database.

---

# Viewing the Database

You can open

```
db.sqlite3
```

using

- SQLite Viewer
- VS Code SQLite Extension
- DB Browser for SQLite

You'll now see

```
Student
```

as a table.

---

# Mini Project

Create a Student Model containing

- Name
- Roll Number
- Email
- Age
- Course

Run migrations.

Verify that the table is created.

---

# 🧩 Folder Structure

```
students/

├── admin.py

├── apps.py

├── migrations/

├── models.py

├── tests.py

├── views.py
```

The only file we'll modify in this lesson is

```
models.py
```

---

# ❌ Common Mistakes

### Forgetting to inherit from `models.Model`

Wrong

```python
class Student:
```

Correct

```python
class Student(models.Model):
```

---

### Forgetting migrations

After modifying models,

always run

```
makemigrations
```

followed by

```
migrate
```

---

### Forgetting to import models

Always

```python
from django.db import models
```

---

# 💡 Best Practices

✔ Use singular model names.

Good

```
Student
```

Bad

```
Students
```

✔ Use meaningful field names.

✔ Keep models focused on one entity.

✔ Add a `__str__()` method (covered in a later lesson).

---

# 📝 Exercises

### Exercise 1

Create a Teacher model.

Fields

- Name
- Subject
- Email

---

### Exercise 2

Create a Course model.

Fields

- Course Name
- Duration
- Fees

---

### Exercise 3

Run migrations.

Verify that all tables are created.

---

# 🎤 Interview Questions

### What is a Django Model?

---

### Why do we use Models?

---

### What does `models.Model` do?

---

### What happens after running `makemigrations`?

---

### What happens after running `migrate`?

---

### How does Django convert Models into database tables?

---

# 📚 Official Documentation

Models

https://docs.djangoproject.com/en/6.0/topics/db/models/

Making Migrations

https://docs.djangoproject.com/en/6.0/topics/migrations/

---

# 📌 Summary

In this lesson, we learned:

- What Django Models are
- Why Models are required
- How Django represents database tables using Python classes
- How fields become columns
- How migrations create database tables
- How to build our first Student model

Models are the foundation of every Django application. In the next lesson, we'll explore the different field types Django provides and learn when to use each one.

---

# ➡️ Next Lesson

**Lesson 09 – Django Model Fields**