# Discovery
Let's see some basic Discovery examples:

| Discovery Goal                | Typical Commands                                                       |
| ----------------------------- | ---------------------------------------------------------------------- |
| and Filesystem Discovery      | `pwd`, `ls /`, `env`, `uname -a`, `lsb_release -a`, `hostname`         |
| User and Groups Discovery     | `id`, `whoami`, `w`, `last`, `cat /etc/sudoers`, `cat /etc/passwd`     |
| Process and Network Discovery | `ps aux`, `top`, `ip a`, `ip r`, `arp -a`, `ss -tnlp`, `netstat -tnlp` |
| Cloud or Sandbox Discovery    | `systemd-detect-virt`, `lsmod`, `uptime`, `pgrep "<edr-or-sandbox>"`   |
:

| Attack Objectives                                     | Typical Commands                                                       |
| ----------------------------------------------------- | ---------------------------------------------------------------------- |
| Find and steal credentials and other sensitive data   | `history \| grep pass`, `find / -name .env`, `find /home -name id_rsa` |
| Identify how suitable the system is for crypto mining | `cat /proc/cpuinfo`, `lscpu \| grep Model`, `free -m`, `top`, `htop`   |
| Scan the internal network for other future victims    | `ping <ip>`, `for ip in 192.168.1.{1..254}; do nc -w 1 $ip 22 done`    |