# Security Awareness Training Program
## CloudPulse Analytics Inc. — Hypothetical Scenario

**Program Owner:** GRC Analyst
**SOC 2 Criteria Addressed:** CC1.4 (Accountability), CC2.2 (Internal Communication), CC6.3 (Access Awareness), CC6.8 (Malware Prevention), CC7.4 (Incident Response Awareness)
**Primary Tool:** KnowBe4 (phishing simulation + LMS)
**Effective Date:** Month 2
**Review Cycle:** Annual program review; quarterly metrics review

---

## Program Purpose

This program ensures all CloudPulse Analytics employees understand their security responsibilities, recognize common attack vectors, and know how to respond. It directly addresses the human layer of CloudPulse's security posture — the most frequently exploited attack surface in SaaS environments.

Human error is involved in over 80% of security breaches. This program treats security awareness as a measurable, ongoing control — not a one-time checkbox.

---

## Program Scope

| Audience | Included | Notes |
|----------|----------|-------|
| Full-time employees | ✅ | All roles, all departments |
| Part-time employees | ✅ | Prorated training schedule |
| Contractors and consultants | ✅ | Mandatory before system access granted |
| Executive team | ✅ | Targeted executive spear-phishing simulations |
| New hires | ✅ | Onboarding security training within Day 1–5 |
| Board members | ⚠️ | Recommended — security briefing annually |

---

## Training Curriculum

### Track 1: All Employees (Annual — Required)

Every employee completes this baseline curriculum once per year. Modules are assigned in KnowBe4 and must be completed within 14 days of assignment.

| Module | Topic | Duration | Format | Frequency |
|--------|-------|----------|--------|-----------|
| SEC-01 | Phishing and Social Engineering | 15 min | Video + quiz | Annual |
| SEC-02 | Password Security and MFA | 10 min | Interactive | Annual |
| SEC-03 | Data Classification and Handling | 10 min | Video + quiz | Annual |
| SEC-04 | Acceptable Use Policy | 10 min | Policy acknowledgement | Annual |
| SEC-05 | Incident Reporting — How and When | 10 min | Scenario-based | Annual |
| SEC-06 | Remote Work Security | 10 min | Video + quiz | Annual |
| SEC-07 | Physical Security and Clean Desk | 8 min | Video | Annual |
| SEC-08 | Insider Threat Awareness | 10 min | Video + quiz | Annual |

**Total baseline time:** ~85 minutes per employee per year

---

### Track 2: Role-Based Training (Targeted)

Additional modules assigned based on role and system access.

| Role Group | Module | Topic | Duration | Trigger |
|------------|--------|-------|----------|---------|
| Engineers / Developers | DEV-01 | Secure coding fundamentals (OWASP Top 10) | 30 min | Annual |
| Engineers / Developers | DEV-02 | Secrets management — no credentials in code | 20 min | Annual |
| Engineers / Developers | DEV-03 | Code review security checklist | 15 min | Annual |
| Finance / Accounting | FIN-01 | Business Email Compromise (BEC) and wire fraud | 20 min | Annual |
| Finance / Accounting | FIN-02 | Invoice fraud and vendor impersonation | 15 min | Annual |
| HR and People Ops | HR-01 | PII handling and employee data protection | 20 min | Annual |
| HR and People Ops | HR-02 | Recruiting phishing — fake job applicants | 15 min | Annual |
| Customer Support | CS-01 | Social engineering via support channels | 15 min | Annual |
| Customer Support | CS-02 | Client data handling and access controls | 15 min | Annual |
| Managers and Directors | MGR-01 | Security responsibilities as a people manager | 20 min | Annual |
| Executive Team | EXEC-01 | Executive targeting — spear phishing and deepfakes | 20 min | Annual |
| All system admins | ADM-01 | Privileged access security | 20 min | Annual |

---

### Track 3: Triggered / Just-in-Time Training

Assigned automatically when an employee fails a phishing simulation or violates a security policy.

