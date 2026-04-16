# SOC 2 Type II Readiness Assessment
## CloudPulse Analytics — Hypothetical Scenario

**Organization:** CloudPulse Analytics Inc.
**Industry:** B2B SaaS — Business Intelligence & Analytics Platform
**Size:** ~80 employees | Cloud-native (AWS)
**Clients:** Enterprise clients across US, EU, APAC
**Prepared By:** GRC Analyst
**Assessment Date:** Month 1
**Target Audit Window:** Months 7–12 (6-month observation period)
**Auditor:** [External CPA firm — TBD]

---

## System Description

CloudPulse Analytics provides a cloud-based business intelligence platform that enables enterprise clients to connect, analyze, and visualize their business data. The system includes:

| Component | Description |
|-----------|-------------|
| Web application | Multi-tenant SaaS platform hosted on AWS (us-east-1, eu-west-1) |
| Data ingestion pipeline | ETL connectors pulling from client source systems |
| Analytics engine | Processing layer for data transformation and reporting |
| Client data storage | Encrypted S3 buckets and RDS instances per tenant |
| Admin portal | Internal tooling for operations and customer support |
| CI/CD pipeline | GitHub Actions → staging → production deployment |
| Identity provider | Okta SSO for internal staff; Auth0 for client authentication |

**Data in scope:** Client business data (financial, operational, HR metrics), client employee PII, CloudPulse employee PII, usage and telemetry data.

---

## SOC 2 Scope

**Trust Service Categories in scope:**

| Category | Included | Rationale |
|----------|----------|-----------|
| Security (CC) | ✅ Yes | Required — all SOC 2 audits |
| Availability (A) | ✅ Yes | Enterprise clients have SLA requirements (99.9% uptime) |
| Confidentiality (C) | ✅ Yes | Client data is confidential by contract |
| Privacy (P) | ✅ Yes | Platform processes client employee PII; EU/US data subjects |

**Excluded:** Processing Integrity (not in scope — CloudPulse does not process financial transactions on behalf of clients)

---

## Readiness Summary

| TSC Category | Criteria Count | Met | Partial | Not Met | Readiness % |
|--------------|---------------|-----|---------|---------|-------------|
| Security (CC) | 33 | 14 | 12 | 7 | 61% |
| Availability (A) | 3 | 1 | 1 | 1 | 50% |
| Confidentiality (C) | 2 | 1 | 1 | 0 | 75% |
| Privacy (P) | 8 | 2 | 4 | 2 | 44% |
| **Total** | **46** | **18** | **18** | **10** | **59%** |

**Overall assessment: 🟡 Moderate — not yet audit-ready. Estimated time to readiness: 4–5 months of focused remediation.**

---

## CC — Common Criteria (Security) — 33 Criteria

### CC1: Control Environment

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC1.1 | Board/management demonstrates commitment to security | CISO appointed; security on board agenda quarterly | ✅ Met | — |
| CC1.2 | Management establishes structures, reporting lines | Org chart with security roles defined | ✅ Met | — |
| CC1.3 | Management establishes competence expectations | Job descriptions include security responsibilities | ⚠️ Partial | Security expectations not in all JDs |
| CC1.4 | Management holds individuals accountable | Annual performance reviews include security KPIs | ⚠️ Partial | KPIs not yet defined for all roles |
| CC1.5 | Management enforces accountability for security | Policy violations tracked and actioned | ❌ Not Met | No policy violation tracking process |

### CC2: Communication and Information

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC2.1 | Entity obtains relevant quality information | Security metrics reported monthly | ✅ Met | — |
| CC2.2 | Entity communicates internally about security | Security updates in all-hands; Slack #security channel | ✅ Met | — |
| CC2.3 | Entity communicates externally about security | Security page on website; client-facing security docs | ⚠️ Partial | Security page outdated; no trust portal |

