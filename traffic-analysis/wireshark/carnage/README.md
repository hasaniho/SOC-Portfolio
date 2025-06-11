# 🕵️‍♂️ Carnage - Wireshark Traffic Analysis Lab

## Overview
This lab simulates a real-world security incident where a user from Bartell Ltd’s Purchasing Department receives a malicious email attachment. After enabling macros in a Word document, their system initiates suspicious outbound connections. As an analyst, I used Wireshark to examine the provided `.pcap` file and answer a set of investigative questions.

## 🛠 Tools Used
- **Wireshark** – for deep packet inspection and protocol analysis
- **VirusTotal** – to confirm indicators of compromise (IOCs)
- **MITRE ATT&CK Framework** – to understand Cobalt Strike behavior and communication patterns
- **OSINT Tools** (Community Threat Intelligence)

## 🎯 Techniques Used
- **Follow TCP/HTTP Streams**: Helped reconstruct communication between the victim and external hosts.
- **Time-Based Packet Sorting**: Rearranged packets chronologically to identify the first HTTP connection.
- **Statistics → Conversations**: Used to highlight the most active IPs and detect possible C2 servers.
- **Custom Columns**: Added `tls.handshake.extensions_server_name` to identify malicious domains over TLS.
- **Advanced Filtering**:
  ```wireshark
  (tcp.port == 443 or tcp.port == 80 or tcp.port == 8080) and tls.handshake.extensions_server_name != ""

## 🧠 Key Filters and Commands Used
http.request
tcp.stream eq [n]
tcp.port == 443 || tcp.port == 80 || tcp.port == 8080
tls.handshake.extensions_server_name != ""
frame.time
ip.addr == [suspicious IP]
