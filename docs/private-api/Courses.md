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
| scenario_ids | body | array of integers | No | IDs of scenarios to put in the course |

**Outputs** (`200`): the created Course, with its `scenarios` array.

**Example**
```
POST https://example.com/api/v1/courses/create
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "Finance Basics", "scenario_ids": [5, 6] }
```

## Update Course
**Endpoint:** `/courses/{id}/update`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Course ID |
| name | body | string | Yes | New name |
| scenario_ids | body | array of integers | No | IDs of the scenarios the course should contain. Replaces the current list. Leave it out to keep the current scenarios |

**Outputs** (`200`): the updated Course, with its `scenarios` array.

**Example**
```
POST https://example.com/api/v1/courses/2/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "Finance Fundamentals", "scenario_ids": [5, 7] }
```

## Delete Course
**Endpoint:** `/courses/{id}/delete`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Course ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/courses/2/delete
Authorization: Bearer eyJhbGciOi...
```

## Add Scenario to Course
**Endpoint:** `/courses/{id}/add_scenario/{scenario_id}`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Course ID |
| scenario_id | path | integer | Yes | Scenario ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/courses/2/add_scenario/5
Authorization: Bearer eyJhbGciOi...
```

## Remove Scenario from Course
**Endpoint:** `/courses/{id}/remove_scenario/{scenario_id}`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Course ID |
| scenario_id | path | integer | Yes | Scenario ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/courses/2/remove_scenario/5
Authorization: Bearer eyJhbGciOi...
```
