# Quality Attribute Trade-offs

## Eventual consistency over strong consistency
- At 100k orders/sec, strong consistency is too expensive in latency. Eventual consistency is decided.
Customer hitting view order immediately after placing order might see a brief delay before the order 
appears.

## Idempotency via queue to prevent duplicates
- In eventual consistent system, the duplicate-order check can't rely on the DB. 
Instead, an idempotency key is written to the queue first, duplicate request is 
caught there before hitting the DB.

## Queue as a source of truth for order creation.
A separate service reads from the queue and creates the orders in DB. This means 
if the order-creation service crashes mid flow, the queue message survives.

## Decouple confirmation from DB persistence.
Don't show "Order Confirmed", show "Order Placed". Confirmation/Failure comes via
notification once the separate service successfully creates the order.
