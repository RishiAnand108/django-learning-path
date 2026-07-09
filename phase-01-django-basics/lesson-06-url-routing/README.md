# Lesson 06 — URL Routing

## Learning Objectives

Learn how Django maps URLs to views.

---

# What is URL Routing?

A URL tells Django which view should handle a request.

---

Topics

path()

include()

URL converters

Dynamic URLs

Named URLs

Reverse URL

---

# Practical

Create

/

about/

contact/

student/1

---

Explain

```python
path("student/<int:id>/", student)
```

Explain converters.

---

# Common Mistakes

Missing trailing slash.

Wrong include().

Incorrect URL names.

---

# Interview Questions

Difference between path() and include()?

Dynamic URLs?