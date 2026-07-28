# D4 Week 3 - RFC and Weighted Trade-off Matrix

## RFC vs ADR
- RFC will be used before decision is finalized and we need input from the affected stakeholders.
RFC document proposes an approach and seek any suggestion or challenge from affected teams on the same.
- ADR is to record the decision which is already made and it is created for institutional memory 
for future reference.

## When I'd write RFC instead of an ADR for Flagship 1
- I would write RFC at the time of proposing approach to make the architectural decisions. 
All the stakeholder will validate the RFC and provide their comments and suggestion on the approach.
## The weighted trade-off matrix - RDS vs DynamoDB for Flagship 1 order data
| Criteria Weighted         | Weight | RDS Score | DynamoDB Score | RDS Weighted | DynamoDB |
|---------------------------|--------|-----------|----------------|--------------|----------|
| Query Pattern Flexibility | 1      | 9         | 2              | 9            | 2        |
| Write Throughput          | 5      | 8         | 9              | 40           | 45       |
| Join Support              | 1      | 9         | 1              | 9            | 1        |
| Schema Flexibility        | 4      | 1         | 9              | 4            | 36       |

## Which technology wins and why - defended
- Query pattern flexibility is not required for order management system with only two query types.
- This is a medium write throughput requirements (50k order/day) which can be handled by DynamoDB.
- Join support is not required for these two fixed queries, Hence DynamoDB would be a better choice.
- We don't need fixed schema requirement, hence DynamoDB would be good fit over RDS (relational DB).

## One thing that changed how i think
- I didn't know about RFC. Its one of the most important architectural decision-making document.
