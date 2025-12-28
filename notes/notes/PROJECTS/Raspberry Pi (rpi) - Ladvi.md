---
tags:
  - on/dev
  - on/HW
---
Information about my Raspberry Pi on [[Byt Ládví, Ladvi]]

Image: Raspberry Pi OS Lite - arm64 (installed headless)
mem: 4GB
user: erik
local hostname: erikrpi.local
public hostname: [rpi.hulmaker.com](rpi.hulmaker.com)

### Setting up a Cloudflare tunnel
see: [ssh overview docs](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/use-cases/ssh/)
**Create a zero-trust Cloudflare tunnel**:
- either with `cloudflared` package, or with GUI
- You need to set internal ip address (try `ip addr`)
- Set rules - allow emails
- this should then create a DNS record on your domain
- run the tunnel on device, make sure the status is healthy (automatic start on service/docker)
- create an application:
	- Set up authentication methods (like google auth to cloudflare)
	- attach to the same domain(subdomain)
	- set browser rendering to SSH
- now you should be able to connect to the hostname with browser.
