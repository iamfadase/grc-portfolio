# Phase 3: GRC Tool Implementation — Vanta
## CloudPulse Analytics Inc. — SOC 2 Type II

**Phase:** 3 of 4
**Tool:** Vanta
**Framework:** SOC 2 Type II (Security, Availability, Confidentiality, Privacy)
**Implementation Owner:** GRC Analyst
**Timeline:** 9 weeks (Months 3–5)
**Goal:** Configure Vanta to automate evidence collection, track control status, and generate the SOC 2 audit report package

---

## Why Vanta for CloudPulse

| Factor | Fit |
|--------|-----|
| Cloud-native SaaS company | ✅ Vanta is built for exactly this — deep AWS, GCP, Azure integrations |
| SOC 2 primary framework | ✅ Vanta's strongest framework; purpose-built for SOC 2 |
| GitHub-based development | ✅ Native GitHub integration — code review, branch protection, secrets scanning |
| Okta / Auth0 for identity | ✅ Both natively supported |
| ~80 employees | ✅ Vanta scales well at this size; onboarding is lightweight |
| Auditor ecosystem | ✅ Vanta has preferred auditor partnerships (A-LIGN, Prescient, etc.) |
| Speed to audit | ✅ Vanta's automated evidence collection significantly reduces audit prep time |

---

## Implementation Overview

| Phase | Weeks | Activities |
|-------|-------|-----------|
| 1 — Account Setup & Scoping | Week 1 | Org setup, framework selection, admin configuration |
| 2 — Integrations | Weeks 2–3 | Connect all cloud, identity, code, and HR systems |
| 3 — Control Mapping & Gaps | Weeks 4–5 | Map TSC controls, assign owners, review automated tests |
| 4 — People & Policies | Week 6 | Onboard all employees, upload and publish policies |
| 5 — Evidence Review & Remediation | Weeks 7–8 | Fix failing controls, verify evidence quality |
| 6 — Audit Readiness Check | Week 9 | Final dashboard review, auditor kickoff |

---

## Phase 1 — Account Setup & Scoping (Week 1)

### Step 1.1: Create Vanta Organization

```
1. Sign up at vanta.com → Start free trial or activate paid account
2. Set organization name: CloudPulse Analytics Inc.
3. Invite Security Admin: GRC Analyst (you)
4. Set company details:
   - Industry: Software / SaaS
   - Company size: 50–200 employees
   - HQ location: [City, State]
   - Fiscal year end: [Month]
```

### Step 1.2: Select Frameworks

```
Navigate to: Settings → Frameworks → Add Framework

Select:
  ✅ SOC 2 Type II
     → Trust Service Categories:
        ✅ Security (CC)
        ✅ Availability
        ✅ Confidentiality
        ✅ Privacy

  Optional (add later if pursuing):
  ⬜ ISO 27001
  ⬜ HIPAA
  ⬜ GDPR
```

### Step 1.3: Define Scope

```
Navigate to: Settings → Scope

Define:
  System name: CloudPulse Analytics Platform
  System description: [Paste from SOC 2 Readiness Assessment — System Description section]
  
  In-scope services:
    ✅ Web application (multi-tenant BI platform)
    ✅ Data ingestion pipeline
    ✅ Analytics engine
    ✅ Admin portal
    ✅ CI/CD pipeline
  
  Out-of-scope:
    ❌ Third-party vendor systems
    ❌ Client-owned infrastructure
```

### Step 1.4: Configure Admin Settings

```
Settings → General:
  - Set fiscal year
  - Configure notification preferences (daily digest recommended)
  - Set evidence review reminder frequency: Monthly

Settings → Roles:
  GRC Analyst → Security Admin (full access)
  CISO → Security Admin
  IT Manager → Control Owner
  HR Director → Control Owner
  Legal → Control Owner
  Engineering Lead → Control Owner
  All others → Employee (limited access)
```

