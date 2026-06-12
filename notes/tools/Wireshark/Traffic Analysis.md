In this note i will explain how to find anomalies on you network with Wireshark.

One of the most popular scanning tool is nmap. As a scanning tool it must generate a lot of traffic.
# Nmap Scans
Nmap use two protocol: UDP and TCP. 
## TCP
### TCP Connect Scan
Use full three-way handshake, usually has a windows size larger than 1024 bytes.
### TCP Syn Scan
Use only SYN and RST, usually have a size less than or equal to 1024 bytes.
## UDP
Nmap try to find open ports and if port unreachable dst host generate icmp message that contain encapsulated original udp request.![UDP scan](../../../assets/udp-nmap-scan.png)

---
# ARP Poisoning & Man In The Middle
Some useful features for wireshark filtering:
- `arp.opcode == 1` - ARP requests
- `arp.opcode == 2` - ARP responses
- `arp.dst.hw_mac==00:00:00:00:00:00` - ARP scanning
- `arp.duplicate-address-detected or arp.duplicate-address-frame` - possible ARP poisoning detection
- `((arp) && (arp.opcode == 1)) && (arp.src.hw_mac == target-mac-address)` - possible ARP flooding
---
# Identifying Hosts
## DHCP Analysis
Wireshark filters:
- `dhcp.option.dhcp == 3` - request
- `dhcp.option.dhcp == 5` - ACK
- `dhcp.option.dhcp == 6` - NAK
- `dhcp.option.hostname contains "keyword"`
- `dhcp.option.domain_name contains "keyword"`
## NetBIOS (NBNS) Analysis
NBNS allows diff app on diff hosts to communicate with each other.
Wireshark filters:
- `nbns`
- `nbns.name contains "keyword"`
## Kerberos Analysis
Sign `$` before the name mean that this is hostname(workstation) and name without `$` mean that this is user.
Wireshark filters:
- `kerberos`
- `kerberos.CNameString contains "keyword"` - CNameString is username
- `kerberos.CNameString and !(kerberos.CNameString contains "$" )`
- `kerberos.pvno == 5` - pvno is protocol version

- `kerberos.realm contains ".org"` - realm is domain name

- `kerberos.SNameString == "krbtg"` 
---
# Tunnelling Traffic
Attackers use tunnelling to bypass security perimeters using the standart and trusted protocols like ICMP and DNS.
## ICMP Analysis
As ICMP is trusted network layer protocol, sometimes it used for Dos attacks, data exfiltration and C2 tunnelling.
I think its good practise to limit ICMP traffic in private network.

Wireshark filter:
- `icmp`
- `data.len > 64 and icmp` - but attackers can modify len of ICMP
## DNS Analysis
Attacker can create domain address and configure it as a C2 channel. After exploitation attacker sends DNS queries to the C2 server.
Mostly these queries are longer than default DNS queries.

Wireshark filter:
- `dns`
- `dns contains "dnscat"` - known pattern
- `dns.qry.name.len > 15 and !mdns` - !mdns disable local link dev queries
---
# CPA(cleartext protocol Analysis) FTP
