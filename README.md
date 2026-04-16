# GRC Analyst Portfolio
### Temidayo Fadase — Cybersecurity (GRC) | Technical & Non-Technical

> A complete, end-to-end GRC analyst portfolio built across two hypothetical firms, two compliance frameworks, and four project phases. Every document reflects real-world GRC analyst work — from risk assessments and compliance tracking to GRC tool implementation, security assessments, and hands-on vulnerability management lab work.

📧 fadasetemidayo@gmail.com

---

## Portfolio at a Glance

| Firm | Framework | Phases Completed | Documents |
|------|-----------|-----------------|-----------|
| TechVision Consulting Ltd. | ISO 27001:2022 | Phase 1 → 3 + Technical | 7 documents |
| CloudPulse Analytics Inc. | SOC 2 Type II | Phase 1 → 4 + Technical | 6 documents |
| Lab Practice | Tenable Nessus | Hands-on scanning | 1 guide |
| **Total** | | | **14 documents** |

---

## Firm 1: TechVision Consulting Ltd.

**Scenario:** 150-person IT consulting and managed services firm. US-based with EU clients. Building an ISO 27001:2022 ISMS from scratch, targeting certification in 12 months.

### Phase 1 — Compliance Framework

#### [ISO 27001 Compliance Tracker](techvision-consulting/phase1-compliance-framework/ISO27001_Compliance_Tracker.md)
Full control-by-control tracker across all 93 Annex A controls (4 domains: Organizational, People, Physical, Technological). Includes implementation status, evidence requirements, control owners, and a 12-month audit calendar. Baseline assessment: ~50% implemented at Month 1.

#### [Information Security Risk Assessment](techvision-consulting/phase1-compliance-framework/ISO27001_Risk_Assessment.md)
Formal risk assessment following ISO/IEC 27005 methodology. Covers 10 high-priority risks (phishing, ransomware, insider threats, cloud misconfigs, GDPR, unpatched software, vendor breaches) with inherent risk scores, treatment controls, residual scores, and a prioritized treatment plan. Includes risk appetite statement.

#### [GRC Capacity Plan](techvision-consulting/phase1-compliance-framework/GRC_Capacity_Plan.md)
Phased resource plan for executing the full GRC program solo. ~904 hours across 4 phases, 7-month calendar timeline at 32 productive hrs/week. Includes utilization model, bottleneck analysis, and scenario planning.

---

### Phase 2 — Internal Audit System

#### [Internal Audit & Evidence Collection System](techvision-consulting/phase2-internal-audit/Phase2_Internal_Audit_System_TechVision.md)
End-to-end internal audit methodology following ISO 19011:2018. Includes 4-day audit schedule with process owner assignments, evidence repository folder structure, per-control evidence checklists (access reviews, vuln management, training, incident response), NCR template with 5-Why root cause analysis, audit report structure, and a 4-week certification readiness checklist.

#### [Compliance Control Review Runbook](techvision-consulting/phase2-internal-audit/Runbook_Compliance_Control_Review.md)
10-step operational runbook for conducting periodic ISO 27001 control reviews. Covers scope definition, control owner notification, evidence collection, control testing, tracker updates, risk register cross-referencing, findings documentation, and archiving. Includes troubleshooting table and escalation paths.

#### [ISMS Status Report Template](techvision-consulting/phase2-internal-audit/ISMS_Status_Report_Template.md)
Monthly compliance status report for CISO and leadership. Includes compliance % by domain, new findings table, risk posture update, milestone calendar, and a decisions-required section for escalating budget and policy approvals.

---

### Phase 3 — GRC Tool Implementation

#### [Hyperproof Implementation Plan](techvision-consulting/phase3-grc-tool-hyperproof/Phase3_Hyperproof_Implementation_TechVision.md)
7-phase implementation guide for configuring Hyperproof to manage TechVision's ISO 27001 program. Covers account setup, framework import, bulk control status import via CSV, Azure AD integration with exact API permission configuration, Tenable.io integration for automated vulnerability evidence, risk module configuration with risk-to-control linking, recurring evidence workflows, and internal/external audit setup. Includes Hyperproof vs. Vanta comparison table.

---

### Technical Programs

#### [Vulnerability Management Program](techvision-consulting/technical-programs/Vulnerability_Management_Program_TechVision.md)
Full vulnerability management program addressing ISO 27001 A.8.8. Includes scanning schedule (continuous agents, weekly network scans, bi-weekly web app scans, annual pen tests), CVSS v3.1 severity classification with risk-adjusted prioritization modifiers (CISA KEV, asset exposure), remediation SLAs (24hr Critical → 90-day Low), emergency patch protocol, triage workflow, exception process, vulnerability tracker schema, and program KPIs.

---

## Firm 2: CloudPulse Analytics Inc.

**Scenario:** ~80-person B2B SaaS company providing a cloud-native business intelligence platform on AWS. Serving enterprise clients globally. Pursuing SOC 2 Type II because enterprise clients require it as a contract condition.

### Phase 1 — SOC 2 Readiness

#### [SOC 2 Type II Readiness Assessment](cloudpulse-analytics/phase1-soc2-readiness/SOC2_Readiness_Assessment.md)
Readiness assessment against all 4 Trust Service Categories: Security (CC — 33 criteria), Availability (3), Confidentiality (2), and Privacy (8). Covers current state for each criterion, gap analysis with 16 prioritized findings, 12-month remediation roadmap from baseline to audit, evidence requirements by category, and an ISO 27001 vs. SOC 2 comparison table.

---

### Phase 3 — GRC Tool Implementation

