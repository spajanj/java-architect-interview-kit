---
layout: default
title: Scenario - Design a Real System
permalink: /scenario
---

# Scenario: Design a Real System

> Give the candidate a whiteboard or diagramming tool.
>
> **Design an e-commerce order-processing platform using Java/Spring Boot. The system handles 5 million orders per day and must remain available if individual downstream systems fail.**

---

## System Diagram

```
Client
   |
API Gateway
   |
Order Service
   |
   +---- Inventory
   +---- Payment
   +---- Pricing
   +---- Fulfillment
   |
Event Streaming
   |
Notifications / Analytics / Audit
```

---

## Progressive Failure Scenarios

| Scenario | Situation | Question |
|----------|-----------|----------|
| **A** | Payment takes 30 seconds to respond | What happens to threads, connections, and the user request? |
| **B** | Payment successfully charges the customer, but the Order Service times out | How do you avoid charging the customer twice? |
| **C** | Kafka is temporarily unavailable | Do you lose the order event? |
| **D** | Inventory reports success but subsequently crashes | How do you maintain business consistency? |

---

> This distinguishes someone who knows architecture terminology from someone who can design production systems.
