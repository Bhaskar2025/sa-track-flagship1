# 4. Choose ECR private over Docker Hub or ECR public

## Status
Accepted

## Context
Need a registry to store container images that will be pulled by AWS App Runner.
Registry should be accessible from AWS infrastructure without managing separate credentials.
We have three options:
ECR private, Docker Hub or ECR public. This ADR shows which one we choose and why.

## Decision
**1. ECR private over Docker Hub**
As I am using AWS as cloud provider for my projects and will use other AWS services,
Same AWS ecosystem means ntive IAM authentication; No separate separate account and creds to manage.
**2. ECR private over ECR public**
As I am working on my personal project for learning, Keeping the repo private makes sense.
It is also more secure as i don't want to expose anything as of now.

## Consequences
- No separate credentials to manage - ECR auth is native IAM.
- ECR storage costs ~$0.10/GB/month - Docker Hub is free up to a limit; deliberate trade-off for IAM integration
- Vendor lock-in - ECR is AWS only; migrating cloud provider means migrating the registry too.
- Private repo add security boundary - App runner needs explicit IAM permission to pull.

## Reversal condition
- If project moves from AWS, or if distributing public base images becomes the requirement, Docker Hub 
 or GitHub Container Registry would be better fit.