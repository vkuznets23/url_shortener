# REST API

## Authentication

| Method | Endpoint              | Description                  |
| ------ | --------------------- | ---------------------------- |
| POST   | /api/v1/auth/register | Register a new user          |
| POST   | /api/v1/auth/login    | Authenticate and receive JWT |

## Links

| Method | Endpoint           | Description              |
| ------ | ------------------ | ------------------------ |
| POST   | /api/v1/links      | Create a shortened URL   |
| GET    | /api/v1/links      | Retrieve all user's URLs |
| GET    | /api/v1/links/{id} | Retrieve a specific URL  |
| PATCH  | /api/v1/links/{id} | Update a URL             |
| DELETE | /api/v1/links/{id} | Delete a URL             |

## Redirect

| Method | Endpoint     | Description                  |
| ------ | ------------ | ---------------------------- |
| GET    | /{shortCode} | Redirect to the original URL |

## Analytics

| Method | Endpoint                      | Description               |
| ------ | ----------------------------- | ------------------------- |
| GET    | /api/v1/links/{id}/statistics | Retrieve click statistics |
