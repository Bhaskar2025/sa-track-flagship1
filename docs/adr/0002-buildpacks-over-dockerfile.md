# 2. Using Spring Boot buildpacks over a hand-rolled Dockerfile

## Status
Accepted

## Context
We need to containerize a Spring Boot service. We have two options: Write a Dockerfile manually or 
use Springboot's built-in buildpacks supported via bootBuildImage. This ADR records which we choose and why.

## Decision
We are using buildpacks provided by springboot configuration as we don't need to write manual Dockerfile.

## Consequences
- No Dockerfile to maintain - reduces manual error and maintenance overhead.
- Less control - buildpacks make base image and JRE decisions automatically.
- Harder to debug - no file to inspect when a build fails; builspacks logs are the only signal.
- Reverse condition - If compliance required a hardened base image, or image size becomes a constraint 
- requiring a multi-stage distroless build, switch to a hand-rolled Dockerfile.