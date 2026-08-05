# ADR-12: Use Spring Data JPA for URL repository

## Status
Accepted [2026]

## Context
- URL shortener needs simple CRUD for `Url` entities (save, lookup by ID/short code, optional list/delete).
- Hand-rolled DAO or direct `EntityManager` usage would add boilerplate for standard operations.

## Decision
- Use Spring Data JPA repository interface:
    - `UrlRepository extends JpaRepository<Url, Long>`
- Add derived query methods (e.g., `findByShortCode`) or `@Query` as needed; avoid custom `EntityManager` unless proven necessary.

## Alternatives considered
1. Hand-rolled DAO with `EntityManager` - Full control but high boilerplate, more error-prone, harder to maintain for simple CRUD.
2. Spring Data JPA with custom fragments - Useful for complex queries, but unnecessary complexity for current requirements.

## Consequences
- Positive:
    - Minimal boilerplate; repository layer is essentially zero code.
    - Aligns with Spring Boot best practices; easy for team to understand.
    - Easy to test with standard Spring test utilities.
- Negative:
    - Less fine-grained control than direct `EntityManager` for advanced tuning.
    - Complex dynamic queries may require Criteria API or `@Query`.

## Review point
- Revisit if we encounter performance or query complexity limits that Spring Data JPA cannot address cleanly.