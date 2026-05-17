Title: Set up alerts Â· Cloudflare Learning Paths
Mapped Topic: DNS, CDN, DDoS, reverse proxy, load balancing
Source URL: https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/set-up-alerts/
Source Type: official_docs
Trust Score: 90
Fetched At: 2026-04-17T07:05:24+00:00
Mapped From CSE.md Section: Part 2: B. Networking and how the Internet really works

# Content

# Set up alerts

Another part of preparing for DDoS attacks is knowing when your application is being attacked.

Cloudflare offers notifications for DDoS attacks, which you can set up on your account.

To set up a notification:

-
In the Cloudflare dashboard, go to the

**Notifications**page.[Go to](https://dash.cloudflare.com/?to=/:account/notifications)**Notifications** -
Select

**Add**. -
Select one of the

[available DDoS alerts](https://developers.cloudflare.com/ddos-protection/reference/alerts/#alert-types)depending on your plan and services:- HTTP DDoS Attack Alert
- Layer 3/4 DDoS Attack Alert
- Advanced HTTP DDoS Attack Alert
- Advanced Layer 3/4 DDoS Attack Alert

-
Enter a notification name and (optionally) a description.

-
Configure a delivery method for the notification. The available delivery methods depend on your Cloudflare plan. For more information, refer to

[Cloudflare Notifications](https://developers.cloudflare.com/notifications/). -
If you are creating a notification for one of the advanced DDoS attack alerts, select

**Next**and define the parameters that will filter the notifications you will receive. -
Select

**Save**.
