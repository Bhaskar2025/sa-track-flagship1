# D3 - Week 2 - Microservices

## What they are
- When different modules have their own DB, deployment pipeline ans scalability infra, 
exposing APIs over NW, fails independently. Its called microservices while monolith is 
a single deployable unit.

## The four forces
- Independent deployability: Every service has own deployment pipeline.
- Independent scalability: The services can be scaled independently depending on their load.
- Failure Independence: Any service failure doesn't affect other services.
- Team autonomy: Teams can work independently and their pace and deployment speed doesn't depend on others.

## The six failure modes
- Distributed monolith: when microservices are created but they depend on each other.
- Chatty services: Orderservice calling Inventory-> product -> payment -> user in a 
synchronous chain and adding latency.
- Distributed transactions: distributed transactions and failures ahs to be handled carefully
using 2 phase commit and saga pattern.
- Shared database: when microservices end up sharing DB and schema, recommendation service 
reading from order service DB.
- operational complexity: there are lot of services, multiple deployment pipeline, logging, tracking.
- NW failure: This is new failure type in microservices which is not there in monolith.

## The distributed monolith - why it's the worst outcome
- When services are not completely independent, they share data or dependent on each other
for completing their tasks, its called distributed monolith, this is worst than modular monolith.
- 