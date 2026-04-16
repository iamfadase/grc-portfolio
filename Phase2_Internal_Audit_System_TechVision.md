# Phase 2: Internal Audit & Evidence Collection System
## TechVision Consulting Ltd. — ISO 27001:2022

**Phase:** 2 of 4
**ISO 27001 Clause:** Clause 9.2 — Internal Audit
**Audit Owner:** GRC Analyst (Lead Internal Auditor)
**Audit Period:** Month 9 (pre-certification)
**Certification Body Audit:** Month 11–12

---

## Purpose

This document defines TechVision's internal audit methodology, audit program, evidence collection system, and nonconformity management process. The internal audit validates that the ISMS is:

1. Conforming to ISO 27001:2022 requirements and TechVision's own policies
2. Effectively implemented and maintained
3. Producing the intended security outcomes

A well-run internal audit directly prepares TechVision for Stage 1 and Stage 2 certification audits by identifying and closing gaps before the external auditor arrives.

---

## Internal Audit Program (Annual)

The annual audit program covers the full ISMS across two audit cycles:

| Audit | Timing | Scope | Purpose |
|-------|--------|-------|---------|
| Audit 1 — Pre-Certification | Month 9 | Full ISMS (all clauses + Annex A) | Find gaps before external audit |
| Audit 2 — Surveillance | Month 21 (Year 2) | Risk-based selection of clauses + controls | Maintain certification |

### Audit 1 Scope — Full ISMS

**ISO 27001 Clauses in scope:**

| Clause | Title | Auditable Elements |
|--------|-------|-------------------|
| 4 | Context of the organization | Internal/external issues, interested parties, ISMS scope |
| 5 | Leadership | Policy, roles, responsibilities, management commitment |
| 6 | Planning | Risk assessment, risk treatment, Statement of Applicability (SoA) |
| 7 | Support | Resources, competence, awareness, communication, documentation |
| 8 | Operation | Operational planning, risk assessment execution, risk treatment execution |
| 9 | Performance evaluation | Monitoring, measurement, internal audit, management review |
| 10 | Improvement | Nonconformities, corrective action, continual improvement |
| Annex A | Controls | All 93 controls per Statement of Applicability |

---

## Audit Methodology

TechVision's internal audit follows the **ISO 19011:2018** guidelines for auditing management systems.

### Audit Techniques

| Technique | When Used | Examples |
|-----------|-----------|---------|
| Document review | All controls | Review policies, procedures, records, logs |
| Interview | Leadership and process owners | Ask how controls work in practice |
| Observation | Physical and operational controls | Watch a process being performed |
| Technical testing | System controls | Test access controls, run scan, check config |
| Sampling | Evidence-heavy controls | Select a sample of records to review |

### Sampling Approach

For controls with large volumes of evidence (e.g., access reviews, change tickets), use statistical sampling:

| Population Size | Minimum Sample |
|----------------|---------------|
| 1–10 records | 100% (review all) |
| 11–50 records | 10 records |
| 51–200 records | 15 records |
| 200+ records | 25 records |

Document your sample selection rationale. Random sampling is preferred; auditors distrust cherry-picked samples.

---

## Audit Planning

### Step 1: Audit Notification (4 weeks before)

Send formal audit notification to all process owners:

```
Subject: ISO 27001 Internal Audit — Notice and Schedule

Dear [Name],

This is formal notification that an ISO 27001 internal audit will be conducted
for the area(s) under your responsibility.

Audit dates: [Date range]
Scope: [Clauses and controls relevant to them]
Lead Auditor: [Your name]

Please ensure the following are available:
- Current documented procedures and policies
- Evidence records from the last 12 months
- System access for any technical testing

A document request list is attached. Please prepare evidence by [date - 2 weeks before audit].

[Your name]
GRC Analyst / Lead Internal Auditor
```

### Step 2: Document Request List

Send a document request to each process owner 2 weeks before audit:

