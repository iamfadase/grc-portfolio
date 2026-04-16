# Runbook: ISO 27001 Compliance Control Review
**Owner:** GRC Analyst | **Frequency:** As Needed (triggered)
**Organization:** TechVision Consulting Ltd.
**Last Updated:** Month 2 | **Last Run:** —

---

## Purpose

This runbook defines the step-by-step procedure for conducting a periodic ISO 27001:2022 compliance control review at TechVision Consulting Ltd. It ensures controls remain implemented and effective, evidence stays current, and the compliance tracker reflects the true state of the ISMS.

**Run this procedure when:**
- A scheduled internal audit is approaching (minimum 4 weeks before)
- A significant organizational change occurs (new system, acquisition, team restructure)
- A security incident has occurred that may have impacted a control
- A new regulatory requirement or contract obligation is introduced
- It has been more than 90 days since the last control review
- Preparing for external ISO 27001 certification or surveillance audit

---

## Prerequisites

Before starting, confirm the following:

- [ ] Access to the ISO 27001 Compliance Tracker (`/compliance/ISO27001_Compliance_Tracker.md`)
- [ ] Access to the Risk Register (`/risk/ISO27001_Risk_Assessment.md`)
- [ ] Access to all evidence repositories (SharePoint/Drive, IT folder, HR folder, Legal folder)
- [ ] GRC tool access (Vanta / Hyperproof / equivalent) if implemented
- [ ] List of current control owners confirmed (CISO, IT Manager, HR Director, Legal, Procurement)
- [ ] Evidence collection templates ready (screenshots, exports, signed documents)
- [ ] Review scope defined — full Annex A (93 controls) or targeted domain review

**Estimated time:** 4–8 hours for a full review; 1–2 hours for a targeted domain review

---

## Procedure

### Step 1: Define Review Scope

Determine whether this is a full review or targeted:

```
Full review:     All 4 domains — A.5, A.6, A.7, A.8 (93 controls)
Targeted review: Select domains based on trigger:
  - Incident occurred → review A.5.24–A.5.28 (incident management)
  - New cloud system added → review A.5.23, A.8.2–A.8.9
  - Staff changes → review A.6.1–A.6.8
  - Audit prep → all domains
```

**Expected result:** A defined list of controls to review is documented before starting.
**If unclear:** Default to full review if 90+ days have passed or an audit is approaching.

---

### Step 2: Pull the Current Compliance Tracker

Open the compliance tracker and note the current status of each in-scope control:

```
File: /compliance/ISO27001_Compliance_Tracker.md
Check each control for:
  - Current status (✅ Implemented / ⚠️ Partial / ❌ Not Started)
  - Last review date
  - Evidence location listed
  - Control owner assigned
```

**Expected result:** A clear picture of what was previously recorded, what's stale, and what needs verification.
**If a control has no last review date:** Treat it as not reviewed — collect fresh evidence.

---

### Step 3: Contact Control Owners

Notify each control owner that a review is in progress and request updated evidence:

```
Message template:

Subject: ISO 27001 Control Review — Evidence Request

Hi [Name],

I'm conducting a compliance control review for our ISO 27001 ISMS.
I need updated evidence for the controls you own by [DATE — 5 business days].

Controls in scope:
- [Control ID] — [Description] — Evidence needed: [type]
- [Control ID] — [Description] — Evidence needed: [type]

Please upload to: [SharePoint/Drive folder path]

Let me know if you have any questions.

Thanks,
[Your name]
```

**Expected result:** Control owners acknowledge the request and commit to a submission date.
**If no response within 2 business days:** Follow up directly. Escalate to CISO if still unresponsive after 4 days.

---

### Step 4: Collect and Verify Evidence

For each control, collect and verify the required evidence. Use the table below as a guide for common evidence types:

| Control Domain | Common Evidence Types |
|----------------|-----------------------|
| A.5 – Organizational | Approved policy documents, signed agreements, meeting minutes, vendor contracts, access matrices |
| A.6 – People | Background check records, training completion logs, signed employment contracts, offboarding checklists |
| A.7 – Physical | CCTV logs, badge access reports, equipment registers, maintenance records |
| A.8 – Technological | System config screenshots, scan reports, patch logs, IAM access reviews, backup test results |

**For each piece of evidence, confirm:**
```
1. Is it dated within the last 90 days (or applicable review period)?
2. Does it match the control requirement exactly?
3. Is it stored in the correct location in the evidence repository?
4. Is it in an auditor-acceptable format (screenshot with timestamp, signed PDF, export with metadata)?
```

**Expected result:** Each reviewed control has at least one piece of current, relevant evidence linked.
**If evidence is missing or outdated:** Mark control as ⚠️ Partial and log the gap in Step 6.

---

### Step 5: Test a Sample of Controls

Don't just check that a control exists — verify it actually works. For at least 20% of controls, perform a brief effectiveness test:

```
Access control (A.5.15 / A.8.3):
  → Attempt to access a restricted system with a non-privileged account
  → Verify access is denied and logged

MFA enforcement (A.8.5):
  → Attempt login without MFA on a test account
  → Confirm it is blocked

Backup integrity (A.8.13):
  → Request a test restore of a non-critical file from the most recent backup
  → Confirm restore completes successfully

Patch management (A.8.8):
  → Pull vulnerability scan report
  → Check that critical CVEs from 30 days ago are patched

Training completion (A.6.3):
  → Pull LMS completion report
  → Verify 100% of active employees have completed current year's training
```

