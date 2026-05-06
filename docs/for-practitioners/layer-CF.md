# Layer CF — Control Framework

**Position in the framework:** S4T = (G, RI, **CF**, OS, VA, L)
**Drives:** C(t) — Control Coverage and Quality Index
**Primary metric:** Percentage of risk-relevant control objectives implemented and verified

---

## What This Layer Does

The Control Framework layer answers a deceptively simple question: **what controls do you actually have in place, and do they cover the assets that matter most?**

In the S4T risk evolution equation:

```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

C(t) has the highest default coefficient (α = 0.35) — meaning control coverage has the largest single impact on risk reduction rate. Every asset without appropriate controls is risk accumulating unaddressed.

C(t) is formally defined as:
> The proportion of risk-relevant control objectives implemented and verified, weighted by asset criticality.

The weighting by asset criticality is important. A control gap on a system containing customer PII contributes more to risk than the same gap on a non-critical development server. The CF layer makes this weighting explicit.

---

## Prerequisites

Before implementing this layer, you should have:
- [ ] Risk appetite statement (from G layer)
- [ ] At least a draft security policy (from G layer)
- [ ] Commitment to complete an asset inventory as the first step of this layer

---

## CF Layer Components

### CF-1: Asset Inventory

**This is the most important step in the entire framework.** You cannot protect what you cannot see. An incomplete asset inventory means you have blind spots — systems with no controls, unmanaged endpoints, forgotten servers — that are invisible to your security programme.

**Asset inventory scope:** Everything that stores, processes, or transmits data your organisation cares about:
- Servers (physical and virtual)
- Workstations and laptops
- Mobile devices (if used for work)
- Network infrastructure (firewalls, switches, routers, WAPs)
- Cloud resources (VMs, storage buckets, databases, SaaS applications)
- IoT and OT devices (if applicable)
- User accounts (including service accounts)
- Third-party systems with access to your data

**Reference implementation:** [OCS Inventory](https://ocsinventory-ng.org/)

OCS Inventory provides automated asset discovery via agents deployed on endpoints, with a web-based management console. Use the deployment scripts in `/scripts/` for installation guidance.

**Asset classification:** For each asset, record:

| Field | Description | Example |
|---|---|---|
| Asset ID | Unique identifier | SRV-001 |
| Name | Hostname or descriptive name | payroll-db-01 |
| Type | Server / Workstation / Network / Cloud / IoT | Server |
| Owner | Business owner (person responsible) | Finance Director |
| Criticality | High / Medium / Low | High |
| Data classification | What data does it store/process? | Confidential (payroll data) |
| Location | Physical or cloud region | Data centre rack B3 / AWS sa-east-1 |
| OS / Platform | Operating system and version | Ubuntu 22.04 LTS |
| IP address | Primary IP | 192.168.10.50 |
| Internet-exposed? | Directly accessible from internet? | No |
| Last reviewed | Date of last review | 2025-01 |

**Criticality definition for your organisation:** Define what "High", "Medium", and "Low" mean in terms of business impact. Example:
- **High:** System outage causes > 4 hours business disruption OR stores/processes Confidential or Restricted data
- **Medium:** System outage causes 1–4 hours disruption OR stores Internal data
- **Low:** System outage causes < 1 hour disruption OR stores only Public data

**Asset inventory is never complete** — it is a living document. Establish a process for adding new assets when they are deployed and removing decommissioned assets. Review the inventory quarterly at minimum.

---

### CF-2: Control Mapping

**What it is:** For each asset, document which security controls are in place and verify they are actually operating correctly.

**S4T minimum control baseline by asset criticality:**

| Control | High Criticality | Medium Criticality | Low Criticality |
|---|---|---|---|
| Wazuh agent deployed | Required | Required | Recommended |
| File integrity monitoring | Required | Recommended | Optional |
| Vulnerability scanning | Weekly | Monthly | Quarterly |
| OS hardening baseline | Required | Required | Recommended |
| MFA for all access | Required | Required | Recommended |
| Automated patch management | Required | Required | Recommended |
| Network segmentation | Required | Recommended | Optional |
| Encrypted backups | Required | Required | Recommended |
| Access review | Quarterly | Bi-annual | Annual |

**Control verification:** Documenting that a control exists is not enough. Each control should be verified as actually operating. Examples:
- Wazuh agent: verify agent status is "Active" in the Wazuh Dashboard
- Backups: verify a backup was successfully restored (not just created) in the last 30 days
- Patch management: verify critical CVEs are patched within SLA via Wazuh vulnerability report
- MFA: verify MFA is enforced at the identity provider level, not just "available"

**Control gap documentation:** For each control gap identified, record:

| Asset | Missing Control | Risk | Remediation Plan | Target Date | Owner |
|---|---|---|---|---|---|
| payroll-db-01 | MFA for admin access | High | Implement TOTP for admin accounts | 2025-03-31 | IT Admin |

---

### CF-3: Security Hardening Baselines

**What it is:** A defined set of configuration standards that all systems of a given type must meet — the minimum secure configuration for servers, workstations, network devices, and applications.

**Reference standard:** [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/) provide hardening guidance for virtually every major platform and are freely available. S4T recommends CIS Benchmark Level 1 as the minimum baseline for all production systems.

**Critical hardening requirements (all platforms):**

**Operating System:**
- Remove or disable all unnecessary services and protocols
- Change all default credentials before connecting to network
- Enable automatic security updates for critical patches
- Configure local firewall to deny by default, allow by exception
- Disable USB storage if not operationally required
- Enable full-disk encryption (BitLocker for Windows, LUKS for Linux)

**Authentication:**
- Enforce strong password policy: minimum 12 characters, complexity required, no password reuse
- Disable local administrator accounts where possible (use centralised IAM)
- Configure account lockout after 5 failed attempts
- Disable interactive login for service accounts

**Logging:**
- Enable audit logging for authentication events, privilege use, and file system changes on critical directories
- Forward logs to Wazuh (centralised SIEM)
- Retain logs for at least 90 days (1 year recommended for regulated environments)

**Network:**
- Disable unused network interfaces
- Configure SSH key-based authentication only (disable password auth)
- Disable Telnet, FTP, and other unencrypted protocols
- Enable TLS 1.2 or higher for all encrypted communications; disable TLS 1.0 and 1.1

**Measuring hardening compliance:** Use CIS-CAT Pro (commercial) or [CIS-CAT Lite](https://www.cisecurity.org/cybersecurity-tools/cis-cat-pro/cis-csat-free-trial/) (free for most benchmarks) to automatically assess your systems against CIS Benchmarks. Target: > 80% compliance score on CIS Level 1 for all High criticality systems.

---

### CF-4: Configuration Management

**What it is:** A process for tracking and controlling changes to system configurations, ensuring that systems remain in their intended secure state.

**Why this matters:** Systems drift from their baseline configuration over time as administrators make changes, applications update themselves, and configurations are modified to solve operational problems. Without configuration management, your hardening work degrades invisibly.

**Minimum configuration management process:**

1. **Document baseline configurations** for each system type (use CIS Benchmarks as the reference)
2. **Use version control** for configuration files and scripts (Git)
3. **Change management process:** Any configuration change to a production system requires:
   - Written justification (why is this change needed?)
   - Approval from system owner
   - Documentation of what changed
   - Post-change verification that the system is still in compliance
4. **Automated configuration monitoring:** Wazuh's Security Configuration Assessment (SCA) module automatically checks systems against compliance baselines continuously

**Infrastructure as Code (IaC):** For cloud environments and new deployments, use tools like Ansible, Terraform, or Puppet to codify configurations. This ensures consistency, enables version control, and makes deviations from baseline detectable automatically.

---

### CF-5: Data Classification Enforcement

**What it is:** Ensuring that the data classification scheme defined in the G layer is actually applied to data in practice.

**Practical data classification implementation:**

| Classification | Storage | Transmission | Access | Retention |
|---|---|---|---|---|
| Public | Any | Any | Any | As needed |
| Internal | Organisational systems only | TLS required | All employees | 3 years |
| Confidential | Encrypted at rest | Encrypted TLS | Need-to-know | 5 years |
| Restricted | Encrypted, access logged | Encrypted TLS | Named individuals only | Per regulation |

**Data discovery:** Most organisations do not know where all their sensitive data is. Use a data discovery scan (tools: [OpenDLP](https://github.com/ezarko/opendlp), or manual search for common patterns like CPF, credit card numbers, email addresses) to find unclassified sensitive data and classify it appropriately.

---

## Measuring C(t)

C(t) — Control Coverage and Quality Index — is the proportion of risk-relevant control objectives implemented and verified, weighted by asset criticality.

**Practical C(t) calculation:**

1. List all High criticality assets and their required controls (from the baseline table in CF-2)
2. For each required control, verify it is implemented and operating (binary: 0 or 1)
3. Calculate coverage per asset: `(controls verified) / (controls required)`
4. Weight by criticality: High assets count 3x, Medium 2x, Low 1x
5. C(t) = weighted average across all assets

**Example:**

| Asset | Criticality | Controls Required | Controls Verified | Coverage | Weight |
|---|---|---|---|---|---|
| payroll-db-01 | High | 8 | 6 | 75% | 3 |
| mail-server-01 | High | 8 | 8 | 100% | 3 |
| workstation-finance-01 | Medium | 6 | 5 | 83% | 2 |
| dev-server-01 | Low | 4 | 3 | 75% | 1 |

```
C(t) = (0.75×3 + 1.00×3 + 0.83×2 + 0.75×1) / (3+3+2+1) = 7.16 / 9 = 0.80
```

The Assessment Tool computes this automatically from your answers to the CF-layer questions. Track C(t) monthly.

**C(t) improvement targets:**
- Starting C(t) < 0.40 (Initial): Focus on High criticality assets first, target 0.60 within 6 months
- C(t) 0.40–0.65 (Developing): Close remaining High criticality gaps, begin Medium assets, target 0.75 within 6 months
- C(t) 0.65–0.80 (Mature): Automate verification, extend to Low criticality, target 0.85+ within 12 months

---

## Common Mistakes in the CF Layer

**Starting with all assets at once.** A complete control mapping across all assets is overwhelming. Start with High criticality assets only, achieve full coverage, then expand to Medium.

**Documenting controls without verifying them.** A Wazuh agent that is installed but not sending data is not a control — it is a false sense of security. Verify every control is actually operating.

**Static asset inventory.** Assets are added and removed continuously. Without a process to update the inventory, it degrades rapidly and gaps appear invisibly.

**Treating hardening as a one-time task.** Systems drift from baseline. Automated continuous monitoring (Wazuh SCA) is the only way to maintain hardening compliance over time.

**Skipping data classification.** Without knowing which systems store sensitive data, you cannot correctly weight your control coverage. Classification is the foundation of prioritisation.

---

## Next Steps

After completing this layer:

1. Your C(t) baseline is established — track it monthly
2. Proceed to [Layer OS — Operational Security](layer-OS.md) to add continuous monitoring to the assets you have inventoried
3. Use the control gap list from CF-2 as your implementation backlog for the next 90 days

For questions, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
