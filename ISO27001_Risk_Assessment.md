# ISO 27001:2022 — Information Security Risk Assessment
## TechVision Consulting Ltd. — Hypothetical Scenario

**Organization:** TechVision Consulting Ltd.
**Scope:** All information assets in scope of the ISMS
**Methodology:** ISO/IEC 27005 — Risk-based approach
**Risk Owner:** Information Security Analyst
**Review Date:** Month 2 (initial baseline)
**Next Review:** Month 8 / annually thereafter

---

## Risk Methodology

### Scoring Scale

**Likelihood**

| Score | Level | Definition |
|-------|-------|------------|
| 1 | Rare | Unlikely to occur; no known history |
| 2 | Unlikely | Could occur but not expected |
| 3 | Possible | May occur occasionally |
| 4 | Likely | Will probably occur |
| 5 | Almost Certain | Expected to occur regularly |

**Impact**

| Score | Level | Definition |
|-------|-------|------------|
| 1 | Negligible | Minimal disruption, no data loss, no financial impact |
| 2 | Minor | Limited disruption, minor data exposure, small financial impact |
| 3 | Moderate | Significant disruption, some data loss, moderate financial/reputational impact |
| 4 | Major | Serious disruption, significant data breach, major financial/legal impact |
| 5 | Critical | Full business disruption, major breach, regulatory fines, loss of client trust |

**Risk Score = Likelihood × Impact**

| Score Range | Risk Level | Action |
|-------------|------------|--------|
| 1–4 | Low | Accept or monitor |
| 5–9 | Medium | Treat within 6 months |
| 10–16 | High | Treat within 3 months |
| 17–25 | Critical | Treat immediately |

### Risk Treatment Options

- **Mitigate** — Implement controls to reduce likelihood or impact
- **Accept** — Document and accept residual risk (within risk appetite)
- **Transfer** — Insurance, third-party (e.g., cyber insurance)
- **Avoid** — Discontinue the activity causing the risk

---

## Asset Inventory (In-Scope)

| Asset ID | Asset Name | Type | Owner | Classification |
|----------|------------|------|-------|----------------|
| A-01 | Client project data | Data | Project Manager | Confidential |
| A-02 | Employee PII (HR records) | Data | HR Director | Restricted |
| A-03 | Source code repositories | Data/Software | CTO | Confidential |
| A-04 | Cloud infrastructure (AWS, Azure) | Infrastructure | IT Manager | Internal |
| A-05 | Email system (M365) | Software | IT Manager | Internal |
| A-06 | Financial records | Data | CFO | Restricted |
| A-07 | Corporate laptops / endpoints | Hardware | IT Manager | Internal |
| A-08 | Office network and Wi-Fi | Infrastructure | IT Manager | Internal |
| A-09 | CRM / project management tool | Software | Operations | Internal |
| A-10 | Backup and DR systems | Infrastructure | IT Manager | Internal |
| A-11 | Vendor / third-party access credentials | Data | IT Manager | Restricted |
| A-12 | Authentication systems (SSO, IAM) | Software | IT Manager | Restricted |

---

## Risk Register

### RISK-001 — Phishing attack leading to credential compromise

