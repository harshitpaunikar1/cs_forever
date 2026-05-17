Title: Augment default analytics Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/advanced/improve-analytics/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:18+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Augment default analytics

Cloudflare provides analytics for [security events](https://developers.cloudflare.com/waf/analytics/security-events/), [traffic patterns](https://developers.cloudflare.com/analytics/account-and-zone-analytics/zone-analytics/), and more according to the level of your zone's plan.

To augment these default analytics and gather more information about potential DDoS attacks, explore the following options.

When traffic [proxied through Cloudflare](https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/proxy-dns-records/) reaches your origin server, it will come from Cloudflare's IP addresses.

If needed, you can [restore the original visitor's IP address](https://developers.cloudflare.com/support/troubleshooting/restoring-visitor-ips/restoring-original-visitor-ips/) so you can have that information in your server logs.

Enterprise customers can set up [Logpush](https://developers.cloudflare.com/logs/logpush/) jobs to regularly send Cloudflare logs to the SIEM system of their choice.

This data can help when looking at long-term DDoS attack trends or when you need custom visualizations.

For more detailed analytics about potential bot attacks, Enterprise customers can also purchase [Bot Management](https://developers.cloudflare.com/bots/get-started/bot-management/).

For a full tour of Bot Analytics, see [our blog post â](https://blog.cloudflare.com/introducing-bot-analytics/). At a high level, the tool includes:

**Requests by bot score**: View your total domain traffic and segment it vertically by traffic type. Keep an eye on*automated*and*likely automated*traffic.**Bot score distribution**: View the number of requests assigned a bot score 1 through 99.**Bot score source**: Identify the most common detection engines used to score your traffic. Hover over a tooltip to learn more about each engine.**Top requests by attribute**: View more detailed information on specific IP addresses and other characteristics.

Bot Analytics shows up to one week of data at a time and can display data up to 30 days old. Bot Analytics displays data in real time in most cases.
