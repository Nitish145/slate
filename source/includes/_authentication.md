# Authentication
In order to make requests that require the user to be authenticated, you must retrieve the token to be able to act on the behalf of the user.

## Sign Up a User
This endpoint gives back the authentication token that encodes user's `id`, `name` and `email`.

### Possible exceptions

| Error Code | Description|
| ---------- |------------------------------------------------------|
| 409        | When user already exists.|
| 422        | Invalid or missing parameters.|

```http
POST /api/v1/auth/signup HTTP/1.1
Accept: application/json
Host: localhost
```
```json
{
  "email": "test@test.com",
  "password": "12345678",
  "name": "Test Name"
}
```
```http
HTTP/1.1 201 CREATED
Content-Type: application/json
```
> JSON response example:

```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjp7InVzZXJfaWQiOjIsInVzZXJuYW1lIjoiTml0aXNoIEFnZ2Fyd2FsIiwiZW1haWwiOiJyb3lhbG5pdGlzaDIxQGdtYWlsLmNvbSJ9LCJleHAiOjE1ODkyMDI5ODF9.tHRLJeQGuLiJ1Ncc2tQSaNiQnbrnERKuOPERfZeNnF8",
}
```

## Log in a User
This endpoint gives back the authentication token that encodes user's `id`, `name` and `email`.

### Possible exceptions

| Error Code | Description|
| ---------- |------------------------------------------------------|
| 401        | Invalid password.|
| 404        | Non existent user tries to login.|

```http
POST /api/v1/auth/login HTTP/1.1
Accept: application/json
Host: localhost
```
```json
{
  "email": "test@test.com",
  "password": "12345678",
}
```
```http
HTTP/1.1 202 ACCEPTED
Content-Type: application/json
```
> JSON response example:

```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjp7InVzZXJfaWQiOjIsInVzZXJuYW1lIjoiTml0aXNoIEFnZ2Fyd2FsIiwiZW1haWwiOiJyb3lhbG5pdGlzaDIxQGdtYWlsLmNvbSJ9LCJleHAiOjE1ODkyMDI5ODF9.tHRLJeQGuLiJ1Ncc2tQSaNiQnbrnERKuOPERfZeNnF8",
}
```
