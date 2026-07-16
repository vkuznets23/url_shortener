# url_shortener
The database is designed to support URL shortening, user management, and click analytics while keeping it simple and easy to extend with additional features in the future.

The project consists of three main entities:

- **Users** – stores user accounts and authentication information.
- **Links** – stores mappings between long URLs and generated short codes.
- **Clicks** – stores click events for analytics, such as the time of the click and the visitor's country.

> **Business rule:** If a user attempts to shorten the same URL with the same settings, the existing active short link should be returned instead of creating a new one. Otherwise, a new short link is created.

<img width="978" height="320" alt="image" src="https://github.com/user-attachments/assets/566133d7-7479-4e1f-8f91-84330d640ca7" />

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
