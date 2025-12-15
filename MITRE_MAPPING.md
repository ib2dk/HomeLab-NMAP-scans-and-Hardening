  MITRE ATT&CK Mapping – Home Lab Nmap Findings

This document maps the findings from the Nmap scans in this home lab to relevant MITRE ATT&CK techniques. The goal is to show how the identified exposures could realistically be abused during different stages of an attack, not to claim exploitation occurred.


  Scope:
  Environment - Personal VMware-based home lab
  Network Range - 192.168.100.0/24
  Methodology - Nmap discovery, service enumeration, and script-based scanning
  Focus - Initial access, discovery, lateral movement, and impact

 
 Summary Table

| Finding           | MITRE Technique           | Technique ID |
| ----------------- | ------------------------- | ------------ |
| Exposed WinRM     | Remote Services           | T1021.006    |
| IIS Exposure      | Exploit Public-Facing App | T1190        |
| Splunk Interfaces | Exploit Public-Facing App | T1190        |
| Multicast Traffic | Network Service Discovery | T1046        |
| Auth Enumeration  | Account Discovery         | T1087        |
| Slowloris DoS     | Network DoS               | T1498        |



  1. Network Discovery & Enumeration

 (a) Technique: Network Service Discovery (T1046)
  	Evidence:  
  	- TCP SYN scan identified exposed services (WinRM, IIS, Splunk)
  	- UDP scan revealed multiple open|filtered discovery-related ports
  	- Service and version detection exposed running applications
    Relevance: An attacker can enumerate live services to understand the attack surface and identify potential entry points.

  (b) Technique: Network Sniffing / Multicast Discovery (T1040 – Supporting)
  	Evidence:  
  	- Discovery scripts identified mDNS and LLMNR traffic
  	- Multicast responses observed across multiple hosts
    Relevance: Multicast traffic can leak hostnames, services, and network structure, aiding internal reconnaissance.


  2. Authentication & Account Discovery

 (a) Technique: Account Discovery (T1087)
  	Evidence:  
  	- Authentication scripts identified exposed authentication surfaces
  	- Splunk interfaces accessible from the subnet
  	- WinRM reachable without network-level restriction
    Relevance: Attackers can enumerate valid users, roles, or authentication endpoints prior to credential attacks.


  3. Lateral Movement

   (a) Technique: Remote Services – WinRM (T1021.006)
  	Evidence:  
  	- TCP 5985 (WinRM) exposed on Windows Server 2025
  	- Service accessible across the subnet
    Relevance: With valid credentials, WinRM can be used to execute commands remotely and move laterally within the network.


  4. Application Layer Exposure

  (a) Technique: Exploit Public-Facing Application (T1190)
  	Evidence:  
  	- IIS web service exposed on Windows 11
  	- Splunk Web Interface exposed on TCP 8000

    Relevance: Web services increase attack surface and may be targeted for exploitation, misconfiguration abuse, or denial-of-service.


  5. Impact

   (a) Technique: Network Denial of Service (T1498)
  Evidence: Slowloris DoS vulnerability detected on Splunk services (CVE-2007-6750)
  Relevance: An attacker could degrade or disrupt service availability without needing authentication.

 
 NOTES:
  - No exploitation was performed.
  - All mappings are based on exposure and attacker capability, not confirmed compromise.
  - This mapping is intended for learning and defensive understanding.


 - Reference
MITRE ATT&CK Framework: [https://attack.mitre.org/](https://attack.mitre.org/)
