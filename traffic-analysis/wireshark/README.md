# Wireshark Traffic Analysis Lab

## 🔍 Overview
This lab, from the TryHackMe **"Wireshark: Traffic Analysis"** room, focused on using Wireshark to examine network traffic and identify signs of suspicious activity. It served as an introduction to traffic analysis techniques used in Security Operations Centers (SOCs).

## 🛠️ Tools Used
- **Wireshark** (graphical packet analysis tool)
- **PCAP files** provided by TryHackMe

## 🔑 Key Filters & What They Reveal

### 📌 DNS Analysis
```wireshark
dns.qry.name.len > 15 and !mdns

