# Web Application Firewall (WAF) Pattern


## 1. Context

In cloud and microservices architectures, web applications are often the front door to your business logic and data. These applications are exposed to the internet, making them potential targets for a variety of cyber attacks like SQL injection, XSS, and CSRF.


## 2. Problem

How do you protect your web applications from a myriad of web-based attacks without affecting legitimate traffic and without requiring changes to the application code?


## 3. Solution

The Web Application Firewall (WAF) Pattern involves deploying a WAF that sits between the web application and the internet. The WAF inspects and filters incoming HTTP/HTTPS requests based on a set of rules designed to identify and mitigate various web application attack vectors.


## 4. Benefits

- **Real-Time Protection**: Offers real-time protection against known and emerging threats.

- **Rule-Based Security**: Allows for custom rule configurations tailored to your application's specific needs.

- **Monitoring and Logging**: Provides detailed logs and metrics, which can be useful for compliance and auditing.


## 5. Drawbacks

- **False Positives/Negatives**: Incorrectly configured or outdated rules can either block legitimate traffic or allow malicious traffic.

- **Performance Impact**: Adds an additional layer that can introduce latency.


## 6. Alternative Solutions

- **Application-Level Security**: Embedding security checks within the application itself, although this may lead to duplicated effort across multiple apps.

- **Network-Level Security**: Relying on lower-level network firewalls, but these won't have the application-level inspection capabilities of a WAF.

## References

- <https://lab.abilian.com/Tech/Security/WAF/>
