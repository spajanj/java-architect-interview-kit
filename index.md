

# Java Architect Interview Questions

> For a Java Architect interview, test architecture judgment rather than only Java syntax. A strong architect should move from requirements to system boundaries, APIs, data consistency, resilience, security, observability, deployment, and concrete Java/Spring implementation choices.

---

## 1. Core Java and JVM

- Explain the JVM memory model: heap, stacks, metaspace, and direct/off-heap memory.
- How does Java Garbage Collection work? Compare G1 GC, ZGC, and Shenandoah. When would you consider each?
- A Java service periodically experiences long GC pauses. How would you diagnose the problem?
- Explain `volatile`, `synchronized`, `AtomicInteger`, and locks. When would you use each?
- What does *happens-before* mean in the Java Memory Model?
- Compare `HashMap`, `ConcurrentHashMap`, and immutable maps in concurrent applications.
- Explain Java's `CompletableFuture`. What problems can arise from using the common ForkJoinPool?
- What are virtual threads, and where would you use or avoid them?

|Aspect|Platform thread|Virtual thread|  
|-------|-------------|-----------|
| Scheduler   | Engineer    | Stuttgart |
| OS-thread relationship | Designer    | Berlin    |


- How would you diagnose a memory leak in a production JVM?
- What Java/JVM metrics would you expose through tools such as Micrometer, Prometheus, Grafana, or Datadog?

**Architect-level follow-up:**

> Your application works perfectly under functional testing but latency jumps dramatically at 1,000 concurrent requests. Walk me through your investigation.

---

## 2. Spring Boot and Enterprise Java

- Explain how Spring Boot auto-configuration works.
- What is the difference between `@Component`, `@Service`, `@Repository`, and `@Configuration`?
- Explain Spring bean scopes and lifecycle.
- How does `@Transactional` work internally? What are common proxy-related surprises?
- Explain transaction isolation levels with practical examples.
- How would you design exception handling consistently across 50+ Spring Boot services?
- Spring MVC versus WebFlux: how do you choose?
- How would you implement centralized configuration and secret management?
- How do you perform graceful shutdown of a Spring Boot microservice?
- How would you standardize Spring Boot services across a large engineering organization?

---

## 3. Architecture and System Design

> These questions should carry significant weight for an architect role.

- Design a system handling 10,000 requests/second. Explain:
  - Traffic management
  - APIs
  - Processing
  - Database
  - Caching
  - Resiliency
  - Observability
  - Scaling

- When would you choose a modular monolith instead of microservices?
- What signals tell you that a domain should become a separate microservice?
- Explain synchronous versus asynchronous communication. Where would you use REST/gRPC versus Kafka?
- Design an idempotent API for payment/order creation.
- How would you prevent duplicate processing when a Kafka consumer crashes after updating the database but before committing its offset?
- Explain the Saga pattern. Compare orchestration and choreography.
- How would you maintain consistency when one business transaction spans several microservices?
- Explain CQRS. When is it useful, and when is it unnecessary complexity?
- Explain Event Sourcing. What operational challenges does it introduce?
- What is the Outbox Pattern? What problem does it solve?
- Your architecture has 100 microservices. How would you prevent excessive service-to-service dependencies?

---

## 4. Scenario: Design a Real System

Give the candidate a whiteboard or diagramming tool:

> Design an e-commerce order-processing platform using Java/Spring Boot. The system handles 5 million orders per day and must remain available if individual downstream systems fail.

### System Diagram

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

### Progressive Failure Scenarios

| Scenario | Situation | Question |
|----------|-----------|----------|
| **A** | Payment takes 30 seconds to respond | What happens to threads, connections, and the user request? |
| **B** | Payment successfully charges the customer, but the Order Service times out | How do you avoid charging the customer twice? |
| **C** | Kafka is temporarily unavailable | Do you lose the order event? |
| **D** | Inventory reports success but subsequently crashes | How do you maintain business consistency? |

> This distinguishes someone who knows architecture terminology from someone who can design production systems.

---

## 5. Microservices and Distributed Systems

- Explain circuit breaker, timeout, retry, and bulkhead patterns.
- In what order should retries and circuit breakers be applied?
- Why can retries make an outage worse?
- Explain exponential backoff and jitter.
- What is distributed tracing and how would you propagate correlation/trace IDs?
- How do you troubleshoot one request traversing 15 microservices?
- How would you version APIs without breaking consumers?
- How do you achieve backward compatibility for Kafka events?
- How would you handle partial failure in a distributed workflow?
- What's your approach to service discovery and load balancing in Kubernetes?

