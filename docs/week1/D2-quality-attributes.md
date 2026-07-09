# D2 - Quality Attributes
## 1. Scalability
- When the user base or data increases, system should be able to add more servers to cater
the data and to serve user requests.
- Systems where it dominates - Google search , Meta, Whatsapp.
- Systems where it's sacrificed - Internal applications, small systems with 100 users.

## 2. Availability
- System should be available to use all the time, should have minimal or no downtime.
Its measures by 99.99 (4 nines), 99.999 (5 nines) etc
- Systems where it dominates - Air Traffic monitor, Google Search
- Systems where it's sacrificed - Batch running systems, internal apps

## 3. Performance 
- It's measured by latency and throughput. latency should be low and throughput 
should be high for a high performance system.
- Systems where it dominates - HFTs , Streaming apps,  Payments
- Systems where it's sacrificed - Batch scripts, internal systems, maintenance apps

## 4. Maintainability
- System should be easy to understand and easy to change.
- Systems where it dominates - Enterprise apps, E-commerce
- Systems where it's sacrificed - throw prototypes, one-off migration scripts

## 5. Reliability
- How system behaves in case of failure. Correctness of the app is measured by reliability.
Reliable system produces correct results even if parts of system fails.
- Systems where it dominates - User facing apps, banking apps
- Systems where it's sacrificed - Social media counts, Analytics

## 6. Security
- System should implement authentication, authorization and encryption to protect the data access.
- Systems where it dominates - Govt sites, Healthcare apps, financial apps
- Systems where it's sacrificed - Public APIs

## 7. Deployability
- Automated pipelines, health checks and rollback in case of failure.
- Systems where it dominates - Startups, sAAS products
- Systems where it's sacrificed - Embedded systems, Desktop softwares

## 8. Observability
- It should be easy to find out what's happening when the application runs and when it fails.
- Systems where it dominates - Distributed systems, production systems with SLOs
- Systems where it's sacrificed - Messaging apps, single server systems

## 9. Extensibility
- It should be easy to add new features, components and integrations into the system without 
modifying the core architecture.
- Systems where it dominates - Enterprise applications
- Systems where it's sacrificed - Small internal applications, hackathon apps, crud apps

## 10. Testability
- System flows should be testable.
- Systems where it dominates - Ecommerce applications, Banking systems, startups
- Systems where it's sacrificed - Systems with external dependencies
