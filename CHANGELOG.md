# Changelog — S4T Framework

All notable changes to the S4T Framework are documented here.

---

## [3.2] — 2025 (Active Development)

### Added
- Advanced threat intelligence platform integration
- Automated orchestration improvements
- Expanded deployment documentation for multi-datacenter environments
- Public download area with adoption metrics at sec4.tech

### Changed
- Refined incident response playbooks
- Updated hardening baselines for Wazuh and pfSense

---

## [3.0] — December 2024

### Added
- **Dynamic Risk Model**: differential equation formalizing cyber risk evolution over time (`dR/dt`)
- **Security Score metric**: computable, real-time maturity benchmarking (`S(t)`)
- **Orchestration-Intelligence coupling**: self-adjusting automation architecture
- BAS (Breach and Attack Simulation) integration for continuous validation
- Empirical validation across 5 organizational environments (18-month longitudinal study)
- Case studies: financial institution (Brazil) and healthcare network

### Changed
- Framework formally defined as 6-tuple: `S4T = (G, RI, CF, OS, VA, L)`
- Risk model upgraded from static `R = f(T, V, C, E)` to dynamic `R(t)`
- Technology-agnostic reference implementation documented

---

## [2.5] — 2023

### Added
- Inventory & Governance pillar with OCS Inventory integration
- Expansion to Germany and Argentina
- Growing adoption base in Brazil across logistics, communications, and accounting sectors

### Changed
- Refined deploy scripts for Wazuh and Zabbix
- Improved documentation for multi-site deployments

---

## [2.0] — 2022

### Added
- Academic paper published: *S4T Framework v2.0: A Resilience-Driven Cybersecurity Framework*
- International expansion: Chile, Peru, United States
- Five core domains formalized:
  1. Governance and Leadership
  2. Risk and Resilience Management
  3. Security Architecture and Engineering
  4. Threat Detection and Intelligence
  5. Incident Response and Recovery
- Resilience lifecycle model (prevention → detection → response → recovery)

### Changed
- Framework repositioned from internal methodology to open academic contribution
- License: Creative Commons Attribution 4.0 International (CC BY 4.0)

---

## [1.5] — 2021

### Added
- Wazuh integration as primary EDR/SIEM platform
- Automated deploy scripts (`autowazuh.sh`)
- Deployment time reduced from days to hours via automation

### Changed
- Detection and response pillar expanded significantly

---

## [1.0] — 2020

### Added
- Four pillars formally defined: Perimeter Protection, Detection & Response, Inventory & Governance, Resilience & Recovery
- First production deployment in Brazil
- pfSense hardened build as perimeter control
- Proxmox VE + PBS as resilience layer

---

## [Concept] — 2019

- Initial experiments in infrastructure security hardening
- First scripts for automated configuration and deploy
- Lab environment testing across firewall, monitoring, and backup components
- Problem statement identified: fragmentation between security tools without unified governance
