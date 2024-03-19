# Database-per-Service Pattern


## 1. Context

In a microservices architecture, each service often requires a different data model, and different services may have different data storage requirements in terms of performance, consistency, and availability. Coupled with the need for each service to be independently deployable, scalable, and maintainable, there arises a necessity to manage the databases of each service in isolation.


## 2. Problem

In a monolithic architecture, services usually share a single database schema, which creates a strong coupling between different parts of the application. As applications scale, or as more services are added, the shared database becomes a bottleneck, limiting the ability to scale, deploy, or modify individual services. Additionally, schema changes in a shared database could potentially break multiple services, making it hard to isolate changes and risks.


## 3. Solution

Assign a dedicated database to each microservice. This allows each service to manage its own database schema and storage mechanisms. The database can be of any type: SQL, NoSQL, in-memory, etc., as long as it fulfills the particular requirements of the service. Data consistency between the services is usually maintained using eventual consistency through mechanisms like event sourcing or message queues.


## 4. Benefits

- **Decoupling**: Each service is decoupled from others, making it easier to make changes, deploy, and scale services independently.

- **Flexibility**: Different services can use different types of databases that are best suited for their specific needs.

- **Fault Isolation**: Issues in one service's database are unlikely to directly affect other services.

- **Optimized Performance**: Since each service is using its own database, it can be optimized for the specific type of queries and operations that the service performs.


## 5. Drawbacks

- **[Data Consistency](./Data Consistency.md)**: Ensuring data consistency across services can be challenging and usually requires additional coordination.

- **Data Duplication**: There might be cases where some data needs to be duplicated across multiple services.

- **Operational Complexity**: Managing multiple databases increases operational overhead, including backups, monitoring, and updates.

- **Data Joins**: Performing operations that would typically involve database joins becomes more complex and usually has to be managed at the application level.


## 6. Alternative Solutions

- **Shared Database**: A single, shared database for all services, though this brings us back to the problems the pattern aims to solve.

- **[API Composition](./API Composition.md)**: Instead of each service owning its data, some services act as aggregators, pulling data from multiple services. However, this could create performance bottlenecks and availability issues.
