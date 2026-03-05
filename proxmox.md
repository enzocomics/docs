# Post-install setup
- Run the post install script: `bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/tools/pve/post-pve-install.sh)"` - [*source*](https://community-scripts.github.io/ProxmoxVE/scripts?id=post-pve-install&category=Proxmox+%26+Virtualization)
- Set up SMTP for datacenter notifications
- Installed Cloudflare's origin certificate onto the node

# Firewall setup
- Set up the datacenter firewall and open up any required ports (http, https, dns, etc) [*source*](https://pve.proxmox.com/wiki/Firewall). This is *required* or none of the lower-level firewalls will work
- Activate the node firewall
- Activate the firewall per virtual machine for:
  -  [Cloudflared](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/configure-tunnels/tunnel-with-firewall/)
  -  [Adguard Home](https://github.com/AdguardTeam/AdGuardHome/wiki/Getting-Started)
  -  [Unifi Controller](https://help.ui.com/hc/en-us/articles/218506997-Required-Ports-Reference)
  -  [Checkmate](https://docs.checkmate.so/users-guide/quickstart):
    - `80` for https
    - `5173` for client UI
    - `52345` for server API


# How I got my VLAN working with Proxmox
1. Create the VLAN on the network. For example, let's call it `homelab` with an ID of 2. Let's say the subnet is `192.168.2.0/24`
2. The port our node will be connecting to should have `homelab` tagged as its native VLAN
3. In Proxmox, create a new linux bridge and specify the bridge port that is connected to the port we just tagged
4. When creating a new virtual machine, the IP address must be static and set to an available address in the subnet. The gateway must also be set (it's probably `192.168.2.1`). DO NOT specify a VLAN ID during the install.
5. ???
6. Profit

# Checkmate
- Installed Golang by downloading the tar and SCPing it into the server
- Installed the server monitoring agent Capture [*source*](https://docs.checkmate.so/users-guide/server-monitoring-agent)
  - Run the capture server: `API_SECRET=<secret_token> GIN_MODE=release ./go/bin/capture &`
  - The `&` will let it run in the background so that exiting the shell won't terminate the process
  - If you want to kill the process in the future, look for the PID with `ps -C capture` and then kill it with `kill <PID>`
- Edited `vite.config.js` in the `/opt/checkmate/client` folder and added the app url to `preview.allowedHosts` [*source*](https://vite.dev/config/preview-options)
