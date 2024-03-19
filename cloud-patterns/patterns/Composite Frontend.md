# Composite Frontend Pattern


## 1. Context

In a microservices architecture, frontend development can also become complex due to multiple services contributing to the UI. Managing this complexity and ensuring a seamless user experience is crucial.


## 2. Problem

How do you maintain a cohesive frontend experience while benefiting from the modularity and independence offered by a microservices architecture?


## 3. Solution

The Composite Frontend Pattern suggests creating a unified frontend that aggregates and composes UI components from multiple frontend microservices. This could be achieved through various techniques like server-side includes, JavaScript frameworks, or edge-side includes.


## 4. Benefits

- **Modularity**: Allows different teams to work on different aspects of the frontend independently.

- **Reuse**: UI components can be reused across different parts of the application or even different applications.

- **Flexibility**: Enables the frontend to evolve independently of backend services, and vice versa.


## 5. Drawbacks

- **Latency**: Aggregating content from multiple services could introduce latency.

- **Complexity**: Managing the composition and ensuring a smooth user experience can be complex.


## 6. Alternative Solutions

- **Single Page Applications (SPA)**: An SPA could interact with multiple services via APIs, but this places more logic on the client side.

- **[Backends for Frontends](./Backends for Frontends.md)**: Tailoring backend services for specific frontend experiences, though this may lead to backend duplication.
