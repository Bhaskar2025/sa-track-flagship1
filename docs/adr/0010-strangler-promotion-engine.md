# ADR-10: Strangler pattern promotion engine migration

## Status
Accepted [2021]

## Context
- Hybris 2205 defaulted to new drool based rule engine; existing legacy promotions would
break. Big-bang migration under upgrade time pressure was too risky for revenue critical
promotions.

## Decision
- Run legacy and new promotion engine simultaneously via promotions.legacy.mode=true
+ spring bean wiring, migrate promotions gradually post go-live.

## Alternatives considered
1. Big-bang rewrite of all promotions before go-live - This was a time-consuming and risky process
because if there is any issue in rewrite it would break the promotions and hard to test.
2. Delay the upgrade until all promotions are rewritten - Rejected because Hybris upgrade was time
critical and delay was not worth due to only promotion piece. 

## Consequences
- Positive:
  - Zero promotion downtime as both the engines can run in parallel.
  - It was safer to gradually migrate the promotions to new rule engine.
  - In case of any promotion fails in new rule engine, it can be rolled back to old promotion engine.
- Negative:
  - Two promotion engines to maintain simultaneously.
  - Memory overhead of running two promotion engines.
  - Adding tech debt - It has to be migrated to new rule engine.

## Review point
- Promotion engine was migrated to new rule engine slowly after 1 year in 2022.