### CC3: Risk Assessment

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC3.1 | Entity specifies risk assessment objectives | Risk assessment policy exists | ✅ Met | — |
| CC3.2 | Entity identifies and analyzes risk | Annual risk assessment conducted | ⚠️ Partial | Last completed 14 months ago — overdue |
| CC3.3 | Entity considers fraud risk | Fraud risk not formally assessed | ❌ Not Met | No fraud risk process |
| CC3.4 | Entity identifies and assesses significant changes | Change management process exists | ⚠️ Partial | Security impact not assessed in all changes |

### CC4: Monitoring Activities

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC4.1 | Entity performs ongoing evaluations | SIEM alerts reviewed daily | ✅ Met | — |
| CC4.2 | Entity evaluates and communicates deficiencies | Security findings tracked in Jira | ✅ Met | — |

### CC5: Control Activities

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC5.1 | Entity selects controls to mitigate risks | Controls mapped to risk register | ⚠️ Partial | Mapping incomplete for new risks |
| CC5.2 | Entity selects and develops general IT controls | IT controls documented | ✅ Met | — |
| CC5.3 | Entity deploys controls through policies and procedures | 8 of 14 core policies published | ⚠️ Partial | 6 policies in draft or missing |

### CC6: Logical and Physical Access Controls

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC6.1 | Entity implements logical access security | Okta SSO + MFA enforced for all staff | ✅ Met | — |
| CC6.2 | Entity controls access prior to issuance | Provisioning workflow exists in IT ticketing | ✅ Met | — |
| CC6.3 | Entity removes access when no longer required | Offboarding checklist triggers access revocation | ✅ Met | — |
| CC6.4 | Entity restricts physical access | Badge access; CCTV at HQ and data centers | ✅ Met | — |
| CC6.5 | Entity discontinues logical access appropriately | Quarterly access reviews | ⚠️ Partial | Last access review was 5 months ago |
| CC6.6 | Entity implements controls for threats from outside | WAF, DDoS protection, firewall rules in place | ✅ Met | — |
| CC6.7 | Entity restricts transmission, movement, and removal | Encryption in transit (TLS 1.2+); no USB policy | ⚠️ Partial | No formal removable media policy |
| CC6.8 | Entity implements controls to prevent or detect malware | EDR deployed on all endpoints; AV on servers | ✅ Met | — |

### CC7: System Operations

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC7.1 | Entity detects and monitors vulnerabilities | Weekly Tenable scans; AWS Inspector enabled | ✅ Met | — |
| CC7.2 | Entity monitors system components | CloudWatch + PagerDuty alerting | ✅ Met | — |
| CC7.3 | Entity evaluates security events | SIEM (Datadog) with alert triage process | ✅ Met | — |
| CC7.4 | Entity responds to identified security incidents | Incident response plan exists | ⚠️ Partial | IRP not tested via tabletop exercise |
| CC7.5 | Entity identifies and discloses breaches | Breach notification procedure documented | ⚠️ Partial | Client notification template missing |

### CC8: Change Management

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC8.1 | Entity authorizes, designs, develops, tests changes | Change management policy; staging environment | ⚠️ Partial | Security review not gated in all PRs |

### CC9: Risk Mitigation

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| CC9.1 | Entity identifies and manages business disruption risks | BCP exists; not tested in 18 months | ⚠️ Partial | BCP test overdue |
| CC9.2 | Entity assesses and manages vendor risk | Top 10 vendors assessed; long tail not covered | ⚠️ Partial | 40+ vendors with no formal assessment |

---

## A — Availability (3 Criteria)

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| A1.1 | Entity maintains current processing capacity | Auto-scaling groups configured; capacity reviewed quarterly | ✅ Met | — |
| A1.2 | Entity authorizes, monitors, and addresses environmental threats | AWS multi-AZ; no multi-region failover | ⚠️ Partial | Single-region risk; DR plan not tested |
| A1.3 | Entity recovers to resume operations | Recovery procedures documented; RTO = 4 hrs, RPO = 1 hr | ❌ Not Met | RTO/RPO never formally tested; last backup restore test: unknown |

