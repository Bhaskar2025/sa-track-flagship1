#D2 Week2 - Modular Monolith

## What it is ?
- Modular monolith is single deployable unit where each module has its own  boundary.
Data ownership is clearly defined, each module has its own tables and DB schema and no 
FK references between them. One module can call other via public API contract and internal
service implementation is package-private.

## The five forces - 
- Enforced boundaries without NW overhead: Microservices enforce boundaries via network.
Modular monolith enforce boundaries via the compiler, you can't call internal code because
its package-private.
- Independent reasoning per module: Each module can be developed, tested, changed independently.
- Domain driven boundaries - Each module follow different business boundary. Separate modules 
for Order, User, Inventory, Payment.
- Clean migration path to Microservices - As modules already have boundaries, data ownership rules,
Its easy to split the module into a microservice. Internal API call can be replaced with
HTTP request call.
- Operational simplicity - One pipeline, One deployment, no network failure and no service dependency.

## The three failure modes - 
- Boundary erosion: Most common and most dangerous failure mode. Over time developers add "just one"
cross module dependency or a direct DB call, system starts degrading. Example: In Hybris, extensions calling
each other spring beans.
- Shared DB anti-pattern: All modules share one DB schema, FK references. Changing the schema requires
changes multiple modules. Example: In Hybris, FK references across extensions, impex loading is shared.
- Deployment coupling at scale: Single deployment unit is a bottleneck to high frequency independent
releases by different teams. Example: Bug in promotion module can block checkout flow.

## The boundary enforcement mechanism
- Package-private visibility enforces that internal modules can't be imported by other modules.
- ArchUnit can enforce this at build time. Automated tests can be written to ensure no internal package is
imported outside.


## When i would choose modular monolith over layered
- When there is plan to scale independently and need to migrate to microservices later.
- In layered architecture, any module can call internal code of other modules while
modular monolith enforces that modules only communicate via public APIs.

## When i would evolve past modular monolith to microservices
- When individual teams want to scale there modules independently and need independent 
deployment pipeline.

