# Findings

## Program Overview

Internal vulnerability scanning conducted against the full `192.168.0.0/24` lab network using **Greenbone Community Edition (OpenVAS)**. The lab simulates a small enterprise environment built on a two-node Proxmox cluster, running Windows Server 2022 (Active Directory), Wazuh SIEM, and supporting Linux VMs.

Findings are documented using professional audit observation methodology — Condition, Criteria, Cause, Risk, and Recommendation — and mapped to the **NIST Cybersecurity Framework (CSF) 2.0**.

This folder is maintained as an ongoing vulnerability management program, not a one-time exercise. Reports will be added as subsequent scans are conducted and remediations are validated.

---

## Assessments

| Date | Scope | Tool | Findings | Remediation Status | Report |
|---|---|---|---|---|---|
| April 2026 | 192.168.0.0/24 — All active hosts | Greenbone CE (OpenVAS) | 3 Medium, 17 Low | Open — pending | [View Report](2026-04_Kelley_Homelab_Vulnerability_Assessment.pdf) |

---

## April 2026 Assessment — Summary

**8 hosts scanned. 20 findings identified. No High or Critical findings.**

| Severity | Count | Key Findings |
|---|---|---|
| Medium | 3 | Cleartext HTTP on gateway, weak RSA certificate, SSL renegotiation DoS on Wazuh SIEM |
| Low | 17 | Weak SSH MAC algorithms (systemic — 5 hosts), TCP/ICMP timestamp disclosure (all hosts) |
| High / Critical | 0 | — |

### Notable Observations
- The SSL/TLS renegotiation vulnerability (Finding 03) exists on the Wazuh SIEM itself — the security monitoring infrastructure. This illustrates why security tools must be hardened with the same rigor as the systems they monitor.
- The weak SSH MAC finding appearing across five of eight hosts indicates a systemic configuration gap rather than an isolated misconfiguration — pointing to the absence of a hardening baseline at deployment.
- The absence of High and Critical findings indicates reasonable default security posture. Remaining findings are configuration hardening items.

---

## NIST CSF 2.0 Mapping

All findings map to the **Protect (PR)** function, with the scan activity itself mapping to **Identify (ID)**.

| Finding | CSF Function | Category | Subcategory |
|---|---|---|---|
| Cleartext HTTP transmission | Protect | Data Security | PR.DS-02 |
| Weak RSA certificate | Protect | Data Security | PR.DS-02 |
| SSL renegotiation DoS (Wazuh) | Protect | Platform Security | PR.PS-02 |
| Weak SSH MAC algorithms | Protect | Platform Security | PR.PS-02 |
| TCP timestamp disclosure | Protect | Platform Security | PR.PS-01 |
| ICMP timestamp disclosure | Protect | Platform Security | PR.PS-01 |
| Greenbone scan activity | Identify | Risk Assessment | ID.RA-01 |

---

## Folder Structure

```
findings/
├── README.md
└── 2026-04_Kelley_Homelab_Vulnerability_Assessment.pdf
```

---

## Tools

| Tool | Version | Role |
|---|---|---|
| Greenbone Community Edition (OpenVAS) | Latest CE | Vulnerability scanning |
| Kali Linux VM | — | Scanner host (192.168.0.105) |

---

*Part of a self-directed IT audit and GRC skills development program. Environment built to simulate enterprise controls for hands-on practice with vulnerability management, SIEM deployment, and framework mapping.*