**Key gap:** Availability evidence requires *tested* recovery — documentation alone will not satisfy auditors.

---

## C — Confidentiality (2 Criteria)

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| C1.1 | Entity identifies and maintains confidential information | Data classification policy; S3 bucket tagging by sensitivity | ✅ Met | — |
| C1.2 | Entity disposes of confidential information | Data retention and deletion schedule exists | ⚠️ Partial | Automated deletion not yet implemented for all data types |

---

## P — Privacy (8 Criteria)

| Criteria | Requirement | Current State | Status | Gap |
|----------|-------------|---------------|--------|-----|
| P1.0 | Privacy notice and communication | Privacy policy published on website | ✅ Met | — |
| P2.0 | Choice and consent | Consent captured at onboarding for client users | ⚠️ Partial | Consent records not systematically stored |
| P3.0 | Collection of personal information | Data minimization principles documented | ⚠️ Partial | Minimization not consistently applied in new features |
| P4.0 | Use, retention, and disposal | Retention schedule exists | ⚠️ Partial | Disposal process not automated |
| P5.0 | Access | Data subject access request (DSAR) process exists | ⚠️ Partial | DSAR response SLA not defined or tracked |
| P6.0 | Disclosure and notification | Third-party data sharing tracked in data map | ❌ Not Met | No formal data map; sharing not fully tracked |
| P7.0 | Quality | Data accuracy process documented | ❌ Not Met | No process for clients to correct inaccurate PII |
| P8.0 | Monitoring and enforcement | Privacy incidents tracked | ✅ Met | — |

---

## Gap Summary — Priority Remediation List

### 🔴 Critical (fix before audit observation window opens)

| # | Gap | TSC | Effort | Owner | Target |
|---|-----|-----|--------|-------|--------|
| 1 | BCP and DR never tested — no evidence of RTO/RPO validation | A1.3 | High | Engineering | Month 3 |
| 2 | Risk assessment overdue (14 months) — must be current | CC3.2 | Medium | GRC Analyst | Month 2 |
| 3 | IRP not tested — tabletop exercise required | CC7.4 | Medium | GRC Analyst + Eng | Month 3 |
| 4 | No data map for third-party data sharing | P6.0 | Medium | Legal + Engineering | Month 3 |
| 5 | 6 core security policies missing or in draft | CC5.3 | Medium | GRC Analyst | Month 2 |

### 🟠 High (fix within 2 months of opening observation window)

| # | Gap | TSC | Effort | Owner | Target |
|---|-----|-----|--------|-------|--------|
| 6 | Quarterly access reviews not current (5 months ago) | CC6.5 | Low | IT | Month 2 |
| 7 | Security gate not enforced in all PRs | CC8.1 | Medium | Engineering | Month 3 |
| 8 | No fraud risk assessment | CC3.3 | Low | GRC Analyst | Month 3 |
| 9 | DSAR SLA not defined or tracked | P5.0 | Low | Legal | Month 3 |
| 10 | Client breach notification template missing | CC7.5 | Low | Legal + GRC | Month 2 |
| 11 | No removable media policy | CC6.7 | Low | IT + HR | Month 2 |
| 12 | Vendor risk not assessed for 40+ vendors | CC9.2 | High | Procurement | Month 5 |

### 🟡 Medium (address before audit)

| # | Gap | TSC | Effort | Owner | Target |
|---|-----|-----|--------|-------|--------|
| 13 | Trust portal / updated security page | CC2.3 | Medium | Marketing + GRC | Month 4 |
| 14 | Automated data deletion not implemented | C1.2, P4.0 | High | Engineering | Month 5 |
| 15 | Consent records not systematically stored | P2.0 | Medium | Engineering | Month 4 |
| 16 | Data accuracy / correction process missing | P7.0 | Medium | Product + Legal | Month 5 |

