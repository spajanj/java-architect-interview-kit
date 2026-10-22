---
layout: default
title: Five Must-Ask Questions
permalink: /must-ask
---

# Five Must-Ask Questions

> If you only have 60 minutes, these five questions expose architectural depth quickly.

---

## 1. Distributed Transaction

> Order Service updates its database and then publishes an event to Kafka. The DB commit succeeds, but Kafka publishing fails. How would you redesign this?

**Look for:** transactional outbox, CDC, retries, idempotency, duplicate handling, and delivery semantics.

---

## 2. Production Incident

> A Spring Boot API's p99 latency jumps from 300 ms to 8 seconds while CPU remains below 30%. How would you diagnose it?

**Look for:** downstream latency, connection pools, thread pools, GC, database behavior, network calls, traces, and saturation — not just "add pods."

---

## 3. Architecture Decision

> Would you build a new application as a modular monolith or microservices? Explain how you would decide.

**Look for:** trade-off reasoning, not "microservices are scalable."

---

## 4. Reliability

> Payment succeeded, but your service timed out before receiving the response. The client retries. How do you prevent duplicate payment?

**Look for:** business idempotency keys, persistent request/result state, provider reconciliation, retry semantics, and handling of uncertain outcomes.

---

## 5. Architecture Exercise

> Design a Java platform capable of processing millions of transactions per day. Draw the architecture and then explain how the design behaves when the database, Kafka, an external API, or an entire availability zone fails.

This single question can expose knowledge of Java, Spring Boot, Kafka, databases, Kubernetes, cloud architecture, resilience, observability, security, and distributed-system trade-offs.
