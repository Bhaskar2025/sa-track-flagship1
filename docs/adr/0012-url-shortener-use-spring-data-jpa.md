# ADR-12: Use Java records for request/response DTOs

## Status
Accepted [2026]

## Context
- URL shortener API needs request/response DTOs (`CreateUrlRequest`, `CreateUrlResponse`).
- Returning JPA entities (`Url`) directly from controllers couples API to persistence model and can leak internal fields.
- Hand-written POJOs for simple DTOs add boilerplate (fields, constructors, getters, equals/hashCode, toString).

## Decision
- Use Java records for request/response DTOs:
  - `public record CreateUrlRequest(String longUrl) {}`
  - `public record CreateUrlResponse(String shortCode) {}`
- Controllers accept and return only DTOs; entities are used only inside service/repository layer.
- Map between DTOs and entities in controller/service (e.g., `new Url(request.getLongUrl())`, `new CreateUrlResponse(shortCode)`).

## Alternatives considered
1. Hand-written POJO classes - Full control but verbose for simple, immutable DTOs.
2. Return entities directly from controllers - Simpler initially but tightly couples API to DB schema, risks over-exposure of fields, and makes versioning harder.

## Consequences
- Positive:
  - Concise, immutable, value-based DTOs with minimal code.
  - Clear API contract separate from persistence model.
  - Easier to evolve API (e.g., change response shape) without touching entity mapping.
- Negative:
  - Records are final; not ideal if DTOs need inheritance or mutable builders.
  - Small mapping overhead between DTOs and entities (acceptable for current scale).

## Review point
- Revisit if we need richer DTO behavior (validation groups, builders, inheritance) that records cannot express cleanly.