---
title: Students
nav_order: 1
parent: Public API
---

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

### Start a Simulation Attempt
Start a new attempt for a scenario within a course assigned to the logged-in student.

**Endpoints:** `/students/me/attempts`

**Method:** `POST`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

|Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| courseId | body | string | Yes | Identifier of the assigned course containing the scenario. |

| scenarioId | body | string | Yes | Identifier of the scenario the student wants to attempt. |

**Request Body:** JSON

**Example Request Body:**
```json
{
  "courseId": "course-001",
  "scenarioId": "scenario-001"
}
```
**Output Fields:**

| Field | Type | Description |

|-------|------|-------------|

| attempt Id | string | Unique identifier of the newly created attempt. |

| courseId | string | Identifier of the course containing the scenario. |

| scenarioId | string | Identifier of the scenario being attempted. |

| completed | boolean | Whether the attempt has finished. |

**Example Successful Response:**
```json
{
  "attemptId": "attempt-001",
  "courseId": "course-001",
  "scenarioId": "scenario-001",
  "completed": false
}
```
**Example Usage:**
```http
POST /students/me/attempts HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Content-Type: application/json
Accept: application/json
{
  "courseId": "course-001",
  "scenarioId": "scenario-001"
}
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.

### Get Attempt Inbox
Retrieve the available inbox messages for an attempt owned by the logged-in student.

**Endpoint:** `/students/me/attempts/{attemptId}/inbox`

**Method:** `GET`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

| Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| attemptId | path | string | Yes | Identifier of the student's attempt. |

No request body is required. The server verifies that the attempt belongs to the authenticated student.

**Outputs Fields:**

| Field | Type | Description |

|-------|------|-------------|

| messages | array of objects | Available inbox messages. Empty if no messages are available. |

| messages[].messageId | string | Unique identifier of the message. |

| messages[].sender | string | Display name of the simulated sender. |

| messages[].subject | string | Subject of the message. |

| messages[].body | string | Text content of the message. |

**Example Successful Response:**
```json
{
  "messages": [
    {
      "messageId": "message-001",
      "sender": "Office Manager",
      "subject": "Customer follow-up",
      "body": "A customer has asked for an update. How would you respond?"
    }
  ]
}
```
**Example Usage:**
```http
GET /students/me/attempts/attempt-001/inbox HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.

### Get Message Response Options
Retrieve the available response choices for a message in an attempt owned by the logged-in student.

**Endpoint:** `/students/me/attempts/{attemptId}/messages/{messageId}/options`

**Method:** `GET`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

| Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| attemptId | path | string | Yes | Identifier of the student's attempt. |

| messageId | path | string | Yes | Identifier of the message within that attempt. |

No request body is required. The server verifies that the attempt belongs to the authenticated student and that the message belongs to the attempt.

**Output Fields:**

| Field | Type | Description |

|-------|------|-------------|

| options | array of objects | Available response choices. Empty if no choices are available. |

| options[].optionId | string | Unique identifier of the response option. |

**Example Successful Response:**
```json
{
  "options": [
    {
      "optionId": "option-001",
      "text": "Acknowledge the request and provide and expected update time."
    },
    {
      "optionId": "option-002",
      "text": "Tell the customer to contact someone else."
    }
  ]
}
```

**Example Usage:**
```http
GET /students/me/attempts/attempt-001/messages/message-001/options HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.

### Submit a Message Response
Submit a selected response option for a message in an attempt owned by the logged-in student.

**Endpoint:** `/students/me/attempts/{attemptId}/messages/{messageId}/responses`

**Method:** `POST`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

| Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| attemptId | path | string | Yes | Identifier of the student's attempt. |

| messageId | path | string | Yes | Identifier of the message within that attempt. |

| optionId | body | string | Yes | Identifier of the selected response option. |

The server verifies that the student owns the attempt, the message belongs to it, and the selected option is valid for the message.

**Request Body:** JSON

**Example Request Body:**
```json
{
  "optionId": "option-001"
}
```

**Output Fields:**

| Field | Type | Description |

|-------|------|-------------|

| attemptId | string | Identifier of the updated attempt. |

| messageId | string | Identifier of the answered message. |

| optionId | string | Identifier of the submitted response option. |

| completed | boolean | Whether the attempt is now complete. |

| feedback | string | Student-facing feedback about the response. Empty if feedback is withheld. |

**Example Successful Response:**
```json
{
  "attemptId": "attempt-001",
  "messageId": "message-001",
  "optionId": "option-001",
  "completed": false,
  "feedback": "Your response has been recorded."
}
```

**Example Usage:**
```http
POST /students/me/attempts/attempt-001/messages/message-001/responses HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
{
  "optionId": "option-001"
}
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.

### Get Attempt Results
Retrieve the final results for a completed attempt owned by the logged-in student.

**Endpoint:** `/students/me/attempts/{attemptId}/results`

**Method:** `GET`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

| Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| attemptId | path | string | Yes | Identifier of the student's attempt. |

No request body is required. The server verifies that the attempt belongs to the authenticated student and is complete before returning final results.

**Output Fields:**

| Field | Type | Description |

|-------|------|-------------|

| attemptId | string | Unique identifier of the completed attempt. |

| scenarioId | string | Identifier of the scenario attempted. |

| score | number | Final score on a scale from 0 to 100. |

| feedback | string | Student-facing summary of performance. |

**Example Successful Response:**
```json
{
  "attemptId": "attempt-001",
  "scenarioId": "scenario-001",
  "score": 85,
  "feedback": "You communicated clearly. Continue practicing how to prioritize request."
}
```

**Example Usage:**
```http
GET /students/me/attempts/attempt-001results HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.

### Get My Attempt History
Retrieve the logged-in student's attempt history for a specified scenario.

**Endpoint:** `/students/me/attempts`

**Method:** `GET`

**Authentication:** Required

**Inputs:**

| Parameter | Location | Type | Required | Description |

|-----------|----------|------|----------|-------------|

| Authorization | header | string | Yes | Bearer token containing the student's JWT. |

| scenarioId | query | string | Yes | Identifier of the scenario whose attempt history is requested. |

No request body is required. Only attempts belonging to the authenticated student is returned.

**Output Fields:**

| Field | Type | Description |

|-------|------|-------------|

| attempts | array of objects | Student's attempt for the specified scenario. Empty if none exist. |

| attempts[].attemptId | string | Unique identifier of the attempt. |

| attempts[].scenarioId | string | Identifier of the scenario attempted. |

| attempts[].completed | boolean | Whether the attempt has finished. |

**Example Successful Response:**
```json
{
  "attempts": [
    {
      "attemptsId": "attempts-001",
      "scenarioId": "scenario-001",
      "completed": true
    },
    {
      "attemptsId": "attempts-002",
      "scenarioId": "scenario-001",
      "completed": false
    }
  ]
}
```

**Example Usage:**
```http
GET /students/me/attempts?scenario-001 HTTP/1.1
Host: api.example.com
Authorization: Bearer <jwt_token>
Accept: application/json
```
`https://api.example.com` is a placeholder for the deployed API's base URL. `<jwt_token>` will be replaced with the access token returned after successful login.