---

## Phase 2 — Integrations (Weeks 2–3)

This is the highest-value phase. Every integration Vanta connects will auto-collect evidence continuously, replacing manual screenshot collection.

### Integration Priority List

Navigate to: Integrations → Browse Integrations

| Priority | Integration | Category | Controls Covered | Setup Complexity |
|----------|-------------|----------|-----------------|-----------------|
| 🔴 P1 | AWS | Cloud | CC6.1, CC6.6, CC7.1, CC7.2, A1.1, A1.2 | Medium |
| 🔴 P1 | GitHub | Code | CC8.1, CC6.1, CC6.4 | Low |
| 🔴 P1 | Okta | Identity | CC6.1, CC6.2, CC6.3, CC6.5 | Low |
| 🔴 P1 | Google Workspace | HR / Email | CC1.4, CC6.3, A.6 | Low |
| 🟠 P2 | Jira | Ticketing | CC8.1, CC7.4 | Low |
| 🟠 P2 | Auth0 | Client Auth | CC6.1, CC6.2 | Low |
| 🟠 P2 | Datadog | Monitoring | CC7.2, CC7.3, A1.1 | Medium |
| 🟠 P2 | PagerDuty | Alerting | CC7.4, A1.1 | Low |
| 🟡 P3 | Rippling / BambooHR | HRIS | CC1.4, CC6.3 | Low |
| 🟡 P3 | Slack | Communication | CC2.2 | Low |
| 🟡 P3 | Gusto / ADP | Payroll | CC6.3 (background checks) | Low |

### AWS Integration Setup

```
Vanta → Integrations → AWS → Connect

Required: AWS IAM role with read-only permissions

Steps:
1. In AWS Console → IAM → Create Role
   - Trusted entity: AWS Account (Vanta's account ID — shown in Vanta UI)
   - Attach policy: SecurityAudit (AWS managed) + VantaAdditionalPermissions (JSON provided by Vanta)
   - Role name: VantaAuditorRole

2. In Vanta:
   - Enter Role ARN
   - Select regions to monitor: us-east-1, eu-west-1
   - Enable: EC2, S3, RDS, IAM, CloudTrail, Config, GuardDuty, SecurityHub

3. Verify:
   - Vanta shows AWS account as "Connected"
   - Initial scan completes within 30 minutes
   - At least 5 AWS-related controls show evidence collected

What Vanta collects from AWS automatically:
  - S3 bucket encryption and public access settings
  - RDS encryption at rest
  - CloudTrail logging status
  - GuardDuty enablement
  - IAM MFA enforcement
  - VPC security group configurations
  - EC2 instance patch status (via SSM)
```

### GitHub Integration Setup

```
Vanta → Integrations → GitHub → Connect

Steps:
1. Click Connect → Authorize Vanta GitHub App
2. Select organization: cloudpulse-analytics
3. Select repositories: All (or select production repos)

What Vanta collects from GitHub automatically:
  - Branch protection rules (main/master requires PR reviews)
  - Required code owner reviews
  - Secret scanning alerts
  - Dependabot alerts (dependency vulnerabilities)
  - Two-factor auth enforcement for org members
  - Admin access review
```

### Okta Integration Setup

```
Vanta → Integrations → Okta → Connect

Required: Okta API token (read-only)

Steps:
1. In Okta Admin → Security → API → Create Token
   - Name: Vanta-Integration-ReadOnly
   - Copy token

2. In Vanta:
   - Enter Okta domain: cloudpulse.okta.com
   - Enter API token

What Vanta collects from Okta automatically:
  - MFA enrollment status per user
  - Active user list (used for employee roster sync)
  - Admin account list
  - Password policy configuration
  - Session policy configuration
  - Inactive account detection
```

---

## Phase 3 — Control Mapping & Gaps (Weeks 4–5)

### Review Automated Test Results

