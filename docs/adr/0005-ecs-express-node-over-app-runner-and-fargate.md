# 5. Use AWS Express Mode over App Runner and Full AWS Fargate

## Status
Accepted

## Context
Need a managed runtime to run the ECR image built and stored in ECR. App Runner was the original plan but its no longer
available for new accounts. Evaluated ECS Express Mode vs ECS Fargate.

## Decision
ECS Express Mode - Managed runtime for simplicity, internally takes care of creating roles, ALB,
Networking, IP address, auto-scaling keeping the complexities abstract. 
Full orchestration is not needed for current setup, Speed and setup time is priority.

## Consequences 
**Positives**
- No need to manage every AES service under ECS - Express mode configures everything by itself, Speed and setup time.
**Negatives**
- Giving control - We don't have control of configuring ALB, scaling, monitoring, networking components.

**Problems hit and diagnosed**
- Port and health check path configuration - Manual configuration required for port 8080 and health check path
, don't use the defaults(port 80 and path /) in express mode service.
- First deploy failed with 'exec  format error'. Build image on AMD64 instead of arm64 (build.gradle bootBuildImage configuration), Supported by AWS Mumbai region.

## Reversal condition
- When the project gets bigger and we need fine-tuning for different AWS services, Moving to ECS Fargate
- would be an ideal choice where we can configure ALB, VPC, Target groups, EC2 instances, scaling.