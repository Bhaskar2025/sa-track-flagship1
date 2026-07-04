# 1. Using AWS Express Move over App Runner and AWS Fargate

## Status
Accepted

## Context
Need a managed runtime to run ECR image. App Runner was the original plan but its no longer
available for new accounts. Evaluated ECS Express Mode vs ECS Fargate.

## Decision
ECS Express Mode - Managed runtime for simplicity, internally takes care of creating roles, ALB,
Networking, IP address, auto-scaling keeping the complexities abstract. 
Full orchestration is not needed for current setup, Speed and setup time is priority.

## Consequences 
- No need to manage every AES service under ECS - Express mode configures everything by itself, Speed and setup time.
- Giving control - We don't have control of configuring ALB, scaling, monitoring, networking components.

## Reversal condition
- When the project gets bigger and we need fine-tuning for different AWS services, Moving to ECS Fargate
- would be an ideal choice where we can configure ALB, VPC, Target groups, VPC, EC2 instances, scaling.