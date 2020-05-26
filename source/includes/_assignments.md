# Assignments

## GET Group's Assignments

You can GET all the assignments for the group you have access to in `/api/v1/groups/:group_id/assignments`. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Query Parameters

| Parameter      | Description                                    |
| -------------- | ---------------------------------------------- |
| `page[number]` | The `number`<sup>th</sup> page of the response |
| `page[size]`   | The `size` of the `per_page` response          |

<aside class="warning">Only users with show access can fetch the assignments</aside>

### Possible exceptions

| Error Code | Description                                                      |
| ---------- | ---------------------------------------------------------------- |
| 401        | When user tries to authenticate with invalid or corrupt `token`. |
| 403        | When user without show access tries to fetch assignments         |
| 404        | When the group identified by :group_id does not exist            |

```http
GET /api/v1/groups/:group_id/assignments HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```

```http
HTTP/1.1 200 OK
```

> JSON response example :

```json
{
  "data": [
    {
      "id": "1",
      "type": "assignment",
      "attributes": {
        "name": "Test assignment 1",
        "deadline": "2021-05-24T11:47:40.244Z",
        "description": "assignment description",
        "created_at": "2020-05-24T11:47:40.244Z",
        "updated_at": "2020-05-24T11:47:40.244Z",
        "status": "open",
        "grading_scale": "no_scale",
        "grades_finalized": false,
        "restrictions": "[]"
      }
    },
    {
      "id": "2",
      "type": "assignment",
      "attributes": {
        "name": "Test assignment 2",
        "deadline": "2021-05-24T11:48:26.739Z",
        "description": "assignment description",
        "created_at": "2020-05-24T11:48:26.740Z",
        "updated_at": "2020-05-24T11:48:26.740Z",
        "status": "open",
        "grading_scale": "no_scale",
        "grades_finalized": false,
        "restrictions": "[]"
      }
    }
  ],
  "links": {
    "self": "http://localhost:3000/api/v1/groups/1/assignments?page[number]=1",
    "first": "http://localhost:3000/api/v1/groups/1/assignments?page[number]=1",
    "prev": null,
    "next": null,
    "last": "http://localhost:3000/api/v1/groups/1/assignments?page[number]=1"
  }
}
```

## GET Assignment details

You can GET assignment details (identified by `:id`) in `/api/v1/assignments/:id/`. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Parameters

| Parameter | Description                               |
| --------- | ----------------------------------------- |
| `id`      | The `id` of the assignment to be detailed |

### Possible exceptions

| Error Code | Description                                                       |
| ---------- | ----------------------------------------------------------------- |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.    |
| 403        | When authenticated user is neither mentor nor user of the Group   |
| 404        | When the requested assignment identified by `id` does not exists. |

```http
GET /api/v1/assignments/:id HTTP/1.1
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
    "type": "assignment",
    "attributes": {
      "name": "Test assignment 1",
      "deadline": "2021-05-24T11:48:26.739Z",
      "description": "assignment description",
      "created_at": "2020-05-24T11:48:26.740Z",
      "updated_at": "2020-05-24T11:48:26.740Z",
      "status": "open",
      "grading_scale": "no_scale",
      "grades_finalized": false,
      "restrictions": "[]"
    }
  }
}
```

## POST Assignment

You can POST assignment in `/api/v1/groups/:group_id/assignments`. Authentication `token` is passed through `Authorization` header and is **required**.

### List of acceptable params for post request include:

| Name            | Type          | Description                                 |
| --------------- | ------------- | ------------------------------------------- |
| `name`          | `String`      | Name of the Assignment                      |
| `deadline`      | `String`      | Updated name of the group                   |
| `description`   | `String`      | Description of the assignment               |
| `grading_scale` | `String`      | grading scale for the assignment            |
| `restrictions`  | `JSON String` | restrictions for assignments in json string |

### URL Parameters

| Parameter  | Description                                      |
| ---------- | ------------------------------------------------ |
| `group_id` | The `id` of the group, assignment is to be added |

<aside class="warning">The grading_scale cannot be changed later on</aside>

### Possible exceptions

| Error Code | Description                                                        |
| ---------- | ------------------------------------------------------------------ |
| 400        | When invalid parameters are used.                                  |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.     |
| 403        | When non-mentor user tries to add the assignment                   |
| 404        | When the requested group identified by `group_id` does not exists. |

```http
POST /api/v1/groups/:group_id/assignments HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```

```json
{
  "name": "Test assignment",
  "deadline": "date_time_string",
  "description": "Test description",
  "grading_scale": "Letter",
  "restrictions": "[]"
}
```

```http
HTTP/1.1 202 ACCEPTED
Content-Type: application/json
```

> JSON response example:

