---
title: Results
nav_order: 6
parent: Private API
---

# Results
Read-only views of student attempts. A student can attempt a scenario many times, and every attempt is listed.

## Get Scenario Attempts
**Endpoint:** `/scenarios/{id}/attempts`\
**Method:** `GET`

Every student's attempts for one scenario.

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Scenario ID |

**Outputs** (`200`): array of attempts
| Field | Type | Description |
|-------|------|-------------|
| attempt_id | integer | Attempt ID |
| user_id | integer | Student's user ID |
| user_name | string | Student's name |
| scenario_id | integer | Scenario ID |
| scenario_name | string | Scenario name |
| total_points | integer | Score for the attempt |
| finished_at | string | When it finished (ISO 8601 datetime) |

**Example**
```
GET https://example.com/api/v1/scenarios/5/attempts
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "attempt_id": 40, "user_id": 1, "user_name": "Alice", "scenario_id": 5, "scenario_name": "Budget Crisis", "total_points": 8, "finished_at": "2026-03-07T12:20:00Z" },
  { "attempt_id": 43, "user_id": 2, "user_name": "Bob", "scenario_id": 5, "scenario_name": "Budget Crisis", "total_points": 5, "finished_at": "2026-03-07T14:05:00Z" },
  ...
]
```

## Get Student Attempts
**Endpoint:** `/users/{id}/attempts`\
**Method:** `GET`

Every attempt by one student, across scenarios.

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Student's user ID |

**Outputs** (`200`): array of attempts, same fields as Get Scenario Attempts.

**Example**
```
GET https://example.com/api/v1/users/1/attempts
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "attempt_id": 40, "user_id": 1, "user_name": "Alice", "scenario_id": 5, "scenario_name": "Budget Crisis", "total_points": 8, "finished_at": "2026-03-07T12:20:00Z" },
  { "attempt_id": 41, "user_id": 1, "user_name": "Alice", "scenario_id": 6, "scenario_name": "Supplier Dispute", "total_points": 6, "finished_at": "2026-03-08T09:45:00Z" },
  ...
]
```

## Get Attempt
**Endpoint:** `/attempts/{id}`\
**Method:** `GET`

One attempt with each answer the student chose and its points.

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Attempt ID |

**Outputs** (`200`)
| Field | Type | Description |
|-------|------|-------------|
| attempt_id | integer | Attempt ID |
| user_id | integer | Student's user ID |
| scenario_id | integer | Scenario ID |
| total_points | integer | Score for the attempt |
| answers | array | Each has `prompt_id` (integer), `answer_id` (integer), `answer_value` (object, `text` string), `points` (integer) |

**Example**
```
GET https://example.com/api/v1/attempts/40
Authorization: Bearer eyJhbGciOi...
```
```json
{ "attempt_id": 40, "user_id": 1, "scenario_id": 5, "total_points": 8, "answers": [{ "prompt_id": 11, "answer_id": 30, "answer_value": { "text": "Acknowledge" }, "points": 3 }, { "prompt_id": 12, "answer_id": 31, "answer_value": { "text": "Reply with a cost plan" }, "points": 5 }] }
```