| Process Owner | Documents/Evidence Requested |
|--------------|------------------------------|
| CISO | ISMS scope, information security policy, management review minutes, risk register |
| IT Manager | Access review records, vulnerability scan reports, patch logs, backup test results, change records |
| HR Director | Training completion records, background check records, employment contracts with IS clauses, offboarding checklists |
| Legal | Vendor contracts with IS clauses, legal register, DPIA register, privacy policy |
| PMO | Project security review records, security gates in project templates |
| Procurement | Vendor risk assessments, supplier agreements |
| All owners | Evidence of control implementation for assigned controls |

### Step 3: Audit Schedule

| Date | Time | Area | Process Owner | Techniques |
|------|------|------|--------------|------------|
| Day 1 AM | 09:00–11:00 | Opening meeting | All owners | Presentation |
| Day 1 AM | 11:00–12:30 | Clauses 4–6 (Context, Leadership, Planning) | CISO | Document review, interview |
| Day 1 PM | 14:00–17:00 | Clause 7 (Support) + HR controls (A.6) | HR Director | Document review, interview |
| Day 2 AM | 09:00–12:00 | Access controls (A.5.15–A.5.18, A.8.2–A.8.5) | IT Manager | Technical testing, document review |
| Day 2 PM | 13:00–16:00 | Vulnerability management + monitoring (A.8.8, A.8.15–A.8.16) | IT Manager | Technical testing, document review |
| Day 3 AM | 09:00–12:00 | Supplier and legal controls (A.5.19–A.5.22, A.5.31–A.5.34) | Legal + Procurement | Document review, interview |
| Day 3 PM | 13:00–15:00 | Physical controls (A.7) | Facilities | Observation, document review |
| Day 3 PM | 15:00–17:00 | Incident management + BCP (A.5.24–A.5.30) | CISO + IT | Document review, interview |
| Day 4 AM | 09:00–12:00 | Development + change management (A.8.25–A.8.32) | Dev Lead | Technical review, document review |
| Day 4 PM | 13:00–15:00 | Audit evidence review and finding analysis | Auditor only | Internal |
| Day 4 PM | 15:00–17:00 | Closing meeting — preliminary findings | All owners | Presentation |

---

## Evidence Collection System

### Evidence Repository Structure

Organize all audit evidence in a structured folder system:

```
/audit/
  /2024-month9-internal-audit/
    /01-context-and-leadership/
      isms-scope-statement-v2.pdf
      information-security-policy-approved.pdf
      management-review-minutes-month8.pdf
    /02-risk-management/
      risk-register-current.xlsx
      risk-assessment-methodology.pdf
      statement-of-applicability-v3.xlsx
    /03-access-controls/
      access-review-q3-2024.xlsx
      okta-mfa-enforcement-screenshot.png
      user-provisioning-sop-v1.pdf
      offboarding-checklist-sample-x5.pdf
    /04-vulnerability-management/
      tenable-scan-report-month8.pdf
      patch-log-month8.csv
      critical-cve-remediation-tickets.pdf
    /05-hr-controls/
      training-completion-report-lms.csv
      background-check-process-doc.pdf
      employment-contract-template-is-clause.pdf
    /06-supplier-management/
      vendor-risk-assessments-top10.pdf
      vendor-contracts-is-clauses-sample.pdf
    /07-incident-management/
      incident-response-plan-v2.pdf
      irp-tabletop-exercise-report.pdf
      incident-log-ytd.xlsx
    /08-physical-controls/
      badge-access-logs-sample.pdf
      cctv-footage-log.pdf
      clean-desk-audit-results.pdf
    /09-findings-and-ncrs/
      audit-findings-log.xlsx
      ncr-001.pdf
      ncr-002.pdf
    /audit-report-final.pdf
```

### Evidence Quality Standards

For each piece of evidence, verify it meets these standards before accepting it:

| Standard | Requirement |
|----------|------------|
| **Currency** | Dated within the audit period (last 12 months) |
| **Relevance** | Directly demonstrates the control requirement |
| **Sufficiency** | Enough volume to support the finding (sampled appropriately) |
| **Authenticity** | Clearly from the stated system (includes system name, timestamp, export metadata) |
| **Completeness** | Full record — not cropped, partial, or cherry-picked |

