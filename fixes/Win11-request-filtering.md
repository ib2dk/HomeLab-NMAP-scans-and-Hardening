Win11(IIS) Request Filtering Fix

Issue: IIS was running with a request filtering configuration error (Property `allowUnlisted` not found under requestFiltering).

Evidence:
- IIS error during configuration
- Nmap detected HTTP service on port 80
- Default IIS configuration exposed

Risk:
- Weakened web-layer protections
- Increased attack surface for malformed requests
- Potential abuse of default IIS behavior

Fix Applied:
- Opened IIS Manager
- Corrected request filtering configuration
- Ensured rules align with supported IIS schema

Validation:
- IIS configuration error resolved
- Web service functional after fix
- No additional misconfiguration detected during re-scan
