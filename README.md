# Practical Network Defense

Team project for Sapienza’s **Practical Network Defense** course. We hardened a multi-zone lab (WAN / DMZ / Internal / Clients) using **OPNsense** firewalls, enforced least-privilege segmentation, enabled proxy-gated egress, centralized logging to **rsyslog + Graylog**, and provided controlled remote access via **road-warrior** and **site-to-site IPSec** VPNs. Validation included connectivity/diagnostic checks, `tcpdump` SNAT tracing, and **Greenbone (GVM)** scans.

---

## Objectives
- Implement the given security policy across firewalls and hosts.
- Provide secure remote access (RW VPN + site-to-site).
- Justify hardening measures and document testing & results.

## Implementation highlights
- **Policy & segmentation:** deny-by-default; only DMZ web exposed; internal DNS resolver; anti-spoofing and clean rule base.
- **Egress control:** Clients’ HTTP/HTTPS forced through a **proxy**; NAT preserved so internal hosts exit via the Main FW public IP.
- **Management plane:** FW GUI over **HTTPS**; **NTP** for time-aligned logs; centralized logs to **rsyslog → Graylog** (separate inputs).
- **Remote access:** **road-warrior VPN** on Main FW (role-based) + **site-to-site IPSec** between Main/Internal.
- **Security scanning:** allowlisted paths for **GVM**; monitored in Graylog.

## Validation
- Functional & negative tests (ping/traceroute only where allowed; proxy-gated browsing from Clients).
- `tcpdump` to verify SNAT/flows; Graylog to confirm log intake and correlation.
- **Greenbone** scans to assess exposure and verify policy effectiveness.
