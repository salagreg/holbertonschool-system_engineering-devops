
<img width="435" height="721" alt="Capture d’écran 2026-01-28 à 17 19 33" src="https://github.com/user-attachments/assets/7e87db1a-3331-4fb7-9ea9-6c8a6a2beffc" />

Infrastructure Explanation:

Why add a clustered load balancer?

We use two HAProxy load balancers in a cluster to:

- Avoid a Single Point of Failure
- Ensure high availability
- Maintain service continuity if one load balancer fails

The cluster enables state synchronization between the two load balancers.

--------------------------------------------------------------------------

Why separate the Web Server, Application Server, and Database?

Each component is placed on its own server to:

- Separate responsibilities
- Improve security
- Facilitate maintenance
- Enable independent scaling

This is a layered architecture, more robust than a single server.

--------------------------------------------------------------------------

Why add firewalls?

Firewalls are used to filter network traffic:

FW1: Protects the infrastructure from the internet

FW2: Isolates the web/app layer

FW3: Protects the database

They reduce the attack surface and prevent unauthorized access.

--------------------------------------------------------------------------

Why add monitoring?

Monitoring allows you to:

- Monitor the status of servers
- Detect failures
- Measure performance
- Trigger alerts

Each component has a monitoring agent.

--------------------------------------------------------------------------

Limitations and problems of this infrastructure:

SSL termination at the load balancer:

- Internal traffic is not encrypted
- Risk in case of compromise of the internal network

Single database for writes:

- Single Point of Failure
- No write scalability

Strict separation but still coupled:

- Each layer depends on the previous one
- Database failure = global failure
