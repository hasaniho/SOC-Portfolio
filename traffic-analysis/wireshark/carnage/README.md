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

## 📊 Summary of Findings

- **Malicious Domains**: 
  - `finejewels.com.au`
  - `api.ipify.org`
  - `thietbiagt.com`
  - `new.americold.com`
  → Identified by analyzing high-volume TCP conversations and inspecting SNI fields in TLS handshake packets
- **Suspicious Email Activity**: 
  - Detected SMTP traffic to `farshin@mailfa.com`
  - Used column customization to add `smtp.req.command` and `smtp.req.argument` fields for easier analysis
