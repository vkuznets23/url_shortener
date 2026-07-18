# DB Design Decisions

## Table of Contents

- [Decision 1: Use PostgreSQL](#decision-1-use-postgresql)
- [Decision 2: Separate Domain Entities](#decision-2-separate-domain-entities)
- [Decision 3: Store Creation Timestamp](#decision-3-store-creation-timestamp)
- [Decision 4: Support Link Expiration](#decision-4-support-link-expiration)
- [Decision 5: Store Individual Click Events](#decision-5-store-individual-click-events)

## Decision 1: Use PostgreSQL

### Context

The application requires persistent storage, relational modeling, and reliable transaction support.

### Decision

Use PostgreSQL as the primary database.

### Consequences

| Advantages                                           | Disadvantages                                      |
| ---------------------------------------------------- | -------------------------------------------------- |
| ACID-compliant transactions ensure data consistency. | Requires running a separate database server.       |
| Support for indexes and constraints.                 | More operational overhead than embedded databases. |
| Integration with Spring Boot and JPA.                |                                                    |
| Widely used in production systems.                   |                                                    |

### Alternatives Considered

- SQLite
- MySQL
- MongoDB

PostgreSQL was selected because it offers strong relational features, excellent tooling, and is commonly used in modern backend applications.

## Decision 2: Separate Domain Entities

### Context

The application manages three different types of data with different lifecycles.

### Decision

Model the domain using three separate tables:

- Users
- Links
- Clicks

### Consequences

| Advantages                                                          | Disadvantages                                |
| ------------------------------------------------------------------- | -------------------------------------------- |
| Clear separation of responsibilities.                               | Requires joins when retrieving related data. |
| Easier maintenance and future extensions.                           |                                              |
| Analytics data does not duplicate information from the Links table. |                                              |

### Alternatives Considered

- Storing click statistics directly in the `links` table.
- Embedding click information as JSON.

Both options were rejected because they limit future analytics capabilities.

## Decision 3: Store Creation Timestamp

### Context

The system needs to know when resources were created.

### Decision

Store a `created_at` timestamp for users and links.

### Consequences

This enables:

- sorting by creation date;
- displaying creation history;
- calculating link lifetime;
- future audit functionality.

### Alternatives Considered

Not storing creation timestamps.

Rejected because creation time is useful for analytics, debugging, and future features with minimal storage overhead.

## Decision 4: Support Link Expiration

### Context

Users should be able to create temporary links.

### Decision

Store an optional `expires_at` timestamp.

A `NULL` value indicates that the link never expires.

### Consequences

The application can determine whether a link is active without recalculating expiration rules.

Future features such as automatic cleanup or scheduled expiration become easier to implement.

### Alternatives Considered

Calculate expiration from `created_at` and a fixed lifetime.

Rejected because different links may have different expiration periods or never expire.

## Decision 5: Store Individual Click Events

### Context

The application provides analytics for shortened URLs.

### Decision

Store every redirect as a separate record.

### Consequences

This enables:

- total click count;
- clicks per day;
- country statistics;
- future analytics features.

### Alternatives Considered

Only storing a click counter in the `links` table.

Rejected because detailed historical analytics would be impossible.
