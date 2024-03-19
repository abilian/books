# Saga Pattern

The "Saga" pattern is valuable design pattern for managing processes and transactions in a microservices architecture.


## 1. Context

In a microservices architecture where each service has its own database, managing distributed transactions becomes complex. Unlike in a monolithic system, you can't rely on ACID transactions to maintain consistency across multiple services.


## 2. Problem

How do you maintain data consistency across multiple services in a microservices architecture, especially when each service manages its own database? Rolling back transactions becomes a challenge because each service may have already committed its own local transactions.


## 3. Solution

The Saga pattern defines a long-lived transaction as a sequence of local transactions, each executed within its respective service. If a local transaction fails, the Saga executes compensating transactions to undo the impact of the preceding transactions, thereby ensuring eventual consistency.

A Saga can be orchestrated either by a central coordinator or choreographed through events or a combination of both.


## 4. Benefits

- **[Data Consistency](./Data Consistency.md)**: Helps maintain eventual consistency across multiple services.

- **Failure Isolation**: If one step fails, compensating transactions can be triggered to roll back the preceding steps.

- **Flexibility**: Allows you to build complex, business-level transactions out of simpler, individual transactions.

- **Decoupling**: Each service can maintain its own local transaction, contributing to loose coupling.


## 5. Drawbacks

- **Complexity**: Implementing Saga and compensating transactions can be complex.

- **Latency**: Waiting for the completion of multiple local transactions can add latency.

- **Eventual Consistency**: Strong consistency is not guaranteed; the system reaches eventual consistency after all compensating transactions have completed.


## 6. Alternative Solutions

- **Two-Phase Commit (2PC)**: A coordinator ensures that all services commit or roll back their transactions, but this can lead to resource locking and reduced availability.

- **Local Transactions**: Using only local transactions would mean that the system can become inconsistent if not carefully managed.
