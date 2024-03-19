# Ambassador Pattern


## 1. Context

In microservices architectures, services often need to communicate with external resources like databases or third-party services. This interaction could involve retries, timeouts, and other complexities that are not core to the service's main responsibility.


## 2. Problem

How can you offload and centralize common connection-related tasks from individual services to make them more focused and easier to manage?


## 3. Solution

The Ambassador Pattern involves creating a helper service, known as an ambassador, to handle all communication with external resources. This ambassador sits as a [Sidecar](./Sidecar.md) to the main service and handles tasks like connection pooling, retries, circuit breaking|Circuit Breaker, and timeouts, thus freeing the main service to focus on its core logic.


## 4. Benefits

- **Separation of Concerns**: The main service can focus on business logic, while the ambassador handles external communications.

- **Reusable Components**: The ambassador can be reused across multiple services, promoting consistency.

- **Easier Monitoring and Logging**: Centralizing external communication through an ambassador can simplify the task of monitoring and logging network activities.


## 5. Drawbacks

- **Additional Complexity**: Introducing another component into the architecture adds complexity in terms of deployment and management.

- **Potential Performance Overhead**: If not implemented efficiently, the ambassador can introduce latency into the system.


## 6. Alternative Solutions

- **Library-based Approaches**: Instead of a separate service, a shared library can offer similar functionalities but must be implemented in each service.

- **[API Gateway](./API Gateway.md)**: A centralized API Gateway could potentially handle some of the responsibilities of an ambassador but at the cost of making the architecture less decentralized.
