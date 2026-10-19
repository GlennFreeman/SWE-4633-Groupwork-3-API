---
title: Users
nav_order: 2
parent: Private API
---

# Users
Admin only. A **User** has `id` (integer), `name` (string), `email` (string), `role` (string: `student`, `instructor` or `admin`). The password is hashed on the server and never returned.

## Get All Users
**Endpoint:** `/users`\
**Method:** `GET`

**Inputs:** none.\
**Outputs** (`200`): array of Users.

**Example**
```
GET https://example.com/api/v1/users
Authorization: Bearer eyJhbGciOi...
```
```json
[
  { "id": 1, "name": "Alice", "email": "alice@example.com", "role": "student" },
  { "id": 2, "name": "Bob", "email": "bob@example.com", "role": "instructor" },
  ...
]
```

## Create User
**Endpoint:** `/users/create`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| name | body | string | Yes | Display name |
| email | body | string | Yes | Must be unique, else `400` |
| password | body | string | Yes | Initial password |
| role | body | string | Yes | `student`, `instructor` or `admin` |

**Outputs** (`200`): the created User.

**Example**
```
POST https://example.com/api/v1/users/create
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "name": "Bob", "email": "bob@example.com", "password": "secret", "role": "instructor" }
```

## Update User
**Endpoint:** `/users/{id}/update`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | User ID |
| name | body | string | No | New name |
| email | body | string | No | New email |
| password | body | string | No | New password |
| role | body | string | No | New role |

**Outputs** (`200`): the updated User.

**Example**
```
POST https://example.com/api/v1/users/2/update
Authorization: Bearer eyJhbGciOi...
Content-Type: application/json

{ "role": "admin" }
```

## Delete User
**Endpoint:** `/users/{id}/delete`\
**Method:** `POST`

**Inputs**
| Name | Location | Type | Required | Description |
|------|----------|------|----------|-------------|
| id | path | integer | Yes | User ID |

**Outputs:** none (`200`).

**Example**
```
POST https://example.com/api/v1/users/2/delete
Authorization: Bearer eyJhbGciOi...
```
