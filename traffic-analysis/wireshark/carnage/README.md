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

## 📊 Summary of Findings
	•	🕸️ Malicious Domains:
	•	finejewels.com.au
	•	thietbiagt.com
	•	new.americold.com
	•	api.ipify.org (used for IP discovery)
Discovered via high-traffic TCP conversations and by inspecting Server Name Indication (SNI) fields in TLS handshakes.
	•	🎯 Cobalt Strike C2 Servers:
	•	IPs identified by filtering HTTP traffic on ports 80/8080, then confirmed using VirusTotal’s Community tab.
	•	Verified based on behavior consistent with Cobalt Strike per MITRE ATT&CK framework.
	•	📨 Suspicious Email Activity:
	•	SMTP traffic observed between the infected host and farshin@mailfa.com.
	•	Used smtp.req.command and smtp.req.argument columns to extract MAIL FROM and RCPT TO fields for deeper analysis.

⸻

## 📝 Notes

This lab showcased how to:
	•	Apply Wireshark display filters effectively
	•	Correlate packet data with open-source intelligence
	•	Identify malware behavior like C2 communications and malspam
  •	Apply similar triage approach to future PCAP-based labs
	•	Think like a SOC analyst during an early-stage incident
