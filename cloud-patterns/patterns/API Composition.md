# API Composition Pattern

The API Composition pattern is crucial for aggregating multiple services in a cohesive and efficient manner.


## 1. Context

In a microservices architecture, a client often needs data that is owned by multiple services. Fetching this data in multiple network calls can be inefficient and can lead to higher latencies.


## 2. Problem

How can a client obtain a composed, meaningful view of data that resides in multiple, independent services without putting the burden of data gathering and composition on the client itself?


## 3. Solution

The API Composition pattern suggests creating a service (or extending an existing service like an API Gateway) to aggregate the required data from multiple services. This service takes a client request, interacts with the necessary services, performs data composition, and returns a unified view to the client.


## 4. Benefits

- **Reduced Latency**: Fewer round-trips are needed between the client and the server, thereby reducing network latency.

- **Decoupling**: Clients are isolated from the details of the underlying services, making it easier to modify or extend services.

- **Optimized Data Retrieval**: Can fetch only the necessary data, avoiding over-fetching or under-fetching of data.

- **Centralized Logic**: Composing data at a central place can make it easier to manage business logic.


## 5. Drawbacks

- **Increased Complexity**: The composition service itself can become a complex component to manage and maintain.

- **Single Point of Failure**: If not designed for fault tolerance, the API composer can become a bottleneck or point of failure.

- **[Data Consistency](./Data Consistency.md)**: As the composer fetches data from multiple services, there could be consistency issues if the data changes in between fetch operations.


## 6. Alternative Solutions

- **Client-Side Composition**: The client could make multiple requests to individual services and perform the composition. However, this offloads complexity to the client.

- **CQRS with Materialized Views**: For read-heavy systems, one could use a separate model to handle reads, where data is already composed into a useful format.
