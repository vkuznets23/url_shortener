# REST API

## Authentication

| Method | Endpoint              | Description                  | Request Body       | Success Response   |
| ------ | --------------------- | ---------------------------- | ------------------ | ------------------ |
| POST   | /api/v1/auth/register | Register a new user          | `RegisterRequest`  | 201 Created        |
| POST   | /api/v1/auth/login    | Authenticate and receive JWT | username, password | 200 OK + JWT token |

### RegisterRequest

```JSON
{
  "username": "vika",
  "password": "password123"
}
```

### LoginRequest

```JSON
{
  "username": "vika",
  "password": "password123"
}
```

## Links

| Method | Endpoint           | Description              | Request Body        | Success Response |
| ------ | ------------------ | ------------------------ | ------------------- | ---------------- |
| POST   | /api/v1/links      | Create a shortened URL   | `CreateLinkRequest` | 201 Created      |
| GET    | /api/v1/links      | Retrieve all user's URLs |                     | 200 OK           |
| GET    | /api/v1/links/{id} | Retrieve a specific URL  |                     | 200 OK           |
| PATCH  | /api/v1/links/{id} | Update a URL             | `UpdateLinkRequest` | 200 OK           |
| DELETE | /api/v1/links/{id} | Delete a URL             |                     | 204 No Content   |

### CreateLinkRequest

```JSON
{
  "title": "example website",
  "long_link": "https://example.com/very/long/url",
}
```

### UpdateLinkRequest

```JSON
{
  "title": "changed example website",
  "expires_at": "2026-12-31T23:59:59Z"
}
```

## Redirect

| Method | Endpoint     | Description                  | Request Body | Response  |
| ------ | ------------ | ---------------------------- | ------------ | --------- |
| GET    | /{shortCode} | Redirect to the original URL |              | 302 Found |

## Analytics

| Method | Endpoint                      | Description               | Request Body | Response |
| ------ | ----------------------------- | ------------------------- | ------------ | -------- |
| GET    | /api/v1/links/{id}/statistics | Retrieve click statistics |              | 200 OK   |
