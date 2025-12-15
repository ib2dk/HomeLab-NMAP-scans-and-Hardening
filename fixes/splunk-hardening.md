Splunk Server Hardening – Ubuntu Linux

Issue: Splunk Web and Management interfaces were exposed on the network.

Evidence:
- Port 8000: Splunk Web Interface
- Port 8089: Splunk Management API
- Slowloris DoS vulnerability detected (CVE-2007-6750)

Risk:
- Denial-of-Service attack
- Service and user enumeration
- Exposure of management interface to unnecessary hosts

Fix Applied:
- Restricted access to Splunk interfaces
- Reduced exposure of management API
- Reviewed service bindings and access scope

Validation:
- Re-scanned exposed ports
- Confirmed reduced accessibility
- No functional impact on Splunk operations
