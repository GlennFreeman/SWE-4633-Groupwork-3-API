## Users API
### Get All Users
Retrieve a paginated list of all users.\
**Endpoint:** `GET /users`\
**Authentication:** Required\
**Query Parameters:**

| Parameter | Type | Required | Default | Description |

|-----------|------|----------|----------|-------------|

| page | integer | No | 1 | Page number |

| limit | integer | No | 10 | Items per page (1-100) |

| sort | string | No | createdAt | Sort field |

| order | string | No | desc | Sort order (asc|desc) |

| search | string | No | - | Search term (name or email) |
### Response:
```json
{
 "data": [
   {
     "id": 1,
     "name": "Alice",
     "email": "alice@example.com",
     "role": "user",
     "createdAt": "2026-03-07T12:00:00Z",
     "updatedAt": "2026-03-07T12:00:00Z"
   },
   {
     "id": 2,
     "name": "Bob",
     "email": "bob@example.com",
     "role": "admin",
     "createdAt": "2026-03-06T12:00:00Z",
     "updatedAt": "2026-03-06T12:00:00Z"
   }
 ],
 "meta": {
   "page": 1,
   "limit": 10,
   "total": 100,
   "totalPages": 10
 }
}
```

# Markdown View
```markdown
## Users API
### Get All Users
Retrieve a paginated list of all users.\
**Endpoint:** `GET /users`\
**Authentication:** Required\
**Query Parameters:**

| Parameter | Type | Required | Default | Description |

|-----------|------|----------|----------|-------------|

| page | integer | No | 1 | Page number |

| limit | integer | No | 10 | Items per page (1-100) |

| sort | string | No | createdAt | Sort field |

| order | string | No | desc | Sort order (asc|desc) |

| search | string | No | - | Search term (name or email) |
### Response:
```json
{
 "data": [
   {
     "id": 1,
     "name": "Alice",
     "email": "alice@example.com",
     "role": "user",
     "createdAt": "2026-03-07T12:00:00Z",
     "updatedAt": "2026-03-07T12:00:00Z"
   },
   {
     "id": 2,
     "name": "Bob",
     "email": "bob@example.com",
     "role": "admin",
     "createdAt": "2026-03-06T12:00:00Z",
     "updatedAt": "2026-03-06T12:00:00Z"
   }
 ],
 "meta": {
   "page": 1,
   "limit": 10,
   "total": 100,
   "totalPages": 10
 }
}
```
