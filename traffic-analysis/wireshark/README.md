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


---

### 🧰 Tool Overview
Brief explanation of what this tool does and why it's used in cybersecurity or SOC environments.

---

### 🧪 Use Case / Lab Example  
Describe a specific thing you did with the tool in this lab. Include commands, filters, artifacts, and/or a screenshot (if possible).

---

### 🎯 Value / Takeaway  
What did you learn? How could this be applied in a real SOC environment?