#### [Vanta Implementation Plan](cloudpulse-analytics/phase3-grc-tool-vanta/Phase3_Vanta_Implementation_CloudPulse.md)
6-phase implementation guide for configuring Vanta to automate SOC 2 evidence collection. Covers org setup and scoping, all integration configurations with exact steps (AWS IAM role with JSON policy, GitHub app authorization, Okta API token setup), control owner assignments, employee onboarding and policy acknowledgements, vendor risk management, readiness score targeting, and auditor portal configuration for the 6-month observation window.

---

### Phase 4 — Security Assessment

#### [Security Assessment — Threat Model, Vulnerability Assessment & Pen Test](cloudpulse-analytics/phase4-security-assessment/Phase4_Security_Assessment_CloudPulse.md)
Comprehensive security assessment covering:
- **STRIDE threat model** across 4 system components (web app, AWS infrastructure, CI/CD pipeline, data ingestion) — 30+ threats scored by likelihood and impact
- **Vulnerability assessment** — 15 findings using Tenable, Prowler, OWASP ZAP, Gitleaks, Trivy, and AWS Inspector — including a critical tenant isolation IDOR, hardcoded AWS key in GitHub, and unencrypted RDS instance
- **Pen test coordination** — Statement of Work, rules of engagement, pre-engagement checklist, and findings integration process
- **Remediation plan** — all 15 findings prioritized with owners, SLAs, and verification procedures

---

### Technical Programs

#### [Security Awareness Training Program](cloudpulse-analytics/technical-programs/Security_Awareness_Training_CloudPulse.md)
Full security awareness program addressing SOC 2 CC1.4, CC2.2, CC6.8, and CC7.4. Covers 4 training tracks (all-staff annual curriculum, role-based modules by department, triggered just-in-time training, and new hire onboarding with Day 1–5 schedule), monthly phishing simulation program with 7 simulation types (email, spear phishing, vishing, smishing, QR code, attachment), metrics dashboard (click rate, report rate, completion rate), and positive security culture principles. Primary tool: KnowBe4.

---

## Lab Practice

#### [Tenable Nessus Hands-On Project Guide](lab-practice/Tenable_Nessus_Project_Guide.md)
7-project practical guide for building Nessus skills using Nessus Essentials (free). Projects include: host discovery scanning, unauthenticated vulnerability scanning, credentialed scanning with comparison analysis, CVSS-based triage and remediation report writing, CIS Benchmark manual configuration review, custom scan policy configuration, and remediation verification through re-scanning. Uses Metasploitable 2 as a vulnerable lab target. Includes resume bullet points and interview Q&A for each skill.

---

## Skills Demonstrated

| Skill Area | Specifics |
|------------|-----------|
| **Compliance Frameworks** | ISO 27001:2022 (all 93 controls), SOC 2 Type II (all 4 TSCs), ISO 27005, ISO 19011 |
| **Risk Management** | Asset-based risk assessment, CVSS triage, STRIDE threat modeling, risk register management |
| **Audit & Evidence** | Internal audit methodology, evidence collection, NCR management, audit report writing |
| **GRC Tools** | Vanta (SOC 2 configuration), Hyperproof (ISO 27001 configuration) |
| **Vulnerability Management** | Tenable Nessus (credentialed + uncredentialed), Prowler, OWASP ZAP, Gitleaks, Trivy |
| **Security Programs** | Vulnerability management program, security awareness training, phishing simulations |
| **Cloud Security** | AWS IAM, S3, RDS, GuardDuty, Inspector, CloudTrail, GitHub Actions security |
| **Documentation** | Runbooks, SOPs, status reports, remediation reports, policy writing |
| **Regulatory Awareness** | GDPR, CCPA, SOC 2, ISO 27001, CISA KEV |

---

## Tools & Technologies

| Category | Tools |
|----------|-------|
| Vulnerability Scanning | Tenable Nessus, AWS Inspector, Prowler (open source) |
| Web Application Testing | OWASP ZAP, Burp Suite Community |
| Secrets Scanning | Gitleaks |
| Container Security | Trivy |
| GRC Platforms | Vanta, Hyperproof |
| Cloud | AWS (IAM, S3, RDS, ECS, CloudTrail, GuardDuty, Inspector) |
| Identity | Okta, Auth0, Azure Active Directory |
| Security Awareness | KnowBe4 |
| SIEM | Datadog, CloudWatch |
| CI/CD | GitHub Actions |

---

## Frameworks & Standards Referenced

- ISO/IEC 27001:2022 — Information Security Management Systems
- ISO/IEC 27005:2022 — Information Security Risk Management
- ISO 19011:2018 — Guidelines for Auditing Management Systems
- AICPA SOC 2 — Trust Services Criteria
- NIST CVSS v3.1 — Common Vulnerability Scoring System
- CISA KEV — Known Exploited Vulnerabilities Catalog
- OWASP Top 10 — Web Application Security Risks
- STRIDE — Threat Modeling Methodology
- CIS Benchmarks — Security Configuration Standards
- GDPR — General Data Protection Regulation

---

## About This Portfolio

I am transitioning into a GRC analyst role with a focus on both technical and non-technical cybersecurity governance, risk, and compliance. This portfolio was built to demonstrate practical, applied GRC skills — not just theoretical knowledge.

Each document was built to reflect real deliverables a GRC analyst would produce on the job:
- The compliance tracker is the kind of working document you maintain daily in a GRC tool
- The risk assessment follows the methodology an ISO 27001 certification auditor will review
- The security assessment mirrors what a GRC analyst coordinates and reports on after an external pen test
- The Nessus guide reflects hands-on practice in a real lab environment

I am actively expanding this portfolio with additional phases and tools.

---

*ISO/IEC 27001:2022 | ISO/IEC 27005:2022 | SOC 2 Type II | STRIDE | CVSS v3.1 | Tenable Nessus | Vanta | Hyperproof*
