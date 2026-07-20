# Database design

This database schema is designed to support URL shortening, user management, and click analytics while remaining simple and extensible for future features.

## Entities

- **Users** – stores user accounts and authentication information.
- **Links** – stores mappings between long URLs and generated short codes.
- **Clicks** – stores click events for analytics, such as the time of the click and the visitor's country.

## Relationships

- One **User** can create many **Links**.
- One **Link** can have many **Click** records.

## Business rule

If a user attempts to shorten the same URL with the same settings, the existing active short link should be returned instead of creating a new one. Otherwise, a new short link is created.

## Constraints

- `username` must be unique.
- `short_code` must be unique.
- Every `Link` belongs to exactly one `User`.
- Every `Click` belongs to exactly one `Link`.
- `expires_at` may be null, indicating that the link never expires.

## Database Schema

<img width="900" height="295" alt="Screenshot 2026-07-20 at 19 42 34" src="https://github.com/user-attachments/assets/a7ac5571-19d5-45b9-b34e-53cbe1e5d654" />


```sql
Table users {
  id integer [primary key]
  username varchar [unique, not null]
  password_hash varchar [not null]
  created_at timestamp [not null]
}

Table links {
id integer [primary key]
user_id integer [not null]
title varchar
long_link varchar [not null]
short_code varchar [unique, not null]
created_at timestamp [not null]
// so user can set (7 days, 10 days, never, etc.)
expires_at timestamp
}

Table clicks {
id integer [primary key]
url_id integer [not null]
clicked_at timestamp [not null]
country_code varchar [not null]
}

Ref: links.user_id > users.id
Ref: clicks.url_id > links.id

```

The initial schema is defined in:

- `V1__init.sql`

```

```
