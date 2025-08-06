---
{"dg-publish":true,"permalink":"/tutorials/host-actual-budget-on-oracle-cloud-vps-with-docker/","tags":["devops","finance","tech/app","tutorial"],"noteIcon":"1","created":"2025-02-07T17:22:42.505+08:00","updated":"2025-07-12T15:37:12.373+08:00"}
---

![Pasted image 20250216012822.png](/img/user/assets/Pasted%20image%2020250216012822.png)
[[tech/Actual Budget\|Actual Budget]] is a local-first personal finance app. It is open-source and can be self-host the Actual Server on your own PC or on the cloud. My approach is to host on my [[tech/Oracle Cloud\|Oracle Cloud]] (the PAYG, but it is within the free tier usage). For HTTPS, I will use [[tech/Tailscale\|Tailscale]] to privately connect between my devices within the Tailnet network. This allows me to view my finance app from my phone and use the Actual API integration. 

# Pre-requisite
- Oracle Cloud VPS, or any server that you use.
- [[tech/Docker\|Docker]] installed in the VPS - [refer here](https://docs.docker.com/engine/install/ubuntu/)
- [[tech/Tailscale\|Tailscale]] installed in the VPS - [refer here](https://tailscale.com/kb/1031/install-linux)

> [!tips]-
> It is easier to remote SSH the VPS using VS Code. (Unless you prefer using vim or nano) 

# Getting Started

## Setup Actual Server

1) Create a directory for actual budget. Go inside the directory, and create a docker compose file.
```bash
mkdir <dir_name>
cd <dir_name>
nano docker-compose.yaml
```
2) In the `docker-compose.yaml`, copy [this repo](https://github.com/actualbudget/actual/blob/master/packages/sync-server/docker-compose.yml). Then, uncomment the port. You may uncomment based on your own configuration, but this is how I did min. 
```yaml
    environment:
      # Uncomment any of the lines below to set configuration options.
      # - ACTUAL_HTTPS_KEY=/data/selfhost.key
      # - ACTUAL_HTTPS_CERT=/data/selfhost.crt
      - ACTUAL_PORT=5006
      - ACTUAL_UPLOAD_FILE_SYNC_SIZE_LIMIT_MB=20
      - ACTUAL_UPLOAD_SYNC_ENCRYPTED_FILE_SYNC_SIZE_LIMIT_MB=50
      # - ACTUAL_UPLOAD_FILE_SIZE_LIMIT_MB=20
      # See all options and more details at https://actualbudget.github.io/docs/Installing/Configuration
      # !! If you are not using any of these options, remove the 'environment:' tag entirely.
```
3) Run the docker-compose using `docker compose up -d`. Now, you should be able to see something like the image below when you type at the search bar `http://<dns>:5006`. The fatal error message is because you need to setup the HTTPS connection. 

![Pasted image 20250210141114.png](/img/user/assets/Pasted%20image%2020250210141114.png)

## Final files
In the end, your `docker-compose.yaml` will look something like this:

```yaml
services:
  actual-ts:
    image: tailscale/tailscale:latest
    container_name: actual-ts
    hostname: actual
    environment:
      - TS_AUTHKEY=tskey-auth-xxx
      - "TS_EXTRA_ARGS=--advertise-tags=tag:container --reset"
      - TS_SERVE_CONFIG=/config/actual.json
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_USERSPACE=false
    volumes:
      - ${PWD}/config:/config
      - actual-ts:/var/lib/tailscale
    devices:
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - net_admin
    restart: unless-stopped
  actual_server:
    image: docker.io/actualbudget/actual-server:latest
    container_name: actualserver
    network_mode: service:actual-ts
    depends_on:
      - actual-ts
    # ports:
    #   # This line makes Actual available at port 5006 of the device you run the server on,
    #   # i.e. http://localhost:5006. You can change the first number to change the port, if you want.
    #   - '5006:5006'
    environment:
      # Uncomment any of the lines below to set configuration options.
      # - ACTUAL_HTTPS_KEY=/data/selfhost.key
      # - ACTUAL_HTTPS_CERT=/data/selfhost.crt
      - ACTUAL_PORT=5006
      - ACTUAL_UPLOAD_FILE_SYNC_SIZE_LIMIT_MB=20
      - ACTUAL_UPLOAD_SYNC_ENCRYPTED_FILE_SYNC_SIZE_LIMIT_MB=50
      # - ACTUAL_UPLOAD_FILE_SIZE_LIMIT_MB=20
      # See all options and more details at https://actualbudget.github.io/docs/Installing/Configuration
      # !! If you are not using any of these options, remove the 'environment:' tag entirely.
    volumes:
      # Change './actual-data' below to the path to the folder you want Actual to store its data in on your server.
      # '/data' is the path Actual will look for its files in by default, so leave that as-is.
      - ./actual-data:/data
    healthcheck:
      # Enable health check for the instance
      test: ["CMD-SHELL", "node src/scripts/health-check.js"]
      interval: 60s
      timeout: 10s
      retries: 3
      start_period: 20s
    restart: unless-stopped

volumes:
  actual-ts:
    driver: local
```

And, your `actual.json` will look something like this:

```json
{
  "TCP": {
    "443": {
      "HTTPS": true
    }
  },
  "Web": {
    "${TS_CERT_DOMAIN}:443": {
      "Handlers": {
        "/": {
          "Proxy": "http://127.0.0.1:5006"
        }
      }
    }
  },
  "AllowFunnel": {
    "${TS_CERT_DOMAIN}:443": false
  }
}
```

Finally, your file hierarchy should look something like this:

![Pasted image 20250216011604.png](/img/user/assets/Pasted%20image%2020250216011604.png)

Hopefully now you can host your own Actual Budget. Happy budgeting!!

# Update Actual Budget

1) Locate to your Actual Budget Repo on your VPS.

2) Use this command to update your Actual Budget:
```bash
docker compose pull && docker compose up -d
```

**Note:** If your client version and server version not match, Press CTRL + F5 to clear browser cache. You should be able to see the latest client version!
![Pasted image 20250712153043.png](/img/user/assets/Pasted%20image%2020250712153043.png)
![Pasted image 20250712153123.png](/img/user/assets/Pasted%20image%2020250712153123.png)
---
**References**
Actual Budget Documentation: https://actualbudget.org/docs/
Tailscale Docker Setup: https://tailscale.com/blog/docker-tailscale-guide