```json
{
  "data": {
    "id": "1",
    "type": "assignment",
    "attributes": {
      "name": "Test Assignment",
      "deadline": "2021-05-26T05:25:30.049Z",
      "description": "test description",
      "created_at": "2020-05-26T05:25:30.049Z",
      "updated_at": "2020-05-26T05:25:30.049Z",
      "status": "open",
      "grading_scale": "Letter",
      "grades_finalized": false,
      "restrictions": "[]"
    }
  }
}
```

## UPDATE Assignment

You can PATCH assignment details in `/api/v1/assignments/:id`. Authentication `token` is passed through `Authorization` header and is **required**.

### List of acceptable params for put/patch request include:

| Name           | Type          | Description                                 |
| -------------- | ------------- | ------------------------------------------- |
| `name`         | `String`      | Name of the Assignment                      |
| `deadline`     | `String`      | Updated name of the group                   |
| `description`  | `String`      | Description of the assignment               |
| `restrictions` | `JSON String` | restrictions for assignments in json string |

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| `id`      | The `id` of the assignment to be updated |

### Possible exceptions

| Error Code | Description                                                       |
| ---------- | ----------------------------------------------------------------- |
| 400        | When invalid parameters are used.                                 |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.    |
| 403        | When non-mentor user tries to update the assignment               |
| 404        | When the requested assignment identified by `id` does not exists. |

```http
PATCH /api/v1/assignments/:id HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```

```json
{
  "name": "Test assignment Updated",
  "deadline": "date_time_string",
  "description": "Test description",
  "restrictions": "[]"
}
```

```http
HTTP/1.1 202 ACCEPTED
Content-Type: application/json
```

> JSON response example:

```json
{
  "data": {
    "id": "1",
    "type": "assignment",
    "attributes": {
      "name": "Test Assignment Updated",
      "deadline": "2021-05-26T05:25:30.049Z",
      "description": "test description",
      "created_at": "2020-05-26T05:25:30.049Z",
      "updated_at": "2020-05-26T05:25:30.049Z",
      "status": "open",
      "grading_scale": "Letter",
      "grades_finalized": false,
      "restrictions": "[]"
    }
  }
}
```

## DELETE Assignment

Group mentor can DELETE a assignment (identified by `:id`) in `/api/v1/assignments/:id/`. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Parameters

| Parameter | Description                              |
| --------- | ---------------------------------------- |
| `id`      | The `id` of the assignment to be deleted |

<aside class="warning">User with mentor or admin access can only delete the assignment</aside>

### Possible exceptions

| Error Code | Description                                                       |
| ---------- | ----------------------------------------------------------------- |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.    |
| 403        | When non-mentor user tries to delete the assignment               |
| 404        | When the requested assignment identified by `id` does not exists. |

```http
DELETE /api/v1/assignment/:id HTTP/1.1
Accept: application/json
Authorization: Token {token}
Host: localhost
```

```http
HTTP/1.1 204 NO CONTENT
Content-Type: application/json
```

## REOPEN Assignment

Mentor can REOPEN a closed assignment to extend the deadline by 1 day in `/api/v1/assignments/:id/reopen`. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Parameters

| Parameter | Description                               |
| --------- | ----------------------------------------- |
| `id`      | The `id` of the assignment to be reopened |

<aside class="notice">Reopened assignment's deadline is increased by one day</aside>

### Possible exceptions

| Error Code | Description                                                         |
| ---------- | ------------------------------------------------------------------- |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.      |
| 403        | When authenticated user is neither mentor nor user of the Group     |
| 404        | When the requested assignment identified by `id` does not exists.   |
| 409        | When the requested assignment identified by `id` is already opened. |

```http
GET /api/v1/assignments/:id/reopen HTTP/1.1
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
  "message": "Assignment has been reopened!"
}
```

## START Assignment

Group Members can start working on the assignment in`/api/v1/assignments/:id/start`. This creates a new private project for he user to work upon. Authentication `token` is passed through `Authorization` header and is **required**.

### URL Parameters

| Parameter | Description                                       |
| --------- | ------------------------------------------------- |
| `id`      | The `id` of the assignment to be start working on |

<aside class="notice">Created Private Project's name is #{username}/#{assignment_name}</aside>

### Possible exceptions

| Error Code | Description                                                              |
| ---------- | ------------------------------------------------------------------------ |
| 401        | When user is not authenticated i.e invalid or corrupt `token`.           |
| 403        | When authenticated user isn't a user of the Group, assignment is part of |
| 404        | When the requested assignment identified by `id` does not exists.        |

```http
GET /api/v1/assignments/:id/start HTTP/1.1
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
  "message": "Voila! Project set up under name #{@project.name}"
}
```
