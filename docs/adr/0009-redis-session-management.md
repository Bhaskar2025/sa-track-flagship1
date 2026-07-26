# ADR-09 - Centralized session management via Redis

## Status
Accepted

## Context
- We had around 16 nodes. There used to be frequent deployments and even though there was no downtime
during deployments. User sessions used to get cleared out during deployments. If user is logged in on
node1 and node1 is going through reboot, user gets logged out. This was affecting the users.

## Decision
- To move the session from the app servers, Redis cluster was chosen with master slave architecture.
Redis sentinel was used for automatic failover.

## Alternatives considered
1. Cookie-based solution - cookie can store limited data and session data might be bigger because stores
lots of user data. cookie is stored in the browser, and it can be hijacked.
2. Sticky sessions - We were using this already, Sessions were sticky to the server and used to get 
cleared on server restart.
3. Non-sticky session replication - It provides replication of session across application servers
in the cluster. It is difficult for logging and troubleshooting as there are lots of servers and
request might travel through different nodes.
4. Session replication via JGroup - In this approach, web server can redirect customer's request 
from failed server to another server in the cluster. This might cause performance issues.

## Consequences
- Positive:
  - Multiple deployments in a day can be achieved without affecting the customers. No user gets logged out
    during the deployments.
- Negative:
  - New redis cluster to manage, and new dependency for user sessions. Added operational complexity 
  and cost for running redis cluster.

## Review point
It was never revisited till 2022 and before i worked in this project.