### Evidence Collection Templates

#### Access Review Evidence Checklist
```
Control: A.5.18 — Access Rights

Evidence to collect:
  [ ] Most recent quarterly access review report
      - Date of review
      - Systems covered
      - Number of accounts reviewed
      - Changes made as a result
  [ ] Screenshot showing current access matrix or IAM configuration
  [ ] At least 3 sample tickets showing access removed after review
  [ ] Evidence that privileged accounts were included in the review
  [ ] Sign-off by IT Manager or CISO

Sample size: Last 2 access review cycles
Auditor test: Request a list of users with admin rights; verify against the review records
```

#### Vulnerability Management Evidence Checklist
```
Control: A.8.8 — Technical Vulnerability Management

Evidence to collect:
  [ ] Scan schedule document (or GRC tool config showing scan frequency)
  [ ] Last 3 months of vulnerability scan reports
  [ ] Remediation tickets for all Critical/High findings in last 90 days
  [ ] Evidence of SLA compliance (date found vs. date resolved)
  [ ] At least 1 example of a Critical vulnerability remediated within 24 hours
  [ ] Exception log (any findings accepted / risk-accepted)

Auditor test: Pull a Critical CVE from last scan; trace it to a remediation ticket with timestamps
```

#### Training Completion Evidence Checklist
```
Control: A.6.3 — Information Security Awareness, Education and Training

Evidence to collect:
  [ ] LMS completion report — all employees — current training year
  [ ] Evidence of role-based training completion (developers, finance, HR)
  [ ] New hire training completion records (sample of last 5 new hires)
  [ ] Training curriculum (what topics are covered, how often updated)
  [ ] Evidence that training content is current (last review/update date)

Auditor test: Select 5 employees at random; confirm they appear in completion report
Red flag: Any active employee with no training completion record
```

#### Incident Response Evidence Checklist
```
Control: A.5.24–A.5.26 — Incident Management

Evidence to collect:
  [ ] Incident Response Plan (current version, with approval date)
  [ ] Tabletop exercise report (date, scenario, participants, findings, follow-up actions)
  [ ] Incident log for last 12 months
  [ ] For any real incidents: timeline, containment actions, lessons learned
  [ ] Evidence that staff know how to report an incident (awareness training records)

Auditor test: Ask process owner to walk through the IRP for a phishing scenario
Red flag: IRP exists but was never tested; no incident log
```

---

## Nonconformity (NCR) Management

When the audit finds a requirement is not met, it is recorded as a Nonconformity (NCR).

### NCR Classification

| Type | Definition | Example |
|------|-----------|---------|
| **Major Nonconformity** | Complete absence of a required control, or systematic failure affecting the ISMS | No risk assessment has ever been conducted; no incident response plan exists |
| **Minor Nonconformity** | Isolated gap or partial implementation that doesn't undermine the overall ISMS | One department missed annual training; access review was 2 weeks late |
| **Observation** | Potential weakness or improvement opportunity; not yet a nonconformity | Process works but is undocumented; control effective but evidence poorly organized |

### NCR Record Template

```markdown
## Nonconformity Report — NCR-[Number]

**Date Raised:** [Date]
**Raised By:** [Auditor name]
**Area / Process:** [Department or control area]
**ISO 27001 Clause / Control:** [e.g., A.8.8 or Clause 9.2]
**NCR Type:** Major / Minor / Observation

### Finding Description
[Describe exactly what was observed. What is present vs. what is required.]

### Objective Evidence
[List the specific evidence reviewed that supports this finding.]
- [Evidence item 1]
- [Evidence item 2]

### Root Cause Analysis
[Why did this gap occur? Use 5-Why analysis if helpful.]
- Why 1:
- Why 2:
- Why 3:

### Corrective Action Plan
| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| [Specific action] | [Name] | [Date] | Open |

### Verification
**Corrective action verified by:** [Auditor name]
**Verification date:** [Date]
**Verification method:** [How you confirmed it was fixed]
**NCR Status:** Open / Closed
```

### NCR Tracker

