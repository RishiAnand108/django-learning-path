# Phase 2 – Django Models & ORM

Welcome to **Phase 2** of the Django Learning Path!

In Phase 1, we learned how to create a Django project, configure applications, define URLs, and render templates. However, our application couldn't store data permanently.

In this phase, we'll explore **Django Models and the Object Relational Mapper (ORM)**—the core components responsible for storing, retrieving, updating, and managing data in a database.

By the end of this phase, you'll be able to design database models, perform CRUD operations, create relationships between models, and build a complete backend for a Student Management System.

---

# 🎯 Learning Objectives

After completing this phase, you will be able to:

- Understand Django Models and their purpose.
- Work with different Django Model Fields.
- Create and apply database migrations.
- Perform CRUD operations using Django ORM.
- Write efficient database queries.
- Understand QuerySets and QuerySet methods.
- Build relationships between models.
- Use model methods and Meta options.
- Design a normalized database.
- Build a complete backend using Django Models.

---

# 📚 Lessons Covered

| Lesson | Topic | Description |
|----------|---------------------------|------------------------------------------------|
| 08 | Django Models | Learn how Django Models represent database tables. |
| 09 | Django Model Fields | Explore different field types and field options. |
| 10 | Django Migrations | Understand migrations and database schema management. |
| 11 | Django ORM Basics | Perform Create, Read, Update and Delete operations. |
| 12 | Querying Data | Learn filtering, ordering, aggregation, QuerySets and advanced ORM queries. |
| 13 | Model Relationships | Understand ForeignKey, OneToOneField and ManyToManyField. |
| 14 | Model Methods & Meta | Customize model behavior using methods and Meta options. |
| 15 | Student Management System | Build a complete backend using everything learned in this phase. |

---

# 🏗 Phase Project

At the end of this phase, you'll build a **Student Management System Backend**.

The project demonstrates:

- Multiple Models
- Model Relationships
- CRUD Operations
- QuerySets
- Migrations
- Model Methods
- Meta Options
- Database Design Best Practices

This project serves as the foundation for the next phase, where you'll build the frontend using Views, Templates, and Forms.

---

# 📂 Folder Structure

```text
phase-02-models-and-orm/
│
├── README.md
│
├── lesson-08-models/
│   └── README.md
│
├── lesson-09-fields/
│   └── README.md
│
├── lesson-10-migrations/
│   └── README.md
│
├── lesson-11-orm-basics/
│   └── README.md
│
├── lesson-12-querying-data/
│   └── README.md
│
├── lesson-13-model-relationships/
│   └── README.md
│
├── lesson-14-model-methods-meta/
│   └── README.md
│
└── lesson-15-student-management-system/
    └── README.md
```

---

# 📖 Prerequisites

Before starting this phase, you should be comfortable with:

- Django Project Structure
- Django Apps
- MTV Architecture
- `manage.py`
- `settings.py`
- URL Routing
- Basic Django Views
- Templates

If you haven't completed these topics, it's recommended to finish **Phase 1 – Django Basics** first.

---

# 🧠 Skills You'll Gain

By the end of this phase, you'll be able to:

- Design relational databases using Django Models.
- Create reusable and maintainable models.
- Manage database schema using migrations.
- Perform CRUD operations with Django ORM.
- Write efficient and readable database queries.
- Build relationships between multiple models.
- Organize business logic using model methods.
- Configure model behavior with the Meta class.

These are essential skills required to build production-ready Django applications.

---

# 💡 Best Practices

- Use meaningful model and field names.
- Keep models focused on a single responsibility.
- Always create and apply migrations after model changes.
- Use the appropriate relationship type (`ForeignKey`, `OneToOneField`, or `ManyToManyField`).
- Add `__str__()` to every model.
- Keep business logic inside models whenever appropriate.
- Use Django ORM instead of writing raw SQL unless necessary.

---

# 📚 Official Django Documentation

- **Models:** https://docs.djangoproject.com/en/6.0/topics/db/models/
- **Model Fields:** https://docs.djangoproject.com/en/6.0/ref/models/fields/
- **Making Queries:** https://docs.djangoproject.com/en/6.0/topics/db/queries/
- **Relationships:** https://docs.djangoproject.com/en/6.0/topics/db/examples/
- **Migrations:** https://docs.djangoproject.com/en/6.0/topics/migrations/

---

# 📝 Phase Checklist

Complete each lesson before moving to the next.

- [ ] Lesson 08 – Django Models
- [ ] Lesson 09 – Django Model Fields
- [ ] Lesson 10 – Django Migrations
- [ ] Lesson 11 – Django ORM Basics
- [ ] Lesson 12 – Querying Data
- [ ] Lesson 13 – Model Relationships
- [ ] Lesson 14 – Model Methods & Meta
- [ ] Lesson 15 – Student Management System

---

# 🚀 What's Next?

After completing this phase, you'll move on to **Phase 3 – Views, Templates & Forms**, where you'll learn how to display and interact with the data you've created in this phase.

You'll cover:

- Function-Based Views
- Class-Based Views
- Django Templates
- Template Inheritance
- Forms & ModelForms
- Form Validation
- Static Files
- Building dynamic web pages

By the end of Phase 3, your Student Management System will evolve from a backend-only application into a fully functional web application.

---

Happy Learning! 🚀