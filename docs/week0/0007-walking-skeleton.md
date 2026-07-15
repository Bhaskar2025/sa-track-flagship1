# ADR 7: Walking Skeleton before real system design

## Status
- Accepted

## Context
- For SA preparation, I had two choices:
  - Do real system design first and build a full scaled application and then deploy to AWS.
  - Start with a walking skeleton with full pipeline and then go deeper into system design 
  and application.

## Decision
- Selected walking skeleton approach. This is to understand the cloud technology and deployment pipeline 
so that all the changes made through the handson will be deployed to live server to get good
understanding of AWS by end of the week 14.

## Alternative considered
1. **Build the real system first, deploy at the end.**  - rejected because deployment becomes a 
big bang risk on an unfamiliar platform under time pressure.
2. **Use Heroku instead of AWS** - rejected because AWS is the target platform; Heroku abstracts
the primitives(IAM, ECR, ECS, ALB) that need to be learned.
3. **Follow roadmap sequentially, no skeleton** - rejected because 7 weeks of local only builds 
creates a large integration gap; late deployment surprises are expensive to fix.

## Consequences
**Positive:**
- Deployment chain validated before domain logic exissts
- AWS primitives (IAM, ECR, ECS, OIDC) learned on a trivial app when mistakes are cheap.
- Every week's build ships through a working pipeline.

**Negative /Accepted trade-offs:**
 - Skeleton has no domain value, throwaway code.
 - 'latest' tag disables rollback
 - Express mode chosen for speed over control.

## Review point
Week 5 - Express Mode graduates to full ECS Fargate
Week 8 - Terraform replaces console-built infrastructure.