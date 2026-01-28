
<img width="487" height="558" alt="Capture d’écran 2026-01-28 à 13 53 48" src="https://github.com/user-attachments/assets/c2d5f9e3-701c-4e30-8ab9-dc8b61b8eed1" />

Infrastructure Explanation:

Why Add Firewalls ?

Firewalls are used to control and filter network traffic.

In this infrastructure:

Firewall 1 protects the load balancer from the internet.

Firewall 2 protects application servers from external access.

Firewall 3 protects the database from unauthorized access.

Firewalls reduce the attack surface and prevent direct access to sensitive components.

--------------------------------------------------------------------------------

Why is Traffic Served via HTTPS ?

The HTTPS protocol encrypts communication between the user and the infrastructure.

This ensures:

data confidentiality;

the integrity of requests and responses;

website authentication via an SSL certificate.

Without HTTPS, data could be intercepted or modified by attackers.

--------------------------------------------------------------------------------

SSL Certificate and SSL Termination ?

An SSL certificate is installed on the load balancer. The load balancer:

decrypts incoming HTTPS traffic

forwards unencrypted HTTP traffic internally

This approach simplifies certificate management but has some limitations (explained later).

--------------------------------------------------------------------------------

Why Add Monitoring ?

Monitoring allows you to:

monitor system health

detect failures as early as possible

analyze performance

trigger alerts automatically

Without monitoring, problems are only discovered when users complain about them.

--------------------------------------------------------------------------------

How Monitoring Tools Collect Data ?

Each server runs a monitoring agent.

This agent:

collects metrics (CPU, memory, disk, network)

collects logs and application data

sends the data to a centralized monitoring service (e.g., Sumo Logic)

This provides real-time visibility into the infrastructure.

--------------------------------------------------------------------------------

Monitoring Web Server Requests Per Second (QPS) ?

To monitor the web server's QPS (requests per second):

Enable access logs or Nginx metrics

Configure the monitoring agent to analyze these logs

Extract the number of requests per second

View and configure alerts for abnormal values

--------------------------------------------------------------------------------

Issues related to this infrastructure :

SSL Termination at the Load Balancer Level ?

Terminating SSL at the load balancer level means that:

Traffic between the load balancer and the servers is not encrypted

Internal attackers could intercept sensitive data

A more secure configuration would use end-to-end encryption.


Single MySQL Server for Write Operations ?

A single MySQL server handles write operations.

Problems:

Single point of failure

Limited write scalability

A failure results in a service interruption

A more robust configuration would use clustering or database partitioning.


Servers with identical components ?

Having the web server, application server, and database on the same machines:

Reduces fault isolation

Complicates scaling

Increases resource contention

In production systems, these components are typically separated by role.
