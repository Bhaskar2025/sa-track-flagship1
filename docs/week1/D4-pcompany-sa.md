# D4 - The Product-Company SA

## What does a product-company SA own that a consulting SA doesn't?
Product company SA owns how his architecture performs in production. He own the production incidents. 
He needs to join the 3 AM calls when anything breaks in the PROD and use the mechanism which he
prepared in case of failure. Consulting SA don't own the production. They just own till architecture 
design document, once its approved, they move to next project.

## What is a "3 am question" and how does it change how you design system?
You have to ask yourself whether the trade off of architecture choice worth joining 3 AM call 
in case of system fails because of that choice. This is a quiestion only for product company
SA. Consulting Sa don't own the PROD.

## Two Architecture decisions from my own work that i can claim honestly:
- Redis HA session management - We used to have frequent deployments and at the time of deployments,
On node restarts, user session used to get cleared out because we were using sticky sessions.
I analysed different approaches like non-sticky session (HArd to debug the logs), cookie-based session
  (not secure), Jgroup session replication (performance issues) and finally selected redis for
session management. We moved user session from app servers to Redis cluster with one master and 2 slaves
with Sentinal to automatically take care of failure.
- Strangler-pattern promotion engine - For  SAP Hybris migration, I enabled legacy promotion engine 
and new promotion engine(drool based) to work together using custom changes to avoid big bang
promotion migration. Which kept running old promotions with new promotions avoiding any migration
failures. This was not supported OOTB.

## One thing from D4 that changes how I see my 14 years of work
Now I can name the decisions I made, explain the trade-offs behind them, and design
future systems with that lens from the start, not just in hindsight.
