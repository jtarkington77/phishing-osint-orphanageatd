# OSINT: orphanageatd[.]org & ScreenConnect Relay (15.204.43.235)

This repo contains OSINT artifacts tied to a phishing flow that delivered a renamed ScreenConnect client:

**Email → Google redirect → `orphanageatd[.]org` → `PdfEdgeViewer.exe` → ScreenConnect MSI → TLS beacon to 15.204.43.235**

## What this repo includes
- `targets/orphanageatd.org/` — DNS, headers, and TLS certificate details for the delivery host
- `targets/184.154.115.26/` — WHOIS/rDNS/IP info for the delivery IP (SingleHop/INAP, US)
- `targets/15.204.43.235/` — WHOIS/rDNS/ASN and connectivity for the ScreenConnect relay
- `notes/` — registrar WHOIS, name server IPs, ASN lookups
- `indicators.csv` — consolidated IOCs for defenders

## Summary
- The lure domain **orphanageatd[.]org** (PDR Registrar, 2021) resolved to **184.154.115.26** (US, shared hosting).
- The download path `/court/PdfEdgeViewer.exe` is an **EXE**, not a PDF.
- Post-execution, the host resolved the ScreenConnect relay domain and connected to **15.204.43.235** over TLS.
- The payload is a **legitimate remote-access client** delivered with a misleading name.

## Defensive Use
- Block/alert on `orphanageatd[.]org` and `instance-*-relay.screenconnect[.]com` where appropriate.
- Monitor outbound TLS to **15.204.43.235** and related ScreenConnect infrastructure.
- Hunt for ScreenConnect service/process creation and the specified registry changes.

*All data here is for defensive research and education. If you are the provider and believe this is in error, open an issue.*
