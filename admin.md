## Admin API
### Register new user
Creates a new user\
**Endpoint:** `POST /admin/register_new_user`\
**Authentication:** Required\
**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|----------|-------------|
| name | string | Yes | Null | Name of new user, preferably formatted "last, first" |
| email | string | Yes | Null | Email of new user, used to log in|
| password | string | No | 1234 | default password for new user, encouraged to change later |
| role | integer | No | 0 | role of new user, see roles table in DB |
**Response:**
```json
{
 "sucessful": True
 "message": "no errors"
}
```
