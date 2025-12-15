WinRM Hardening – Windows Server 2025

Issue: Nmap scans identified TCP port 5985 (WinRM) exposed on the domain controller and reachable from the entire subnet.

Evidence:
- Scan: TCP SYN / Service Detection
- Port: 5985/tcp
- Service: Microsoft HTTPAPI (WinRM)

Risk:
- Lateral movement using valid domain credentials
- Remote command execution if an account is compromised
- Expanded attack surface for internal attackers

Fix Applied:
- Restricted WinRM access to specific management hosts
- Verified firewall rules to limit subnet-wide access
- Ensured WinRM is not exposed unnecessarily

Validation:
- Re-ran Nmap scan
- Confirmed restricted access behavior
- No unintended service exposure observed
