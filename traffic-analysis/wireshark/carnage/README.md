# 🕵️‍♂️ Carnage – Wireshark Traffic Analysis Lab

## 📁 Overview

This TryHackMe challenge simulates a real-world malware infection scenario. A user at Bartell Ltd downloaded a malicious Word doc and enabled macros, triggering suspicious outbound connections. I was tasked with analyzing the `.pcap` file to uncover the attack timeline, malicious domains, and C2 infrastructure. 

## 🧠 Objective

Analyze the PCAP file using Wireshark to:
- Identify the first HTTP connection
- Extract domains and IPs involved in malicious activity
- Detect Cobalt Strike C2 infrastructure
- Practice OSINT + packet filtering techniques
- Observe SMTP traffic to detect malspam

- **Room:** [Carnage](https://tryhackme.com/room/carnage)
---

## 🛠️ Tools & Techniques Used

- **Wireshark**: for inspecting packets, following TCP/HTTP streams, analyzing conversations, and filtering protocols
- [**VirusTotal**](https://virustotal.com): confirmed malicious IPs associated with Cobalt Strike (via Community tab)
- [**MITRE ATT&CK**](https://attack.mitre.org/): used to research typical Cobalt Strike behavior and ports (80/8080)
- **CanaryTokens** & **IPVoid** (not used in this lab, but relevant tools in similar investigations)

---

## 🧪 Key Techniques & Filters

Here are some of the key filters and approaches I used:

```wireshark
# Rearrange packets chronologically
Sort by time column

# Follow full TCP/HTTP stream to read files and commands
Follow TCP Stream
Follow HTTP Stream

# Detect all HTTP connections
http.request

# Show DNS queries
dns.qry.name

# Filter by specific IP
ip.addr == x.x.x.x

# Filter by domain name
Applied servername extension as a column

# Filter for TLS handshakes and extract domains
tcp.port == 443 && tls.handshake.extensions_server_name

# Combined port + TLS filter
(tcp.port == 443 or tcp.port == 80 or tcp.port == 8080) && tls.handshake.extensions_server_name != ""

# Detect malspam
smtp contains "MAIL FROM"
```
---

---

## 📊 Summary of Findings

- **🕸️ Malicious Domains**:
  - `finejewels.com.au`
  - `thietbiagt.com`
  - `new.americold.com`
  - `api.ipify.org` *(used for IP discovery)*  
  > Identified through high-volume TCP conversations and inspecting SNI fields in TLS handshake packets.

- **🎯 Cobalt Strike C2 Servers**:
  - Two IPs associated with outbound HTTP (port 80/8080) activity
  - Verified as Cobalt Strike infrastructure via **VirusTotal** (Community tab)
  - Tactics aligned with **MITRE ATT&CK** techniques

- **📨 Suspicious Email Activity**:
  - SMTP traffic from victim host to `farshin@mailfa.com`
  - Added columns like `smtp.req.command` and `smtp.req.argument` to Wireshark for faster visibility

---

## 📝 Notes

This lab demonstrates how to:

- Use Wireshark filters and sorting to reconstruct attacker behavior
- Follow TCP/HTTP streams to extract payloads and observe C2 traffic
- Enrich PCAP findings with OSINT tools like VirusTotal and MITRE ATT&CK
- Apply similar triage approach to future PCAP-based labs
- Customize Wireshark views (e.g., TLS SNI, SMTP columns) for deeper insight during investigations
