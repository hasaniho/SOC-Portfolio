🕵️ Wireshark: Carnage – Traffic Analysis Challenge

🔧 Tool Overview

Wireshark is a network protocol analyzer used to inspect packet-level data from network traffic. It's widely used in cybersecurity for tasks like threat hunting, incident response, and malware analysis.
In this challenge, I used Wireshark to investigate a suspicious .pcap file and answer questions based on observed network activity.

## 🔍 Scenario

Eric Fischer from the Purchasing Department at Bartell Ltd received a suspicious Word document via email. After clicking "Enable Content," his workstation began making suspicious outbound connections. The SOC team received an alert from the endpoint agent and retrieved a `.pcap` file from the network sensor. 
My task: analyze the packet capture to identify malicious activity.

🧠 Skills Practiced

* Creating and applying display filters
* Identifying file downloads via HTTP
* Extracting command-and-control (C2) indicators
* DNS query analysis
* Reconstructing file types from TCP streams

🔍 Key Filters & Syntax Used

Below are examples of display filters and techniques used to answer the challenge questions:
# Find all HTTP requests
http.request

# Filter by IP address
ip.addr == 192.168.56.101

# Identify DNS queries
dns.qry.name

# Extract TCP stream for file download
tcp.stream eq 2# Carnage – Wireshark Traffic Analysis Challenge

## 🧠 Overview
This TryHackMe lab focused on analyzing malicious traffic using Wireshark. I reviewed a PCAP file to identify suspicious behavior, attacker IPs, and compromised credentials.

## 🛠️ Skills & Tools Used
- Wireshark (filtering, export objects, following TCP streams)
- PCAP analysis
- Basic malware behavior analysis

## 🎯 Objectives
- Identify malicious IPs and compromised hosts
- Follow network traffic to detect C2 behavior
- Extract credentials from traffic

## 📌 Key Takeaways
- Used filters like `http.request`, `ftp`, `ip.addr == x.x.x.x`
- Extracted data via "Follow TCP Stream" and "Export Objects"
- Discovered credentials via cleartext FTP traffic

## 📁 Files
- `carnage_notes.md`: My step-by-step analysis
- Screenshots of evidence
