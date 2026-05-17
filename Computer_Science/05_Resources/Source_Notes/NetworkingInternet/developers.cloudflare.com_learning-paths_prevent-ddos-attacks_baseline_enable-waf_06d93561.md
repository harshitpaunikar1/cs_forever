Title: Enable WAF Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/enable-waf/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:22+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Enable WAF

Once you [proxy your DNS records](https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/proxy-dns-records/), you should enable rulesets for Cloudflare's [Web Application Firewall (WAF)](https://developers.cloudflare.com/waf/).

The available rulesets depend on your zone's plan, but all customers have access at least to the Cloudflare Free Managed Ruleset, which provides mitigations against high and wide-impacting vulnerabilities.

For more details and potential customizations, refer to [Managed rulesets](https://developers.cloudflare.com/waf/managed-rules/).
