Title: Proxy DNS records Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/proxy-dns-records/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:23+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Proxy DNS records

The first - and often easiest - step of DDoS protection is making sure your DNS records are [proxied](https://developers.cloudflare.com/dns/proxy-status/) through Cloudflare.

Without Cloudflare, DNS lookups for your application's URL return the IP address of your [origin server â](https://www.cloudflare.com/learning/cdn/glossary/origin-server/).

| URL | Returned IP address |
|---|---|
`example.com` | `192.0.2.1` |

When using Cloudflare with [unproxied DNS records](https://developers.cloudflare.com/dns/proxy-status/), DNS lookups for unproxied domains or subdomains also return your origin's IP address.

Another way of thinking about this concept is that visitors directly connect with your origin server.

flowchart LR accTitle: Connections without Cloudflare A[Visitor] <-- Connection --> B[Origin server]

With Cloudflare â meaning your domain or subdomain is using [proxied DNS records](https://developers.cloudflare.com/dns/proxy-status/) â DNS lookups for your application's URL will resolve to [Cloudflare anycast IPs â](https://www.cloudflare.com/ips/) instead of their original DNS target.

| URL | Returned IP address |
|---|---|
`example.com` | `104.16.77.250` |

All requests intended for proxied hostnames are directed to Cloudflare first and then forwarded to your origin server.

flowchart LR accTitle: Connections with Cloudflare A[Visitor] <-- Connection --> B[Cloudflare global network] <-- Connection --> C[Origin server]

Cloudflare assigns specific anycast IPs to your domain dynamically and these IPs may change at any time. This is an expected part of the operation of our anycast network and does not affect the proxy behavior described above.

When your traffic is proxied through Cloudflare, Cloudflare can automatically stop [DDoS attacks](https://developers.cloudflare.com/ddos-protection/about/) from ever reaching your application (and your origin server).

Proxied traffic also benefits from the default optimizations of the Cloudflare [cache](https://developers.cloudflare.com/cache/). Cloudflare caches [certain types of resources](https://developers.cloudflare.com/cache/concepts/default-cache-behavior/#default-cached-file-extensions) automatically, which both speeds up your application's performance and reduces the overall number of requests.

Proxying your DNS records in Cloudflare also hides the IP address of your origin server (because requests to your application resolve to Cloudflare anycast IP addresses instead).

This obscurity makes it harder for someone to connect directly to your origin, which - by extension - also makes it harder to target your origin with a DDoS attack.

Before proxying your records, you should likely [allow Cloudflare IP addresses](https://developers.cloudflare.com/fundamentals/concepts/cloudflare-ip-addresses/) at your origin to prevent requests from being blocked.

Then, [update your Cloudflare DNS records](https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/#edit-dns-records) so their **Proxy status** is **Proxied**.
