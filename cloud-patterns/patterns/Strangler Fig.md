# Strangler Fig Pattern


## 1. Context

When dealing with legacy systems that need to be replaced or upgraded, a "big bang" approach of complete replacement is often risky, expensive, and disruptive.


## 2. Problem

How can you incrementally replace or upgrade an existing system with minimal risk and disruption to ongoing operations?


## 3. Solution

The Strangler Fig Pattern involves building a new system around the boundaries of the existing one. As features from the old system are replaced, the new system takes over those responsibilities, strangling the old system gradually until it is fully replaced. This often involves routing mechanisms that direct requests either to the new or the old system based on what parts have been replaced.


## 4. Benefits

- **Incremental Migration**: Allows for gradual replacement of the legacy system, mitigating risks associated with big changes.

- **Flexibility**: Enables teams to test new features or components incrementally before fully committing to the new system.

- **Business Continuity**: Ensures that the existing system remains operational during the transition, thus maintaining business processes and user experience.


## 5. Drawbacks

- **Complexity**: Initial setup can be complex because both systems have to coexist and be compatible during the transition.

- **Potential for Tech Debt**: If not executed carefully, remnants of the old system might remain, leading to technical debt.


## 6. Alternative Solutions

- **[Blue-Green Deployment](./Blue-Green Deployment.md)**: Useful for releasing a new version of an application but doesn’t provide the gradual replacement that Strangler Fig offers.

- **Feature Flags**: Enables toggling features on and off but generally applies to individual features rather than entire systems.
