Home Lab – Nmap Scans & System Hardening

This repository documents hands-on Nmap scanning, findings, and remediation steps carried out on my personal home lab to practice network discovery, exposure analysis, and basic system hardening using real systems in a controlled environment.

Disclaimer: This lab was conducted only on virtual machines I own and control. All IP addresses are private and used strictly for learning and testing purposes.

(A) Lab Overview

Network Range: `192.168.100.0/24`

| IP Address     | System              | Purpose                |
| -------------- | ------------------- | ---------------------- |
| 192.168.100.10 | Windows Server 2025 | Domain Controller      |
| 192.168.100.30 | Windows 11          | Workstation (IIS)      |
| 192.168.100.50 | Ubuntu Linux        | Splunk Server          |
| 192.168.100.40 | Kali Linux          | Scan Host (Attack Box) |


(B) Scans Performed:

| # | Scan Type                   | Command                                             | Purpose                                                             |
| - | --------------------------- | --------------------------------------------------- | ------------------------------------------------------------------- |
| 1 | TCP SYN Scan (Top 20 Ports) | `sudo nmap -sS --top-ports 20 192.168.100.0/24`     | Identify commonly exposed TCP services using half-open SYN scanning |
| 2 | UDP Scan (Top 20 Ports)     | `sudo nmap -sU --top-ports 20 192.168.100.0/24`     | Detect exposed UDP services used for discovery or lateral movement  |
| 3 | Service & OS Detection      | `sudo nmap -sV -O 192.168.100.0/24`                 | Identify running services, versions, and OS fingerprints            |
| 4 | Vulnerability Scripts       | `sudo nmap -sV --script vuln 192.168.100.0/24`      | Identify known vulnerabilities and insecure configurations          |
| 5 | Authentication Scripts      | `sudo nmap -sV --script auth 192.168.100.0/24`      | Identify authentication mechanisms and user enumeration surfaces    |
| 6 | Discovery Scripts           | `sudo nmap -sV --script discovery 192.168.100.0/24` | Enumerate multicast, IPv6, mDNS, and LLMNR discovery mechanisms     |


(C) Key Findings:

(I) Windows Server 2025 – 192.168.100.10

| Finding          | Details                        | Risk                            |
| ---------------- | ------------------------------ | ------------------------------- |
| Exposed Port     | TCP 5985 (WinRM)               | Lateral movement via WinRM      |
| Service          | Microsoft HTTPAPI              | Network reconnaissance          |
| Network Behavior | mDNS / LLMNR multicast traffic | Credential abuse if compromised |


 (II) Windows 11 – 192.168.100.30

| Finding          | Details                              | Risk                             |
| ---------------- | ------------------------------------ | -------------------------------- |
| Exposed Port     | TCP 80 (IIS 10.0)                    | Unnecessary web service exposure |
| Configuration    | Default IIS configuration            | -                                |
| Issue            | Request Filtering misconfiguration   | Weakened web-layer protections   |
| Network Behavior | Multicast discovery traffic observed | Internal reconnaissance          |


(III) Ubuntu Linux (Splunk) – 192.168.100.50

| Finding       | Details                                   | Risk                          |
| ------------- | ----------------------------------------- | ----------------------------- |
| Exposed Ports | TCP 8000 (Web), TCP 8089 (Management API) | Management interface exposure |
| Vulnerability | Slowloris DoS (CVE-2007-6750)             | Denial-of-Service             |
| Exposure      | Authentication & user enumeration surface | Service enumeration           |
| Network       | Multicast and IPv6 traffic observed       | Internal discovery            |


(IV) Kali Linux – 192.168.100.40

| Finding        | Details                     | Risk |
| -------------- | --------------------------- | ---- |
| Open Ports     | None detected               | -    |
| Firewall State | Default hardened posture    | -    |
| Observation    | Hardened baseline confirmed | -    |


(D) Hardening Actions

Detailed remediation steps are documented in the `/fixes` directory.

| Area      | Action                                               |
| --------- | ---------------------------------------------------- |
| WinRM     | Restricted access scope and hardened authentication  |
| Win11/IIS | Corrected request filtering configuration            |
| Splunk    | Reduced web and management interface exposure        |
| Multicast | Disabled or limited LLMNR and mDNS where unnecessary |

Each fix is directly tied to findings from the scans above.


(E) MITRE ATT&CK Mapping: Identified findings are mapped to relevant MITRE ATT&CK techniques in `MITRE_MAPPING.md` to show how these exposures could be leveraged in real-world attacks.

(F) Screenshots: All screenshots are stored in the `/screenshots` directory.
