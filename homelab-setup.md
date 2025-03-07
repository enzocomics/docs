Start off with a fresh install of Proxmox (Debian).
- Run post-install scripts ([source](https://community-scripts.github.io/ProxmoxVE/scripts)): `bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/misc/post-pve-install.sh)"` 

## **Install Fail2Ban**
- `apt install fail2ban`
- Create local config filese: `cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local` and `cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
- Edit `jail.local` and set the following:
```conf
[default]
backend = systemd
destemail = (your email)
sender = (email of the server)

[sshd]
enabled = true
```
- `systemctl enable fail2ban` and `systemctl start fail2ban`
- Check if it's running: `service --status-all` or `service fail2ban status`

## **Install Speedtest**
(Because I wanted to know if my 2.5gb ethernet card was working)
- `curl` doesn't work directly from github for some reason, so download the file locally: https://github.com/taganaka/SpeedTest/archive/refs/heads/master.zip
- From the local folder, copy the zip to the server `scp SpeedTest-master.zip root@server:/root/.`
- Install dependencies: `apt install zip build-essential libcurl4-openssl-dev libxml2-dev libssl-dev cmake`
- Open the archive: `unzip SpeedTest-master.zip`
- Navigate to the folder `cd SpeedTest-master` and then run `cmake -DCMAKE_BUILD_TYPE=Release .` and `make install`
- Run the program: `SpeedTest`