| NCR # | Type | Clause/Control | Finding Summary | Owner | Due Date | Status |
|-------|------|----------------|-----------------|-------|----------|--------|
| NCR-001 | Minor | A.6.3 | 3 employees missing annual security training | HR | Month 10 | Open |
| NCR-002 | Minor | A.8.8 | Vulnerability scan reports not retained for 12 months | IT | Month 10 | Open |
| NCR-003 | Major | A.5.24 | IRP exists but has never been tested via tabletop or real incident | CISO | Month 10 | Open |
| NCR-004 | Minor | A.5.19 | 40% of vendors have no documented risk assessment | Procurement | Month 11 | Open |
| NCR-005 | Observation | A.5.37 | SOPs for cloud operations exist but are not version-controlled | IT | Month 11 | Open |

---

## Internal Audit Report

### Report Structure

```markdown
# ISO 27001 Internal Audit Report
**Organization:** TechVision Consulting Ltd.
**Audit Date(s):** [Date range]
**Lead Auditor:** [Name]
**Audit Scope:** Full ISMS — ISO 27001:2022 Clauses 4–10 and Annex A
**Distribution:** CISO, Department Heads, Management Review

---

## Executive Summary

[2–3 paragraphs. State: overall ISMS conformance, key strengths observed, number and type
of nonconformities, and overall readiness for external certification audit.]

Overall conformance: [X]% of requirements met / partially met
Major NCRs: [X] — must be closed before certification audit
Minor NCRs: [X] — should be closed before certification audit
Observations: [X]

---

## Audit Objectives and Scope
[State what was audited, what was excluded, and why]

## Methodology
[Techniques used: document review, interview, technical testing, observation, sampling]

## Findings Summary

### Strengths (Areas of Good Practice)
- [Strength 1]
- [Strength 2]

### Nonconformities
[Table of all NCRs with type, clause, and summary]

### Observations
[List of observations]

## Corrective Action Requirements

Major NCRs must be closed and verified before the external audit (Stage 2).
Minor NCRs should be closed before the external audit.
Target completion: [Date]

## Conclusion and Certification Readiness

[State whether the ISMS is ready for external audit, with conditions if applicable.]

---
Signed: [Lead Auditor] | Date: [Date]
```

---

## Certification Audit Preparation Checklist

Use this 4-week before external audit:

```
4 Weeks Before:
  [ ] All Major NCRs from internal audit are closed and verified
  [ ] Statement of Applicability (SoA) is finalized and signed
  [ ] Risk register is current (reviewed within last 90 days)
  [ ] Management review meeting has been held and documented
  [ ] All Annex A controls have at least one piece of current evidence

2 Weeks Before:
  [ ] Evidence repository is organized per folder structure above
  [ ] All control owners have confirmed their evidence is complete
  [ ] Internal audit report is finalized and distributed
  [ ] Auditor logistics confirmed (access, meeting rooms, system access)

1 Week Before:
  [ ] Dry run — present ISMS overview to CISO as if to external auditor
  [ ] Brief all process owners on what to expect during interviews
  [ ] Confirm all staff know: be honest, say "I don't know" if unsure, don't guess

Audit Week:
  [ ] Welcome auditor; provide ISMS overview (Stage 1: document review)
  [ ] Facilitate interviews — be present but don't answer for process owners
  [ ] Respond to evidence requests within same business day
  [ ] Track all auditor questions and findings in real time
```

---

## Useful Definitions for Interviews

Prepare to explain these concepts clearly — auditors will ask:

| Term | What to Say |
|------|------------|
| ISMS | "The set of policies, processes, and controls we use to manage information security systematically" |
| Risk appetite | "The level of risk TechVision is willing to accept — we accept residual risks scored 6 or below" |
| Statement of Applicability | "The document that lists all 93 ISO 27001 Annex A controls, whether we've included or excluded each, and why" |
| Nonconformity | "A gap where we don't meet a requirement — we log it, find the root cause, and fix it" |
| Continual improvement | "We regularly review our ISMS, learn from incidents and audits, and make it better over time" |
