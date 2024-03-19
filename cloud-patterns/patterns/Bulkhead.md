# Bulkhead Pattern


## 1. Context

In a distributed system, especially in microservices architectures, services often rely on each other for functionality. When one service becomes a bottleneck, it has the potential to affect the entire system, causing widespread outages or degraded performance.


## 2. Problem

How can you prevent failures in one part of a system from cascading to other parts, thereby ensuring that a failure in one component doesn't bring down the whole system?


## 3. Solution

The Bulkhead Pattern segregates services and resources into isolated "compartments" or "bulkheads," similar to the watertight compartments in a ship. If a failure occurs in one bulkhead, it's contained and doesn't affect the others. Resources are allocated so that no single point of failure will consume all available resources.


## 4. Benefits

- **Fault Isolation**: Failures are isolated to individual bulkheads, minimizing the impact on the entire system.

- **Resource Optimization**: Helps in better resource allocation by segregating the system into different parts.

- **Improved Resilience**: Enhances the system's ability to continue functioning even when some components fail.


## 5. Drawbacks

- **Resource Allocation Challenge**: Requires careful planning to allocate resources efficiently across bulkheads.

- **Increased Complexity**: Introduces an additional layer of complexity in system architecture.

- **Potential Underutilization**: Allocating resources to a bulkhead that is not under load can lead to resource wastage.


## 6. Alternative Solutions

- **Rate Limiting**: Controls the number of requests to prevent overload but does not isolate failures.

- **[Circuit Breaker](./Circuit%20Breaker.md)**: Prevents failure cascade but also doesn’t offer resource isolation like bulkheads.