---

## 6. Kafka and Messaging

- Explain Kafka partitions, offsets, consumer groups, and rebalancing.
- How do you choose the number of partitions?
- How do you guarantee ordering where the business requires it?
- What does "exactly once" mean in Kafka, and what doesn't it guarantee?
- How would you design retry and dead-letter handling?
- How do you safely evolve an event schema?
- Kafka consumer lag is continuously increasing. How would you investigate it?
- A poison message repeatedly crashes your consumer. How would you design around this?

---

## 7. Database Architecture

- SQL versus NoSQL: how do you make the decision?
- Explain optimistic and pessimistic locking.
- How would you prevent two concurrent requests from purchasing the last available item?
- Explain database connection pooling. What happens when the pool is exhausted?
- What causes the N+1 query problem in Hibernate/JPA?
- When would you deliberately avoid JPA/Hibernate?
- Explain database sharding and its trade-offs.
- How would you implement caching with Redis while preventing stale data?
- Explain the cache-aside pattern.
- What is a cache stampede, and how would you mitigate it?

---

## 8. Kubernetes, Cloud and Deployment

- Explain Kubernetes readiness, liveness, and startup probes.
- A Java pod is repeatedly OOMKilled. How would you investigate it?
- How should JVM heap limits relate to Kubernetes container memory limits?
- Horizontal versus vertical scaling: when would you choose each?
- Explain blue-green versus canary deployments.
- How would you implement zero-downtime deployment for an API?
- How would you autoscale a Kafka consumer application?
- CPU utilization is only 20%, but requests are timing out. Why might adding more pods not solve the problem?

---

## 9. Security

- Explain OAuth 2.0 and OpenID Connect.
- JWT versus opaque tokens: what are the trade-offs?
- Where should authentication and authorization occur in a microservices architecture?
- How would you implement service-to-service authentication?
- How do you manage secrets in Kubernetes/cloud environments?
- What controls would you introduce for OWASP risks such as SQL injection and SSRF?
- How would you design audit logging without exposing sensitive information?

---

## 10. Observability and Production Troubleshooting

- Explain the difference between logs, metrics, and traces.
- Which metrics would you define for a critical Java API?
- What are p50, p95, and p99 latency, and why can averages be misleading?
- Production latency increased after a deployment. How would you isolate the cause?

**Scenario:** One microservice has:

| Metric | Value |
|--------|-------|
| CPU | 30% |
| Memory | 60% |
| p95 latency | 4 seconds |
| DB connection pool | 100% utilized |

> What would you investigate first, and why?

---

## Five Must-Ask Questions (60-minute format)

These five questions expose architectural depth quickly.

### 1. Distributed Transaction

> Order Service updates its database and then publishes an event to Kafka. The DB commit succeeds, but Kafka publishing fails. How would you redesign this?

Look for: transactional outbox, CDC, retries, idempotency, duplicate handling, and delivery semantics.

### 2. Production Incident

> A Spring Boot API's p99 latency jumps from 300 ms to 8 seconds while CPU remains below 30%. How would you diagnose it?

Look for: downstream latency, connection pools, thread pools, GC, database behavior, network calls, traces, and saturation — not just "add pods."

### 3. Architecture Decision

> Would you build a new application as a modular monolith or microservices? Explain how you would decide.

Look for: trade-off reasoning, not "microservices are scalable."

### 4. Reliability

> Payment succeeded, but your service timed out before receiving the response. The client retries. How do you prevent duplicate payment?

Look for: business idempotency keys, persistent request/result state, provider reconciliation, retry semantics, and handling of uncertain outcomes.

### 5. Architecture Exercise

> Design a Java platform capable of processing millions of transactions per day. Draw the architecture and then explain how the design behaves when the database, Kafka, an external API, or an entire availability zone fails.

This single question can expose knowledge of Java, Spring Boot, Kafka, databases, Kubernetes, cloud architecture, resilience, observability, security, and distributed-system trade-offs.

---

## Suggested Scoring Rubric

For each major architecture question, use a **0–4 evidence-based rubric**:

| Score | Meaning |
|-------|---------|
| **0** | Doesn't understand the concept |
| **1** | Knows terminology |
| **2** | Can explain the mechanism |
| **3** | Can apply it to the scenario and identify trade-offs |
| **4** | Can reason through failure modes, alternatives, operational implications, and justify the final choice |

> For an Architect role, put less weight on memorizing annotations/APIs and much more weight on the candidate's ability to say **"I would choose X instead of Y because..."** — then defend that choice when requirements or failure conditions change.
