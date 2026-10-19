## User Mangagement API

### Create New User Account

Create a new account and fill personal info fields.

**Endpoint:** `/user_management/create_account`

**Method:** `POST`

**Authentication:** Required

**Request Body:** JSON

| Field | Type    | Required | Description |
|-----------|---------|----------|-------------|
| name     | string |   Yes    | Name of the account. |
| email     | string |   Yes    | Email address associated with the account. |
|password   | string  |   Yes    | Password of the account. |
| role     | int |   Yes    | Role associated with the account. |

**Example Request Body:**

```json
{
    "name": "jdoe134",
    "email": "jdoe1337@gmail.com",
    "password": "123",
    "role": 1
}
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the account's information was valid and an account was created or not. |

**Example Output Body:**

```json
{
    "success": true
}
```

### Get User Information

Create a new account and fill personal info fields.

**Endpoint:** `/user_management/get_account_info`

**Method:** `GET`

**Authentication:** Required

**Request Body:** JSON

| Field | Type | Description |
|-----------|------|-------------|
| email   | string | Email address of the account to retrieve. |

**Example Request Body:**

```http
GET /user_management/get_account_info?email=jdoe1337%40gmail.com
```

**Output Fields:**


| Field | Type    | Description |
|-----------|---------|-------------|
| success     | boolean | Indicates whether the account information was successfully retrieved. |
| name     | string | Name of the account. |
| email     | string | Email address associated with the account. |
| role     | int | Role associated with the account. |

**Example Output Body:**

```json
{
    "success": true
    "name": "jdoe134",
    "email": "jdoe1337@gmail.com",
    "role": 1
}
```

### Update User Account Information

Updates one or more fields for an existing user account. Only fields included in the request body are changed.

**Endpoint:** `/user_management/update_account`

**Method:** `PATCH`

**Authentication:** Required

**Query Parameters:**

| Field | Type | Required | Description |
|---|---|---|---|
| email | string | Yes | Email address associated with the account to update. |

**Request Body:** JSON

| Field | Type | Required | Description |
|---|---|---|---|
| name | string | No | New name for the account. |
| email | string | No | New email address for the account. |
| role | integer | No | New account role; changes must be limited to authorized users. |

At least one editable field must be required.

**Example Request:**

```http
PATCH /user_management/update_account?email=jdoe1337%40gmail.com
Content-Type: application/json
```

**Example Request Body:**

```json
{
  "name": "jdoe135",
  "email": "jdoe135@gmail.com"
}
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Indicates whether the account was successfully updated. |

**Example Output Body:**

```json
{
    "success": true
}
```

### Delete User Account

Deletes the user account associated with the specified email address. This action should be restricted to the account owner or an administrator.

**Endpoint:** `/users/delete_account`

**Method:** `Delete`

**Authentication:** Required

**Query Parameters:**

| Field | Type | Required | Description |
|---|---|---|---|
| email | string | Yes | Email address associated with the account to delete. |

**Example Request:**

```http
DELETE /user_management/delete_account?email=jdoe1337%40gmail.com
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Indicates whether the account was successfully deleted. |

**Example Output Body:**

```json
{
    "success": true
}
```
