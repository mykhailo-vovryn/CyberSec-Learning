We can divide types of initial access into two groups:

- **Exposed services** — misconfigured or poorly protected services
  (e.g. T1133 External Remote Services: threat actors look for exposed
  RDP/VNC/SSH with weak passwords to get remote access)
- **User-driven methods** — social engineering (phishing, infected USB)

## IA via RDP

RDP is so often breached that there is a funny name for it —
**Ransomware Deployment Protocol**.

This often happens due to weak passwords or bad configuration.

To detect brute force:
- `4625` — failed login attempts
- `4624` — successful login (confirms successful brute force)

## IA via Phishing

Phishing emails can contain malicious attachments with **masked extensions**,
for example `image.png.exe`.

Legacy executable extensions to watch for:
- `.com`
- `.scr`  
- `.cpl`

Attacker can change the target of an **LNK file** to run malicious scripts.
LNK file execution may appear in browser logs — be careful and check those.