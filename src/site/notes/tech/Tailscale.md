---
{"dg-publish":true,"permalink":"/tech/tailscale/","tags":["tech/vpn","network"],"noteIcon":"1","created":"2025-01-22T22:31:12.068+08:00","updated":"2025-02-10T14:51:01.152+08:00"}
---

![unnamed.webp](/img/user/assets/unnamed.webp)
site: [here](https://tailscale.com/)

**what is it?**
- mesh [[tech/Virtual Private Network (VPN)\|VPN]]
	- connect devices and services securely across different networks.
	- encrypted point-to-point connection.
- peer-to-peer mesh network, but can act as traditional VPN by routing all traffic through an exit node.

**what is it use for?**
- private network, data is not exposed to the internet.
- can host private website that is only accessible with devices that is enable with the same Tailscale network.

---
## Commands

1) Share services publically available to the Internet.
```
tailscale funnel
```

2) Share services locally to other devices in tailnet node.
```
tailsacle serve
```

