# Backends for Frontends (BFF) Pattern


## 1. Context

When you have multiple types of clients—such as mobile, web, and IoT—that consume your backend services, you may find that each client has different needs and constraints.


## 2. Problem

How can you provide a tailored API experience for different client types without overcomplicating the backend services?


## 3. Solution

The Backends for Frontends Pattern suggests creating separate backend services that are specifically tailored for the needs of each type of client. Each BFF acts as an intermediary between the client and the core backend services, translating or aggregating as necessary.


## 4. Benefits

- **Optimized Client Experience**: Tailored APIs mean clients get exactly what they need and nothing they don't.

- **Simplified Clients**: Clients can be simplified as some of the business logic can be handled in the BFF.

- **Isolation**: Changes in one BFF are less likely to impact other types of clients.


## 5. Drawbacks

- **Increased Complexity**: Managing multiple BFFs can increase the complexity of your architecture.

- **Code Duplication**: Shared logic across BFFs can result in duplicated code.


## 6. Alternative Solutions

- **Graphql**: Allows clients to query exactly what they need, though it may not handle all the client-specific logic that can be dealt with in a BFF.

- **Versioned APIs**: Different API versions can be exposed for different clients, though this may not provide as tailored an experience as BFFs.
