Title: Customize Cloudflare security Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/advanced/customize-security/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:17+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Customize Cloudflare security

Another way of reducing origin traffic is customizing the Cloudflare WAF and other security features. The fewer malicious requests that reach your application, the fewer that could reach (and overwhelm) your origin.

To reduce incoming malicious requests, you could:

- Create
[WAF custom rules](https://developers.cloudflare.com/waf/custom-rules/)for protection based on specific aspects of incoming requests. - Adjust DDoS rules to handle
[false negatives and false positives](https://developers.cloudflare.com/ddos-protection/managed-rulesets/http/http-overrides/override-examples/). - Build
[rate limiting rules](https://developers.cloudflare.com/waf/rate-limiting-rules/)to protect against specific patterns of requests. - Enable
[bot protection](https://developers.cloudflare.com/bots/get-started/)or set up[Bot Management for Enterprise](https://developers.cloudflare.com/bots/get-started/bot-management/)to protect against automated abuse. - Explore
[network-layer DDoS attack protection](https://developers.cloudflare.com/ddos-protection/managed-rulesets/network/). - Review the rest of Cloudflare's
[security options](https://developers.cloudflare.com/learning-paths/application-security/account-security/).
