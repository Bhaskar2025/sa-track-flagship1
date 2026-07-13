#D5 Architecture vs Design + Interview Format

## The three signals - architecture vs design
- Service Boundary - When the decision crosses service boundary and two different teams are affected.
Its architecture otherwise its a design decision.
- Database Ownership - When you determine who owns what data, its architecture. Data is hard to migrate.
If you are talking about internal schema structure and relationships, its design.
- Quality attributes at system level - When quality attributes at systems level are impacted by the decision,
then its architecture. When quality attributes at single service or operation are impacted, its design.

## The five interview stages
- Scoping - What are the core operations of the system and understand which quality attributes are preferred.
- Scale estimation - Back of envelop calculation to know storage requirements and requests per second.
This is to determine whether system need sharding, caching, replication etc.
- High level design - Draw and name all the components and communication between them. Name the components
and mention the communication style among them.
- Deep dive into one component - Deep dive into one component and explain it in detail.Interviewer probes
failure modes, scaling and consistency and how do you recover when it breaks.
- Trade off defense - This is to counter the trade off decisions and you should reason and justify them.

## My mock today
- Scenario: Notification system for e-commerce - Design a Notification System where order events like
"Order Placed", "Order Shipped", "Order Delivered" and "Order Cancelled" are notified to the customer 
on SMS, Email and Push notification. Important events like "Order Cancelled" should not get lost.
- Strongest stage: Scoping
- Weekest stage: High level design - Missed data storage and scaling on first pass.
- One thing i did differently from Week0 rep: Did correct scoping, listed out operations first.
- One thing i'd fix if i ran it again: Consider data layer and scaling requirements in the design diagram.

## The opening move for any consistency question
- What are the operations, consistency is not decided at system level, its decided at operation level.

## The gateway bottleneck fix
- Add multiple SMS gateway with routing layer in front to handle the notification load. 
Its called provider failover.