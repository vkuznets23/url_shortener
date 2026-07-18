# Requirements

This document describes the functional and non-functional requirements of the URL Shortener application. It defines the expected system behavior, supported use cases, and key quality attributes that guide the implementation.

## Actors

- **User** — a person who can register, authenticate, create, and manage shortened URLs.

## Assumptions

- Only authenticated users can create and manage shortened URLs.
- Redirecting via a short URL is available without authentication.
- Expired URLs cannot be accessed.
- Each short code uniquely identifies a single active URL.

## Use Cases

### User Authentication

- Register a new account.
- Log into the application.

### URL Management

- Create a shortened URL.
- Specify an optional expiration date.
- View all previously created URLs.
- Delete a URL.

### URL Redirection

- Be redirected to the original URL.

### Analytics

- View click statistics for a shortened URL.

## Functional Requirements

The system shall:

- Allow users to register and log into the application.
- Generate a unique short code for each newly created URL.
- Redirect requests for valid short URLs to the original destination.
- Allow users to specify an optional expiration date.
- Record every successful redirect for analytics.
- Allow users to retrieve and delete only their own URLs.
- Return the existing active short URL if the same user attempts to shorten the same URL with the same settings.

## Non-Functional Requirements

The application should:

- Store URL mappings and user data in a persistent database.
- Store user passwords as securely hashed values.
- Support concurrent client requests without data corruption.
- Frequently accessed URL mappings should be cached to improve redirect performance.
- Expose a RESTful API.
- Validate incoming requests.
- Be containerized using Docker.
- Provide automated tests for the core business logic.
