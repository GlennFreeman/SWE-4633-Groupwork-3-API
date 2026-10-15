## Admin API
### Register new user
Creates a new user\
**Endpoint:** `POST /admin/register_new_user`\
**Authentication:** Required\
**Query Parameters:**
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|----------|-------------|
| name | string | Yes | - | Name of new user, preferably formatted "last, first" |
| email | string | Yes | - | Email of new user, required to log in|
| password | string | No | 1234 | Default password for new user, encouraged to change later |
| role | integer | No | 0 | Role of new user, see roles table in DB for valid values|
### Response:
```json
{
 "sucessful": true
 "message": "no errors"
}
```
