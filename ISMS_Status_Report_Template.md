# ISMS Compliance Status Report
**Organization:** TechVision Consulting Ltd.
**Report Period:** [Month / Quarter]
**Prepared By:** GRC Analyst
**Distributed To:** CISO, Department Heads
**Date:** [Date]

---

## Executive Summary

> [2–3 sentences. State overall compliance posture, most critical finding, and one action leadership needs to take or approve. Example: "The ISMS is on track for certification with 68% of ISO 27001 controls fully implemented, up from 50% last month. A critical gap in DLP tooling remains unresolved and requires budget approval by [date]. No new high-severity incidents occurred this period."]

---

## Overall Compliance Status

| Metric | This Period | Last Period | Trend |
|--------|-------------|-------------|-------|
| Controls Implemented (✅) | 28 / 93 | 28 / 93 | ➡️ |
| Controls Partial (⚠️) | 38 / 93 | 38 / 93 | ➡️ |
| Controls Not Started (❌) | 27 / 93 | 27 / 93 | ➡️ |
| **Overall Completion** | **50%** | **50%** | ➡️ |
| Open Findings (High/Critical) | 5 | — | 🔴 |
| Findings Remediated This Period | 0 | — | — |
| Risk Register: Critical Risks | 2 | 2 | ➡️ |
| Risk Register: High Risks | 5 | 5 | ➡️ |

**Status: 🟡 On Track / 🔴 At Risk / 🟢 Healthy**
*(Update each period)*

---

## Control Implementation Progress by Domain

| Domain | Total Controls | ✅ Done | ⚠️ Partial | ❌ Not Started | % Complete |
|--------|---------------|---------|------------|----------------|------------|
| A.5 – Organizational | 37 | 12 | 14 | 11 | 51% |
| A.6 – People | 8 | 3 | 3 | 2 | 56% |
| A.7 – Physical | 14 | 5 | 5 | 4 | 54% |
| A.8 – Technological | 34 | 8 | 16 | 10 | 47% |
| **Total** | **93** | **28** | **38** | **27** | **50%** |

---

## New Findings This Period

| Finding ID | Control | Description | Severity | Owner | Due Date | Status |
|------------|---------|-------------|----------|-------|----------|--------|
| F-001 | A.8.12 | DLP tool not deployed — client data at risk of exfiltration | 🔴 High | IT Manager | Month 5 | Open |
| F-002 | A.6.3 | 3 employees have not completed annual security training | 🟡 Medium | HR Director | Month 3 | Open |
| F-003 | A.8.8 | 2 servers with unpatched critical CVEs (CVSS 9.1 and 8.8) | 🔴 High | IT Manager | Month 3 | Open |
| F-004 | A.6.7 | No remote work security policy — 40% of staff work remotely | 🟡 Medium | HR + IT | Month 2 | Open |
| F-005 | A.8.33 | Production client data used in development test environment | 🔴 High | Dev Lead | Month 4 | Open |

---

## Remediation Progress (Prior Findings)

| Finding ID | Description | Owner | Original Due | Updated Status |
|------------|-------------|-------|-------------|----------------|
| — | No prior findings yet — this is the first review period | — | — | — |

---

## Risk Posture Update

| Risk ID | Risk Name | Inherent Score | Residual Score | Change | Notes |
|---------|-----------|----------------|----------------|--------|-------|
| RISK-001 | Phishing / credential compromise | 20 🔴 | 9 🟡 | ➡️ | MFA enforced; email sandbox in procurement |
| RISK-002 | Ransomware | 20 🔴 | 6 🟡 | ➡️ | EDR deployment planned Month 3 |
| RISK-004 | Cloud misconfiguration | 16 🔴 | 6 🟡 | ➡️ | CIS baseline review in progress |
| RISK-007 | GDPR non-compliance | 12 🟠 | 6 🟡 | ➡️ | DPIAs in draft; DPO not yet appointed |

**Risk appetite threshold: Residual score ≤ 6. All risks above threshold are actively being treated.**

---

## Milestone / Audit Calendar Status

| Milestone | Target Date | Status | Notes |
|-----------|-------------|--------|-------|
| ISMS scope finalized | Month 1 | ✅ Complete | — |
| Asset inventory complete | Month 2 | 🔄 In Progress | Cloud assets not yet inventoried |
| Risk assessment baseline | Month 2 | ✅ Complete | 10 risks documented |
| Statement of Applicability (SoA) draft | Month 3 | ⏳ Planned | — |
| Policy library complete | Month 3 | 🔄 In Progress | 6 of 15 policies approved |
| Risk treatment plan approved | Month 4 | ⏳ Planned | — |
| Internal audit (Stage 1) | Month 9 | ⏳ Planned | — |
| External certification audit | Month 12 | ⏳ Planned | — |

---

## Decisions Required from Leadership

> List anything that requires a management decision, budget approval, or executive sign-off this period.

| # | Decision Needed | Owner | Urgency | Impact if Delayed |
|---|----------------|-------|---------|-------------------|
| 1 | Approve budget for DLP tool (~$X/month) | CISO / CFO | 🔴 High | F-001 remains open; client data exfiltration risk unmitigated |
| 2 | Appoint DPO or data steward for GDPR compliance | CEO / CISO | 🟡 Medium | GDPR risk remains high; DPIAs cannot be finalized |
| 3 | Approve remote work security policy for distribution | CISO / HR | 🟡 Medium | 40% of staff working without formal security guidelines |

---

## Actions This Period

| Action | Owner | Due | Status |
|--------|-------|-----|--------|
| Complete cloud asset inventory (AWS, Azure) | IT Manager | Month 2 | 🔄 In Progress |
| Draft remote work security policy | HR + IT | Month 2 | 🔄 In Progress |
| Patch 2 servers with critical CVEs | IT Manager | Month 3 | ⏳ Not Started |
| Complete 3 outstanding employee security training | HR | Month 3 | ⏳ Not Started |
| Finalize encryption policy | IT + Dev | Month 3 | 🔄 In Progress |
| Begin Statement of Applicability (SoA) | GRC Analyst | Month 3 | ⏳ Not Started |

---

## Notes / Comments

> [Any additional context, observations, or items not captured above.]

---

*This report was produced following the ISO 27001 Compliance Control Review Runbook. Next review scheduled: [Date or trigger condition].*
