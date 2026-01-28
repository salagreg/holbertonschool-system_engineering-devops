<img width="389" height="578" alt="Capture d’écran 2026-01-28 à 11 45 31" src="https://github.com/user-attachments/assets/4e1c8015-0dae-4a6e-ba6a-db0726efff79" />


Infrastructure Explanation:

Why Add a Load Balancer?

The load balancer (HAProxy) is added to:

- Distribute incoming traffic across multiple servers

- Improve availability

- Reduce the risk of overloading a single server

Without a load balancer, all traffic would converge on a single server, creating a single point of failure.

----------------------------------------------------------------------

Why Add Multiple Servers?

We add two servers to:

- Handle higher incoming traffic

- Improve reliability

- Allow one server to fail while the other continues to process requests

Each server contains:

- A web server (Nginx)

- An application server

- The application code

- A database instance

----------------------------------------------------------------------

Load Balancer Algorithm ?

The load balancer is configured with a Round Robin algorithm.

How it Works:

Each new request is sent to the next server in the list.

Traffic is distributed evenly.
Simple and efficient for servers of similar capacity.

----------------------------------------------------------------------

Active-active vs active-passive configuration ?

This infrastructure uses an active-active configuration.

Active-active:

Both servers handle traffic simultaneously.

Better performance and optimized resource utilization.

Active-passive:

One server is active.

The other is in standby mode and is only used if the first one fails.

----------------------------------------------------------------------

Primary-replica database cluster operation ?

The database is configured according to a primary-replica architecture.

The primary database:

- handles all write operations (INSERT, UPDATE, DELETE).

The replicated database:

- receives data from the primary database via replication.

- It is primarily used for read operations.

- Replication is generally asynchronous.

----------------------------------------------------------------------

Difference between the primary and replicated databases for the application ?

The application:

- writes data to the primary database

- reads data from the replicated database (or the primary database if necessary)

- This improves performance and scalability for read-intensive workloads.

----------------------------------------------------------------------

Issues related to this infrastructure ?

Single Points of Failure (SPOFs) :

The load balancer is an SPOF (single instance).

The primary database is an SPOF for write operations.

Security issues :

No firewall

No HTTPS (unencrypted data)

The databases are directly exposed on the servers.

Lack of monitoring :

No visibility into server status
No alerts in case of failure

Problems may only be detected by users.
