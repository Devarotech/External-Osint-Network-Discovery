<div align="center">

# External OSINT Footprinting & Active Network Discovery

**Offensive Security Assessment · Week 02 · Networkwalks Cybersecurity & Ethical Hacking Internship**

[![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue?logo=kalilinux)](https://www.kali.org/)
[![Scanning](https://img.shields.io/badge/Scanning-Nmap%20%7C%20Zenmap-red)](https://nmap.org/)
[![Focus](https://img.shields.io/badge/Focus-OSINT%20%26%20Network%20Discovery-green)]()
[![Status](https://img.shields.io/badge/Status-Completed-success)]()

</div>

## Overview

This repository documents a practical, non-destructive security assessment completed during Week 02 of the **Networkwalks Cybersecurity & Ethical Hacking Internship**.

The work covered two modules:

- **W2-PM1 — External Domain Footprinting:** OSINT, web technology fingerprinting, HTTP header inspection, WAF detection, and DNS enumeration using Kali Linux.
- **W2-PM5 — Active Network Scanning:** Local interface auditing, host discovery, port scanning, and network topology visualization using Windows, Nmap, and Zenmap.

The purpose was to collect and interpret reconnaissance evidence, identify attack-surface exposures, and propose defensive hardening measures. **No exploitation or malicious payload delivery was performed.**

## Objectives

1. Gather publicly observable information about an authorized domain.
2. Identify web technologies, DNS records, and HTTP response information.
3. Detect the presence of a Web Application Firewall.
4. Audit local network interfaces and IP configurations.
5. Discover active hosts and exposed TCP services in authorized networks.
6. Visualize discovered network relationships with Zenmap.
7. Assess the security relevance of observations and recommend remediation.

## Scope and Rules of Engagement

| Assessment area | Scope |
|---|---|
| External domain footprinting | `networkwalks.com` |
| External Nmap test target | `scanme.nmap.org` |
| Local virtual lab network | `10.0.0.0/24` |
| Wireless LAN | `192.168.43.0/24` |
| Approach | Authorized, non-destructive reconnaissance and scanning |

The report records written authorization for the external educational testing scope. Local network activities were performed in the user's own lab/administered environment. Testing must not be repeated against any system without explicit permission.

## Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Reconnaissance environment |
| `whois` | Domain registration and nameserver information |
| `whatweb` | Web technology fingerprinting |
| `nslookup` | DNS resolution |
| `curl -I` | HTTP response header inspection |
| `wafw00f` | Web Application Firewall detection |
| `dnsrecon` | DNS record enumeration |
| `ipconfig /all` | Windows interface and network configuration audit |
| Nmap | Host discovery and port/service scanning |
| Zenmap | Nmap GUI and topology visualization |

## Methodology and Key Commands

### Phase 1 — External Domain Footprinting (W2-PM1)

Commands executed from Kali Linux:

```bash
whois networkwalks.com
whatweb networkwalks.com
nslookup networkwalks.com
curl -I https://networkwalks.com
wafw00f networkwalks.com
dnsrecon -d networkwalks.com
```

The workflow collected domain registration details, identified web technologies and server information, resolved the domain, inspected HTTP response headers, fingerprinted the detected WAF, and enumerated DNS records.

### Phase 2 — Local Network Auditing and Active Scanning (W2-PM5)

Windows interface audit:

```cmd
ipconfig /all
```

Nmap scans recorded in the report:

```bash
nmap -T4 -F 10.0.0.10
nmap -T4 -F 192.168.43.27/24
nmap -T4 -A -v -Pn scanme.nmap.org
```

The activities identified local network configuration details, open services on the lab host, active devices on the wireless subnet, a Zenmap Fisheye topology view, and a 25-hop route to the authorized Nmap test host.

## Summary of Observations

| Observation | Reported result | Assessment note |
|---|---|---|
| Domain and DNS footprint | Registrar, nameservers, DNS records, and DNSSEC status identified | Reconnaissance information; review configuration and exposure |
| Web stack fingerprinting | Apache and WordPress-related technologies identified | Version disclosure is not proof of a vulnerability |
| WAF fingerprinting | ModSecurity (SpiderLabs) detected | Presence of a WAF does not establish its effectiveness |
| Local host scan | TCP 135, 139, and 445 reported open on `10.0.0.10` | Review whether these services are required and appropriately restricted |
| Wireless subnet discovery | Three active hosts reported | Maintain an authorized asset inventory |
| Topology mapping | Zenmap Fisheye view generated | Useful for documenting known network relationships |
| External route discovery | 25-hop route reported to `scanme.nmap.org` | Route visibility is not a vulnerability finding |

## Risk Assessment

The report categorized the following observations:

| Finding | Reported severity |
|---|---|
| CMS, plugin, and BIND version disclosure | Medium |
| DNSSEC unsigned and cPanel SRV records exposed | Medium |
| WordPress REST API references and server headers visible | Low |
| Web and mail services mapped to the same IPv4 address | Low |
| WAF vendor fingerprinted | Low |
| Active hosts and SMB/NetBIOS ports on the local LAN | Medium |

**Important interpretation:** These are reconnaissance findings and attack-surface observations, not confirmed exploitable vulnerabilities. Vulnerability validation would require a separate, explicitly authorized assessment. Public WordPress REST API availability, an open port, or a disclosed version should not automatically be labelled a vulnerability without further evidence.

## Defensive Recommendations

1. Reduce unnecessary software and server version disclosure.
2. Maintain a patch-management process for web applications, plugins, and server packages.
3. Review WordPress REST API exposure and apply access controls only where justified by application requirements.
4. Review DNSSEC and SPF configuration with the domain administrator.
5. Maintain and monitor the WAF and its rulesets.
6. Restrict unnecessary inbound SMB, NetBIOS, and RPC access on untrusted networks.
7. Perform periodic authorized asset discovery and investigate unknown devices.
8. Keep network topology and asset inventories current.
9. Document written authorization and rules of engagement before every assessment.

## Evidence


| Filename | Evidence |
|---|---|
| `01-whois.png` | Domain registration lookup |
<img width="273" height="197" alt="whois-cmd" src="https://github.com/user-attachments/assets/3081bd69-4489-4bc1-b35f-6d23aa70eb2a" />

| `02-whatweb.png` | Web technology fingerprinting |
<img width="279" height="171" alt="whatweb -cmd" src="https://github.com/user-attachments/assets/1ac3d769-3929-4b05-bab7-84c5ddbcacb2" />

| `03-nslookup.png` | DNS resolution |
<img width="123" height="75" alt="nslookup-cmd" src="https://github.com/user-attachments/assets/c2f1c257-553e-476a-ae28-404fd8d99958" />

| `04-curl-headers.png` | HTTP response headers |
<img width="277" height="145" alt="curl -I cmd" src="https://github.com/user-attachments/assets/9ed702ba-4699-4cf4-94a4-99806e28653b" />

| `05-Wafw00f.png` | WAF detection |
<img width="277" height="149" alt="wafw00f-cmd" src="https://github.com/user-attachments/assets/ef8a0a19-77b1-47c0-9894-43bc72627138" />

| `06-Dnsrecon.png` | DNS enumeration |
<img width="409" height="255" alt="dnsrecon-cmd" src="https://github.com/user-attachments/assets/bbbbf090-018b-42e4-8a9c-d95400b193f9" />

| `07-lab-interface.png` | Lab interface configuration |
<img width="447" height="297" alt="ipconfig_all" src="https://github.com/user-attachments/assets/d0ded1dc-28fa-4054-b72e-5be627b42aed" />

| `08-Zenmap-local-scan.png` | Local host scan |
<img width="852" height="382" alt="Ip-ZenMAP" src="https://github.com/user-attachments/assets/ee568fdd-4d83-4d67-8139-6c8fc305a05f" />

| `09-Zenmap-topology-redacted.png` | Wireless subnet topology |
<img width="405" height="331" alt="zenMap-Topology" src="https://github.com/user-attachments/assets/28e51bfb-4afa-478f-bf81-63c5743deb46" />

| `10-External-scan.png` | Authorized external scan |
<img width="605" height="346" alt="zenMapwith-lengend" src="https://github.com/user-attachments/assets/a0b84c28-e557-47ed-9d59-3b113709d111" />
| `11-Scanme-scan.png` | Authorized external scan |

## Repository Structure


```text
external-osint-network-discovery/
├── README.md
├── screenshots/
│   └── README.md
└── reports/
    └── README.md
```

## Skills Demonstrated

- Open-Source Intelligence (OSINT)
- External domain footprinting
- DNS enumeration and analysis
- Web technology fingerprinting
- HTTP response header inspection
- WAF detection
- Windows network configuration auditing
- Host discovery and TCP port scanning
- Nmap and Zenmap
- Network topology visualization
- Security risk assessment
- Technical documentation and remediation reporting

## Conclusion

This project strengthened my understanding of reconnaissance as a foundational part of penetration testing and defensive security. By combining external OSINT with active network discovery, I practiced collecting technical evidence, interpreting exposed services and infrastructure details, and translating observations into practical hardening recommendations.

The key lesson: **reconnaissance is not just collecting information; it is understanding what that information means for security.**

---

## Project Information

| Field | Details |
|---|---|
| Project | External OSINT Footprinting & Active Network Discovery |
| Program | Networkwalks Cybersecurity & Ethical Hacking Internship |
| Cohort | B084 Networkwalks |
| Modules | W2-PM1 and W2-PM5 |
| Assessment date | 13 November 2026 |
| Author | Najeem Omokunmi Atanda |
| GitHub | [@Devarotech](https://github.com/Devarotech) |

**Authorization and ethics:** This repository is for educational and defensive security learning. Only assess systems for which you have explicit authorization. The observations documented here do not constitute proof of exploitable vulnerabilities.
