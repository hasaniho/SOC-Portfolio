# Wireshark Traffic Analysis Lab

TryHackMe Lab: Wireshark Traffic Analysis  
Skills practiced: Packet capture analysis, DNS filtering, HTTP method inspection, FTP command tracking.

## Summary
This lab focused on analyzing PCAP files using Wireshark to extract intelligence on DNS queries, HTTP traffic, and FTP activity.

## Key Filters Used
- `dns.qry.name.len > 15 and !mdns`
- `ftp.request.command and ftp.request.arg and ftp.response.code`
- `http.request.method == "POST"`
