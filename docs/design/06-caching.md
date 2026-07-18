## Context

Redirects are the most frequent operation in the system.

## Decision

Use Redis as a cache for frequently accessed URL mappings.

## Consequences

- Lower database load.
- Faster redirects.
- Additional infrastructure component to maintain.

## Alternatives Considered

- PostgreSQL only.
- In-memory application cache.
