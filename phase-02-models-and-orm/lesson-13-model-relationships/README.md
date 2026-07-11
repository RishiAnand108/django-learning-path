# Lesson 13 – Django Model Relationships

## 📖 Overview

In the previous lessons, we learned how to create models, define fields, and perform CRUD operations using Django ORM. However, real-world applications rarely consist of a single table.

For example:

- A Student belongs to a Department.
- A Student can enroll in multiple Courses.
- Every Student has one Profile.

To represent these real-world connections, Django provides **Model Relationships**.

Relationships allow multiple models to work together while keeping the database organized and avoiding duplicate data.

In this lesson, we'll learn the three types of relationships supported by Django:

- ForeignKey
- OneToOneField
- ManyToManyField

---

# 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Understand why relationships are required.
- Learn the three types of model relationships.
- Create One-to-Many relationships.
- Create One-to-One relationships.
- Create Many-to-Many relationships.
- Query related objects using Django ORM.
- Understand the `on_delete` parameter.
- Use `related_name` for reverse relationships.

---

# 🤔 Why Do We Need Relationships?

Imagine storing student information like this:

| Student | Department |
|----------|------------|
| Rahul | Computer Science |
| Priya | Computer Science |
| Amit | Mechanical |

If thousands of students belong to the same department, storing the department name repeatedly wastes storage and makes updates difficult.

Instead, we create separate tables.

Department Table

| ID | Name |
|----|------|
|1|Computer Science|
|2|Mechanical|

Student Table

|ID|Name|Department|
|--|----|----------|
|1|Rahul|1|
|2|Priya|1|
|3|Amit|2|

This is called a **relationship**.

---

# 🌍 Real-World Analogy

Imagine a college.

A college has

- Departments
- Students
- Courses
- Teachers

Everything is connected.

Students belong to departments.

Teachers teach courses.

Students enroll in multiple courses.

Instead of storing everything inside one table, we connect different tables using relationships.

---

# Types of Relationships

Django supports three relationship fields.

1. ForeignKey (One-to-Many)
2. OneToOneField (One-to-One)
3. ManyToManyField (Many-to-Many)

---

# 1️⃣ ForeignKey (One-to-Many)

A ForeignKey represents a **One-to-Many** relationship.

One department can have many students.

One student belongs to only one department.

```
Department

↓

Student

↓

Student

↓

Student
```

Example

```python
from django.db import models

class Department(models.Model):

    name = models.CharField(max_length=100)


class Student(models.Model):

    name = models.CharField(max_length=100)

    department = models.ForeignKey(

        Department,

        on_delete=models.CASCADE
    )
```

---

## Understanding `on_delete`

The `on_delete` argument tells Django what should happen to related records when the parent object is deleted.

Example:

If the Computer Science department is deleted,

what should happen to its students?

Django provides several options.

### CASCADE

```python
on_delete=models.CASCADE
```

Deleting the department also deletes all related students.

---

### PROTECT

```python
on_delete=models.PROTECT
```

Prevents deletion if related students exist.

---

### SET_NULL

```python
department = models.ForeignKey(

Department,

null=True,

on_delete=models.SET_NULL
)
```

If the department is deleted,

the student's department becomes NULL.

---

### SET_DEFAULT

Assigns a default value.

---

### DO_NOTHING

Performs no action.

Use carefully.

---

# Query Example

Retrieve all students from a department.

```python
department = Department.objects.get(id=1)

department.student_set.all()
```

---

# 2️⃣ OneToOneField (One-to-One)

A OneToOne relationship means

one object is connected to exactly one other object.

Example

Every student has one profile.

Every profile belongs to one student.

```
Student

↓

Student Profile
```

Example

```python
class Student(models.Model):

    name = models.CharField(max_length=100)


class StudentProfile(models.Model):

    student = models.OneToOneField(

        Student,

        on_delete=models.CASCADE
    )

    address = models.TextField()

    phone = models.CharField(max_length=15)
```

Retrieve profile

```python
student.profile
```

---

# 3️⃣ ManyToManyField (Many-to-Many)

A ManyToMany relationship means

