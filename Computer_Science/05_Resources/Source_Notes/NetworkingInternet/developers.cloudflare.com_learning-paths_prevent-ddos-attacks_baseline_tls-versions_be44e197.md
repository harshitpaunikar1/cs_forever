Title: Update TLS versions Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/tls-versions/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:24+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Update TLS versions

In some circumstances - specifically when an application allows client-initiated SSL/TLS renegotiation - previous versions of SSL/TLS can be more vulnerable to DDoS attacks.

When you use an SSL/TLS certificate issued by Cloudflare 1, you can reduce the impact of this vulnerability by:

- Updating the
[Minimum TLS Version](https://developers.cloudflare.com/ssl/edge-certificates/additional-options/minimum-tls/)accepted by your application. - Allowing
[TLS 1.3](https://developers.cloudflare.com/ssl/edge-certificates/additional-options/tls-13/).

For more details on this vulnerability, refer to [Secure Server- and Client-Initiated SSL Renegotiation â](https://crashtest-security.com/secure-client-initiated-ssl-renegotiation/).
