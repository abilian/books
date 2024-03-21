# Annex: Alternativs to uWSGI

There are no direct alternatives to uWSGI that encompass all its functionalities, but rather two complementary categories of tools:

- Web and Application Servers: This category includes tools like Gunicorn, Daphne, Nginx (with modules like Phusion Passenger for app serving), Apache with mod_wsgi, and others. These tools are focused on serving web applications by handling HTTP requests, executing application code, and delivering content to clients. They provide the direct interface between web clients (browsers) and backend applications, similar to uWSGI, particularly in environments that use specific protocols like WSGI, ASGI, etc.

- Process Managers and Supervisors: This category includes tools like PM2, Circus, Supervisor, and others. These tools are designed to manage processes, ensuring they start, remain running, and restart if they crash. They are more about maintaining application uptime and managing the application's operational aspects rather than directly handling web requests.
    
## Web and Application Servers

### Gunicorn

- **Focus**: Gunicorn is a Python WSGI HTTP Server for UNIX systems. It's designed to serve web applications using the WSGI standard, which is widely used in the Python ecosystem, particularly with frameworks like Flask and Django.
- **Features**: Gunicorn excels in simplicity and speed, offering straightforward deployment for WSGI applications. It supports worker processes for handling requests and is compatible with various web frameworks in Python.
- **Use Case Comparison**: Gunicorn is specifically tailored for Python web applications, making it a direct alternative to uWSGI for Python developers seeking a lightweight, easy-to-configure option. Unlike uWSGI, it does not have built-in support for other languages or protocols.

Link: <https://gunicorn.org/>

### Daphne

- **Focus**: Daphne is an HTTP, HTTP2, and WebSocket protocol server for ASGI and ASGI-HTTP, the asynchronous standard interface for Python applications, offering high performance for Django Channels and other ASGI applications.
- **Features**: It supports asynchronous request handling, making it suitable for WebSockets, long polling, and other scenarios that require maintaining open connections.
- **Use Case Comparison**: Daphne serves a niche within the Python community, particularly for applications requiring asynchronous capabilities. While uWSGI supports async modes and protocols beyond WSGI, Daphne is a more focused choice for ASGI applications.

Link: <https://github.com/django/daphne>

### Phusion Passenger

- **Focus**: Phusion Passenger is a web and application server designed to handle multiple languages and frameworks with ease, including Ruby, Python, Node.js, and Meteor.
- **Features**: It integrates with Nginx and Apache, offers advanced process management, smart spawning, automatic scaling, and provides detailed analytics for monitoring.
- **Use Case Comparison**: Passenger is broader in language support compared to uWSGI and offers a robust solution for mixed-language environments. It's particularly favored for Ruby applications but stands as a strong contender for Python and others with its comprehensive feature set.

Link: <https://www.phusionpassenger.com/>

### Waitress

- **Focus**: Waitress is a production-quality pure-Python WSGI server for Python 2 and 3 applications. It's designed as a simple, no-frills option for serving WSGI applications.
- **Features**: Waitress is known for its straightforward implementation, compatibility with most web frameworks, and its ability to run on both Windows and UNIX systems.
- **Use Case Comparison**: Waitress is an alternative to uWSGI for developers seeking a Python-specific server that is easy to set up and deploy, especially on Windows platforms where uWSGI installation can be challenging.

Link: <https://docs.pylonsproject.org/projects/waitress/>

### Nginx

- **Focus**: Nginx is primarily a web server and reverse proxy but can serve as an application server when configured with modules like Phusion Passenger. It's known for its high performance, stability, and efficient handling of static content and load balancing.
- **Features**: Nginx excels in handling high volumes of concurrent connections with a low memory footprint, offering features like SSL/TLS termination, reverse proxying, caching, and load balancing.
- **Use Case Comparison**: While Nginx itself is not an application server, its ability to integrate with modules like Phusion Passenger allows it to serve applications directly. It's a versatile choice for serving static content and application routing but relies on external modules for application execution.

