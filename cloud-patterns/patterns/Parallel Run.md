# Parallel Run Pattern


## 1. Context

This pattern is particularly useful when migrating from an old system to a new one, or when introducing substantial changes to an existing application. It's often employed in environments where system correctness and data consistency are critical, such as financial systems, healthcare, and other regulated industries.


## 2. Problem

When introducing a new system or a major update to an existing one, there's a risk of introducing errors, inconsistencies, or performance issues. Traditional testing environments may not capture all the nuances of a live system. How can we ensure that the new system behaves as expected when compared to the old one, especially under real-world conditions?


## 3. Solution

Run the old and new systems in parallel for a predetermined period or until confidence is gained in the new system's behavior. Both systems operate on real-world data but only the old system's output is used for official or critical tasks. The output of the new system is used solely for validation against the old system. Differences are logged and analyzed to understand any discrepancies and to adjust the new system accordingly.


## 4. Benefits

- **Reduced Risk**: Allows for real-world testing without affecting the business logic or data integrity of the existing system.

- **Confidence Building**: Running both systems simultaneously and comparing their outputs can significantly increase confidence in the new system before making it the system of record.

- **Issue Identification**: Helps in uncovering subtle issues, data inconsistencies, or performance problems that might not be evident in a staging environment.

- **Graceful Transition**: Provides a safe pathway for migrating from an old system to a new one, allowing for iterative fixes and gradual cutover.


## 5. Drawbacks

- **Resource Intensive**: Requires extra computational and human resources to run both systems simultaneously and to analyze the results.

- **Complexity**: Managing the parallel run can be complex, requiring synchronization of data inputs and careful monitoring to compare outputs.

- **Data Skew**: There could be scenarios where the new system behaves differently because it has not been "warmed up" like the old system, leading to potential skew in comparative analysis.

- **Time-consuming**: Depending on the complexity of the systems and the degree of confidence required, the parallel run could take a substantial amount of time.


## 6. Alternative Solutions

- **A/B Testing**: Allows for comparing two versions but generally not suited for system-wide changes or where data consistency is critical.

- **Shadow Testing**: Similar to a parallel run but only involves sending requests to the new system for testing purposes without comparing outputs in real-time.
