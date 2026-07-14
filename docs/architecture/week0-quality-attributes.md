# Week 0 - Quality Attributes Design Doc

## Dominant quality attributes
### 1. Deployability - 
End to to git pipeline was created for deployability. Whenever users pushes/merges to main branch of
the repo, github action will trigger. It will authenticate to ECR using OIDC connect, Build the image,
Push it to ECR and then deploy to ECS express mode, do health checks.

### 2. Security - 
- Using OIDC connect for authentication, no long lived secret tokens. Configured IAM roles only for ECR and 
Express mode, keeping the blast radius small. MFA for root user.

### 3. Maintainability
- Documented all the ADRs which keeps track of all the architecture decisions. Added C4 diagram to give
clear understanding of the system. Clean gihub repo maintained.

## Explicitly sacrificed
### Scalability 
- Using single farget instance for walking skeleton which has single point for failure as this is a test
code, not real users.
### Availability 
- As there is single farget instance, aplication will be down until its gets rebooted. If deployment fails,
rollback will not work automatically as there is only latest tag maintained which disabled the rollback button.
### Observability
Though health check is maintained but there is no fine grained logging configured for the application yet.

## Why these trade offs were right for the walking skeleton
- Deployability and Security are core, we will keep using them till next iterations and its hard to change
decisions later.
- Maintainability is a good habit, if we don't do it now, it will create confusion later point and i won't 
even remember why I made this decision.
- Scalability and Availability are not required for walking skeleton for single user and no real users.
- Observability is required when system becomes little complex.
