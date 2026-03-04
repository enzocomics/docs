# How I got my VLAN working with Proxmox
1. Create the VLAN on the network. For example, let's call it `homelab` with an ID of 2. Let's say the subnet is `192.168.2.0/24`
2. The port our node will be connecting to should have `homelab` tagged as its native VLAN
3. In Proxmox, create a new linux bridge and specify the bridge port that is connected to the port we just tagged
4. When creating a new virtual machine, the IP address must be static and set to an available address in the subnet. The gateway must also be set (it's probably `192.168.2.1`). DO NOT specify a VLAN ID during the install.
5. ???
6. Profit
