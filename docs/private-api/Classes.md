---
title: Classes
nav_order: 3
parent: Private API
---

# Classes
A **Class** has `id` (integer) and `name` (string). Students are enrolled in a class, and courses are assigned to a class. Students see the scenarios of the courses assigned to their classes.

## Get All Classes
**Endpoint:** `/classes`\
**Method:** `GET`

**Inputs:** none.\
**Outputs** (`200`): array of Classes.

**Example**
```
GET https://example.com/api/v1/classes
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "id": 1, "name": "MGT 7999 Fall 2026" },
  { "id": 2, "name": "MGT 7999 Spring 2027" },
  ...
]
```
