# Layer OS — Operational Security

**Position in the framework:** S4T = (G, RI, CF, **OS**, VA, L)
**Drives:** O(t) — Operational Maturity and Response Velocity
**Primary metric:** Mean Time to Respond (MTTR)

---

## What This Layer Does

The Operational Security layer is where your security programme becomes real. Governance sets the strategy, Risk Intelligence provides context, and the Control Framework defines what to implement — but OS is where those decisions translate into continuous, daily operations.

OS encompasses four integrated capabilities:

1. **Detection** — knowing when something is wrong
2. **Response** — containing and resolving incidents
3. **Patch management** — systematically reducing your vulnerability surface
4. **Identity and access management** — controlling who can do what

In the S4T risk evolution equation, O(t) is the coefficient on operational maturity:

```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

A higher O(t) means faster detection and response — which directly reduces risk accumulation rate. In the 18-month validation study, MTTR improvement from 72h to 18h (d = 3.9) was the primary driver of O(t) improvement and was directly attributable to the Orchestration layer's automated response workflows.

---

## Prerequisites

Before implementing this layer, you should have:
- [ ] Asset inventory completed (from CF layer)
- [ ] Risk appetite statement defined (from G layer)
- [ ] Network topology documented (from CF layer)
- [ ] At least one server or VM available for security tooling

If you are starting here without completing those prerequisites, go back to [Getting Started](getting-started.md).

---

## OS Layer Components

### OS-1: Endpoint Detection and Response (EDR)

**What it is:** Continuous monitoring of all endpoints — servers, workstations, laptops — for malicious activity, suspicious behaviour, and policy violations.

**Why it matters:** Without EDR, you are blind to what is happening on your endpoints. Most attacks involve endpoint compromise at some stage, and without visibility you cannot detect or respond.

**Reference implementation:** [Wazuh](https://wazuh.com/)

Wazuh is the recommended EDR/SIEM platform for S4T reference deployments. It is open source, actively maintained, and covers endpoint monitoring, log management, vulnerability detection, and compliance reporting in a single platform.

**Deployment steps:**

1. **Deploy Wazuh Server** — use the automated deployment script in `/scripts/autowazuh.sh`. This installs and configures Wazuh Manager, Indexer, and Dashboard on a single server (minimum 4 CPU cores, 8GB RAM recommended for up to 100 agents).

```bash
# From the S4T repository scripts directory
chmod +x autowazuh.sh
sudo ./autowazuh.sh
```

2. **Deploy agents on all endpoints.** Wazuh agents are lightweight (< 100MB) and available for Linux, Windows, and macOS. For Linux endpoints:

```bash
# On each endpoint, after obtaining the Wazuh agent package
sudo WAZUH_MANAGER="<your-wazuh-server-ip>" \
     WAZUH_AGENT_NAME="<hostname>" \
     dpkg -i wazuh-agent_*.deb
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

3. **Configure baseline detection rules.** S4T minimum baseline use-cases for Wazuh:
   - Failed authentication attempts (> 5 in 60 seconds → alert)
   - Privilege escalation (sudo usage by non-authorised users → alert)
   - Lateral movement indicators (new connections to internal hosts on non-standard ports)
   - File integrity monitoring on critical directories (`/etc`, `/bin`, `/usr/bin`, Windows `System32`)
   - Process creation monitoring (new processes spawned by web servers or databases)

4. **Configure the Wazuh Dashboard** for daily use. Create saved searches for:
   - All critical and high severity alerts (review daily)
   - Authentication failures by source IP (review daily)
   - Agent connectivity status (any offline agents → investigate)

**Measuring O(t) for EDR coverage:**
- Target: 100% of in-scope endpoints running Wazuh agents
- Metric: `(endpoints with active agent) / (total in-scope endpoints)`
- Check weekly via Wazuh Dashboard → Agents

---

### OS-2: SIEM (Security Information and Event Management)

**What it is:** Centralised collection, correlation, and analysis of security events from across your environment. Wazuh includes SIEM functionality natively.

**Key use-cases to implement first:**

| Use-case | Priority | Detection logic |
|---|---|---|
| Brute force login | High | > 5 failed logins from same IP in 60s |
| Account lockout | High | Account locked after failed attempts |
| Off-hours access | Medium | Successful login outside business hours |
| New admin account | High | New user added to privileged group |
| Outbound to threat intel IPs | High | Connection to known-malicious IP (feed from RI layer) |
| Large data exfiltration | High | > 100MB outbound to external IP in short window |
| Lateral movement | High | SMB/RDP connections between internal hosts |

