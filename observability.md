---
layout: default
title: Observability and Production Troubleshooting
permalink: /observability
---

# Observability and Production Troubleshooting

- Explain the difference between logs, metrics, and traces.
- Which metrics would you define for a critical Java API?
- What are p50, p95, and p99 latency, and why can averages be misleading?
- Production latency increased after a deployment. How would you isolate the cause?

---

## Scenario

One microservice has:

| Metric | Value |
|--------|-------|
| CPU | 30% |
| Memory | 60% |
| p95 latency | 4 seconds |
| DB connection pool | 100% utilized |

> What would you investigate first, and why?
