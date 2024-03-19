# Expand and Contract (Parallel Change) Pattern


## 1. Context

This pattern is beneficial in situations where a system's data schema or interface needs to be modified while ensuring that the system remains backward-compatible. It is particularly useful in distributed systems or microservices architectures where different components may be running different versions of the software.


## 2. Problem

Changing a system's schema or interface usually involves breaking changes that can disrupt service continuity. This can lead to downtime, inconsistent data, and increased complexity in rollback strategies. How can you introduce such changes while ensuring that the existing system remains operational and backward-compatible?


## 3. Solution

Implement the change in a way that allows the new and old versions of the schema or interface to coexist. Initially, "expand" the system to support both versions. During this phase, the system writes data in both the old and new format, but reads using the old format. Once you are confident that the new schema or interface is stable and all components can handle it, you "contract" by removing support for the old version, migrating all components to use the new format, and cleaning up any old data or code paths.


## 4. Benefits

- **Backward Compatibility**: Allows the system to remain backward-compatible during the transition, reducing the risks associated with the change.

- **Smooth Transition**: Enables a phased rollout of changes, allowing for testing and gradual adoption, thus minimizing the impact of the change.

- **Simplifies Rollbacks**: Since the old version remains functional for a time, rolling back changes is simpler and less risky.

- **Facilitates Distributed Systems**: Particularly useful in microservices architectures where different services might be using different versions of an interface or schema.


## 5. Drawbacks

- **Increased Complexity**: Managing two versions simultaneously can add complexity in terms of code, database schema, and operations.

- **Resource Overhead**: Duplicate storage and additional logic to handle both versions may consume more resources, both computationally and in terms of storage.

- **Maintenance Burden**: It requires rigorous testing to ensure both old and new versions work as expected. This involves an additional layer of quality assurance and possibly more complex deployment strategies.

- **Temporal Coupling**: Until the system fully contracts to the new version, you are in a transitional state that must be carefully managed to prevent errors or data inconsistencies.


## 6. Alternative Solutions

- **Versioning**: Introduce version numbers in APIs or data schemas, but this usually results in maintaining multiple, long-lived versions.

- **Flag-based Routing**: Use feature flags to direct traffic to services running the old or new version. This, however, does not deal with data schema changes.

