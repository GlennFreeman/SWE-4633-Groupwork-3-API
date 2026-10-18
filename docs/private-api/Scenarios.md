---
title: Scenarios
nav_order: 1
parent: Private API
---

# Scenarios
A **Scenario** is a set of prompts (simulated emails). Each prompt has answers worth points. An answer points to the next prompt, or to nothing to end the scenario.

## Get All Scenarios
**Endpoint:** `/scenarios`\
**Method:** `GET`

**Inputs:** none.\
**Outputs** (`200`): array of scenarios, each with `id` (integer), `name` (string), `first_prompt_id` (integer or null).

**Example**
```
GET https://example.com/api/v1/scenarios
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "id": 5, "name": "Budget Crisis", "first_prompt_id": 11 },
  { "id": 6, "name": "Supplier Dispute", "first_prompt_id": 20 },
  ...
]
```

## Get Scenario
**Endpoint:** `/scenarios/{id}`\
**Method:** `GET`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Scenario ID |

**Outputs** (`200`)
| Field | Type | Description |
|-------|------|-------------|
| id | integer | Scenario ID |
| name | string | Scenario name |
| first_prompt_id | integer | Prompt shown first |
| prompts | array | All [Prompts](link_to_prompts_later) in the scenario, with the answer key |

**Example**
```
GET https://example.com/api/v1/scenarios/5
Authorization: Bearer eyJhbGciOi...
```
```json
{ "id": 5, "name": "Budget Crisis", "first_prompt_id": 11, "prompts": [{ "id": 11, "value": { "from": "CEO", "subject": "Welcome", "body": "..." }, "answers": [{ "id": 30, "value": { "text": "Acknowledge" }, "points": 3, "next_prompt_id": null }] }] }
```

## Create Scenario
**Endpoint:** `/scenarios/create`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| name | body | string | Yes | Scenario name |

**Outputs** (`200`): the created scenario (`id`, `name`, `first_prompt_id` null until set).

**Example**
```
POST https://example.com/api/v1/scenarios/create
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "Budget Crisis" }
```
