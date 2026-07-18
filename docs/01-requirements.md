# Requirements

## Functional Requirements

The application should allow users to:

- Register and log into the system.
- Create shortened URLs from long URLs.
- Specify an optional expiration date for a shortened URL.
- Retrieve all URLs they have created.
- Delete their own URLs.
- Redirect visitors from a short URL to the original URL.
- Record every redirect for analytics purposes.
- View click statistics for their URLs.

## Non-Functional Requirements

The application should:

- Store URL mappings and user data in a persistent database.
- Generate unique short codes.
- Securely store user passwords using hashing.
- Handle multiple concurrent requests.
- Use Redis to cache frequently accessed URL mappings.
- Validate incoming requests.
- Provide automated tests for the core business logic.
- Be containerized using Docker.