Link: <https://nginx.com> or <https://freenginx.org/>

### Apache httpd with mod_wsgi

- **Focus**: Apache httpd is a widely-used web server that, when combined with the mod_wsgi module, can host Python WSGI applications. It offers a comprehensive set of features for web hosting and application serving.
- **Features**: The combination of Apache httpd and mod_wsgi provides robustness, a wide range of HTTP features, SSL/TLS support, and extensive configurability. Apache httpd is known for its flexibility and support for a variety of modules and programming languages.
- **Use Case Comparison**: This setup is a classic and proven solution for Python applications, offering deep integration with the Apache ecosystem. It's a solid choice for environments where Apache httpd's extensive feature set and modularity are desired, contrasting with uWSGI's focus on performance and protocol support.

- Link: <https://modwsgi.readthedocs.io/>

## Process Managers and Supervisors

### PM2
 
- **Focus**: PM2 is a powerful, widely-used process manager for Node.js applications, though it can manage applications in other languages as well. It provides an easy way to manage and daemonize applications, allowing them to run in the background as services.
- **Features**: PM2 includes features such as load balancing, zero-downtime reloading, monitoring, and logging. It is particularly favored in Node.js ecosystems for its comprehensive application management capabilities.
- **Use Case Comparison**: While PM2 is not a web server or application server in the same vein as uWSGI, it's particularly useful for process management, auto-restarting crashed applications, and simplifying deployment workflows.

Link: <https://pm2.keymetrics.io/>

### Supervisor

- **Focus**: Supervisor is a client/server system that allows its users to monitor and control a number of processes on UNIX-like operating systems. It's widely used for managing server-side applications.
- **Features**: Key features include the ability to control startup and shutdown of managed processes, automatic restart of crashed or exited processes, and logging support.
- **Use Case Comparison**: Like Circus, Supervisor is focused on process management rather than serving web requests. It's useful for ensuring that uWSGI or other web application servers are automatically restarted in the event of failure.

Link: <http://supervisord.org/>

### Circus

- **Focus**: Circus is a process watcher and manager similar to Supervisor, designed to monitor and control processes and sockets. It is language-agnostic and can be used to manage any kind of process.
- **Features**: Circus offers features like process monitoring, socket serving, background process management, and graceful restarts & upgrades. It includes a command-line tool and a Python API for managing processes.
- **Use Case Comparison**: Circus is more about process management rather than directly serving web applications. It doesn't replace uWSGI's web serving capabilities but can be used alongside uWSGI to manage its processes and ensure they remain running.

Link: <https://circus.readthedocs.io/en/latest/>


### Process Compose

- **Focus**: Process Compose offers a streamlined and flexible solution for scheduling and orchestrating non-containerized applications. Designed for scenarios where Docker's complexity (e.g., managing Docker files, volumes, networks, and registries) is unwelcome, it stands out for its simplicity and reliance on a single, dependency-free binary thanks to its Go-based architecture.

- **Features**: With Process Compose, users can execute processes either in parallel or sequentially, manage process dependencies and execution order, and specify process recovery policies. It supports manual process restarts, argument passing in bash or zsh style, environment variable configuration at both the process and global levels, and detailed logging capabilities. Additional functionalities include health checks, a Terminal User Interface (TUI) or CLI modes, process forking, a REST API compliant with OpenAPI (Swagger), log caching, and the ability to act as both a server and a client. Configurability extends to shortcuts, file merging, namespaces, process replication, and foreground process execution.

- **Use Case Comparison**: Unlike docker-compose, Process Compose is tailored for managing applications without the overhead of containerization. Its configuration closely mimics docker-compose's for familiarity, but with modifications to accommodate non-containerized environments. This makes it an ideal tool for developers seeking docker-compose-like orchestration capabilities without committing to Docker's ecosystem.

Link: <https://github.com/F1bonacc1/process-compose>