**Expected result:** Sampled controls demonstrate active effectiveness, not just documented existence.
**If a control fails the test:** Mark as ❌ Not Working, log as a finding, and escalate to the control owner immediately.

---

### Step 6: Update the Compliance Tracker

Update each reviewed control in the tracker with:

```
Fields to update for each control:
  - Status: ✅ Implemented / ⚠️ Partial / ❌ Not Started / ❌ Not Working
  - Evidence Location: [link or folder path]
  - Last Reviewed: [today's date]
  - Gap / Notes: [describe any finding, missing evidence, or partial implementation]
```

**Expected result:** Compliance tracker reflects the current true state of all reviewed controls.
**If updating a GRC tool (Vanta/Hyperproof):** Sync changes and trigger any automated evidence re-collection where available.

---

### Step 7: Update the Risk Register

Cross-reference findings with the risk register. If any control failure introduces or worsens a risk:

```
1. Open /risk/ISO27001_Risk_Assessment.md
2. Find the risk(s) linked to the failed/degraded control
3. Update:
   - Residual risk score (if control is no longer effective, residual may increase)
   - Treatment status (change to ⚠️ Degraded or 🔴 Re-opened if needed)
   - Notes field with date and finding summary
4. If residual score exceeds risk appetite (> 6): escalate to CISO
```

**Expected result:** Risk register reflects any changes in control effectiveness.
**If a critical risk is re-opened:** Notify CISO within 24 hours.

---

### Step 8: Log Findings and Gaps

Compile all findings into a review findings log:

```markdown
## Control Review Findings Log
**Review Date:** [Date]
**Scope:** [Full / Domain / Triggered by: X]
**Reviewed by:** [Name]

| Control ID | Finding | Severity | Owner | Remediation Deadline |
|------------|---------|----------|-------|----------------------|
| A.8.12 | DLP tool still not deployed — gap from Month 1 | High | IT Manager | [Date] |
| A.6.3 | 3 employees missing annual security training | Medium | HR Director | [Date] |
| A.8.8 | 2 servers with unpatched critical CVEs | High | IT Manager | [Date +7 days] |
```

**Expected result:** All findings are documented with owners and deadlines.
**If more than 5 High/Critical findings exist:** Escalate to CISO and schedule an emergency remediation meeting.

---

### Step 9: Produce the Status Report

Generate the compliance status report using the ISMS Status Report template:

```
File: /planning/ISMS_Status_Report_Template.md

Update:
  - Overall compliance % (controls implemented / total)
  - New findings from this review
  - Remediation progress on prior findings
  - Risk posture changes
  - Upcoming audit milestones
```

**Expected result:** A one-page status report ready to share with CISO/management.
**Distribute to:** CISO, relevant department heads, and store in the board/management folder.

---

### Step 10: Archive the Review

```
Create a review record folder:
  Location: /evidence/control-reviews/[YYYY-MM]/

Contents to archive:
  - Completed findings log (from Step 8)
  - Exported compliance tracker snapshot (PDF or copy)
  - Evidence files collected during this review
  - Status report (from Step 9)

Update the audit calendar in the Compliance Tracker:
  - Mark this review as complete
  - Set next review trigger date (90 days or next event)
```

**Expected result:** A complete, auditable record of this review exists and can be produced for external auditors.

---

## Verification Checklist

Before closing out the review, confirm all of the following:

- [ ] All in-scope controls have an updated status and last review date
- [ ] All evidence is current (dated within review period) and stored in the correct location
- [ ] All findings are logged with owners and remediation deadlines
- [ ] Risk register updated where control effectiveness changed
- [ ] Status report produced and distributed
- [ ] Review archived in the evidence folder
- [ ] Audit calendar updated

---

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Control owner not responding | Unaware of importance or conflicting priorities | Escalate to their manager; CC the CISO on follow-up |
| Evidence exists but is outdated | No recurring evidence collection process | Set up automated evidence collection in GRC tool; add calendar reminders |
| GRC tool showing different status than tracker | Manual and automated tracking out of sync | Use GRC tool as system of record; archive manual tracker as snapshot |
| Multiple controls failing in same domain | Systemic process breakdown in that area | Schedule a targeted deep-dive with the domain owner; escalate if critical |
| Evidence not accepted by auditor | Wrong format, missing metadata, or insufficient detail | Request re-collection in correct format; refer to auditor's evidence guide |
| New system found not in asset inventory | Asset inventory is incomplete | Add to asset register; assess whether new controls are needed |

---

## Rollback / Undo

This is a documentation and review process — no system changes are made during the review itself. If an incorrect status update was made to the compliance tracker:

```
1. Open the compliance tracker
2. Revert the incorrect field to its prior value
3. Add a note explaining the correction and date
4. If the GRC tool was also updated, revert there too
```

---

## Escalation

| Situation | Contact | Method | Timeframe |
|-----------|---------|--------|-----------|
| Critical control failure (e.g., MFA not working) | CISO + IT Manager | Direct message + email | Within 1 hour |
| Control owner unresponsive after 4 days | CISO | Email | Same day |
| Residual risk exceeds risk appetite | CISO | Email with risk register excerpt | Within 24 hours |
| 5+ High/Critical findings in a single review | CISO + department heads | Meeting request | Within 48 hours |
| Evidence of active breach discovered during review | CISO + Incident Response team | Phone call + IRP activation | Immediately |

---

## Review History

| Date | Run By | Scope | Findings | Notes |
|------|--------|-------|----------|-------|
| Month 1 | GRC Analyst | Full (baseline) | 27 not started, 38 partial | Initial baseline — see Compliance Tracker |
| — | — | — | — | — |
