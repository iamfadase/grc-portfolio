# Phase 3: GRC Tool Implementation — Hyperproof
## TechVision Consulting Ltd. — ISO 27001:2022

**Phase:** 3 of 4
**Tool:** Hyperproof
**Framework:** ISO 27001:2022 (primary) + GDPR (secondary)
**Implementation Owner:** GRC Analyst
**Timeline:** 9 weeks (Months 3–5)
**Goal:** Configure Hyperproof to centralize ISMS controls, automate evidence collection, manage risks, and streamline audit workflows

---

## Why Hyperproof for TechVision

| Factor | Fit |
|--------|-----|
| Multi-framework need (ISO 27001 + GDPR) | ✅ Hyperproof excels at managing multiple frameworks simultaneously with cross-mapped controls |
| Consulting firm — complex org structure | ✅ Hyperproof's program management approach suits distributed control ownership |
| Mature compliance journey | ✅ Hyperproof gives more configurability than Vanta — suited to orgs building custom workflows |
| ISO 27001 depth | ✅ Full Annex A control library built in; risk management module included |
| Audit management | ✅ Strong audit workflow features — ideal for managing external ISO 27001 certification audits |
| Evidence labeling and organization | ✅ Hyperproof's evidence management is best-in-class for audit-heavy processes |

---

## Implementation Overview

| Phase | Weeks | Activities |
|-------|-------|-----------|
| 1 — Account Setup & Configuration | Week 1 | Org setup, framework import, user roles |
| 2 — Control Library Setup | Weeks 2–3 | Import ISO 27001 controls, assign owners, link policies |
| 3 — Integrations | Weeks 3–4 | Connect cloud, identity, ticketing systems |
| 4 — Risk Module Configuration | Week 5 | Import risk register, configure scoring, link to controls |
| 5 — Evidence Workflows | Weeks 6–7 | Build evidence collection workflows, upload existing evidence |
| 6 — Audit Program Setup | Week 8 | Configure internal + external audit workflows |
| 7 — Training & Rollout | Week 9 | Train control owners; go-live |

---

## Phase 1 — Account Setup & Configuration (Week 1)

### Step 1.1: Create Hyperproof Organization

```
1. Sign up at hyperproof.io → Start trial or activate account
2. Organization name: TechVision Consulting Ltd.
3. Invite Super Admin: GRC Analyst (you)
4. Configure basic settings:
   - Company size: 50–200 employees
   - Industry: IT Consulting / Professional Services
   - Primary timezone: [Your timezone]
```

### Step 1.2: Configure User Roles

Hyperproof has a role hierarchy. Set up before inviting users:

```
Navigate to: Settings → Users & Permissions

Roles to configure:
  Super Admin → GRC Analyst (full system access)
  Program Manager → CISO (view all programs, approve risks)
  Control Owner → IT Manager, HR Director, Legal, Procurement (manage assigned controls)
  Auditor → External auditor account (read-only, evidence access)
  Reviewer → Department heads (review and approve evidence)
  Viewer → General staff (read-only access to assigned items)

Invite users:
  Navigate to Settings → Users → Invite
  Enter email + select role
  Users receive setup email
```

### Step 1.3: Import Frameworks

```
Navigate to: Programs → New Program → From Template

Select:
  ✅ ISO/IEC 27001:2022
     → This imports all 93 Annex A controls pre-mapped
     → Clauses 4–10 requirements included

  ✅ GDPR (add as secondary framework)
     → Cross-mapped controls will appear automatically

Program settings:
  Name: TechVision ISMS — ISO 27001:2022
  Description: Information Security Management System for TechVision Consulting Ltd.
  Program owner: GRC Analyst
  Target certification date: Month 12
```

---

## Phase 2 — Control Library Setup (Weeks 2–3)

### Review and Customize Imported Controls

Hyperproof imports all 93 Annex A controls. For each control:

```
Navigate to: Programs → TechVision ISMS → Controls

For each control, configure:
  1. Status: Not Started / In Progress / Implemented
     → Import statuses from existing Compliance Tracker
  2. Owner: Assign to relevant person
  3. Linked policies: Attach relevant policy document
  4. Evidence requirements: Define what evidence is needed
  5. Test procedure: How will this control be tested?
  6. Review frequency: How often should evidence be refreshed?
```

