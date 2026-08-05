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
    - `public record CreateURLResponse(String shortCode) {}`
- Never return entities directly from controllers; always map to/from DTOs.

## Alternatives considered
1. Hand-written POJO classes - Full control but verbose for simple, immutable DTOs.
2. Return entities directly from controllers - Simpler initially but tightly couples API to DB schema, 
would expose Url.id directly in the API response - an internal primary key with no business meaning 
to a client.

## Consequences
- Positive:
    - Concise, immutable, value-based DTOs with minimal code.
    - Clear API contract separate from persistence model.
    - Easier to evolve API without changing entity structure.
- Negative:
  - saved.getId() requires DB round trip already inherent to save() no extra cost.

## Review point
-  Add basic validation on CreateURLRequest.longUrl before app accepts input from anywhere beyond
your own testing - currently nothing stops an empty string or malformed value from being persisted.