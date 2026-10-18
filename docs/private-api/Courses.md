---
title: Courses
nav_order: 2
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

## Get Course
**Endpoint:** `/courses/{id}`\
**Method:** `GET`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Course ID |

**Outputs** (`200`)
| Field | Type | Description |
|-------|------|-------------|
| id | integer | Course ID |
| name | string | Course name |
| scenarios | array | Scenarios in the course, each with `id` (integer), `name` (string) |

**Example**
```
GET https://example.com/api/v1/courses/2
Authorization: Bearer eyJhbGciOi...
```
```json
{
  "id": 2,
  "name": "Finance Basics",
  "scenarios": [
    { "id": 5, "name": "Budget Crisis" },
    { "id": 6, "name": "Supplier Dispute" },
    ...
  ]
}
```

## Create Course
**Endpoint:** `/courses/create`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| name | body | string | Yes | Course name |

**Outputs** (`200`): the created Course.

**Example**
```
POST https://example.com/api/v1/courses/create
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "Finance Basics" }
```
