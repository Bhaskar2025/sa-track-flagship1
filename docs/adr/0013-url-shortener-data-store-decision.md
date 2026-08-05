# ADR-13: Use H2 file mode for data store

## Status
Accepted [2026]

## Context
- URL shortener needs a persistent store for URL mappings.
- Options: H2 in-memory, H2 file mode, or PostgreSQL/RDS.
- Goal: keep setup simple for initial version while ensuring data survives restarts.

## Decision
- Use H2 database in file mode (e.g., `jdbc:h2:file:/tmp/data/urlshortener`) as the data store.

## Alternatives considered
1. H2 in-memory - Simplest but all data lost on application restart; unsuitable for any real usage.
2. PostgreSQL/RDS - Production-grade, multi-user, and durable; but adds operational complexity (DB provisioning, credentials, networking, backups) at this stage.

## Consequences
- Positive:
  - Data persists across restarts without external DB setup.
  - Minimal operational overhead; single JVM process with embedded DB file.
  - Easy to migrate to PostgreSQL later (same JPA layer, just change datasource).
- Negative:
  - Not suitable for high concurrency or multi-instance deployments.
  - In containerized deployments, each redeploy silently erases all data because the file lives in the container's ephemeral filesystem, not durable storage.
  - Multi-instance or rolling redeploy leads to split-brain data (each instance sees only its own local file).
  - File can grow unbounded; backup/restore is manual.
  - Single point of failure; no built-in high availability.

## Review point
- Revisit when we need horizontal scaling, multi-instance deployment, or stronger durability/backup guarantees; target migration to PostgreSQL/RDS at that time.