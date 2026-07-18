# Architecture

## Overview

The URL Shortener is a monolithic backend application built with Kotlin and Spring Boot. It follows a layered architecture that separates responsibilities between the API, business logic, data access, and persistence layers.

The application uses PostgreSQL as the primary database, Redis for caching frequently accessed URLs, and JWT for stateless authentication.

## Technology Choices

| Technology  | Purpose                                    |
| ----------- | ------------------------------------------ |
| Kotlin      | Primary programming language               |
| Spring Boot | REST API framework                         |
| PostgreSQL  | Persistent data storage                    |
| Redis       | Cache for frequently accessed URL mappings |
| Flyway ??   | Database schema versioning                 |
| Docker      | Containerization                           |
| JWT         | Stateless authentication                   |
