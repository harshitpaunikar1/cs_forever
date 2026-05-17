Title: Monitors and health checks Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/load-balancing/concepts/health-checks/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:27+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Monitors and health checks

There's more to a load balancer than just distributing traffic, however.

After all, what good would it be if your load balancer and pools send a request to a server that's offline? Or one that's already overloaded with traffic? Ideally, your load balancer should only forward requests that a server can take care of.

That's where another part of the load balancing equation comes in: monitors and health checks.

flowchart RL accTitle: Load balancing monitor flow accDescr: Monitors issue health monitor requests, which validate the current status of servers within each pool. Monitor -- Health Monitor ----> Endpoint2 Endpoint2 -- Response ----> Monitor subgraph Pool Endpoint1((Endpoint 1)) Endpoint2((Endpoint 2)) end

A monitor issues health checks periodically to evaluate the health of each server within a pool.

Requests issued by a monitor at regular interval and â depending on the monitor settings â return a **pass** or **fail** value to make sure an endpoint is still able to receive traffic.

Each health monitor request is trying to answer two questions:

**Is the endpoint offline?**: Does the endpoint respond to the health monitor request at all? If so, does it respond quickly enough (as specified in the monitor's**Timeout**field)?**Is the endpoint working as expected?**: Does the endpoint respond with the expected HTTP response codes? Does it include specific information in the response body?

If the answer to either of these questions is "No", then the endpoint fails the health monitor request.

This system of request and response ensures that a load balancer knows which servers can handle incoming requests.