```
Navigate to: Controls → Filter by: Failing

For each failing control:
  1. Click control → Review what Vanta tested
  2. Understand why it's failing:
     - Missing integration? → Add integration (Phase 2)
     - Config gap? → Fix the configuration
     - Policy not uploaded? → Upload policy (Phase 4)
     - Evidence needs manual upload? → Collect and upload
  3. Assign control owner
  4. Set remediation due date
```

### Assign Control Owners

```
Navigate to: Controls → Select control → Edit → Assign Owner

Recommended assignments:
  CC6 (Access Controls) → IT Manager
  CC7 (System Operations) → IT Manager + GRC Analyst
  CC8 (Change Management) → Engineering Lead
  CC1–CC3 (Governance, Risk) → GRC Analyst + CISO
  A1 (Availability) → Engineering Lead
  C1 (Confidentiality) → GRC Analyst + Legal
  P criteria (Privacy) → Legal + GRC Analyst
  People controls → HR Director
```

### Manual Evidence Upload (Non-Automated Controls)

Some controls cannot be automated. Upload evidence manually:

```
Navigate to: Controls → [Control] → Evidence → Upload

| Control | Manual Evidence Required |
|---------|-------------------------|
| CC3.2 — Risk assessment | Upload risk register PDF |
| CC3.3 — Fraud risk | Upload fraud risk assessment |
| CC7.4 — Incident response | Upload IRP + tabletop exercise report |
| CC9.2 — Vendor risk | Upload vendor risk assessment records |
| P5.0 — DSAR process | Upload DSAR procedure and log |
| P6.0 — Data map | Upload third-party data sharing map |
| A1.3 — Recovery testing | Upload backup restore test results |
```

---

## Phase 4 — People & Policies (Week 6)

### Onboard All Employees

```
Navigate to: People → Import Employees

Option A (Automated — preferred):
  → Sync from Google Workspace / Okta integration
  → Employees auto-populate with name, email, role, start date

Option B (Manual):
  → Upload CSV with: first name, last name, email, department, title, start date

After import:
  → Assign departments to each employee
  → Mark contractors vs. full-time
  → Assign role-based training tracks
```

### Security Training in Vanta

```
Navigate to: People → Training

Configure:
  - Required training: Security Awareness (annual)
  - Deadline: 14 days from assignment
  - New hire training: Assigned automatically on employee creation
  - Reminders: 7 days before due, day of due date

Vanta built-in training modules:
  ✅ Security awareness (general)
  ✅ HIPAA (if applicable)
  ✅ PCI DSS (if applicable)

For KnowBe4 integration:
  → Vanta → Integrations → KnowBe4 → Connect
  → Training completion syncs automatically as evidence
```

### Upload Policies

```
Navigate to: Policies → Upload Policy

Required policies for SOC 2 (upload all as PDF):
  [ ] Information Security Policy
  [ ] Acceptable Use Policy
  [ ] Access Control Policy
  [ ] Incident Response Plan
  [ ] Business Continuity Plan
  [ ] Vendor Management Policy
  [ ] Password Policy
  [ ] Encryption Policy
  [ ] Data Classification Policy
  [ ] Remote Work Policy
  [ ] Change Management Policy
  [ ] Privacy Policy

For each policy:
  - Set review frequency: Annual
  - Assign policy owner
  - Enable employee acknowledgement (Vanta sends signature requests)
  - Set acknowledgement deadline: 14 days
```

---

## Phase 5 — Evidence Review & Remediation (Weeks 7–8)

### Vanta Readiness Score Target

```
Navigate to: Dashboard → Readiness Score

Target before audit window opens: ≥ 85%

Score breakdown:
  - Automated tests passing: [X]%
  - Manual evidence uploaded: [X]%
  - Policies acknowledged: [X]%
  - Training completed: [X]%
  - Vendor reviews complete: [X]%
```

### Fix Failing Controls — Priority Order

Work through failing controls in this order:

