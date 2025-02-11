---
{"dg-publish":true,"permalink":"/tech/virtual-private-server-vps/","tags":["cloud","devops"],"noteIcon":"1","created":"2025-01-22T23:23:01.613+08:00","updated":"2025-02-07T17:21:21.349+08:00"}
---

what is it?
- isolated, virtual environment on a physical server.
	- owned & operated by cloud provider.


---
## Code snippet
> List of frequent command I use when using Oracle VPS (OS: Linux Ubuntu)

- SSH to VPS from CMD/Powershell (Windows)
```bash
ssh username@vps_ip_address
```
Note: instead of typing the VPS IP Address, can use domain name for easier to remember. 

- Update & upgrade
```bash
sudo apt update && sudo apt upgrade
```

- Delete folder with all it's subdirectories
```bash
sudo rm -rf dir_name
```