many students

can enroll in

many courses.

```
Student

↓

Course

↓

Student

↓

Course
```

Example

```python
class Course(models.Model):

    name = models.CharField(max_length=100)


class Student(models.Model):

    name = models.CharField(max_length=100)

    courses = models.ManyToManyField(Course)
```

Now

Rahul

can enroll in

Python

Django

Machine Learning

Similarly,

Python

can have

Rahul

Priya

Amit

---

# Behind the Scenes

When using ManyToManyField,

Django automatically creates an intermediate table.

Example

```
Student

Course

Student_Course
```

The junction table stores

Student ID

Course ID

You don't need to create it manually.

---

# `related_name`

Instead of using

```python
department.student_set.all()
```

you can define

```python
department = models.ForeignKey(

Department,

on_delete=models.CASCADE,

related_name="students"
)
```

Now

```python
department.students.all()
```

This makes the code more readable.

---

# Mini Project

Create three models.

Department

```python
name
```

Course

```python
name
```

Student

```python
name

email

department

courses
```

Run migrations.

Insert sample data.

Retrieve:

- All students
- Students of one department
- Courses of one student

---

# Relationship Summary

| Relationship | Field |
|--------------|-------|
| One-to-Many | ForeignKey |
| One-to-One | OneToOneField |
| Many-to-Many | ManyToManyField |

---

# ❌ Common Mistakes

### Forgetting `on_delete`

`ForeignKey` requires the `on_delete` argument.

---

### Using ForeignKey instead of ManyToMany

One student can study multiple courses.

Use

```python
ManyToManyField
```

instead of

```python
ForeignKey
```

---

### Forgetting Migrations

Whenever relationships are added,

run

```bash
python manage.py makemigrations

python manage.py migrate
```

---

# 💡 Best Practices

✔ Use `ForeignKey` for parent-child relationships.

✔ Use `OneToOneField` for extending models.

✔ Use `ManyToManyField` when both models can have multiple related records.

✔ Always choose the correct `on_delete` behavior.

✔ Use `related_name` for cleaner reverse queries.

---

# 📝 Exercises

## Exercise 1

Create

Department

and

Student

using ForeignKey.

---

## Exercise 2

Create

StudentProfile

using OneToOneField.

---

## Exercise 3

Create

Course

using ManyToManyField.

---

## Exercise 4

Retrieve all students from the Computer Science department.

---

## Exercise 5

Retrieve all courses enrolled by Rahul.

---

# 🎤 Interview Questions

### What is a ForeignKey?

---

### Difference between

ForeignKey

and

ManyToManyField?

---

### What is OneToOneField?

---

### What does `on_delete=models.CASCADE` do?

---

### What is `related_name`?

---

### When should you use ManyToManyField?

---

# 📚 Official Documentation

Model Relationships

https://docs.djangoproject.com/en/6.0/topics/db/examples/many_to_one/

ForeignKey

https://docs.djangoproject.com/en/6.0/ref/models/fields/#foreignkey

OneToOneField

https://docs.djangoproject.com/en/6.0/ref/models/fields/#onetoonefield

ManyToManyField

https://docs.djangoproject.com/en/6.0/topics/db/examples/many_to_many/

---

# 📌 Summary

In this lesson, we learned how Django models relate to one another using **ForeignKey**, **OneToOneField**, and **ManyToManyField**. We explored when to use each relationship type, how Django manages related data, the importance of the `on_delete` parameter, and how `related_name` makes reverse lookups more readable.

Understanding model relationships is essential for designing normalized databases and building scalable Django applications.

---

# 🧪 Quick Recap

✅ I understand One-to-One relationships.

✅ I understand One-to-Many relationships.

✅ I understand Many-to-Many relationships.

✅ I know how `ForeignKey` works.

✅ I understand the purpose of `on_delete`.

✅ I know when to use `related_name`.

---

# ➡️ Next Lesson

**Lesson 14 – Model Methods & Meta Options**

In the next lesson, we'll learn how to customize Django models using methods like `__str__()`, define custom model methods, and configure model behavior with the `Meta` class.