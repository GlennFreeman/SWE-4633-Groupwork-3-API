---
title: Private API
nav_order: 3
has_children: true
---

# Example CMS Private API

Internal services used by the faculty CMS. These are not meant to be called by outside clients. See [Why These Are Private](justification.html).

**Base URL:** `https://example.com/api/v1`\
**Format:** JSON over HTTPS. Send `Content-Type: application/json` on requests with a body.\
**Methods:** `GET` reads data. `POST` changes data (create, update, delete, login). The action is named in the path, for example `/users/{id}/delete`.\
**Authentication:** Every endpoint needs the header `Authorization: Bearer <token>` (string, from `POST /auth/login` in the public API). The token's role must be `instructor` or `admin`. Users endpoints are `admin` only. Students get `403`.

## Errors
Errors return `{ "error": "message" }` (string) with a status code.

| Status | Meaning |

|--------|---------|

| 400 | Missing or invalid input |

| 401 | Missing or invalid token |

| 403 | Role not allowed |

| 404 | Not found |

## Shared objects
**Prompt** (instructor view, includes the answer key)

| Field | Type | Description |

|-------|------|-------------|

| id | integer | Prompt ID |

| value | object | The email: `from` (string), `subject` (string), `body` (string) |

| answers | array | Each has `id` (integer), `value` (object, `text` string), `points` (integer), `next_prompt_id` (integer or null; null ends the scenario) |

A scenario with one path through its prompts is linear. Answers pointing to different prompts make it branching.

## Endpoints

| Page | Endpoints |

|------|-----------|

| [Users](users.html) | `/users` list, create, update, delete (admin only) |

| [Classes](classes.html) | `/classes` list, get, create, update, delete, students and courses in a class |

| [Courses](courses.html) | `/courses` list, create, update, delete, scenarios in a course |

| [Scenarios](scenarios.html) | `/scenarios` list, get, create, update, delete, plus `/prompts` and `/answers` |

| [Results](results.html) | `/scenarios/{id}/attempts`, `/users/{id}/attempts`, `/attempts/{id}` |

| [Why These Are Private](justification.html) | Justification |
