# Choreography Pattern


## 1. Context

In a microservices architecture where you have multiple services that need to collaborate to fulfill business requirements, centralized orchestration can become a bottleneck or a single point of failure.


## 2. Problem

How do you coordinate multiple services in a loosely-coupled way, without introducing a centralized orchestrator that could become a bottleneck or single point of failure?


## 3. Solution

The Choreography Pattern proposes that each service involved in the operation knows exactly what its responsibilities are and what subsequent steps to trigger. Services listen for specific events and react based on them, without requiring a centralized coordinator.


## 4. Benefits

- **Decentralization**: Avoids the bottleneck of a single orchestrator.

- **Loose Coupling**: Services are not tightly coupled to a specific workflow.

- **Scalability**: Easier to scale individual components independently.


## 5. Drawbacks

- **Complexity**: The lack of centralized control can make the system harder to understand or debug.

- **Eventual Consistency**: As services are loosely coupled and react to events, consistency can be a concern.


## 6. Alternative Solutions

- **[Saga](./Saga.md)**: Provides a way to manage long-running transactions and can include compensating transactions but is often more centralized.

- **Orchestration**: Using a centralized orchestrator for complex workflows, accepting the trade-offs of tighter coupling and potential bottlenecks.