**Integration with RI layer:** Configure Wazuh to consume threat intelligence feeds from MISP or OpenCTI. Any connection to a known-malicious IP or domain triggers an alert automatically.

**Alert tuning is critical.** Untuned SIEMs generate thousands of false positives per day, creating alert fatigue that causes real incidents to be missed. Dedicate the first 30 days after deployment to tuning — suppress known-good events and refine thresholds until your daily alert volume is manageable (target: < 50 actionable alerts per day for a small organisation).

---

### OS-3: Patch Management

**What it is:** A systematic, documented process for identifying, prioritising, and applying software patches and security updates.

**Why it matters:** Unpatched vulnerabilities are the most common initial access vector. In the validation study, critical vulnerability reduction from 100 to 33 per month (−67%) was achieved primarily through implementing structured patch management with defined SLAs.

**S4T patch management SLAs:**

| Severity | CVSS Score | Patch SLA |
|---|---|---|
| Critical | 9.0 – 10.0 | 24 hours |
| High | 7.0 – 8.9 | 7 days |
| Medium | 4.0 – 6.9 | 30 days |
| Low | 0.1 – 3.9 | 90 days |

These are the default SLAs derived from the validation study. Your risk appetite statement may require more aggressive timelines for internet-exposed systems.

**Implementation steps:**

1. **Enable Wazuh vulnerability detection.** Wazuh scans agents for installed packages and correlates against the NVD CVE database automatically.

2. **Configure vulnerability reports.** Set up a weekly automated report of all critical and high CVEs across your agent fleet. Review every Monday morning.

3. **Document your patch process.** Define: Who approves patches? Who applies them? How are production systems tested before patching? What is the rollback procedure?

4. **Track SLA compliance.** Metric: `(patches applied within SLA) / (total patches due)`. Target: > 90% SLA compliance for critical and high severity.

**For Windows environments:** Windows Server Update Services (WSUS) or Microsoft Endpoint Configuration Manager integrate well with Wazuh for combined patch tracking and deployment.

**For Linux environments:** Automate package updates with `unattended-upgrades` (Debian/Ubuntu) or `dnf-automatic` (RHEL/Fedora) for non-breaking security patches, with manual review for major version updates.

---

### OS-4: Identity and Access Management (IAM)

**What it is:** Controls over who has access to what systems and data, under what conditions, and with what level of privilege.

**IAM is the highest-leverage control in most organisations.** Credential theft and privilege abuse appear in the majority of significant breaches. Strong IAM reduces the blast radius of any compromise.

**S4T IAM baseline requirements:**

**Multi-Factor Authentication (MFA)**
- Required for: all remote access (VPN, RDP, SSH), all cloud services, all administrative consoles, all email access
- Recommended: TOTP-based MFA (Google Authenticator, Authy) or hardware keys (YubiKey)
- Not acceptable as a second factor: SMS-based OTP (SIM swapping risk)

**Principle of Least Privilege**
- Every user account should have only the permissions required for their role
- No shared administrative accounts
- Administrative actions should be performed with dedicated admin accounts, not day-to-day accounts
- Review and remove all dormant accounts (no login in 90+ days)

