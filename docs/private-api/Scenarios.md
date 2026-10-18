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
| prompts | array | All [Prompts](index.html#shared-objects) in the scenario, with the answer key |

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

## Update Scenario
**Endpoint:** `/scenarios/{id}/update`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Scenario ID |
| name | body | string | No | New name |
| first_prompt_id | body | integer | No | Prompt to show first |

**Outputs** (`200`): the updated scenario.

**Example**
```
POST https://example.com/api/v1/scenarios/5/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "first_prompt_id": 11 }
```

## Add Prompt
**Endpoint:** `/scenarios/{id}/add_prompt`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Scenario ID |
| value | body | object | Yes | The email: `from` (string), `subject` (string), `body` (string) |

**Outputs** (`200`): the created [Prompt](index.html#shared-objects) with an empty `answers` array.

**Example**
```
POST https://example.com/api/v1/scenarios/5/add_prompt
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "value": { "from": "CFO", "subject": "Budget cut", "body": "We need to cut 10%." } }
```

## Update Prompt
**Endpoint:** `/prompts/{id}/update`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Prompt ID |
| value | body | object | Yes | New email content |

**Outputs** (`200`): the updated Prompt.

**Example**
```
POST https://example.com/api/v1/prompts/12/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "value": { "from": "CFO", "subject": "Budget cut", "body": "Cut 15% instead." } }
```

## Delete Prompt
**Endpoint:** `/prompts/{id}/delete`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Prompt ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/prompts/12/delete
Authorization: Bearer eyJhbGciOi...
```

## Add Answer
**Endpoint:** `/prompts/{id}/add_answer`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Prompt ID the answer belongs to |
| value | body | object | Yes | Answer text: `text` (string) |
| points | body | integer | Yes | Points awarded for choosing this answer |
| next_prompt_id | body | integer | No | Prompt to show next. Omit to end the scenario |

**Outputs** (`200`): the created answer with `id` (integer), `value` (object), `points` (integer), `next_prompt_id` (integer or null).

**Example**
```
POST https://example.com/api/v1/prompts/11/add_answer
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "value": { "text": "Acknowledge" }, "points": 3, "next_prompt_id": 12 }
```

## Update Answer
**Endpoint:** `/answers/{id}/update`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Answer ID |
| value | body | object | No | New answer text |
| points | body | integer | No | New points |
| next_prompt_id | body | integer | No | New next prompt (`null` to end the scenario) |

**Outputs** (`200`): the updated answer.

**Example**
```
POST https://example.com/api/v1/answers/30/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "points": 5 }
```

## Delete Answer
**Endpoint:** `/answers/{id}/delete`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | Answer ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/answers/30/delete
Authorization: Bearer eyJhbGciOi...
```
