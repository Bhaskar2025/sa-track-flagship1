# D5 Week 3 - Fully Graded Mock (Rate Limiter)

## Scenario
- Designed a rate limiter for 100 requests per min per API key service.

## Rubric scores - all six dimensions
| Dimention                  | Score | Why                                                                                                              |
|----------------------------|-------|------------------------------------------------------------------------------------------------------------------|
| Scoping                    | 4/5   | Real consequential questions asked before designing                                                              |
| Capacity Estimation        | 4/5   | Correct Maths but named redis before justifying reasoning                                                        |
| High-level design          | 4/5   | Complete first pass with major components, missing counter mechanism & window strategy                           |
| Deep dive                  | 4/5   | Correct traced the fixed window failure, Named redis data structure unprompted, needed push on throughput number |
| Failure modes & Trade-offs | 4/5   | Good maths backed reasoning on fail open decision, Needed corrections on 10x scale                               |
| Communication              | 4/5   | Generally clear but repeatedly reached for confident conclusions in place of reasoning                           |

## The one recurring pattern across today's mock
- Confident conclusion before reasoning 
  1. Redis is fast enough to process 25000 requests per second.
  2. Calculation for 10x was incorrect.

## The rule I'm taking forward
- I would do the reasoning and calculation first before giving confident conclusions.
## One thing i did well today that wasn't there in earlier mocks
- Created the complete high-level design diagram in first pass having all the main components.