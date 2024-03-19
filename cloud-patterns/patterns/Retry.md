# Retry Pattern


## 1. Context

In distributed systems, transient failures like network glitches, temporary service unavailability, or timeouts can occur. These are often self-correcting issues that might be resolved without human intervention.


## 2. Problem

How can you make a system more resilient to transient failures, ensuring that it does not fail immediately but instead tries to complete the operation that caused the failure?


## 3. Solution

The Retry Pattern suggests that an operation should be retried if it fails due to transient conditions. This can be implemented with a fixed number of retries, with an increasing delay between each retry (often called "backoff"), or until a certain condition is met.


## 4. Benefits

- **Increased Resilience**: Improves the system's ability to handle transient failures without requiring immediate human intervention.

- **Better Resource Utilization**: Sometimes resources become temporarily unavailable; retrying helps in utilizing them as soon as they become available.

- **Improved User Experience**: Users may not even notice that a transient fault occurred if the retry is successful.


## 5. Drawbacks

- **Resource Intensiveness**: Constant retries can put additional load on a system, possibly making a bad situation worse.

- **Increased Latency**: Each retry attempt adds to the latency of the operation.

- **Complexity**: Implementing a robust retry mechanism that considers varying types of failures can be complex.


## 6. Alternative Solutions

- **[Circuit Breaker](./Circuit%20Breaker.md)**: Can be used to stop all attempts to invoke a service that is likely to fail, allowing it to recover.

- **[Timeout and Retries](./Timeout%20and%20Retries.md)**: Can be combined with the Retry Pattern to ensure that each retry is time-bounded.


## 7. Tools

- Retrying library for Python [tenacity.readthedocs.io](http://tenacity.readthedocs.io)

- Production-grade retries for Python [stamina.hynek.me/](https://stamina.hynek.me/)
