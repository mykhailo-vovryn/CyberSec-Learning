We can divide types if initial access into two groups:
- Exposed services - some misconfigured or bad protected, vulnerable (for exampple [T1133 / External Remote Services (opens in new tab)](https://attack.mitre.org/techniques/T1133/): Threat actors will look for exposed RDP/VNC/SSH with weak passwords to get remote access to the machine)
- User-driven methods - its social engineering (phishing, USB infected)
# IA via RDP
RDP is so often breached that there is funny name for it **R**ansomware **D**eployment **P**rotocol. This often happen due to bad password or bad configuration.
To check brut force just check 4625 event ID and 4624 for sucesfull brut force.
# IA via Phishing
In phishing mails can be malicious attachment with masced extenshions for example image.png.exe, and there are few legacy steel exutable windows extensions: .com, .scr, .cpl.
attacker can change target of lnk type of file in order to run scripts.
LNK file execion may be doing bu browser in log be cearfull