## Student API

### Student Login
Verify a student's email and password.
**Endpoint:** `/students/login`
**Method:** `POST`
**Authentication:** Not required before login
**Request Body:** JSON
| Parameter | Type    | Required | Description |
|-----------|---------|----------|-------------|
| email     | integer |   Yes    | Email address associated with the student's account. |
|Password   | string  |   Yes    | Password for the student's account. |

**Example Request Body:**

```json
{
  "email": "student@example.com",
  "password": "ExamplePassword123!"
}
```
**Output Fields:**
| Parameter | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the student's email and password were wrified successfully. |

**Example Successful Response:**

```json
{
  "success": true
}
```

**Example Usage:**

```http
POST /students/login HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "email": "student@example.com"
  "password": "ExamplePassword123!"
}
```

`https://api.example.com` is a placeholder for the deployed API's base URL.
