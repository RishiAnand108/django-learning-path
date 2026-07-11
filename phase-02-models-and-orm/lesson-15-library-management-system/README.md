# Lesson 15 – Student Management System (Phase 2 Project)

## 📖 Overview

Congratulations! 🎉

You have completed all the core concepts of Django Models and ORM.

Throughout this phase, you've learned:

- Creating Models
- Model Fields
- Migrations
- CRUD Operations
- QuerySets
- Model Relationships
- Model Methods
- Meta Options

Now it's time to combine everything into a single project.

In this lesson, we'll build a **Student Management System** that demonstrates how Django Models and the ORM work together in a real-world application.

Unlike previous lessons, this project focuses on applying everything you've learned rather than introducing new concepts.

---

# 🎯 Learning Objectives

By the end of this project, you will be able to:

- Design a normalized database.
- Create multiple related models.
- Apply migrations.
- Insert sample data.
- Perform CRUD operations.
- Query related data using the ORM.
- Configure model methods and Meta options.
- Build a scalable database structure.

---

# 🏗 Project Overview

The Student Management System will manage:

- Students
- Departments
- Courses

Each student belongs to one department.

Each student can enroll in multiple courses.

The project focuses only on the backend data layer.

No templates or forms are required at this stage.

---

# 📂 Project Structure

```
student_management/

├── manage.py

├── student_management/

│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py

└── students/

    ├── admin.py
    ├── apps.py
    ├── migrations/
    ├── models.py
    ├── tests.py
    └── views.py
```

---

# Database Design

```
Department

──────────────

id

name

        ▲

        │

        │ ForeignKey

        │

Student

──────────────

id

name

email

age

department

        │

        │ ManyToMany

        ▼

Course

──────────────

id

name
```

---

# Models Used

## Department

```python
class Department(models.Model):

    name = models.CharField(max_length=100)

    def __str__(self):

        return self.name
```

---

## Course

```python
class Course(models.Model):

    name = models.CharField(max_length=100)

    def __str__(self):

        return self.name
```

---

## Student

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    email = models.EmailField(unique=True)

    department = models.ForeignKey(

        Department,

        on_delete=models.CASCADE,

        related_name="students"
    )

    courses = models.ManyToManyField(

        Course,

        related_name="students"
    )

    def __str__(self):

        return self.name

    def is_adult(self):

        return self.age >= 18

    class Meta:

        ordering = ["name"]
```

---

# Apply Migrations

Generate migration files.

```bash
python manage.py makemigrations
```

Apply them.

```bash
python manage.py migrate
```

---

# Insert Sample Data

Create Departments.

```
Computer Science

Information Technology

Mechanical
```

Create Courses.

```
Python

Django

Machine Learning

Database Systems
```

Create Students.

```
Rahul

Priya

Amit

Sneha

Rohit
```

Assign

- Department
- Courses

to each student.

---

# CRUD Operations

## Create

Create new students.

---

## Read

Retrieve

- All students
- Students from one department
- Students enrolled in Python

---

## Update

Update

- Course
- Age
- Email

---

## Delete

Delete

- Student
- Course

---

# Query Examples

Retrieve all students.

```python
Student.objects.all()
```

Students older than 20.

```python
Student.objects.filter(age__gt=20)
```

Students in Computer Science.

```python
Student.objects.filter(

department__name="Computer Science"
)
```

Students enrolled in Django.

```python
Student.objects.filter(

courses__name="Django"
)
```

Sort by age.

```python
Student.objects.order_by("-age")
```

Count students.

```python
Student.objects.count()
```

---

# Expected Database Tables

```
students_department

students_course

students_student

students_student_courses
```

Notice that Django automatically creates the **junction table** (`students_student_courses`) for the ManyToMany relationship.

---

# Concepts Used

This project combines everything from Phase 2.

| Lesson | Concept |
|---------|---------|
| Lesson 08 | Models |
| Lesson 09 | Fields |
| Lesson 10 | Migrations |
| Lesson 11 | CRUD using ORM |
| Lesson 12 | QuerySets |
| Lesson 13 | Relationships |
| Lesson 14 | Model Methods & Meta |

---

# Mini Challenges

### Challenge 1

Add a Teacher model.

---

### Challenge 2

Assign teachers to departments.

---

### Challenge 3

Add a Fees field.

---

### Challenge 4

Find students enrolled in more than one course.

---

### Challenge 5

Count students in every department.

---

# Best Practices

✔ Use meaningful model names.

✔ Keep relationships normalized.

✔ Add `__str__()` to every model.

✔ Use `related_name` for reverse queries.

✔ Commit migration files to Git.

✔ Keep business logic inside models.

---

# Common Mistakes

❌ Forgetting migrations after modifying models.

❌ Using `get()` instead of `filter()`.

❌ Not defining `on_delete`.

❌ Forgetting `related_name`.

❌ Using `FloatField` for money.

---

# 📝 Exercises

1. Add a `Teacher` model and relate it to `Department`.
2. Add a `Date of Birth` field to `Student`.
3. Create five new students using the Django Shell.
4. Retrieve all students enrolled in "Machine Learning".
5. Display all students in alphabetical order.

---

# 🎤 Interview Questions

- Explain the database design of this project.
- Why is `ForeignKey` used for `Department`?
- Why is `ManyToManyField` used for `Course`?
- What happens when a department is deleted?
- How does Django create the intermediate table?
- Why is `related_name` useful?
- What is the benefit of Django ORM over raw SQL?

---

# 📚 Official Documentation

Models

https://docs.djangoproject.com/en/6.0/topics/db/models/

Making Queries

https://docs.djangoproject.com/en/6.0/topics/db/queries/

Relationships

https://docs.djangoproject.com/en/6.0/topics/db/examples/

---

# 📌 Summary

In this capstone project, we brought together everything learned in Phase 2 to design and build the backend of a Student Management System.

We created multiple models, established relationships, applied migrations, inserted sample data, performed CRUD operations, queried related records, and improved our models using custom methods and Meta options.

By completing this project, you now have a strong understanding of Django's data layer and are ready to move on to the next phase, where you'll learn how to present this data using Views, Templates, and Forms.

---

# 🧪 Phase 2 Checklist

- ✅ Created Models
- ✅ Used Different Field Types
- ✅ Applied Migrations
- ✅ Performed CRUD Operations
- ✅ Queried Data with ORM
- ✅ Implemented Relationships
- ✅ Added Model Methods
- ✅ Used Meta Options
- ✅ Built a Student Management Backend

---

# ➡️ Next Phase

## **Phase 3 – Views, Templates & Forms**

In the next phase, we'll learn how to display data from our database using Django Views and Templates, build forms for user input, validate submitted data, and create a complete web interface for the Student Management System.