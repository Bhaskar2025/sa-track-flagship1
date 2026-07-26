# 6. Use GitHub Actions OIDC over Secret Keys 

## Status
Accepted

## Context
GitHub Actions pipeline need to authenticate to AWS to push the images to ECR and trigger 
ECS Express mode deployments. Three decisions needed:
Authentication mechanism, image tag strategy, and IAM permission scope.

## Decision
**1.OIDC over stored AWS keys in GitHub Secrets**
OIDC issues a cryptographically signed token per workflow run, scoped to the specific repo and branch,
valid for 15 mins, AWS trusts GitHub as an identity provider via the IAM OIDC provider
configuration. No credentials stored in GitHub, nothing to rotate, nothing to leak.
**2.latest tag over SHA tags**
Using latest tag to simplicity for initial code to test and complete the chain.
I will switch to SHA once i  need rollback and traceability for the images and deployments.
**3.Scoped IAM policy over Administrator Access**
Pipeline only needs ECR push + ECS update. Least-privilege limits blast radius if OIDC trust is abused.

## Consequences
**Positives**
- No long-lived credentials in GitHub - nothing to rotate and leak.
- Trust policy scoped to main branch only, prevents deployment trigger for feature branches.
- Scoped IAM policy - pipeline can't touch anything outside ECR + ECS
**Negatives**
- Latest tag make rollback harder - As every image has latest tag only, 
- ECS doesn't differentiate between deployment tags making rollback disabled.
- 
## Reversal condition
- switch stored keys if GitHub can't be trusted as an identity provider in the org's security policy.
- Switch to SHA tags later for immutable, traceable deploys