### Bulk Status Import

Instead of updating all 93 controls manually, use Hyperproof's import feature:

```
Navigate to: Controls → Import → Download Template (CSV)

Fill CSV with data from existing ISO27001_Compliance_Tracker.md:
  - Control ID (e.g., A.5.1)
  - Status (Implemented / Partial / Not Started)
  - Owner (email address)
  - Notes / gaps

Upload CSV → Hyperproof updates all controls in bulk
```

### Control Owner Assignment Guide

| Control Domain | Recommended Owner |
|----------------|------------------|
| A.5 (Organizational) — governance | GRC Analyst |
| A.5 (Organizational) — vendor/supplier | Procurement Manager |
| A.5 (Organizational) — incident/BCP | CISO |
| A.5 (Organizational) — legal/privacy | Legal |
| A.6 (People) | HR Director |
| A.7 (Physical) | Facilities Manager |
| A.8 (Technological) — access, endpoints | IT Manager |
| A.8 (Technological) — development | Dev Lead |
| A.8 (Technological) — monitoring, vuln | IT Manager + GRC Analyst |

### Link Policies to Controls

```
Navigate to: Documents → Upload → [Policy PDF]

For each uploaded policy, tag with related controls:
  Information Security Policy → A.5.1, A.5.2
  Access Control Policy → A.5.15–A.5.18, A.8.2–A.8.5
  Incident Response Plan → A.5.24–A.5.28
  Vulnerability Management Policy → A.8.8
  Acceptable Use Policy → A.5.10
  Privacy Policy → A.5.34
  Business Continuity Plan → A.5.29–A.5.30

Hyperproof automatically creates the control ↔ policy relationship
```

---

## Phase 3 — Integrations (Weeks 3–4)

Hyperproof integrations pull evidence automatically. Priority integrations for TechVision:

### Integration List

```
Navigate to: Integrations → Browse

| Priority | Integration | Purpose | Controls |
|----------|-------------|---------|----------|
| P1 | Microsoft 365 | User roster, email security, SharePoint docs | A.6, A.5.10, A.8.5 |
| P1 | Azure Active Directory | Identity, access controls, MFA status | A.5.15–A.5.18, A.8.2–A.8.5 |
| P1 | AWS | Cloud config, encryption, logging | A.5.23, A.8.9, A.8.13 |
| P2 | Jira / ServiceNow | Change tickets, incident tickets | A.8.32, A.5.24–A.5.26 |
| P2 | Tenable.io | Vulnerability scan evidence | A.8.8 |
| P2 | KnowBe4 | Security training completion | A.6.3 |
| P3 | BambooHR / Rippling | Employee data, onboarding/offboarding | A.6.1, A.6.5 |
| P3 | Slack | Communication records | A.5.4 |
```

### Azure AD Integration

```
Hyperproof → Integrations → Azure Active Directory → Connect

Required: Azure App Registration with read permissions

In Azure Portal:
  1. Azure Active Directory → App registrations → New registration
     Name: Hyperproof-Integration
     Supported account types: Single tenant
  2. Add API permissions:
     Microsoft Graph → Application permissions:
       User.Read.All
       Group.Read.All
       AuditLog.Read.All
       Policy.Read.All
  3. Create client secret → Copy value
  4. Note: Tenant ID, Client ID, Client Secret

In Hyperproof:
  Enter Tenant ID, Client ID, Client Secret → Connect

What Hyperproof collects:
  - All user accounts (active/inactive)
  - MFA registration status per user
  - Admin role assignments
  - Conditional access policies
  - Sign-in risk policies
  - Guest account inventory
```

### Tenable.io Integration (Vulnerability Evidence)

```
Hyperproof → Integrations → Tenable.io → Connect

Required: Tenable API key (access key + secret key)

In Tenable.io:
  → Account → API Keys → Generate

In Hyperproof:
  → Enter Access Key + Secret Key → Connect

Configure:
  → Map Tenable scan data to control A.8.8
  → Set evidence refresh: Weekly (matches scan schedule)

What Hyperproof collects:
  - Latest vulnerability scan results
  - Critical/High finding counts
  - Scan date (evidence currency)
  - Asset coverage %

Use this to auto-populate evidence for A.8.8 — auditors see scan data without manual exports
```

---

