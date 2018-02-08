---
layout: post
title: Resilient architecture
categories:
  - software-development
date: 2018-02-08
---

Building services with resilience is the new key of software development.

## Principles

Few principles might help a lot building resilient architectures. The first one is the *Event-Driven Architecture* where circuit breaker are managing the pressure on the platform. With this architecture, non critical processes can be delayed until system goes green and circuit breaker are in charge to dilute input requests to backward services.

### Idempotency

The first rule to implement on any action of your system is idempotency. Idempotency is the mechanism that makes that the reception of the same action several times are leading to the exact same state.

Make your payload unique, one from each other, with uniquely structures or *universal unique id*. This is true for your HTTP Requests as well as any message published on message brokers. Ensure this assertion true from the very first line of your code to the last one.

### Fail fast

As the availability of a system is given by [^1]:

$$ AVAILABILITY = \frac{MTTF}{MTTF + MTTR}$$

where $MTTF$ is the mean time to failure and $MTTR$ is the mean time to recovery ; it is important to recover blazing fast and thus send failure fast in order to the supervision layer to boot new services as soon as possible.

In other words, crash fast. Do not retry requests in failure but answer fast that you failed. This is allowing the client of your service to find quickly the most efficient fallback or to fail fast in turn.

If you lose connection to a critical service such as your database or message broker: crash.

### Concurrence

This is a consequence of the *idempotency* principle, duplicating the same action on several systems is drastically reducing the $MTTF$. The same action must then lead to the same result.

### Fault tolerance

In some situations, data available in different systems are not consistent. There, reconciliation algorithms such as byzantine fault tolerance [^2] algorithms are required to choose the correct response value and identify possible service in error.

### health check

Because your service is deployed in a modern supervised system, it must be monitored efficiently. The most evident way to do this for web servers is to expose a non authenticated route at the root level `/heartbeat` or `/healtz`, and simply answer the HTTP status code 200.

For workers, updating regularly a file and checking its last updated date will allow you to check that your system is still alive.

---

[^1]: [Patterns of resilience](https://www.slideshare.net/ufried/patterns-of-resilience)
[^2]: [Byzantine fault tolerance](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance)
