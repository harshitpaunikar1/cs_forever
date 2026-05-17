Title: Protect origin IP address Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/advanced/protect-origin-ip/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:20+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Protect origin IP address

Though Cloudflare automatically hides your origin server IP address when you [proxy your DNS records](https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/proxy-dns-records/), there are other ways to discover an IP address.

To prevent attackers from discovering your origin's IP address, review the following suggestions.

DNS records are in the public domain, meaning that - even though your IP addresses are hidden once you proxy your DNS records - someone could uncover historical records of your addresses.

For additional security, you could rotate the IP addresses of your origin server, which would also require [updating your DNS records](https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/#edit-dns-records) within Cloudflare.

Unproxied DNS records - also known as **DNS-only** records - can sometimes contain origin IP information, especially those used for FTP or SSH.

Review these records to make sure they do not contain origin IP information or use [Cloudflare Spectrum](https://developers.cloudflare.com/spectrum/) to proxy these records.

If you need to have **DNS-only** records that contain origin IP information, use non-standard names for these records. This action makes dictionary scans of your DNS less likely to expose your origin IP address.

For example, instead of `ftp.example.com`

, you could use `827450184590183489.example.com`

or `cloudflare-docs-are-great.example.com`

.

If possible, do not host a mail service on the same server as the web resource you want to protect, since emails sent to non-existent addresses get bounced back to the attacker and reveal the mail server IP address.

Cloudflare recommends using non-contiguous IPs from different IP ranges.
