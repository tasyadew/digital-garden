---
{"dg-publish":true,"permalink":"/thoughts/setting-up-my-own-homelab/","noteIcon":"1","created":"2025-01-25T13:12:00.702+08:00","updated":"2025-01-25T13:55:54.697+08:00"}
---


A homelab is where I can safely test and practice setting up private networks, experiment with open-source applications, and host them on my own server.

This fun project all started when [Google Photos announced the end of their unlimited free photo backup](https://blog.google/products/photos/storage-changes/). I loved the freedom of having extra space on my phone after backing up photos to the cloud. Back in 2017, with 64GB of storage and no SD card slot, managing storage was a real challenge. Fast forward to 2021, when the unlimited backup service was discontinued, I had to keep all my photos on my phone. That experience reminded me that Google Photos is a SaaS (Software as a Service), and these services can change or disappear at any time. I also started becoming more privacy-conscious. Knowing my personal photo collection was stored on Google's servers began to feel unsettling.

In 2024, disaster struck when my phone got soft-bricked, and I lost all the photos I hadn't backed up. While I missed Google Photos' convenience, I didn’t want to pay for Google One. That’s when I discovered [[tech/Network Attached Storage (NAS)\|NAS]]. The idea of building my own version of Google Photos was exciting! While researching NAS, I stumbled into the world of self-hosting. I realized I could repurpose an old PC I had lying around and turn it into my own server. From there, I started trying out self-hosted apps like **Immich**, **Actual Budget**, **Metabase**, **Plex**, and **Pi-hole**. It felt like I’d unlocked a whole new area of programming!

I quickly realized how much I enjoyed devops work—deploying apps on servers and the cloud was incredibly rewarding. However, I struggled with the networking side of things. Once, I misconfigured Pi-hole, which ended up taking down my entire home network and left my family without WiFi. (Oops!)

Through trial and error, I’ve learned a lot about networking and security. One of the most important lessons is that ==not all services should be exposed to the Internet==. Some services, especially those handling sensitive data, should only be accessible through private networks using tools like **Tailscale** or **Cloudflare Tunnel**. By default, a home network should always be private.

Imagine if all the data on my phone was accessible to the public—_I’d be cooked._