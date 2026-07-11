# Lesson 11 – Django ORM Basics

## 📖 Overview

In the previous lesson, we learned how to create database tables using Django Migrations. However, an empty database is not very useful. We need a way to insert, retrieve, update, and delete data.

Django provides the **Object Relational Mapper (ORM)**, which allows developers to interact with the database using Python code instead of writing SQL queries.

The ORM automatically translates Python code into SQL behind the scenes, making database operations easier, safer, and database-independent.

In this lesson, we'll learn the fundamentals of Django ORM and perform basic CRUD (Create, Read, Update, Delete) operations.

---

# 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand what ORM is.
- Learn why Django ORM is useful.
- Create new records.
- Retrieve records.
- Update records.
- Delete records.
- Understand how Django converts ORM queries into SQL.
- Perform CRUD operations using Django Shell.

---

# 🤔 What is ORM?

ORM stands for **Object Relational Mapper**.

It is a layer between your Python application and the database.

Instead of writing SQL like:

```sql
SELECT * FROM student;
```

you simply write

```python
Student.objects.all()
```

The ORM converts Python code into SQL automatically.

---

# 🌍 Real-World Analogy

Imagine visiting a restaurant.

You don't go into the kitchen and cook your own food.

Instead,

You tell the waiter what you want.

The waiter communicates with the kitchen.

The chef prepares the food.

The waiter brings the food back to you.

Similarly,

Python Code

↓

Django ORM

↓

SQL

↓

Database

↓

Result

The ORM acts like the waiter between your application and the database.

---

# Why Use Django ORM?

Without ORM

```sql
INSERT INTO student(name, age)

VALUES ('Rahul',20);
```

With ORM

```python
Student.objects.create(

    name="Rahul",

    age=20
)
```

ORM is

- Easier to read
- Database independent
- More secure
- Less error-prone
- Faster to develop

---

# 🧠 Behind the Scenes

When you write

```python
Student.objects.all()
```

Django generates SQL similar to

```sql
SELECT * FROM students_student;
```

You never have to write SQL manually.

---

# Opening Django Shell

To interact with the ORM, open the Django shell.

```bash
python manage.py shell
```

This provides an interactive Python environment with access to your Django project.

---

# Importing the Model

```python
from students.models import Student
```

Now you're ready to interact with the database.

---

# CRUD Operations

CRUD stands for:

- Create
- Read
- Update
- Delete

These are the four basic database operations.

---

# 🟢 Create

Create a new student.

```python
Student.objects.create(

    name="Rahul",

    age=20,

    email="rahul@example.com",

    course="B.Tech"
)
```

A new row is inserted into the database.

---

# Another Way to Create

```python
student = Student(

    name="Priya",

    age=21,

    email="priya@example.com",

    course="BCA"
)

student.save()
```

`save()` writes the object to the database.

---

# 🔵 Read

Retrieve all students.

```python
Student.objects.all()
```

Retrieve one student.

```python
Student.objects.get(id=1)
```

Retrieve students matching a condition.

```python
Student.objects.filter(course="B.Tech")
```

Count records.

```python
Student.objects.count()
```

Check if data exists.

```python
Student.objects.exists()
```

---

# 🟡 Update

Retrieve a student.

```python
student = Student.objects.get(id=1)
```

Modify a field.

```python
student.age = 22
```

Save changes.

```python
student.save()
```

---

# 🔴 Delete

Delete one student.

```python
student = Student.objects.get(id=1)

student.delete()
```

Delete all students.

```python
Student.objects.all().delete()
```

Use carefully.

---

# Common ORM Methods

| Method | Purpose |
|---------|----------|
| create() | Create new object |
| save() | Save object |
| all() | Retrieve all objects |
| get() | Retrieve one object |
| filter() | Retrieve matching objects |
| count() | Count records |
| exists() | Check if records exist |
| delete() | Delete records |

---

# Mini Project

Create five students.

Retrieve all students.

Retrieve one student.

Update one student's course.

Delete one student.

Verify changes using

```python
Student.objects.all()
```

---

# Folder Structure

```
students/

├── models.py

├── admin.py

├── views.py
```

For this lesson, we only use

- models.py
- Django Shell

---

# ❌ Common Mistakes

### Forgetting to save

Wrong

```python
student.age = 22
```

Correct

```python
student.age = 22

student.save()
```

---

### Using get() when multiple objects exist

Wrong

```python
Student.objects.get(course="B.Tech")
```

If multiple students belong to B.Tech,

this raises

```
MultipleObjectsReturned
```

Use

```python
Student.objects.filter(course="B.Tech")
```

instead.

---

### Forgetting to import models

```python
from students.models import Student
```

---

### Deleting all records accidentally

Be careful with

```python
Student.objects.all().delete()
```

It removes every record from the table.

---

# 💡 Best Practices

✔ Use `create()` for simple object creation.

✔ Use `save()` when updating an object.

✔ Use `filter()` when multiple results are expected.

✔ Use `get()` only when exactly one object should exist.

✔ Test ORM queries in Django Shell before using them in views.

---

# 📝 Exercises

## Exercise 1

Insert three students into the database.

---

## Exercise 2

Retrieve all students.

---

## Exercise 3

Update one student's email address.

---

## Exercise 4

Delete one student.

---

## Exercise 5

Count the total number of students.

---

# 🎤 Interview Questions

### What is ORM?

---

### Why do we use Django ORM?

---

### Difference between

```python
create()
```

and

```python
save()
```

---

### Difference between

```python
get()
```

and

```python
filter()
```

---

### What does

```python
count()
```

return?

---

### Why is ORM better than raw SQL?

---

# 📚 Official Documentation

Making Queries

https://docs.djangoproject.com/en/6.0/topics/db/queries/

QuerySet API

https://docs.djangoproject.com/en/6.0/ref/models/querysets/

---

# 📌 Summary

In this lesson, we learned how Django ORM allows developers to interact with the database using Python instead of SQL.

We performed the four basic CRUD operations:

- Create
- Read
- Update
- Delete

We also explored commonly used ORM methods like `create()`, `save()`, `all()`, `get()`, `filter()`, `count()`, `exists()`, and `delete()`.

Understanding these operations is essential because almost every Django application relies on the ORM to manage data.

---

# 🧪 Quick Recap

✅ I understand what ORM is.

✅ I can create new records.

✅ I can retrieve records.

✅ I can update records.

✅ I can delete records.

✅ I know the difference between `get()` and `filter()`.

---

# ➡️ Next Lesson

**Lesson 12 – Querying Data with Django ORM**

In the next lesson, we'll explore advanced querying techniques such as `exclude()`, `order_by()`, `values()`, `values_list()`, `Q` objects, `annotate()`, `aggregate()`, and more to efficiently retrieve and analyze data.