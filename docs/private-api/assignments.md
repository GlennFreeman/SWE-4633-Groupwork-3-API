## Assignments

### Assign Course to Student
Assigns a specified course to a student.

**Endpoint:** `/assignments/students/assign`

**Method:** `POST`

**Authentication:** Required

**Request Body:** JSON

**Inputs:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| courseId | string | Yes | ID of the course to assign |
| studentId | string | Yes | ID of the student receiving the course |

**Example:**
```http
POST https://example.com/api/v1/assignments/students/assign
Content-Type: application/json

{ "courseId": "CS4504", "studentId": "student123" }
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the course was successfully assigned to the student. |

**Example Output Body:**

```json
true
```

### Unassign Course from Student
Removes a specified course assignment from a student.

**Endpoint:** `/assignments/students/unassign`

**Method:** `POST`

**Authentication:** Required

**Request Body:** JSON

**Inputs:**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| courseId | string | Yes | ID of the course to unassign |
| studentId | string | Yes | ID of the student whose assignment will be removed |


**Example**
```http
POST https://example.com/api/v1/assignments/students/unassign
Content-Type: application/json

{ "courseId": "CS4504", "studentId": "student123" }
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the course was successfully removed from the student. |

**Example Output Body:**
```json
true
```

### Assign Course to Class
Assigns a specified course to a class.

**Endpoint:** `/assignments/classes/assign`

**Method:** `POST`

**Authentication:** Required

**Request Body:** JSON

**Inputs**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| courseId | string | Yes | ID of the course to assign |
| classId | string | Yes | ID of the class receiving the course |


**Example**
```http
POST https://example.com/api/v1/assignments/classes/assign
Content-Type: application/json

{ "courseId": "CS4504", "classId": "class101" }
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the course was successfully assigned to the class. |

**Example Output Body:**
```json
true
```

### Unassign Course from Class
Removes a specified course assignment from a class.

**Endpoint:** `/assignments/classes/unassign`

**Method:** `POST`

**Authentication:** Required

**Request Body:** JSON

**Inputs**
| Name | Type | Required | Description |
|------|------|----------|-------------|
| courseId | string | Yes | ID of the course to unassign |
| classId | string | Yes | ID of the class whose assignment will be removed |

**Example**
```http
POST https://example.com/api/v1/assignments/classes/unassign
Content-Type: application/json

{ "courseId": "CS4504", "classId": "class101" }
```

**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| success   | boolean | Whether the course was successfully removed from the class. |

**Example Output Body:**
```json
true
```

### Get My Assigned Courses
Retrieves the list of courses assigned to the authenticated user.

**Endpoint:** `/assignments/my-courses`

**Method:** `GET`

**Authentication:** Required

**Request Body:** JSON

**Inputs:** none. The authenticated user is identified through the authorization context.

**Example**
```http
GET https://example.com/api/v1/assignments/my-courses
Authorization: Bearer eyJhbGciOi...
```
**Output Fields:**
| Field | Type | Description |
|-----------|------|-------------|
| courses   | course array | An array of the courses that the user has. |

**Example Output Body:**
```json
[]
```