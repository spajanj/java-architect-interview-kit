# Architecture and System Design

[← Spring Boot](spring-boot.md) | [Home](index.md) | [Scenario →](scenario.md)

> These questions should carry significant weight for an architect role.

---

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
