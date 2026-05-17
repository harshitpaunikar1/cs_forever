Title: Optimize caching Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/advanced/optimize-caching/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:19+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Optimize caching

The more content is cached, the fewer requests go back to your origin server (whether due to legitimate or illegitimate traffic).

A few ways to optimize Cloudflare caching include:

- Creating
[cache rules](https://developers.cloudflare.com/cache/how-to/cache-rules/)to customize the cache properties of specific HTTP requests. - Enabling the
[Tiered Cache](https://developers.cloudflare.com/cache/how-to/tiered-cache/)feature, which dramatically increases cache hit ratios. - Reviewing our other various
[configuration options](https://developers.cloudflare.com/cache/get-started/), which may vary based on your plan and application setup.
