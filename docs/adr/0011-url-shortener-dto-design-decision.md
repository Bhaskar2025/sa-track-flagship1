# ADR-11: Use Java records for CreateURLRequest/Response DTOs

## Status
Accepted [2026]

## Context
- URL shortener API needs request/response DTOs (e.g., `CreateURLRequest`, `CreateURLResponse`).
- Returning JPA entities directly from controllers couples API to persistence model and leaks internal fields.
- Hand-written POJO classes for simple DTOs add boilerplate (fields, constructors, getters, equals/hashCode, toString).

## Decision
- Use Java records for request/response DTOs:
    - `public record CreateURLRequest(String longUrl) {}`
    - `public record CreateURLResponse(String shortCode, String longUrl) {}`
- Never return entities directly from controllers; always map to/from DTOs.

## Alternatives considered
1. Hand-written POJO classes - Full control but verbose for simple, immutable DTOs.
2. Return entities directly from controllers - Simpler initially but tightly couples API to DB schema, risks over-exposure of fields, and makes versioning harder.

## Consequences
- Positive:
    - Concise, immutable, value-based DTOs with minimal code.
    - Clear API contract separate from persistence model.
    - Easier to evolve API without changing entity structure.
- Negative:
    - Records are final; not suitable if DTOs need inheritance or mutable builders.
    - Slight mapping overhead between DTOs and entities (mitigated by simple mapping logic).

## Review point
- Revisit if we need richer DTO behavior (validation groups, builders, inheritance) that records cannot express cleanly.