# Users

## Get All Users
You can GET all users in /api/v1/users. Authentication `token` is passed through `Authorization` header and is **required**. 

### Possible exceptions

| Error Code | Description|
| ---------- |------------------------------------------------------|
| 401        | When user is not authenticated i.e invalid or corrupt `token`.|

```http
GET /api/v1/users HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```
```http
HTTP/1.1 200 OK
```
> JSON response example:

```json
{
    "data": [
        {
            "id": "4",
            "type": "users",
            "attributes": {
                "name": "Nitish Aggarwal"
            }
        },
        {
            "id": "2",
            "type": "users",
            "attributes": {
                "name": "Nitish Aggarwal"
            }
        },
        {
            "id": "3",
            "type": "users",
            "attributes": {
                "name": "Nitish Aggarwal"
            }
        },
        {
            "id": "5",
            "type": "users",
            "attributes": {
                "name": "Abhishek"
            }
        },
        {
            "id": "7",
            "type": "users",
            "attributes": {
                "name": null
            }
        }
    ],
    "meta": {
        "current_page": 1,
        "next_page": 2,
        "prev_page": null,
        "total_pages": 4,
        "total_count": 17
    }
}
```

## GET a Specific User
You can GET particular user details in /api/v1/users/{:id}. Authentication `token` is passed through `Authorization` header and is **required**. 

### URL Parameters

Parameter | Description
--------- | -----------
`id` | The `id` of the user to retrieve

### Possible exceptions

| Error Code | Description|
| ---------- |------------------------------------------------------|
| 401        | When user is not authenticated i.e invalid or corrupt `token`.|
| 404        | When the requested user identified by `id` does not exists.|

```http
GET /api/v1/users/1 HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```
```http
HTTP/1.1 200 OK
```
> JSON response example:

```json
{
    "data": {
        "id": "1",
        "type": "user",
        "attributes": {
            "id": 1,
            "email": "test@test1.com",
            "name": "Test User 1",
            "admin": false,
            "country": null,
            "educational_institute": null,
            "subscribed": true,
            "created_at": "2020-03-22T12:41:28.931Z",
            "updated_at": "2020-03-22T12:41:29.803Z"
        }
    }
}
```

## UPDATE a Specific User
You can UPDATE a specific user details in /api/v1/users/{:id}. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Parameters

Parameter | Description
--------- | -----------
`id` | The `id` of the user to update

### Possible exceptions

| Error Code | Description|
| ---------- |------------------------------------------------------|
| 401        | When user is not authenticated i.e invalid or corrupt `token`.|
| 403        | When the requested user identified by `id` differs from `authenticated user`|
| 404        | When the requested user identified by `id` does not exists.|

```http
PATCH /api/v1/users/1 HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```
```json
{
	"name": "Test User 1 updated"
}
```
```http
HTTP/1.1 202 ACCEPTED
```
> JSON response example:

```json
{
    "data": {
        "id": "1",
        "type": "user",
        "attributes": {
            "id": 1,
            "email": "test@test1.com",
            "name": "Test User 1 updated",
            "admin": false,
            "country": null,
            "educational_institute": null,
            "subscribed": true,
            "created_at": "2020-03-22T12:41:28.931Z",
            "updated_at": "2020-03-22T12:41:29.803Z"
        }
    }
}
```

