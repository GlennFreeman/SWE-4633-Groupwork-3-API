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

## Get Class
**Endpoint:** `/classes/{id}`\
**Method:** `GET`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

**Outputs** (`200`)

| Field | Type | Description |

|-------|------|-------------|

| id | integer | Class ID |

| name | string | Class name |

| students | array | Enrolled students, each with `id` (integer), `name` (string), `email` (string) |

| courses | array | Assigned courses, each with `id` (integer), `name` (string) |

**Example**
```
GET https://example.com/api/v1/classes/1
Authorization: Bearer eyJhbGciOi...
```
```json
{ "id": 1, "name": "MGT 7999 Fall 2026", "students": [{ "id": 1, "name": "Alice", "email": "alice@example.com" }], "courses": [{ "id": 2, "name": "Finance Basics" }] }
```

## Create Class
**Endpoint:** `/classes/create`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| name | body | string | Yes | Class name |

**Outputs** (`200`): the created Class.

**Example**
```
POST https://example.com/api/v1/classes/create
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "MGT 7999 Spring 2027" }
```

## Rename Class
**Endpoint:** `/classes/{id}/update`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

| name | body | string | Yes | New name |

**Outputs** (`200`): the updated Class.

**Example**
```
POST https://example.com/api/v1/classes/1/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "MGT 7999 Fall 2026 Section B" }
```

## Delete Class
**Endpoint:** `/classes/{id}/delete`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/classes/1/delete
Authorization: Bearer eyJhbGciOi...
```

## Add Student to Class
**Endpoint:** `/classes/{id}/add_student/{user_id}`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

| user_id | path | integer | Yes | Student's user ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/classes/1/add_student/3
Authorization: Bearer eyJhbGciOi...
```

## Remove Student from Class
**Endpoint:** `/classes/{id}/remove_student/{user_id}`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

| user_id | path | integer | Yes | Student's user ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/classes/1/remove_student/3
Authorization: Bearer eyJhbGciOi...
```

## Assign Course to Class
**Endpoint:** `/classes/{id}/add_course/{course_id}`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

| course_id | path | integer | Yes | Course ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/classes/1/add_course/2
Authorization: Bearer eyJhbGciOi...
```


## Unassign Course from Class
**Endpoint:** `/classes/{id}/remove_course/{course_id}`\
**Method:** `POST`

**Inputs**

| Name | Location | Type | Required | Description |

|------|----------|------|----------|-------------|

| id | path | integer | Yes | Class ID |

| course_id | path | integer | Yes | Course ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/classes/1/remove_course/2
Authorization: Bearer eyJhbGciOi...
```
