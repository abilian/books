# Pessimistic Locking Pattern


## 1. Context

In systems where multiple actors (be it users, services, or nodes) may be attempting to modify shared resources concurrently, ensuring data consistency is a challenge. Pessimistic locking is commonly employed in environments where operations are complex, long-running, and where a high degree of certainty is required that a resource will not be modified by another actor during the operation. This is often the case in traditional, monolithic applications and less latency-sensitive systems like batch processing jobs or certain kinds of databases.


## 2. Problem

In a system where multiple actors can perform actions on shared resources, there is a risk of conflicting modifications leading to inconsistent states or data corruption. How can we ensure that when one actor is modifying a resource, others are prevented from doing so?


## 3. Solution

Pessimistic locking solves this problem by ensuring exclusive access to a resource for the duration of an operation. When an actor wishes to modify a resource, it first obtains a lock. If the lock is granted, the actor proceeds with the operation and releases the lock upon completion. Any other actor attempting to access the resource while it's locked will either be blocked or will receive an error, depending on the implementation.


## 4. Benefits

- **[Data Consistency](./Data Consistency.md)**: By ensuring that only one actor can modify a resource at a given time, pessimistic locking provides a strong guarantee against data corruption.

- **Simplifies Error Handling**: There is less need for complex merge or conflict resolution logic since conflicts are prevented upfront.

- **Predictability**: Since a resource is locked for the duration of an operation, it's easier to reason about the system's behavior and ensure that transactions are completed without interruption.


## 5. Drawbacks

- **Reduced Concurrency**: Locking resources can significantly limit the system's ability to perform concurrent operations, leading to potential bottlenecks.

- **Risk of Deadlocks**: If improperly managed, acquiring multiple locks can lead to a deadlock situation where different actors are waiting for locks held by each other.

- **Latency and Timeout Issues**: Waiting for a lock to be released can introduce latency. Moreover, defining the optimal timeout duration can be challenging.

- **Resource Intensive**: Depending on the implementation, maintaining locks can consume system resources and complicate system design.


## 6. Alternative Solutions

- **[Optimistic Locking](./Optimistic Locking.md)**: Allows multiple actors to proceed with reads and writes based on versions and performs checks only at commit time to ensure no conflicts.

- **[Transactional Memory](./Transactional Memory.md)**: Allows code to be executed in a transactional context, providing automatic rollback capabilities in the event of conflicts, at the cost of additional system complexity.

- **[Event Sourcing](./Event Sourcing.md)**: By transforming operations into a sequence of immutable events, one can reconstruct the state of a resource without the need for locks, although this approach comes with its own complexities.
