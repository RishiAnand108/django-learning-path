# Lesson 09 – Django Model Fields

## 📖 Overview

In the previous lesson, we learned that a **Django Model** represents a database table. However, a table is useful only when it contains meaningful columns to store different types of information.

These columns are defined using **Model Fields**.

A field tells Django **what type of data** should be stored, how it should be validated, and how it should be represented in the database.

In this lesson, we'll explore the most commonly used field types, understand when to use them, and learn about important field options like `null`, `blank`, `default`, and `choices`.

---

# 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand what Model Fields are.
- Learn the most commonly used Django field types.
- Choose the appropriate field for different types of data.
- Understand field options such as `null`, `blank`, `default`, and `choices`.
- Build a Student model using multiple field types.

---

# 🤔 What is a Model Field?

A Model Field defines the type of data that will be stored in a database column.

Every field inside a Django model becomes a column in the corresponding database table.

For example:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
```

creates a column named `name` that stores text.

---

# 🌍 Real-World Analogy

Imagine filling out a college admission form.

Each field expects a different type of input.

| Field | Expected Data |
|--------|---------------|
| Name | Text |
| Age | Number |
| Email | Email Address |
| Date of Birth | Date |
| Admission Fee | Decimal |
| Active | Yes / No |

Similarly, Django Model Fields define what type of data each column can store.

---

# 🏗️ Common Django Field Types

## CharField

Used for storing short text.

Examples:

- Name
- City
- Country
- Course

```python
name = models.CharField(max_length=100)
```

`max_length` is mandatory because Django needs to know the maximum number of characters allowed.

---

## TextField

Used for storing long text.

Examples:

- Description
- Feedback
- Blog Content

```python
description = models.TextField()
```

Unlike `CharField`, it does not require `max_length`.

---

## IntegerField

Stores whole numbers.

Examples:

- Age
- Quantity
- Marks

```python
age = models.IntegerField()
```

---

## FloatField

Stores decimal numbers.

Example:

```python
rating = models.FloatField()
```

Example values:

```
4.5
3.75
9.8
```

---

## DecimalField

Used for financial calculations where precision is important.

```python
fees = models.DecimalField(max_digits=8, decimal_places=2)
```

Example:

```
15000.00
```

Unlike FloatField, DecimalField avoids rounding errors.

---

## BooleanField

Stores only two values.

```python
is_active = models.BooleanField(default=True)
```

Possible values:

- True
- False

---

## EmailField

Stores email addresses.

```python
email = models.EmailField()
```

Django automatically validates the format.

---

## DateField

Stores only dates.

```python
date_of_birth = models.DateField()
```

Example:

```
2026-07-12
```

---

## DateTimeField

Stores both date and time.

```python
created_at = models.DateTimeField(auto_now_add=True)
```

Useful for:

- Created Time
- Updated Time
- Login Time

---

## ImageField

Stores image paths.

```python
profile_picture = models.ImageField(upload_to="students/")
```

Requires Pillow:

```bash
pip install pillow
```

---

## FileField

Stores uploaded files.

```python
resume = models.FileField(upload_to="documents/")
```

Useful for

- PDFs
- Resumes
- Documents

---

# 🛠 Field Options

## null=True

Allows the database to store NULL values.

```python
phone = models.CharField(max_length=15, null=True)
```

---

## blank=True

Allows forms to accept empty values.

```python
phone = models.CharField(max_length=15, blank=True)
```

---

## null vs blank

| null | blank |
|------|-------|
| Database | Form Validation |
| SQL Concept | Django Concept |

In most text fields:

```python
blank=True
```

is usually enough.

---

## default

Provides a default value.

```python
country = models.CharField(max_length=50, default="India")
```

---

## unique

Ensures duplicate values are not allowed.

```python
email = models.EmailField(unique=True)
```

Every student must have a unique email address.

---

## choices

Restricts values to predefined options.

```python
GENDER_CHOICES = [

    ("M", "Male"),

    ("F", "Female"),

    ("O", "Other"),
]

gender = models.CharField(

    max_length=1,

    choices=GENDER_CHOICES
)
```

Only the specified choices can be saved.

---

# 💻 Complete Example

```python
from django.db import models

class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    email = models.EmailField(unique=True)

    course = models.CharField(max_length=50)

    fees = models.DecimalField(max_digits=8, decimal_places=2)

    is_active = models.BooleanField(default=True)

    created_at = models.DateTimeField(auto_now_add=True)
```

---

# 🧠 Behind the Scenes

When Django sees

```python
email = models.EmailField(unique=True)
```

it generates SQL similar to

```sql
email VARCHAR(...) UNIQUE
```

The ORM converts Python field definitions into database columns automatically.

---

# 🛠 Mini Project

Create a **Student Registration Model** with the following fields:

- Name
- Roll Number
- Email
- Age
- Date of Birth
- Course
- Fees
- Profile Picture
- Active Status
- Created At

Run:

```bash
python manage.py makemigrations

python manage.py migrate
```

---

# ❌ Common Mistakes

### Using CharField without `max_length`

Wrong:

```python
name = models.CharField()
```

Correct:

```python
name = models.CharField(max_length=100)
```

---

### Using FloatField for Money

Avoid:

```python
price = models.FloatField()
```

Use:

```python
price = models.DecimalField(max_digits=10, decimal_places=2)
```

---

### Forgetting `upload_to` in ImageField

Always organize uploaded files into folders.

---

# 💡 Best Practices

- Use meaningful field names.
- Prefer `DecimalField` for currency.
- Use `EmailField` instead of `CharField` for emails.
- Use `choices` whenever the values are limited.
- Avoid unnecessary `null=True` on text fields.

---

# 📝 Exercises

### Exercise 1

Create a Teacher model using:

- Name
- Subject
- Experience
- Email

---

### Exercise 2

Create a Product model with:

- Name
- Price
- Description
- Available

---

### Exercise 3

Add a Gender field using `choices`.

---

# 🎤 Interview Questions

1. What is a Model Field?

2. Difference between CharField and TextField?

3. Difference between FloatField and DecimalField?

4. Difference between null and blank?

5. Why do we use choices?

6. What does unique=True do?

7. Why is max_length required in CharField?

---

# 📚 Official Documentation

Django Model Field Reference

https://docs.djangoproject.com/en/6.0/ref/models/fields/

Model Field Options

https://docs.djangoproject.com/en/6.0/topics/db/models/

---

# 📌 Summary

In this lesson, we explored Django Model Fields and learned how different field types represent different kinds of data. We also covered important field options such as `null`, `blank`, `default`, `choices`, and `unique`, which help control validation and database behavior.

Choosing the right field type is essential because it directly affects how your data is stored, validated, and queried.

---

# ➡️ Next Lesson

**Lesson 10 – Migrations**

In the next lesson, we'll learn how Django converts Models into actual database tables using migrations and understand what happens behind the scenes when we run `makemigrations` and `migrate`.