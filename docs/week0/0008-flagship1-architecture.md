# ADR-08: Architectural style for Flagship 1

## Status
- Accepted

## Context
- Flagship 1 is a production grade distributed order management system built as a portfolio piece for
a product company SA role. Single spring boot service deployed on ECS fargate. Integrates with DynamoDB,
SQS/EventBridge, and AWS services. Must demonstrate architectural thinking, operability, and real
distributed patterns.

## Decision
- Modular monolith internally structured with hexagonal architecture, communicating between modules
via event driven patterns using SQS as the broker.
- Alternatives considered:
  - Layered architecture - Rejected because it doesn't provide module boundaries, cross module
  coupling would pile up and compiler don't prevent it.
  - Microservices - Microservices will add too much overhead for a flagship project build 
  for portfolio for a single developer.
  
## Consequences
Positives:
-   Modular monolith prevents the cross-module coupling that accumulated Hybris over 7 years - 
    compiler enforces what discipline couldn't
- Event-driven architecture flow demonstrate real distributed system pattern (outbox, 
  saga, idempotency) that product company SA needs.
- Hexagonal architecture isolated DynamoDB and SQS from domain logic, swapping AWS services
  doesn't touch business logic.
Negative / Accepted trade-off: 
- Event-driven adds asynchronous complexity, testing the order flow end-to-end
  requires a running SQS instance or a test double, which is slower than testing
  a synchronous call chain.

## Review point
- When flagship 1 is complete. If a module demonstrate clear independence scaling needs, 
  extract it as a microservice at that point.