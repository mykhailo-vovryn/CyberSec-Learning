## Command and Control (C2)

> The adversary is trying to communicate with compromised systems to control them. Command and Control consists of techniques that adversaries may use to communicate with systems under their control within a victim network. Adversaries commonly attempt to mimic normal, expected traffic to avoid detection.
> — [MITRE ATT&CK TA0011](https://attack.mitre.org/tactics/TA0011/)

## Persistence Overview
...
## Persistence Overview

Persistence = maintaining reliable, long-term access that survives reboots
and password changes.

Common methods:
- Create backdoor or web shell
- Create new admin user — detected by `4720` (user creation)
- Add user to privileged group — detected by `4732`
- Reset existing account password — detected by `4724`

## Tasks and Services

Two most common persistence methods:

**Via Windows Services:**
```cmd
sc create "BadService" binpath= "C:\malware.exe" start= auto
```
- Launch of sc.exe: Sysmon `1`
- Service creation: Security `4697`

**Via Scheduled Tasks:**
```cmd
schtasks /create /tn "BadTask" /tr "C:\malware.exe" /sc onstart /ru System
```
- Launch of schtasks.exe: Sysmon `1`
- Scheduled task creation: Security `4698`

## Run Keys and Startup

**Startup folder:**
```cmd
copy C:\malware.exe "%AppData%\Microsoft\Windows\Start Menu\Programs\Startup\malware.exe"
```
Detection: Sysmon `11` (file creation)
Apps launched from startup folder have parent process `explorer.exe`

**Registry Run keys:**
```cmd
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v BadKey /t REG_SZ /d "C:\malware.exe"
```
Detection: Sysmon `13` (registry value set)