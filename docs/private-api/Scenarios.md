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
