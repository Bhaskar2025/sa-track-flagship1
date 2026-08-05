# D6 Quality attribute doc: URL Shortener

## Dominant attributes

**1. Simplicity**
- Minimal moving parts: single Spring Boot service, embedded H2 file DB, no external infrastructure.
- Evidence: One repository interface (`JpaRepository<Url, Long>`), no custom DAO, no Flyway/Liquibase, no external DB.

## Sacrificed attribute - named honestly

**Scalability / High Availability**

- What is actually given up:
    - System cannot scale horizontally; running multiple instances leads to split-brain data (each instance has its own H2 file).
    - In containerized deployments, every redeploy that replaces the container filesystem silently erases all URL data because the DB file lives in ephemeral storage.
    - No built-in high availability; if the process or disk dies, service is down and recovery is manual.

- Why this is accepted:
    - This is an initial version / learning project where speed and simplicity matter more than production-grade scale and resilience.
    - Acceptable as long as:
        - Traffic is low and single-instance deployment is sufficient.
        - Data loss on redeploy is tolerable (e.g., test/demo environment, or data can be recreated).
    - It stops being acceptable when:
        - The service is used in production with real users and cannot tolerate data loss on redeploy.
        - We need multiple instances for capacity or reliability.
        - At that point, migration to a shared, durable database (e.g., PostgreSQL/RDS) and proper backup/HA strategy becomes mandatory.

## Whats present but not dominant

- **Security** – Basic HTTP endpoints; no auth, rate limiting, or abuse protection yet.
- **Performance** – Adequate for low traffic; no explicit latency/throughput targets or tuning.
- **Maintainability** – Reasonable structure (controllers, DTOs, repository), but no formal versioning or API evolution strategy yet.