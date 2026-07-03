# 1. AWS access model for solo learning account

## Status
Accepted

## Context
Setting up AWS access for solo learner building a personal portfolio.
Three access decisions needed: authentication method, permission scope, and MFA on the daily user.

## Decision
**1. Standalone IAM user over IAM Identity Center (SSO)**
IAM Identity Center is AWS's modern recommended approach for managing access, 
especially in teams. For a solo learner optimizing on setup and speed, a standalone
IAM user is simpler and sufficient.
**2. AdministratorAccess over lease privilege**
Per function, least privilege based role is recommended in AWS. But as our setup is for solo user,
who does everything like development, ops, billing, Giving AdministratorAccess for keeping 
the role less complex and reduce overhead would be fine. 
**3. Skipped MFA on daily IAM user**
Working on a personal laptop only used by me, console login risk is low for IAM use.
MFA for root is already enabled.

## Consequences
- Faster setup, lower friction for daily work.
- Not lease privilege - Broader blast radius if credentials leak.
- Compensated by strict access-key hygine, Never committed to repo.
- 
## Reversal condition
- Move to IAM identity center if it becomes a team account.
- Move to least privilege scoped roles before any production use.
- Enable IAM user MFA if laptop is ever shared