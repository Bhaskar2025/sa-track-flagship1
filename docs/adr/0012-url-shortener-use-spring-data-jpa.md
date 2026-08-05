# ADR-12: Use Spring Data JPA for URL repository

## Status
Accepted [2026]

## Context
- URL shortener needs simple CRUD for `Url` entities (save, lookup by ID).
- Hand-rolled DAO or direct `EntityManager` would add boilerplate for standard operations.

## Decision
- Use Spring Data JPA repository interface:
  - `UrlRepository extends JpaRepository<Url, Long>`
- Use only basic CRUD methods (`save`, `findById`) as in current controller; no custom query methods added yet.

## Alternatives considered
1. Hand-rolled DAO - Custom DAO class implementing all CRUD operations; more code and maintenance for no extra benefit at this scale.
2. Direct `EntityManager` use - Inject `EntityManager` and manually implement persistence logic; full control but high boilerplate and error surface for simple CRUD.

## Consequences
- Positive:
  - Minimal boilerplate; repository layer is essentially zero code.
  - Aligns with Spring Boot best practices; easy for team to understand.
  - Easy to test with standard Spring test utilities.
- Negative:
  - `saved.getId()` requires DB round trip already inherent to `save()`; no extra cost but ID is only available after persist.

## Review point
- Revisit if we hit performance or query complexity limits that Spring Data JPA cannot address cleanly (e.g., heavy custom pagination, advanced fetch tuning).