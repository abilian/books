# Optimistic Locking Pattern


## 1. Context

Optimistic locking is particularly useful in high-concurrency, distributed systems where performance and scalability are key concerns. It's often employed in modern web applications, RESTful APIs, and microservices-based architectures where multiple clients might attempt to update the same resource nearly simultaneously but conflicts are relatively rare.


## 2. Problem

Ensuring consistent updates to shared resources in a distributed or concurrent system is challenging. Traditional locking mechanisms can be a bottleneck, causing performance degradation and reducing system availability. How can we allow for high concurrency while still preventing conflicts when updating shared resources?


## 3. Solution

Optimistic locking avoids locks and instead relies on conflict detection. It allows multiple actors to perform reads and writes in parallel. Each actor retrieves a version of the resource and proceeds to make changes locally. When an actor tries to persist the changes, the system checks that the resource's version has not changed since the actor retrieved it. If there is no version conflict, the changes are committed, and the version is updated. Otherwise, the transaction is aborted, and the actor must retry the operation, typically after fetching the updated resource.


## 4. Benefits

- **High Concurrency**: Optimistic locking allows multiple actors to read and modify resources without waiting for locks, offering a more scalable solution for high-concurrency environments.

- **Increased Throughput**: Since most operations proceed without waiting, the system can achieve higher throughput compared to pessimistic locking strategies.

- **Simplicity**: Avoids the complexities and pitfalls associated with managing locks, such as deadlocks or lock contention.

- **Fine-Grained Control**: Versioning can be implemented at the level of individual fields or components of a resource, allowing for more fine-grained conflict resolution.


## 5. Drawbacks

- **Conflict Overhead**: When conflicts occur, the transaction has to be retried, which could involve refetching the resource, recomputing changes, and attempting to commit again, adding latency and computational overhead.

- **Stale Reads**: There's a risk that an actor might read stale data if another actor commits changes in the interim between read and commit.

- **Complexity for End Users**: Depending on the application, the onus of resolving conflicts and retrying operations may be passed onto the end-users, complicating their interaction with the system.


## 6. Alternative Solutions

- **[Pessimistic Locking](./Pessimistic Locking.md)**: Offers stronger guarantees at the cost of reduced concurrency and potential for deadlocks.

- **CRDTs or Operational Transformation**: These can resolve conflicts automatically but come with their own complexities and may not be suitable for all kinds of data or operations.

- **Two-Phase Commit**: Provides strong consistency guarantees but at the cost of higher latency and complexity, making it unsuitable for many internet-scale applications.