**Privileged Access Management (PAM)**
- All privileged access (root, Domain Admin, database admin) should be logged and audited
- Consider a PAM solution for larger environments ([CyberArk](https://www.cyberark.com/), [Teleport](https://goteleport.com/) open source, [HashiCorp Vault](https://www.vaultproject.io/) for secrets)
- For smaller environments: `sudo` logging configured in Wazuh is a minimum baseline

**Service accounts**
- Document all service accounts and their purpose
- Service accounts should have the minimum permissions required
- Service account credentials should be rotated at least annually
- Never use service accounts for interactive login

**Measuring IAM coverage:**
- Metric: `(accounts with MFA enabled) / (total accounts requiring MFA)`
- Target: 100% MFA coverage for all remote access and privileged accounts
- Check monthly via your identity provider's admin console

---

### OS-5: Incident Response

**What it is:** A documented, tested process for detecting, containing, eradicating, and recovering from security incidents.

**The incident response plan does not need to be long.** A one-page document that answers the five key questions is better than a 50-page manual that no one reads:

1. **Who declares an incident?** (Define the threshold — e.g., any Wazuh critical alert or confirmed malware detection)
2. **Who is notified, and how fast?** (Names, phone numbers, escalation path)
3. **Who has authority to isolate affected systems?** (Often the most important decision in the first 30 minutes)
4. **Where is the evidence preserved?** (Logs, memory dumps, disk images — and who is responsible)
5. **When is the incident considered resolved?** (Root cause identified, vulnerability remediated, monitoring confirmed clean)

**Incident severity classification:**

| Severity | Definition | Response time |
|---|---|---|
| P1 — Critical | Active breach, data exfiltration in progress, ransomware | Immediate (< 15 min) |
| P2 — High | Confirmed malware, credential compromise, C2 communication | < 1 hour |
| P3 — Medium | Suspicious activity, policy violation, unconfirmed indicator | < 4 hours |
| P4 — Low | Minor policy violation, informational alert | < 24 hours |

**Integration with Wazuh:** Configure Wazuh active response to automatically isolate endpoints when specific rules fire (e.g., confirmed ransomware indicators, active C2 communication). This reduces MTTR by eliminating the human decision step for the most time-critical scenarios.

**Test your IR plan.** Run a tabletop exercise at least once per year — simulate a scenario (ransomware, credential breach, data exfiltration) and walk through your response plan. The goal is to identify gaps before an actual incident reveals them.

---

### OS-6: Network Segmentation

**What it is:** Dividing your network into isolated zones that limit the lateral movement an attacker can achieve after initial compromise.

**Minimum viable segmentation for most organisations:**

| Zone | Description | What belongs here |
|---|---|---|
| DMZ | Internet-facing services | Web servers, mail servers, VPN endpoints |
| Internal | Standard user workstations | Employee laptops, desktops |
| Servers | Internal servers | File servers, database servers, application servers |
| Management | Security and administration | Wazuh, monitoring, backup systems |
| OT/IoT | Operational technology (if applicable) | Industrial systems, IP cameras, printers |

**Implement segmentation with pfSense or OPNsense.** Both support VLAN-based segmentation with firewall rules between zones. Use the deployment scripts in `/scripts/` for reference configurations.

**Key rules to implement:**
- No direct traffic from Internal to Servers without explicit allow rules
- Management zone can reach all other zones; other zones cannot reach Management
- DMZ cannot initiate connections to Internal or Servers
- All inter-zone traffic is logged

---

## Measuring O(t)

O(t) — Operational Maturity and Response Velocity — is computed from two primary inputs:

**Detection rate:** What percentage of simulated attacks (from the VA layer's BAS campaigns) does your OS layer detect?

**Mean Time to Respond (MTTR):** From alert generation to incident resolution, how many hours does it take on average?

The S4T Assessment Tool computes O(t) from your answers to the OS-layer questions. To track it manually:

```
O(t) = 0.5 × (Detection_Rate) + 0.5 × (1 - normalised_MTTR)
```

Where normalised MTTR maps your actual MTTR to a 0–1 scale:
- MTTR ≥ 72h → 0.0
- MTTR = 24h → 0.5
- MTTR ≤ 4h → 1.0

**Monthly tracking table:**

| Month | MTTR (hours) | Detection Rate (%) | O(t) | Notes |
|---|---|---|---|---|
| Baseline | | | | |
| Month 3 | | | | |
| Month 6 | | | | |
| Month 12 | | | | |

---

## Common Mistakes in the OS Layer

**Deploying EDR without tuning.** An untuned Wazuh deployment will generate thousands of low-quality alerts per day. Spend the first 30 days tuning before expecting operational value.

**No defined IR process before first incident.** When an actual incident occurs, you do not have time to design your response. Define and document the process before you need it.

**MFA on some accounts but not all.** A single account without MFA is a potential entry point. Coverage must be complete for remote access and privileged accounts.

**Patch management without SLAs.** "We patch when we can" is not patch management. Define SLAs and measure compliance.

**No segmentation.** A flat network means a compromised workstation can reach every server. Segmentation limits blast radius at minimal cost.

---

## Next Steps

After completing this layer:

1. Run your first BAS campaign (see [Layer VA](layer-VA.md)) to measure what your new OS controls actually detect
2. Review your Security Score — O(t) improvement should be visible in the next Assessment
3. Proceed to [Layer RI — Risk Intelligence](layer-RI.md) to add threat context to your SIEM

For questions or implementation help, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
