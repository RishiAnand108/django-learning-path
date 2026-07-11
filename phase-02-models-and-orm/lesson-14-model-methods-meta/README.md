# Lesson 14 – Model Methods & Meta Options

## 📖 Overview

In the previous lessons, we learned how to create models, define fields, perform CRUD operations, query data, and establish relationships between models.

However, a Django model is more than just a collection of database fields. Models can also contain **custom methods** and **metadata** that make them easier to use, organize, and maintain.

Model methods allow us to add business logic directly to our models, while the **Meta** class lets us configure how Django should behave with the model.

In this lesson, we'll learn how to use model methods like `__str__()`, create custom methods, and configure model behavior using the Meta class.

---

# 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand why model methods are useful.
- Use the `__str__()` method.
- Create custom model methods.
- Understand the purpose of the Meta class.
- Configure model ordering.
- Set verbose names.
- Add model constraints.
- Follow Django best practices for clean models.

---

# 🤔 Why Do We Need Model Methods?

Consider the following Student model.

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()
```

If you retrieve an object,

```python
student = Student.objects.first()

print(student)
```

The output will be

```
Student object (1)
```

This is not very useful.

Instead, we want Django to display

```
Rahul
```

This is where the `__str__()` method comes in.

---

# 🌍 Real-World Analogy

Imagine a school ID card.

Instead of showing

```
Student #1452
```

it displays

```
Rahul Sharma
```

The `__str__()` method works in a similar way.

It tells Django how an object should be represented as a human-readable string.

---

# What is `__str__()`?

The `__str__()` method returns a readable string representation of an object.

Without it

```
Student object (1)
```

With it

```
Rahul
```

---

# Implementing `__str__()`

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    def __str__(self):

        return self.name
```

Now,

```python
Student.objects.first()
```

displays

```
Rahul
```

inside

- Django Admin
- Django Shell
- Query Results

---

# Why is `__str__()` Important?

Without `__str__()`

```
Student object (1)

Student object (2)

Student object (3)
```

With `__str__()`

```
Rahul

Priya

Amit
```

Much easier to understand.

---

# Custom Model Methods

Models can contain custom methods.

Example

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    def is_adult(self):

        return self.age >= 18
```

Usage

```python
student = Student.objects.first()

student.is_adult()
```

Output

```
True
```

Custom methods help keep business logic inside the model.

---

# Another Example

```python
class Student(models.Model):

    first_name = models.CharField(max_length=50)

    last_name = models.CharField(max_length=50)

    def full_name(self):

        return f"{self.first_name} {self.last_name}"
```

Usage

```python
student.full_name()
```

Output

```
Rahul Sharma
```

---

# What is the Meta Class?

The `Meta` class is used to configure how Django behaves with your model.

It does **not** create database fields.

Instead, it provides metadata about the model.

Example

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    class Meta:

        ordering = ["name"]
```

Now every query returns students sorted alphabetically by name.

---

# Common Meta Options

## ordering

Sort records automatically.

```python
class Meta:

    ordering = ["name"]
```

Descending order

```python
ordering = ["-age"]
```

---

## verbose_name

Change the singular name.

```python
class Meta:

    verbose_name = "Student"
```

---

## verbose_name_plural

Change the plural name.

```python
class Meta:

    verbose_name_plural = "Students"
```

Useful in Django Admin.

---

## db_table

Specify a custom database table name.

```python
class Meta:

    db_table = "student_details"
```

Instead of

```
students_student
```

the table becomes

```
student_details
```

---

## constraints

Add database-level rules.

Example

```python
from django.db import models

class Meta:

    constraints = [

        models.UniqueConstraint(

            fields=["email"],

            name="unique_email"

        )

    ]
```

This prevents duplicate email addresses.

---

# Complete Example

```python
from django.db import models

class Student(models.Model):

    first_name = models.CharField(max_length=50)

    last_name = models.CharField(max_length=50)

    age = models.IntegerField()

    email = models.EmailField(unique=True)

    def __str__(self):

        return self.full_name()

    def full_name(self):

        return f"{self.first_name} {self.last_name}"

    def is_adult(self):

        return self.age >= 18

    class Meta:

        ordering = ["first_name"]

        verbose_name = "Student"

        verbose_name_plural = "Students"
```

---

# 🧠 Behind the Scenes

When Django loads a model,

it also reads the Meta class.

The Meta class tells Django

- how to order records,
- how the model should appear in the Admin Panel,
- what table name to use,
- and which database constraints should be enforced.

---

# Mini Project

Update the existing Student model.

Add

- `__str__()`
- `full_name()`
- `is_adult()`

Configure

- ordering
- verbose_name
- verbose_name_plural

Run

```bash
python manage.py makemigrations

python manage.py migrate
```

Verify the changes in the Django Admin.

---

# ❌ Common Mistakes

### Forgetting to return a string

Wrong

```python
def __str__(self):

    return self.age
```

Correct

```python
def __str__(self):

    return self.name
```

---

### Putting business logic inside views

Instead of

```python
if student.age >= 18:
```

create

```python
student.is_adult()
```

inside the model.

---

### Forgetting the Meta indentation

Always define Meta inside the model class.

---

# 💡 Best Practices

✔ Always define `__str__()`.

✔ Keep business logic inside models.

✔ Use the Meta class for configuration.

✔ Use meaningful model methods.

✔ Keep models readable and maintainable.

---

# 📝 Exercises

## Exercise 1

Implement `__str__()` in the Teacher model.

---

## Exercise 2

Create a `full_name()` method.

---

## Exercise 3

Create an `is_minor()` method.

---

## Exercise 4

Sort students by age using the Meta class.

---

## Exercise 5

Rename the database table using `db_table`.

---

# 🎤 Interview Questions

### What is the purpose of `__str__()`?

---

### Why do we use custom model methods?

---

### What is the Meta class?

---

### Difference between `verbose_name` and `verbose_name_plural`?

---

### What does `ordering` do?

---

### Why should business logic be placed inside models?

---

# 📚 Official Documentation

Model Instance Methods

https://docs.djangoproject.com/en/6.0/topics/db/models/

Model Meta Options

https://docs.djangoproject.com/en/6.0/ref/models/options/

---

# 📌 Summary

In this lesson, we learned how to improve Django models using custom methods and the Meta class. We explored the importance of `__str__()` for readable object representations, created reusable model methods to encapsulate business logic, and configured model behavior using Meta options such as `ordering`, `verbose_name`, `verbose_name_plural`, and `db_table`.

These features make Django models cleaner, easier to maintain, and more suitable for real-world applications.

---

# 🧪 Quick Recap

✅ I know why `__str__()` is important.

✅ I can create custom model methods.

✅ I understand the purpose of the Meta class.

✅ I can configure ordering.

✅ I can customize model names in Django Admin.

✅ I know how to add database constraints.

---

# ➡️ Next Lesson

**Lesson 15 – Student Management System (Phase 2 Project)**

In the next lesson, we'll combine everything we've learned in Phase 2 to build a complete **Student Management System**, using models, fields, migrations, relationships, and Django ORM to create a well-structured backend.