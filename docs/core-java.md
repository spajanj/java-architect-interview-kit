# Core Java and JVM

[← Home](index.md) | [Spring Boot →](spring-boot.md)

---

- Explain the JVM memory model: heap, stacks, metaspace, and direct/off-heap memory.
- How does Java Garbage Collection work? Compare G1 GC, ZGC, and Shenandoah. When would you consider each?
- A Java service periodically experiences long GC pauses. How would you diagnose the problem?
- Explain `volatile`, `synchronized`, `AtomicInteger`, and locks. When would you use each?
- What does *happens-before* mean in the Java Memory Model?
- Compare `HashMap`, `ConcurrentHashMap`, and immutable maps in concurrent applications.
- Explain Java's `CompletableFuture`. What problems can arise from using the common ForkJoinPool?
- What are virtual threads, and where would you use or avoid them?
- How would you diagnose a memory leak in a production JVM?
- What Java/JVM metrics would you expose through tools such as Micrometer, Prometheus, Grafana, or Datadog?

---

## Architect-Level Follow-Up

> Your application works perfectly under functional testing but latency jumps dramatically at 1,000 concurrent requests. Walk me through your investigation.
