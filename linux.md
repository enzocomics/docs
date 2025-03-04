- Commands preceded by `#`: require root privileges, either directly as `root` or with `sudo`
- `hostnamectl`: view operating software information

- `sudo -i` - switch to root environment 
- `# apt update` - fetch the list of updated packages
- `# apt upgrade` - download & install updated packages
- `df -h` - view disk usage


- `# service --status-all` - list all active/inactive services
- `# timedatectl` - display time info
- `# timedatectl set-timezone America/Vancouver` - change the time zone to PST


- `# smartctl -h` - view commands for `smartctl`, a utility program to control the SMART (self-monitoring, analyrics & reporting technology system) built in to modern disk drives
- `# smartctl --scan` - scan for disk drives, i.e. `/dev/sda`
- `# smartctl -t long /dev/sda` - execute a long smart test on disk drive `/dev/sda`


- `curl -O <url_of_file>` - download a file from a URL and save it under the same name 
