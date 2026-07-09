# D3 - Trade offs

## System 1: Ride sharing app

Ride hailing app. Millions of drivers and riders simultaneously. Rider requests a ride, sees nearby drivers on real time map, gets matched driver, price is calculated and payment is processed.

Name 3 competing quality attributes, tradeoffs, what sacrificed and what costs the user.

**Operations**

1. **Showing nearby drivers on the map**
    - Availability over Consistency - Eventual consistency is fine, showing most drivers immediately is better than showing all drivers after delay.
    - Consistency vs Latency - Choose latency, show instantly.

2. **Matching driver to rider**
    - Consistency over Availability - Consistency wins. Correct match should be there even if there is some delay.
    - Consistency vs Latency - Choose consistency, delay is fine.

3. **Payment processing**
    - Consistency vs Availability - Consistency for payments, wait is fine but transaction should have no duplicates.
    - Consistency vs Latency - Choose consistency, delay is fine.

## System 2: Netflix

230 million subscribers, streaming videos globally, personalized recommendations for user, multiple devices per user, content licensed per country, billing monthly.

Name 3 competing quality attributes, tradeoffs, what sacrificed and what costs the user.

**Operations**

1. **Streaming videos**
    - Availability over Consistency - Serve videos immediately at available quality. Quality can be inconsistent (adapt quality to bandwidth).

2. **Personalized recommendations**
    - Availability over Consistency - Recommendations should be available with eventual consistency.
    - Performance vs Consistency - Performance wins. Show recommendations immediately.

3. **Content on multiple devices and countries**
    - **Content on multiple devices** - Consistency over latency. If you find the same video on another device, it might take some time, but the video should be there and should stream from the same timestamp.
    - **Content in multiple countries** - Reliability over user experience. System should enforce licensing and show correctness. Videos available in one country may not be there in another.

4. **Monthly billing**
    - Consistency over Performance - Monthly batch processing may take time, but billing should be for the correct amount without duplicate deductions.