## Phase 4 — Risk Module Configuration (Week 5)

Hyperproof has a dedicated risk register that links directly to controls.

### Import Risk Register

```
Navigate to: Risks → Import Risks → Download Template

Fill CSV from existing ISO27001_Risk_Assessment.md:
  - Risk ID (RISK-001 through RISK-010)
  - Risk name
  - Description
  - Likelihood score (1–5)
  - Impact score (1–5)
  - Inherent risk score (auto-calculated)
  - Treatment option (Mitigate / Accept / Transfer / Avoid)
  - Owner

Upload CSV → All 10 risks imported
```

### Configure Risk Scoring

```
Navigate to: Settings → Risk Settings

Set scoring matrix:
  Likelihood scale: 1 (Rare) to 5 (Almost Certain)
  Impact scale: 1 (Negligible) to 5 (Critical)
  Risk score: Likelihood × Impact
  
  Thresholds:
    1–4: Low (green)
    5–9: Medium (yellow)
    10–16: High (orange)
    17–25: Critical (red)

Risk appetite: Accept risks ≤ 6; treat all risks > 6
```

### Link Risks to Controls

```
Navigate to: Risks → [Risk Name] → Linked Controls → Add

For each risk, link the mitigating controls:

  RISK-001 (Phishing):
    → Link to: A.6.3 (training), A.8.5 (MFA), A.8.7 (AV/EDR)

  RISK-002 (Ransomware):
    → Link to: A.8.7, A.8.13, A.8.14, A.8.8, A.8.22

  RISK-004 (Cloud misconfiguration):
    → Link to: A.5.23, A.8.2, A.8.5, A.8.9

Benefit: When a linked control fails or evidence expires, 
Hyperproof flags the associated risk as "at risk"
```

### Risk Dashboard

```
Navigate to: Risks → Dashboard

Hyperproof generates:
  - Risk heatmap (likelihood vs. impact)
  - Risk trend over time
  - Controls linked to highest risks
  - Risks above risk appetite threshold
  - Treatment progress by owner

Export as PDF for management review meetings
```

---

## Phase 5 — Evidence Workflows (Weeks 6–7)

### Create Evidence Collection Requests

Hyperproof's "Labels" feature creates repeatable evidence requests sent to control owners:

```
Navigate to: Controls → [Control] → Evidence → Request Evidence

Configure request:
  - Evidence name: e.g., "Quarterly Access Review — Q3"
  - Description: "Please upload the completed access review report showing all user accounts reviewed, changes made, and approver sign-off"
  - Assigned to: IT Manager
  - Due date: [Date]
  - Recurrence: Quarterly

When due, Hyperproof sends automated reminder to control owner
Control owner uploads directly into Hyperproof
GRC Analyst receives notification to review and approve
```

### Recurring Evidence Schedule

Set up automated reminders for all recurring evidence:

| Evidence | Control | Frequency | Owner | Hyperproof Recurrence |
|----------|---------|-----------|-------|-----------------------|
| Vulnerability scan report | A.8.8 | Monthly | IT Manager | Monthly (auto via Tenable integration) |
| Access review report | A.5.18 | Quarterly | IT Manager | Quarterly |
| Training completion report | A.6.3 | Quarterly | HR Director | Quarterly |
| Backup test results | A.8.13 | Quarterly | IT Manager | Quarterly |
| Vendor risk review | A.5.19 | Annual | Procurement | Annual |
| Management review minutes | Clause 9.3 | Annual | CISO | Annual |
| IRP tabletop exercise | A.5.24 | Annual | CISO | Annual |
| Internal audit report | Clause 9.2 | Annual | GRC Analyst | Annual |

### Upload Historical Evidence

Upload all evidence collected during Phase 1 (baseline) and Phase 2 (audit):

```
Navigate to: Controls → [Control] → Evidence → Upload

Batch upload tip:
  Hyperproof allows multi-file upload per control
  Tag each file with:
    - Evidence date
    - Collection method (screenshot, export, interview notes)
    - Reviewer: GRC Analyst
    - Status: Approved / Pending Review
```

---

## Phase 6 — Audit Program Setup (Week 8)

### Configure Internal Audit