| Trigger | Module Assigned | Deadline |
|---------|----------------|----------|
| Clicked phishing link | TRIG-01: Why You Got Phished | 48 hours |
| Submitted credentials in phishing sim | TRIG-02: Credential Phishing Deep Dive | 24 hours |
| Opened phishing attachment | TRIG-03: Malicious Attachments Explained | 48 hours |
| Reported a security incident | TRIG-04: Good Job — What Happens Next | 7 days (positive reinforcement) |
| Policy violation (e.g., shared password) | TRIG-05: Policy Refresher + Acknowledgement | 48 hours |
| Second phishing failure in 90 days | TRIG-06: 1:1 coaching with GRC Analyst | Within 1 week |

---

### Track 4: New Hire Onboarding (Day 1–5)

All new employees must complete the onboarding security track before being granted access to production systems.

| Day | Activity | Format | Owner |
|-----|----------|--------|-------|
| Day 1 | Welcome to Security at CloudPulse (overview) | Slide deck + video | GRC Analyst |
| Day 1 | Acceptable Use Policy — read and sign | Policy acknowledgement | HR + GRC |
| Day 2 | SEC-01 (Phishing), SEC-02 (Passwords + MFA) | KnowBe4 modules | Self-paced |
| Day 3 | SEC-03 (Data classification), SEC-05 (Incident reporting) | KnowBe4 modules | Self-paced |
| Day 4 | Role-based track modules (Track 2) | KnowBe4 modules | Self-paced |
| Day 5 | Security quiz — must score ≥ 80% to pass | KnowBe4 assessment | Self-paced |

**Access gating:** Production system access is not granted until Day 5 assessment is passed.

---

## Phishing Simulation Program

### Purpose

Phishing simulations measure real-world susceptibility and create teachable moments. They are not punitive — they are training tools. Results are used to improve the program, not to discipline employees.

### Simulation Schedule

| Simulation Type | Frequency | Template Rotation | Difficulty |
|----------------|-----------|-------------------|------------|
| General phishing (credential harvest) | Monthly | Rotated from KnowBe4 library | Beginner → Advanced over time |
| Spear phishing (personalized) | Quarterly | Custom — uses employee name, role, manager name | Advanced |
| Executive spear phishing | Quarterly | C-suite targeted; uses board member or investor names | Advanced |
| Vishing (voice phishing) | Bi-annually | IT helpdesk impersonation call | Advanced |
| Smishing (SMS phishing) | Bi-annually | Fake HR/payroll SMS | Intermediate |
| Attachment-based | Quarterly | Fake invoice, contract, or shared doc | Intermediate |
| QR code phishing | Quarterly | Fake parking, building notice, or HR flyer | Intermediate |

### Simulation Design Principles

```
1. Rotate templates — never reuse the same template within 6 months
2. Match current threat landscape — use themes attackers actually use right now
   (KnowBe4 has current-events templates — use them)
3. Vary difficulty over time — start easy, increase sophistication as employees improve
4. Include all departments — no exempt teams; executives included always
5. Never simulate MFA bypass or credential theft without CISO approval
6. Never use real external brands in a way that could confuse employees permanently
```

### What Happens When Someone Clicks

```
Immediate (automated by KnowBe4):
  → Employee lands on a safe "You were phished" landing page
  → Brief 2-minute in-the-moment explanation of what gave it away
  → TRIG-01 or TRIG-02 training module auto-assigned (due 48 hours)

Day 2:
  → Manager notified (aggregate, not named — unless repeat offender)

If second click within 90 days:
  → GRC Analyst schedules 1:1 coaching session
  → TRIG-06 assigned
  → Noted in employee security training record

If three or more failures in 6 months:
  → Escalate to HR and manager for additional support
  → Consider access restriction review
```

### What Happens When Someone Reports (Correct Behavior)

```
  → Positive reinforcement email sent automatically ("Great catch — here's what to look for")
  → TRIG-04 module assigned (explains what happens to reported phishing)
  → Employees who report before clicking are tracked as "heroes"
  → Top reporters recognized quarterly (without naming individuals publicly unless they opt in)
```

