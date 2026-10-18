## Student API

### Student Login
Verify a student's email and password.

**Endpoint:** `/students/login`

**Method:** `POST`

**Authentication:** Not required before login

**Request Body:** JSON

| Field | Type    | Required | Description |
|-----------|---------|----------|-------------|
| email     | string |   Yes    | Email address associated with the student's account. |
|password   | string  |   Yes    | Password for the student's account. |

**Example Request Body:**

```json
{
  "email": "student@example.com",
  "password": "ExamplePassword123!"
}
```
**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the student's credentials were verified successfully. |
| accessToken | string | JWT returned after successful login, used to authenticate later requests. |

**Example Successful Response:**

```json
{
  "success": true,
  "accessToken": "<jwt_token>"
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

### Get My Assigned Courses
Retrieve the courses assigned to the logged-in student, including courses assigned directly or through their class.

**Endpoint:** `/students/me/courses`

**Method:** `GET`

**Authentication:** Required

**Inputs:**
| Header | Type | Required | Description|
|--------|------|----------|------------|
|Authorization| string | Yes | Bearer token containing JWT returned after successful login. |

No path parameters, query parameters, or request body are required. The server identifies the student from the verified JWT.

**Output Fields:**
| Field | Type | Description |
|-------|------|-------------|
| courses | array of objects | Courses assigned to the authenticated student. Empty if no courses are assigned. |
| courses[].courseID | string | Unique identifier of the assigned course. | 
| courses[].title | string | Title of the assigned course. |

**Example Successful Response:**
```json
{
  "courses": [
{
  "courseID": "course-001",
  "title": "Workplace Communication"
},
{
  "courseID": "course-002",
  "title": "Managing Customer Concerns"
}
  ]
}
```
**Example Usage:**
```http
GET /students/me/courses HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.