```
Navigate to: Audits → New Audit

Type: Internal Audit
Name: TechVision ISO 27001 Internal Audit — Month 9
Audit period: Month 9 (1 week)
Lead auditor: GRC Analyst
Framework: ISO 27001:2022

Hyperproof generates:
  - Audit checklist from all controls
  - Evidence status per control
  - Findings log
  - NCR tracker
```

### Configure External (Certification) Audit

```
Navigate to: Audits → New Audit

Type: External Audit
Name: ISO 27001 Certification Audit — Month 11
Audit period: Months 11–12
Auditor firm: [Certifying body name]
External auditor email: [Auditor email — read-only access]

Configure auditor access:
  → Auditor sees: All controls, evidence, policies, risk register
  → Auditor cannot: Edit anything, see employee PII
  → Evidence request feature: Auditor can request additional evidence directly in Hyperproof
```

### Audit Dashboard

```
Navigate to: Audits → [Audit] → Dashboard

Shows:
  - % of controls with complete evidence
  - Open findings / NCRs
  - Evidence freshness (% current vs. stale)
  - Outstanding evidence requests
  - Days until audit
```

---

## Phase 7 — Training & Rollout (Week 9)

### Control Owner Training

Deliver a 30-minute walkthrough to all control owners covering:

```
Agenda:
  1. Why we're using Hyperproof (10 min)
     - Single source of truth for the ISMS
     - Reduces audit prep from weeks to hours
     - Your evidence request workflow explained

  2. How to upload evidence (10 min)
     - Navigate to your assigned controls
     - Upload files, add dates and notes
     - Mark evidence as complete

  3. How to handle evidence requests (5 min)
     - You'll receive email reminders
     - Click link → upload → done

  4. Q&A (5 min)

Training materials: Hyperproof has built-in help docs at help.hyperproof.io
```

### Go-Live Checklist

```
Before declaring Phase 3 complete:
  [ ] All 93 controls imported with correct status
  [ ] All controls have assigned owners
  [ ] All policies uploaded and linked to controls
  [ ] All integrations connected and returning data
  [ ] Risk register imported (10 risks) and linked to controls
  [ ] Historical evidence uploaded for all Implemented controls
  [ ] Recurring evidence schedules configured
  [ ] Internal audit configured (Month 9)
  [ ] External audit configured (Month 11)
  [ ] All control owners have logged in and confirmed access
  [ ] GRC Analyst has reviewed dashboard — no unexpected failures
```

---

## Hyperproof vs. Vanta — Side-by-Side

Knowing this comparison is valuable for interviews:

| Feature | Hyperproof | Vanta |
|---------|-----------|-------|
| **Best for** | Multi-framework, consulting, mature GRC | SaaS companies, SOC 2, speed to audit |
| **ISO 27001 depth** | ⭐⭐⭐⭐⭐ Excellent | ⭐⭐⭐⭐ Good |
| **SOC 2 automation** | ⭐⭐⭐⭐ Good | ⭐⭐⭐⭐⭐ Best in class |
| **Risk management** | ⭐⭐⭐⭐⭐ Built-in risk register | ⭐⭐⭐ Basic |
| **Customizability** | ⭐⭐⭐⭐⭐ Highly configurable | ⭐⭐⭐ More opinionated |
| **Integrations** | ⭐⭐⭐⭐ Strong | ⭐⭐⭐⭐⭐ Strongest |
| **Ease of use** | ⭐⭐⭐⭐ Moderate learning curve | ⭐⭐⭐⭐⭐ Very easy |
| **Auditor portal** | ⭐⭐⭐⭐⭐ Excellent | ⭐⭐⭐⭐ Good |
| **Approx. cost** | ~$20,000–40,000/yr | ~$15,000–35,000/yr |
| **Free trial** | Yes — hyperproof.io | Yes — vanta.com |

---

## Key Hyperproof Terms for Interviews

| Term | Meaning |
|------|---------|
| Program | A compliance initiative tied to a framework (e.g., "ISO 27001 Program") |
| Control | A specific requirement — Hyperproof pre-loads all Annex A controls |
| Label | A tag applied to evidence for organization and searchability |
| Evidence request | An automated ask sent to a control owner to upload proof |
| Workstream | A grouping of controls by department or theme |
| Audit | A formal review event — can be internal or external |
| Finding | A gap identified during an audit — tracked to closure in Hyperproof |
| Risk register | The built-in list of risks linked to controls and owners |
