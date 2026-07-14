# 1. Use default actuator health path

## Status
Accepted

## Context
Need a health endpoint for Week-0 walking skeleton, deployed via App Runner.
Actuator exposes /actuator/health by default; it can be remapped to /health via management.exdpoints.web.base=path.

## Decision
Keep the default /actuator/health path.

## Consequences
- Idiomatic Spring conversion - recognizable to any Spring engineer reading this repo.
- No operational cost: App Runner's health check config accepts any path, so remapping would have bought nothing.
- Anyone probing this service for health must know the /actuator prefix.