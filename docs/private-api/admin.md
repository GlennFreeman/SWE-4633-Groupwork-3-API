---
title: Admin
nav_order: 8
parent: Private API
---
## Admin API
### Register new user
Creates a new user\
**Endpoint:** `POST /admin/register_new_user`\
**Authentication:** Required\
**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|----------|-------------|
| email | string | Yes | - | Email of new user, required to log in |
| name | string | Yes | - | Name of new user, preferably formatted "last, first" |
| password | string | No | 1234 | Default password for new user, encouraged to change later |
| role | integer | No | 0 | Role of new user, see roles table in DB for valid values |
### Response:
```json
{
 "sucessful": true
 "message": "no errors"
}
```

### Update user
Updates a user's information\
**Endpoint:** `POST /admin/update_user`\
**Authentication:** Required\
**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|----------|-------------|
| user_email | string | Yes | - | Email of user to be updated |
| new_email | string | No | - | If included overwrites specified user's email |
| new_name | string | No | - | If included overwrites specified user's name |
| new_password | string | No | - | If included overwrites specified user's password |
| new_role | integer | No | - | If included overwrites specified user's role, see roles table in DB for valid values |
### Response:
```json
{
 "sucessful": true
 "message": "no errors"
}
```

### Delete user
Deletes a user\
**Endpoint:** `POST /admin/delete_user`\
**Authentication:** Required\
**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|----------|-------------|
| email | string | Yes | - | Email of user to be deleted |
| password | string | Yes | - | Password of admin currently logged in, included for security purposes |
### Response:
```json
{
 "sucessful": true
 "message": "no errors"
}
```
