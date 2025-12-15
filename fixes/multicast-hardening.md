Multicast & Discovery Hardening (LLMNR / mDNS)

Issue: Discovery scripts identified multicast and name resolution traffic on the network.

Evidence:
- Nmap discovery script results
- LLMNR and mDNS traffic observed
- IPv6-related discovery behavior

Risk:
- Network reconnaissance
- Name resolution poisoning
- Leakage of internal host information

Fix Applied:
- Disabled or limited LLMNR where unnecessary
- Reduced mDNS exposure
- Reviewed IPv6 and discovery-related settings

Validation:
- Discovery scripts show reduced multicast responses
- No negative impact on normal network operations