---

## Remediation Roadmap

```
Month 1 — Baseline & Planning
  ✦ Complete this readiness assessment
  ✦ Brief leadership; get buy-in and budget
  ✦ Assign control owners

Month 2 — Foundation
  ✦ Complete overdue risk assessment (CC3.2)
  ✦ Finish and approve 6 missing policies (CC5.3)
  ✦ Run quarterly access review (CC6.5)
  ✦ Draft breach notification template (CC7.5)
  ✦ Publish removable media policy (CC6.7)

Month 3 — Testing & Evidence
  ✦ Run DR tabletop / backup restore test (A1.3) ← most important
  ✦ Run IRP tabletop exercise (CC7.4)
  ✦ Build data map of third-party data sharing (P6.0)
  ✦ Enforce security gate in all PR merges (CC8.1)
  ✦ Complete fraud risk assessment (CC3.3)

Month 4 — Client-Facing & Compliance
  ✦ Launch trust portal (CC2.3)
  ✦ Implement consent record storage (P2.0)
  ✦ Define DSAR SLA and begin tracking (P5.0)

Month 5 — Long Tail
  ✦ Vendor risk assessments for remaining vendors (CC9.2)
  ✦ Implement automated data deletion (C1.2, P4.0)
  ✦ Build data correction process for clients (P7.0)

Month 6 — Pre-Audit Readiness Check
  ✦ Full gap re-assessment (rerun this document)
  ✦ Evidence repository review — confirm all evidence current
  ✦ Auditor kickoff meeting

Months 7–12 — Observation Period
  ✦ Auditor collects evidence of controls operating over time
  ✦ Maintain all controls continuously
  ✦ Respond promptly to auditor requests
```

---

## Evidence Requirements by Category

Auditors will request evidence across the observation period. Start collecting now.

| Category | Evidence Examples | Collection Cadence |
|----------|--------------------|-------------------|
| Access controls | Okta provisioning logs, access review screenshots, offboarding tickets | Monthly |
| Vulnerability management | Tenable scan reports, remediation tickets | Monthly |
| Incident response | Incident tickets, tabletop exercise report | Per occurrence |
| Change management | PR history with security approvals, CAB records | Per change |
| Availability | Uptime reports, PagerDuty incident logs, backup restore test results | Monthly |
| Vendor management | Vendor assessments, signed DPAs, BAAs | Per vendor / annually |
| Privacy | DSAR log, consent records, data map | Monthly |
| Training | LMS completion reports | Quarterly |
| Policies | Signed acknowledgements, policy version history | Annually |

---

## Comparison: ISO 27001 vs SOC 2

Since you're building both, here's how they map — useful for interviews and portfolio context.

| Dimension | ISO 27001 | SOC 2 |
|-----------|-----------|-------|
| Origin | International standard (ISO) | US standard (AICPA) |
| Output | Certificate | Audit report (Type I or II) |
| Controls | 93 controls (Annex A) | Trust Service Criteria (principles-based) |
| Who requires it | Enterprise/global clients, EU | US enterprise clients, SaaS buyers |
| Focus | ISMS management system | Controls operating effectiveness |
| Evidence | Implementation | Operating over a period of time (Type II) |
| Overlap | ~70% of controls overlap | ~70% of controls overlap |

**Tip for your portfolio:** Note that ISO 27001 + SOC 2 together cover nearly every compliance requirement an enterprise client will ask for. Candidates who understand both stand out significantly.

---

## Next Steps

- [ ] Socialize this assessment with CISO and Engineering leadership
- [ ] Assign owners to all critical and high gaps
- [ ] Select a SOC 2 auditor (Common options: Schellman, A-LIGN, Prescient, Vanta Audit)
- [ ] Decide whether to use a GRC platform to automate evidence collection (Vanta, Drata, Secureframe)
- [ ] Begin Month 2 remediation tasks
- [ ] Set audit window start date (Month 7 target)