| Field | Detail |
|-------|--------|
| **Asset** | A-05 (Email), A-12 (IAM), A-01 (Client data) |
| **Threat** | External attacker sends phishing email to employee |
| **Vulnerability** | Insufficient security awareness training; no email sandboxing |
| **Likelihood** | 5 — Almost Certain (phishing is the #1 attack vector for consulting firms) |
| **Impact** | 4 — Major (credential theft → lateral movement → client data breach) |
| **Risk Score** | **20 — Critical** |
| **Treatment** | Mitigate |
| **Controls** | A.6.3 (awareness training), A.8.5 (MFA), A.8.7 (email filtering/AV) |
| **Residual Likelihood** | 3 |
| **Residual Impact** | 3 |
| **Residual Score** | **9 — Medium** |
| **Owner** | IT Manager + HR |
| **Target Date** | Month 2 |
| **Status** | 🔄 In Treatment |

---

### RISK-002 — Ransomware attack encrypting client and internal data

| Field | Detail |
|-------|--------|
| **Asset** | A-01, A-03, A-04, A-10 |
| **Threat** | Ransomware deployed via phishing or unpatched vulnerability |
| **Vulnerability** | Unpatched endpoints; no network segmentation; backup not tested |
| **Likelihood** | 4 — Likely |
| **Impact** | 5 — Critical (full data loss, business disruption, client notification) |
| **Risk Score** | **20 — Critical** |
| **Treatment** | Mitigate |
| **Controls** | A.8.7 (AV/EDR), A.8.13 (backups), A.8.14 (redundancy), A.8.8 (patching), A.8.22 (segmentation) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 3 |
| **Residual Score** | **6 — Medium** |
| **Owner** | IT Manager |
| **Target Date** | Month 3 |
| **Status** | ⏳ Planned |

---

### RISK-003 — Insider threat: data exfiltration by employee

| Field | Detail |
|-------|--------|
| **Asset** | A-01, A-02, A-03, A-06 |
| **Threat** | Disgruntled or opportunistic employee copies and leaks data |
| **Vulnerability** | No DLP tool; no user behavior monitoring; excessive access rights |
| **Likelihood** | 3 — Possible |
| **Impact** | 4 — Major (client data breach, reputational damage, legal liability) |
| **Risk Score** | **12 — High** |
| **Treatment** | Mitigate |
| **Controls** | A.8.12 (DLP), A.5.18 (access reviews), A.8.16 (monitoring), A.5.3 (SoD) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 3 |
| **Residual Score** | **6 — Medium** |
| **Owner** | IT Manager + HR |
| **Target Date** | Month 5 |
| **Status** | ⏳ Planned |

---

### RISK-004 — Unauthorized access to cloud infrastructure

| Field | Detail |
|-------|--------|
| **Asset** | A-04 (AWS/Azure), A-01, A-03 |
| **Threat** | Attacker exploits misconfigured cloud resource or stolen IAM credentials |
| **Vulnerability** | No formal cloud security baseline; privileged accounts not well managed |
| **Likelihood** | 4 — Likely |
| **Impact** | 4 — Major (data exposure, service disruption, compliance breach) |
| **Risk Score** | **16 — High** |
| **Treatment** | Mitigate |
| **Controls** | A.5.23 (cloud security), A.8.2 (privileged access), A.8.5 (MFA), A.8.9 (config mgmt) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 3 |
| **Residual Score** | **6 — Medium** |
| **Owner** | IT Manager |
| **Target Date** | Month 3 |
| **Status** | 🔄 In Treatment |

---

### RISK-005 — Third-party / vendor data breach

| Field | Detail |
|-------|--------|
| **Asset** | A-01, A-11 (vendor credentials) |
| **Threat** | A vendor or contractor with access to TechVision data suffers a breach |
| **Vulnerability** | Inconsistent vendor security assessments; no supply chain risk program |
| **Likelihood** | 3 — Possible |
| **Impact** | 4 — Major (client data breach via third party; regulatory liability) |
| **Risk Score** | **12 — High** |
| **Treatment** | Mitigate + Transfer |
| **Controls** | A.5.19 (vendor risk), A.5.20 (supplier agreements), A.5.21 (ICT supply chain) |
| **Additional** | Cyber insurance (transfer residual) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 3 |
| **Residual Score** | **6 — Medium** |
| **Owner** | Procurement + Legal |
| **Target Date** | Month 6 |
| **Status** | ⏳ Planned |

---

### RISK-006 — Loss or theft of employee laptop

| Field | Detail |
|-------|--------|
| **Asset** | A-07 (endpoints), A-01, A-02 |
| **Threat** | Laptop stolen from employee while working remotely or traveling |
| **Vulnerability** | No remote wipe enforced; disk encryption inconsistent |
| **Likelihood** | 3 — Possible |
| **Impact** | 3 — Moderate (data on device exposed if unencrypted) |
| **Risk Score** | **9 — Medium** |
| **Treatment** | Mitigate |
| **Controls** | A.7.9 (off-premises assets), A.8.1 (endpoint management), MDM enrollment |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 2 |
| **Residual Score** | **4 — Low** |
| **Owner** | IT Manager |
| **Target Date** | Month 2 |
| **Status** | 🔄 In Treatment |

---

### RISK-007 — Non-compliance with GDPR (EU client data)

| Field | Detail |
|-------|--------|
| **Asset** | A-01, A-02 (EU data subjects) |
| **Threat** | Data breach or improper handling of EU personal data triggers GDPR enforcement |
| **Vulnerability** | Incomplete DPIAs; no Data Protection Officer; retention schedule not enforced |
| **Likelihood** | 3 — Possible |
| **Impact** | 4 — Major (fines up to 4% global revenue; client contract penalties) |
| **Risk Score** | **12 — High** |
| **Treatment** | Mitigate |
| **Controls** | A.5.34 (PII protection), A.5.31 (legal requirements), A.5.33 (records), A.5.12 (classification) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 3 |
| **Residual Score** | **6 — Medium** |
| **Owner** | Legal + Analyst |
| **Target Date** | Month 4 |
| **Status** | ⏳ Planned |

---

### RISK-008 — Vulnerable or unpatched software exploited

| Field | Detail |
|-------|--------|
| **Asset** | A-04, A-07, A-09 |
| **Threat** | Attacker exploits known CVE in unpatched system |
| **Vulnerability** | No formal patch management schedule; vulnerability scanning is ad hoc |
| **Likelihood** | 4 — Likely |
| **Impact** | 3 — Moderate (system compromise, potential data exposure) |
| **Risk Score** | **12 — High** |
| **Treatment** | Mitigate |
| **Controls** | A.8.8 (vulnerability management), A.8.9 (config baseline), A.8.19 (software install) |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 2 |
| **Residual Score** | **4 — Low** |
| **Owner** | IT Manager |
| **Target Date** | Month 3 |
| **Status** | ⏳ Planned |

---

### RISK-009 — Production data used in development/testing environments

| Field | Detail |
|-------|--------|
| **Asset** | A-01, A-02, A-03 |
| **Threat** | Developer inadvertently exposes client or employee PII via test environment |
| **Vulnerability** | No data masking; no test data management procedure |
| **Likelihood** | 3 — Possible |
| **Impact** | 3 — Moderate (data exposure, client contract breach) |
| **Risk Score** | **9 — Medium** |
| **Treatment** | Mitigate |
| **Controls** | A.8.33 (test information), A.8.11 (data masking), A.8.31 (environment separation) |
| **Residual Likelihood** | 1 |
| **Residual Impact** | 2 |
| **Residual Score** | **2 — Low** |
| **Owner** | CTO / Dev Lead |
| **Target Date** | Month 4 |
| **Status** | ⏳ Planned |

---

### RISK-010 — Business disruption due to cloud provider outage

| Field | Detail |
|-------|--------|
| **Asset** | A-04, A-10 |
| **Threat** | AWS or Azure region outage disrupts client delivery |
| **Vulnerability** | No multi-region redundancy; DR plan not tested |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 4 — Major (client SLA breach, revenue loss) |
| **Risk Score** | **8 — Medium** |
| **Treatment** | Mitigate + Transfer |
| **Controls** | A.8.14 (redundancy), A.5.29 (IS during disruption), A.5.30 (ICT continuity) |
| **Additional** | Business interruption insurance |
| **Residual Likelihood** | 2 |
| **Residual Impact** | 2 |
| **Residual Score** | **4 — Low** |
| **Owner** | IT Manager |
| **Target Date** | Month 6 |
| **Status** | ⏳ Planned |

---

## Risk Summary Dashboard

| Risk ID | Risk Name | Inherent Score | Level | Treatment | Residual Score | Status |
|---------|-----------|----------------|-------|-----------|----------------|--------|
| RISK-001 | Phishing / credential compromise | 20 | 🔴 Critical | Mitigate | 9 | 🔄 In Treatment |
| RISK-002 | Ransomware | 20 | 🔴 Critical | Mitigate | 6 | ⏳ Planned |
| RISK-003 | Insider threat / data exfiltration | 12 | 🟠 High | Mitigate | 6 | ⏳ Planned |
| RISK-004 | Cloud infrastructure unauthorized access | 16 | 🟠 High | Mitigate | 6 | 🔄 In Treatment |
| RISK-005 | Vendor / third-party breach | 12 | 🟠 High | Mitigate + Transfer | 6 | ⏳ Planned |
| RISK-006 | Laptop loss or theft | 9 | 🟡 Medium | Mitigate | 4 | 🔄 In Treatment |
| RISK-007 | GDPR non-compliance | 12 | 🟠 High | Mitigate | 6 | ⏳ Planned |
| RISK-008 | Unpatched software exploited | 12 | 🟠 High | Mitigate | 4 | ⏳ Planned |
| RISK-009 | Production data in test environments | 9 | 🟡 Medium | Mitigate | 2 | ⏳ Planned |
| RISK-010 | Cloud provider outage | 8 | 🟡 Medium | Mitigate + Transfer | 4 | ⏳ Planned |

**Risk Appetite Statement:** TechVision accepts residual risks scored ≤ 6. Risks above 6 after treatment must be escalated to the CISO and documented with a formal acceptance decision.

---

## Risk Treatment Plan — Priority Order

| Priority | Risk ID | Key Action | Owner | Cost | Timeline |
|----------|---------|------------|-------|------|----------|
| 1 | RISK-001 | Deploy email security (sandboxing) + role-based training | IT + HR | $ | Month 2 |
| 2 | RISK-004 | Cloud security baseline review (CIS Benchmarks) | IT | $$ | Month 3 |
| 3 | RISK-002 | Test backups + deploy EDR on all endpoints | IT | $$ | Month 3 |
| 4 | RISK-008 | Establish monthly patching cycle + vulnerability scans | IT | $ | Month 3 |
| 5 | RISK-006 | Enforce full-disk encryption + MDM remote wipe | IT | $ | Month 2 |
| 6 | RISK-007 | Complete DPIAs + appoint DPO or data steward | Legal | $ | Month 4 |
| 7 | RISK-003 | Deploy DLP + run quarterly access reviews | IT | $$$ | Month 5 |
| 8 | RISK-009 | Implement data masking in dev environments | Dev | $$ | Month 4 |
| 9 | RISK-005 | Roll out vendor risk assessment program | Procurement | $$ | Month 6 |
| 10 | RISK-010 | Test DR plan + evaluate multi-region failover | IT | $$ | Month 6 |

---

## Statement of Risk Appetite

TechVision Consulting's risk appetite is **Low to Medium**:

- **Zero tolerance:** Intentional unauthorized access to client data; GDPR/regulatory violations
- **Low tolerance:** Ransomware; critical system outages; third-party breaches
- **Medium tolerance:** Temporary service disruptions; minor data quality issues
- **Accepted:** Residual risks scored ≤ 6 after treatment controls are in place

---

## Next Steps

- [ ] Complete asset inventory (Month 2) — ensure all assets are captured before final risk assessment
- [ ] Validate risk scores with IT Manager and CISO (Month 2)
- [ ] Map each risk to ISO 27001 Annex A controls — document in Statement of Applicability (Month 3)
- [ ] Begin treatment of Critical risks immediately (RISK-001, RISK-002)
- [ ] Review and update risk register every 6 months or after a significant change
