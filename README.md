# CyberDefenders — Lockdown Lab Writeup

Network and memory forensics investigation of a compromised IIS server (September 2026).

📄 **Full report (Azerbaijani, 8 pages):** [`report/Lockdown_Lab_Report_AZ.pdf`](report/Lockdown_Lab_Report_AZ.pdf)
🔗 Lab: [CyberDefenders](https://cyberdefenders.org/) · My profile: [khidirovidris](https://cyberdefenders.org/p/khidirovidris-cyberdef)

## Scenario

A SOC team saw suspicious outbound traffic from an internet-facing IIS server. Evidence: a PCAP, a full memory image and a malware sample.

## Attack chain I reconstructed

`Port scan (Nmap) → SMB share enumeration → web shell upload (shell.aspx) → reverse shell (TCP 4443) → persistence`

## Method

| Phase | Tool | What I found |
|---|---|---|
| Network (PCAP) | Wireshark | Scanning host, Nmap NSE user-agent, accessed SMB shares, web shell request, reverse shell port |
| Memory | Volatility 3 (`windows.info`, `netscan`, `psscan`, `pstree`) | IIS worker process `w3wp.exe` holding the reverse shell, its parent and child processes, persistence |
| Malware | `strings`, VirusTotal | Static indicators and threat intel on the sample |

The time of the reverse shell in the PCAP matches the connection time in the memory image, so both artifacts confirm the same event.

**Author:** Idris Khidirov — [LinkedIn](https://www.linkedin.com/in/idris-khidirov-132532328)
