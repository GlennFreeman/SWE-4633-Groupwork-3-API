---
title: Public API
nav_order: 2
has_children: true
---

# Example Student Client Public API

Services for the student-facing client. Anyone can build a client against these. Faculty and admin services are in the separate private API.

**Base URL:** `https://example.com/api/v1`\
**Format:** JSON over HTTPS. Send `Content-Type: application/json` on requests with a body.\
**Methods:** `GET` reads data. `POST` changes data (create, update, delete, login). The action is named in the path, for example `/me/scenarios/{scenario_id}/start_attempt`.\
**Authentication:** Every endpoint except login needs the header `Authorization: Bearer <token>` (string, the token returned by login). Students can only read and change their own data.

## Errors
Errors return `{ "error": "message" }` (string) with a status code.

| Status | Meaning |

|--------|---------|

| 400 | Missing or invalid input |

| 401 | Missing, invalid or wrong credentials |

| 403 | Not allowed (e.g. scenario not assigned to you) |

| 404 | Not found |

## Shared object: Prompt
A prompt is one simulated email plus the replies the student can choose from. Answer points and next-prompt links are never included.

| Field | Type | Description |

|-------|------|-------------|

| id | integer | Prompt ID |

| value | object | The email: `from` (string), `subject` (string), `body` (string) |

| answers | array | Reply options. Each has `id` (integer) and `value` (object with `text` string) |

## Endpoints

| Page | Endpoints |

|------|-----------|

| [Auth](auth.html) | `POST /auth/login` |

| [Scenarios](scenarios.html) | `GET /me/scenarios` |

| [Attempts](attempts.html) | `POST /me/scenarios/{scenario_id}/start_attempt`, `POST /me/attempts/{attempt_id}/submit_answer`, `GET /me/attempts` |
