---
title: Courses
nav_order: 4
parent: Private API
---

# Courses
A **Course** has `id` (integer) and `name` (string), and groups scenarios. A course is given to students by assigning it to a class.

## Get All Courses
**Endpoint:** `/courses`\
**Method:** `GET`

**Inputs:** none.\
**Outputs** (`200`): array of Courses, each with `id` (integer) and `name` (string).

**Example**
```
GET https://example.com/api/v1/courses
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "id": 2, "name": "Finance Basics" },
  { "id": 3, "name": "Operations" },
  ...
]
```