```
1. All CC6 (Access Controls) — auditors focus heavily here
2. All CC7 (System Operations) — SIEM, monitoring, incident response
3. Availability (A1) — backup testing is the most common failure
4. Privacy (P) — data map and DSAR are usually gaps
5. CC8 (Change Management) — PR review enforcement
6. Vendor controls (CC9.2) — longest to fix; start early
```

### Vendor Risk in Vanta

```
Navigate to: Vendors → Add Vendor

For each vendor with access to CloudPulse systems or data:
  1. Add vendor name, category, data accessed
  2. Request security questionnaire (Vanta sends automatically)
  3. Upload vendor's SOC 2 report or ISO certificate if available
  4. Set review frequency: Annual
  5. Mark DPA/BAA status

Priority vendors to add first:
  - AWS (SOC 2 report available at aws.amazon.com/compliance)
  - GitHub
  - Okta
  - Auth0
  - Datadog
  - Any vendor processing EU personal data (DPA required)
```

---

## Phase 6 — Audit Readiness Check (Week 9)

### Pre-Audit Checklist in Vanta

```
Navigate to: Audits → New Audit → SOC 2 Type II

Set:
  - Audit period start: [Month 7]
  - Audit period end: [Month 12]
  - Auditor: [Firm name — e.g., A-LIGN, Prescient]

Vanta generates:
  - Auditor portal with read-only access
  - Evidence packages per control
  - Readiness report

Before sharing auditor access, confirm:
  [ ] Readiness score ≥ 85%
  [ ] No Critical failing controls
  [ ] All policies acknowledged by ≥ 95% of employees
  [ ] Training completion ≥ 95%
  [ ] Vendor reviews complete for all Tier 1 vendors
  [ ] Manual evidence uploaded for all non-automated controls
```

### Invite Auditor

```
Navigate to: Audits → [Audit Name] → Invite Auditor

Enter auditor's email → They receive read-only access to:
  - All controls and evidence
  - Policy documents
  - Employee training records
  - Vendor assessments
  - Test results

During audit observation period (Months 7–12):
  - Vanta continues collecting evidence automatically
  - Review Vanta dashboard weekly
  - Respond to auditor requests within 24 hours
  - Do NOT change control configurations during the observation period
    without documenting the change reason
```

---

## Ongoing Operations — Post-Implementation

| Activity | Frequency | Vanta Location |
|----------|-----------|---------------|
| Review failing automated tests | Weekly | Dashboard → Failing Controls |
| Review new employee onboarding | Weekly | People → New Hires |
| Policy acknowledgement follow-up | Monthly | Policies → Outstanding |
| Vendor questionnaire follow-up | Monthly | Vendors → Pending |
| Training completion review | Monthly | People → Training |
| Readiness score review | Monthly | Dashboard |
| Evidence freshness check | Quarterly | Controls → Evidence age |
| Framework re-scoping | Annually | Settings → Frameworks |

---

## Vanta Cost Reference (Approximate)

| Plan | Approx. Cost | Best For |
|------|-------------|---------|
| Starter | ~$15,000/year | Startups, SOC 2 only |
| Growth | ~$25,000–35,000/year | SOC 2 + 1 additional framework |
| Enterprise | Custom | Multiple frameworks, large org |

*Free trial available. Discounts for first-year startups common.*

---

## Key Vanta Terms for Interviews

| Term | Meaning |
|------|---------|
| Automated test | A check Vanta runs against a connected system (e.g., "Is MFA enabled?") |
| Manual test | Evidence you upload yourself (e.g., tabletop exercise report) |
| Readiness score | % of controls with passing evidence — your audit health indicator |
| Observation period | The time window auditors observe controls operating (SOC 2 Type II) |
| Auditor portal | Read-only view Vanta generates for your external auditor |
| Policy acknowledgement | Employee e-signature on a security policy — tracked automatically |