---

## Metrics and KPIs

### Core Metrics (Tracked Monthly)

| Metric | Definition | Target | Red Flag |
|--------|-----------|--------|----------|
| **Phishing click rate** | % of employees who clicked in last simulation | < 5% | > 15% |
| **Credential submission rate** | % who submitted credentials after clicking | < 2% | > 8% |
| **Report rate** | % who reported phishing (via "Phish Alert" button) | > 70% | < 30% |
| **Training completion rate** | % of assigned modules completed within deadline | > 95% | < 85% |
| **New hire completion rate** | % of new hires who complete onboarding track by Day 5 | 100% | < 100% |
| **Repeat clicker rate** | % of employees who click in 2+ sims in 90 days | < 3% | > 8% |

### Trend Metrics (Tracked Quarterly)

| Metric | Goal |
|--------|------|
| Click rate trend (QoQ) | Decreasing quarter over quarter |
| Report rate trend (QoQ) | Increasing quarter over quarter |
| Time to report (avg) | < 5 minutes from phishing email receipt |
| Departments with highest click rates | Identify and target with role-based training |
| Departments with highest report rates | Recognize and amplify |

### SOC 2 Evidence This Program Produces

| Evidence | Control | Collected How |
|----------|---------|---------------|
| Training completion reports | CC1.4, CC2.2 | KnowBe4 LMS export (monthly) |
| Phishing simulation results | CC6.8, CC7.4 | KnowBe4 campaign report (per simulation) |
| New hire onboarding records | CC6.3 | KnowBe4 + HR system |
| Policy acknowledgement records | CC5.3 | KnowBe4 policy manager |
| Triggered training assignments | CC6.8 | KnowBe4 smart groups + assignments |

---

## Reporting

### Monthly Report (GRC Analyst → CISO)

```markdown
## Security Awareness Monthly Report — [Month]

### Phishing Simulations
- Simulations run: [X]
- Click rate: [X]% (target: < 5%)
- Credential submission rate: [X]% (target: < 2%)
- Report rate: [X]% (target: > 70%)
- Repeat clickers (90-day): [X] employees

### Training Completion
- Modules completed: [X] / [X assigned]
- Completion rate: [X]% (target: > 95%)
- Overdue modules: [X] (employees: [names or teams])

### New Hires
- Hired this month: [X]
- Completed onboarding track by Day 5: [X] / [X]

### Actions Taken
- [Employee cohort] assigned [module] due to click rate spike
- [Department] flagged for targeted training next month
```

### Quarterly Trends Report (for Leadership + SOC 2 Evidence)

Include 12-month trend charts for:
- Click rate (should decline)
- Report rate (should increase)
- Completion rate (should stay high)
- Department breakdown heatmap

---

## Positive Security Culture Principles

A good awareness program doesn't just train — it builds culture:

```
Do:
  ✅ Celebrate employees who report phishing
  ✅ Share anonymized "close call" stories in team meetings
  ✅ Make security easy — one-click reporting button in email
  ✅ Communicate results transparently ("our click rate improved by X%")
  ✅ Acknowledge that even experts get fooled sometimes

Don't:
  ❌ Name and shame employees who click phishing sims
  ❌ Use security awareness as a disciplinary tool (first and second failures)
  ❌ Treat it as a checkbox exercise — training must be engaging
  ❌ Send simulations during known high-stress periods (year-end close, product launches)
  ❌ Overwhelm employees — no more than 1 simulation per month
```

---

## Tools Reference

| Tool | Purpose | Notes |
|------|---------|-------|
| KnowBe4 | Phishing simulations + LMS | Industry standard; free trial available at knowbe4.com |
| Proofpoint Security Awareness | Alternative to KnowBe4 | Strong enterprise option |
| Cofense | Phishing simulation focus | Good for large orgs |
| Google Workspace / M365 "Phish Alert" | One-click phishing report button | Built into email; configure in KnowBe4 |
| Slack #security-awareness channel | Culture + communication | Share tips, close calls, monthly metrics |
