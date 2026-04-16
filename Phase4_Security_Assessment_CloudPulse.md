# Phase 4: Security Assessment
## CloudPulse Analytics Inc. — Hypothetical Scenario

**Phase:** 4 of 4
**Assessment Type:** Internal Security Assessment (Threat Modeling + Vulnerability Assessment + Pen Test Coordination)
**Assessor:** GRC Analyst (internal lead)
**External Pen Test Firm:** SecureStrike Consulting (hypothetical)
**SOC 2 Criteria Addressed:** CC3.2, CC7.1, CC7.4, CC8.1, A1.2
**Assessment Window:** Months 5–6
**Report Date:** Month 6

---

## Assessment Scope

| Component | In Scope | Method |
|-----------|----------|--------|
| Web application (BI platform) | ✅ | STRIDE threat model + DAST + pen test |
| AWS infrastructure | ✅ | Config review + STRIDE + vuln scan |
| Authentication systems (Okta, Auth0) | ✅ | Config review + threat model |
| CI/CD pipeline (GitHub Actions) | ✅ | Config review + STRIDE |
| Data ingestion pipeline | ✅ | STRIDE threat model |
| Admin portal | ✅ | STRIDE + pen test |
| Internal corporate network | ❌ | Out of scope — covered by TechVision model |
| Client-owned infrastructure | ❌ | Out of scope |

---

## Part 1: Threat Model — STRIDE Methodology

STRIDE is a structured threat modeling framework developed by Microsoft. It identifies threats across 6 categories for each system component.

### STRIDE Categories

| Category | Threat Type | Example |
|----------|------------|---------|
| **S** — Spoofing | Impersonating another user or system | Attacker uses stolen credentials to log in as a legitimate user |
| **T** — Tampering | Modifying data or code without authorization | Attacker modifies a client's dashboard data in the database |
| **R** — Repudiation | Denying an action was taken | User claims they didn't delete data; no audit log to prove otherwise |
| **I** — Information Disclosure | Exposing data to unauthorized parties | S3 bucket misconfigured as public; client data exposed |
| **D** — Denial of Service | Making the system unavailable | DDoS attack on the BI platform disrupts client access |
| **E** — Elevation of Privilege | Gaining more access than authorized | Low-privilege user exploits a bug to gain admin access |

---

### System Data Flow Diagram

```
[Client Browser]
      |
      | HTTPS (TLS 1.3)
      ↓
[CloudFront CDN / WAF]
      |
      ↓
[Application Load Balancer]
      |
      ↓
[ECS/EKS — Web App Containers]  ←→  [Auth0 (Client Auth)]
      |                                    |
      ↓                                    ↓
[API Gateway]                    [Okta (Internal Staff Auth)]
      |
      ↓
[Data Ingestion Pipeline]  ←→  [Client Source Systems (ETL)]
      |
      ↓
[Analytics Engine (Lambda/ECS)]
      |
      ↓
[RDS (PostgreSQL)] ←→ [S3 (Client Data Buckets)]
      |
      ↓
[Admin Portal]  ←→  [CloudWatch / Datadog (Monitoring)]
      |
      ↓
[GitHub Actions (CI/CD)] → [ECR (Container Registry)] → [ECS Deploy]
```

---

### STRIDE Threat Analysis

#### Component: Web Application (Client-Facing BI Platform)

| STRIDE | Threat | Likelihood | Impact | Risk | Mitigating Controls |
|--------|--------|-----------|--------|------|---------------------|
| **S** | Attacker uses stolen Auth0 credentials to access another client's data | 4 | 5 | 🔴 20 | MFA enforcement, session timeout, anomalous login detection |
| **S** | Session token stolen via XSS and used to hijack session | 3 | 4 | 🟠 12 | HttpOnly/Secure cookies, Content Security Policy, XSS filtering |
| **T** | Client modifies API request to alter another tenant's data (tenant isolation bypass) | 3 | 5 | 🔴 15 | Tenant ID validation on every API call, row-level security in RDS |
| **T** | Attacker intercepts and modifies data in transit | 2 | 4 | 🟡 8 | TLS 1.2+ enforced; HSTS enabled |
| **R** | User denies making a change to shared dashboard | 2 | 3 | 🟡 6 | Audit logging of all data modification events |
| **I** | Verbose error messages expose stack traces with internal paths | 3 | 3 | 🟡 9 | Generic error messages in production; detailed logs server-side only |
| **I** | Multi-tenant data leak — tenant A queries tenant B's data | 3 | 5 | 🔴 15 | Strict tenant isolation; RLS policies; penetration test specifically for this |
| **D** | DDoS attack takes down platform during client business hours | 3 | 4 | 🟠 12 | CloudFront + WAF rate limiting; AWS Shield Standard |
| **E** | Low-privilege user manipulates API to access admin endpoints | 3 | 5 | 🔴 15 | Authorization checks on every endpoint; principle of least privilege |

**Highest-risk web app threat: Tenant isolation bypass (T, I, E) — requires dedicated pen test focus.**

---

#### Component: AWS Infrastructure

| STRIDE | Threat | Likelihood | Impact | Risk | Mitigating Controls |
|--------|--------|-----------|--------|------|---------------------|
| **S** | Attacker uses compromised IAM access key to assume AWS role | 4 | 5 | 🔴 20 | No long-lived IAM keys; use IAM roles; GuardDuty anomaly detection |
| **S** | Attacker spoofs CloudWatch alerts to trigger false incident response | 2 | 3 | 🟡 6 | Alert integrity via CloudTrail; SNS signed notifications |
| **T** | Attacker modifies S3 bucket policy to exfiltrate client data | 3 | 5 | 🔴 15 | S3 Block Public Access; SCPs preventing policy changes; S3 Object Lock |
| **T** | Attacker tampers with CloudTrail logs to cover tracks | 2 | 4 | 🟡 8 | CloudTrail log file validation enabled; logs written to separate, locked account |
| **R** | Admin claims they didn't delete an S3 bucket; no logging to prove it | 2 | 3 | 🟡 6 | CloudTrail enabled in all regions; CloudWatch Events on bucket deletion |
| **I** | S3 bucket misconfigured as public; client data exposed | 3 | 5 | 🔴 15 | AWS Config rule: s3-bucket-public-read-prohibited; S3 Block Public Access |
| **I** | RDS snapshot shared publicly by mistake | 2 | 5 | 🟠 10 | SCP denying public snapshots; AWS Config rule |
| **D** | Attacker spins up thousands of EC2 instances (resource exhaustion) | 2 | 3 | 🟡 6 | AWS Service Quotas; billing alerts; GuardDuty CryptoCurrency threat detection |
| **E** | Overly permissive IAM role allows privilege escalation via sts:AssumeRole | 4 | 5 | 🔴 20 | IAM Access Analyzer; least-privilege policies; no wildcard permissions |

**Highest-risk AWS threat: IAM privilege escalation and S3 exposure — validate with IAM Access Analyzer and config audit.**

---

#### Component: CI/CD Pipeline (GitHub Actions → ECR → ECS)

| STRIDE | Threat | Likelihood | Impact | Risk | Mitigating Controls |
|--------|--------|-----------|--------|------|---------------------|
| **S** | Attacker compromises a developer's GitHub account to push malicious code | 3 | 5 | 🔴 15 | GitHub MFA enforcement; branch protection requiring PR reviews |
| **T** | Malicious dependency injected via compromised third-party package (supply chain) | 3 | 5 | 🔴 15 | Dependabot; SBOM generation; pin dependency versions |
| **T** | Attacker modifies GitHub Actions workflow file to exfiltrate secrets | 3 | 5 | 🔴 15 | Protect .github/workflows; require code owner review for workflow changes |
| **I** | Secret/API key accidentally committed to GitHub repo | 4 | 4 | 🟠 16 | GitHub secret scanning; Gitleaks pre-commit hook; no hardcoded secrets |
| **I** | GitHub Actions logs expose environment variables or secrets | 3 | 4 | 🟠 12 | Mask secrets in Actions; never echo secrets in run steps |
| **E** | Compromised GitHub Actions runner gains AWS credentials via OIDC misconfiguration | 3 | 5 | 🔴 15 | Scope OIDC trust policy tightly; limit to specific repos and branches |

**Highest-risk CI/CD threat: Supply chain attack and secrets exposure — requires SBOM and secrets scanning controls.**

---

#### Component: Data Ingestion Pipeline (ETL from Client Systems)

| STRIDE | Threat | Likelihood | Impact | Risk | Mitigating Controls |
|--------|--------|-----------|--------|------|---------------------|
| **S** | Attacker impersonates a client's data source to inject malicious data | 2 | 4 | 🟡 8 | Mutual TLS for ETL connectors; API key rotation |
| **T** | Client data tampered with in transit between source and CloudPulse | 2 | 4 | 🟡 8 | TLS in transit; data integrity checksums |
| **T** | SQL injection via malformed client data payload into processing pipeline | 3 | 4 | 🟠 12 | Input validation and parameterized queries in pipeline code |
| **I** | ETL error logs contain PII from client data | 3 | 3 | 🟡 9 | PII scrubbing in log pipeline; structured logging with field masking |
| **D** | Client sends malformed large payload causing pipeline to crash | 2 | 3 | 🟡 6 | Payload size limits; rate limiting on ingestion API |

---

## Part 2: Vulnerability Assessment

### Assessment Approach

The vulnerability assessment was conducted using:
- **Tenable.io** — credentialed network and cloud scans
- **AWS Inspector v2** — automated EC2 and container image scanning
- **OWASP ZAP** — web application DAST scanning
- **Prowler** — AWS security best practice assessment (open source)
- **Trivy** — container image vulnerability scanning
- **Gitleaks** — secrets scanning across GitHub repositories

---

### Findings — Critical & High

#### VULN-001 — IAM User with Long-Lived Access Keys and Admin Permissions

| Field | Detail |
|-------|--------|
| **Severity** | 🔴 Critical |
| **CVSS Score** | 9.8 |
| **Tool** | Prowler |
| **Asset** | AWS IAM — account: cloudpulse-prod |
| **Finding** | IAM user `deploy-bot` has AdministratorAccess policy attached and a long-lived access key (created 387 days ago, never rotated) |
| **Risk** | If this key is compromised, an attacker has full AWS account access — can read all S3 data, create/destroy resources, exfiltrate everything |
| **Exploitation** | Keys exposed in GitHub repo, Slack, or phishing → attacker runs `aws s3 cp s3://client-data . --recursive` |
| **Remediation** | Replace long-lived key with IAM role + OIDC for CI/CD; remove AdministratorAccess; apply least-privilege policy |
| **SLA** | 24 hours |
| **Status** | 🔴 Open |

---

#### VULN-002 — Multi-Tenant Data Isolation Bypass via IDOR

| Field | Detail |
|-------|--------|
| **Severity** | 🔴 Critical |
| **CVSS Score** | 9.1 |
| **Tool** | Manual pen test (OWASP Testing Guide — IDOR) |
| **Asset** | Web application — `/api/v2/dashboards/{dashboard_id}` |
| **Finding** | The dashboard API endpoint accepts a `dashboard_id` parameter but does not validate that the requesting user's tenant matches the dashboard's tenant. A user from Tenant A can access Tenant B's dashboards by incrementing the dashboard ID. |
| **Risk** | Complete breach of client data isolation — any client can read any other client's business data |
| **Exploitation** | Authenticated user sends `GET /api/v2/dashboards/1001` → receives another tenant's dashboard data |
| **Remediation** | Add server-side tenant ID validation on every API endpoint: `assert dashboard.tenant_id == current_user.tenant_id`; implement row-level security (RLS) in RDS |
| **SLA** | 24 hours — **stop the observation period if not fixed** |
| **Status** | 🔴 Open — Priority 1 |

---

#### VULN-003 — RDS PostgreSQL Instance Not Encrypted at Rest

| Field | Detail |
|-------|--------|
| **Severity** | 🔴 Critical |
| **CVSS Score** | 9.0 |
| **Tool** | Prowler + AWS Config |
| **Asset** | RDS instance: `cloudpulse-analytics-prod-db-02` (us-east-1) |
| **Finding** | One of three production RDS instances does not have encryption at rest enabled. This instance stores processed analytics output for 12 client tenants. |
| **Risk** | If AWS physical media is compromised or RDS snapshot is shared accidentally, client data is readable in plaintext |
| **Remediation** | Create encrypted snapshot of instance → restore to new encrypted RDS instance → update connection strings → terminate unencrypted instance. Requires maintenance window. |
| **SLA** | 7 days (requires planned maintenance) |
| **Status** | 🟠 In Remediation |

---

#### VULN-004 — Hardcoded AWS Secret Key in GitHub Repository

| Field | Detail |
|-------|--------|
| **Severity** | 🔴 Critical |
| **CVSS Score** | 9.8 |
| **Tool** | Gitleaks |
| **Asset** | GitHub repo: `cloudpulse/data-pipeline` — commit `a3f92c1` (11 months ago) |
| **Finding** | AWS secret access key for IAM user `pipeline-service` committed in plaintext in `.env.example` file. Key has not been rotated since commit. |
| **Risk** | Key is likely indexed by tools that scan GitHub for secrets (e.g., TroveHog, GitGuardian). Attacker may already have access. |
| **Remediation** | Immediately rotate the key; treat as compromised — check CloudTrail for unauthorized usage in the last 11 months; remove from git history using `git filter-repo`; enable GitHub secret scanning going forward |
| **SLA** | Immediate — treat as active incident |
| **Status** | 🔴 Open — Incident declared |

---

#### VULN-005 — Missing Content Security Policy (CSP) Headers

| Field | Detail |
|-------|--------|
| **Severity** | 🟠 High |
| **CVSS Score** | 7.4 |
| **Tool** | OWASP ZAP + manual review |
| **Asset** | Web application — all pages |
| **Finding** | The application does not set a Content-Security-Policy header. This allows execution of inline scripts and loading of resources from arbitrary domains, enabling Cross-Site Scripting (XSS) attacks. |
| **Risk** | XSS → session token theft → account takeover without needing credentials |
| **Remediation** | Implement CSP header: `Content-Security-Policy: default-src 'self'; script-src 'self' [approved CDNs]; object-src 'none'`. Start with report-only mode, then enforce. |
| **SLA** | 7 days |
| **Status** | 🟠 Open |

---

#### VULN-006 — GitHub Actions Workflow Allows Arbitrary Code Execution via Pull Request

| Field | Detail |
|-------|--------|
| **Severity** | 🟠 High |
| **CVSS Score** | 8.1 |
| **Tool** | Manual GitHub Actions review |
| **Asset** | GitHub Actions workflow: `ci.yml` |
| **Finding** | The CI workflow uses `pull_request_target` trigger with `actions/checkout@v3` checking out the PR branch code. This allows an external contributor's PR to execute arbitrary code within the workflow, which has access to repository secrets. |
| **Risk** | Malicious contributor submits a PR that exfiltrates `AWS_SECRET_ACCESS_KEY` and other secrets from the Actions environment |
| **Remediation** | Replace `pull_request_target` with `pull_request` for untrusted code; add `if: github.event.pull_request.head.repo.full_name == github.repository` condition; restrict secret access to protected branches only |
| **SLA** | 7 days |
| **Status** | 🟠 Open |

---

#### VULN-007 — Auth0 Allows Password-Only Login (No MFA Enforcement for Client Users)

| Field | Detail |
|-------|--------|
| **Severity** | 🟠 High |
| **CVSS Score** | 7.5 |
| **Tool** | Auth0 configuration review |
| **Asset** | Auth0 tenant: `cloudpulse-prod` |
| **Finding** | Client user authentication via Auth0 does not enforce MFA. MFA is optional — only 23% of client users have enrolled. |
| **Risk** | Credential stuffing or phishing of a client user's password → full access to that client's BI data |
| **Remediation** | Enable MFA enforcement in Auth0 → Actions → Require MFA; configure adaptive MFA (trigger on suspicious login signals); communicate to clients with 30-day notice |
| **SLA** | 30 days (requires client communication) |
| **Status** | 🟠 In Planning |

---

### Findings — Medium

| ID | Finding | CVSS | Asset | Remediation |
|----|---------|------|-------|-------------|
| VULN-008 | S3 access logging not enabled on 4 of 11 buckets | 5.3 | S3 | Enable S3 server access logging → centralized log bucket |
| VULN-009 | CloudTrail not enabled in eu-west-1 region | 5.3 | AWS | Enable CloudTrail in all regions; use multi-region trail |
| VULN-010 | ECS task definitions using `privileged: true` | 6.5 | ECS | Remove privileged flag unless explicitly required |
| VULN-011 | Security group allows inbound 0.0.0.0/0 on port 22 (SSH) | 6.5 | EC2 | Restrict SSH to VPN/bastion IP range only; prefer SSM Session Manager |
| VULN-012 | Container images using `latest` tag | 5.0 | ECR/ECS | Pin to specific image digest; update Dependabot to track |
| VULN-013 | JWT tokens have no expiry set for API sessions | 5.4 | Web App | Set JWT exp claim; implement refresh token rotation |
| VULN-014 | Verbose stack traces returned to API clients on 500 errors | 5.3 | Web App | Implement generic error handler; log details server-side only |
| VULN-015 | No SBOM generated for production container images | 5.0 | CI/CD | Add `syft` or `trivy sbom` step to GitHub Actions pipeline |

---

## Part 3: Penetration Test Coordination

### Scope of Work — External Pen Test

CloudPulse engaged **SecureStrike Consulting** to conduct an external black-box + gray-box penetration test.

```
Test type: Black-box (external) + Gray-box (authenticated)
Duration: 2 weeks
Start date: Month 5, Week 3
End date: Month 5, Week 4 (report Month 6, Week 1)

Authorized targets:
  - https://app.cloudpulse.io (production — read-only testing)
  - https://staging.cloudpulse.io (full testing authorized)
  - AWS account: 123456789012 (non-destructive only)
  - GitHub org: cloudpulse-analytics (review only — no code changes)

Out of scope:
  - Social engineering of CloudPulse employees
  - Physical access testing
  - Denial of service attacks against production
  - Client systems or data
  - Any third-party infrastructure

Rules of engagement:
  - No automated scanning against production without prior approval
  - Halt testing immediately if a critical vulnerability is found; notify GRC Analyst
  - All findings treated as confidential; pen test firm signs NDA
  - CloudPulse retains all evidence and reports

Emergency contact:
  GRC Analyst: [email + phone]
  CISO: [email + phone]
  Available during test window: 09:00–18:00 EST
```

### Pre-Engagement Checklist

```
3 weeks before:
  [ ] Statement of Work (SoW) signed
  [ ] NDA signed by pen test firm
  [ ] Rules of Engagement document signed
  [ ] Test accounts provisioned (gray-box: 2 test tenants, 1 admin)
  [ ] Staging environment confirmed as production-equivalent
  [ ] CloudPulse WAF rules set to "detect" mode (not block) for test IPs
  [ ] IT Manager briefed — pen test traffic is expected; do not block

1 week before:
  [ ] Kick-off call with pen test team
  [ ] Share architecture diagram and system description
  [ ] Confirm emergency contact availability
  [ ] Confirm test IPs to whitelist (if any)
  [ ] Enable enhanced logging for test period

Day of test start:
  [ ] Confirm test team has access to test accounts
  [ ] GRC Analyst and IT Manager monitoring logs
  [ ] Incident response team on standby (not activated — just aware)
```

### Pen Test Findings Integration

```
When pen test report arrives (Month 6, Week 1):

1. Review all findings with IT Manager and CISO within 48 hours

2. For each pen test finding:
   a. Cross-reference with internal vuln assessment
      - Already known? → Update existing finding with pen test validation
      - New finding? → Create new VULN entry

   b. Classify severity (use pen tester's CVSS + your risk context)

   c. Assign owner and set SLA

   d. Add to remediation plan

3. Critical findings: treat as incidents — activate remediation SLA immediately

4. Upload pen test report to:
   - Vanta → Controls → CC7.1, CC3.2 → Evidence
   - SOC 2 auditor portal
   - Internal evidence repository
```

---

## Part 4: Remediation Plan

### Priority Matrix

All findings ranked by Effective Risk Score (CVSS × asset criticality):

| ID | Finding | Severity | SLA | Owner | Status | Deadline |
|----|---------|----------|-----|-------|--------|----------|
| VULN-004 | Hardcoded AWS secret in GitHub | 🔴 Critical | Immediate | IT + Dev | 🚨 Incident | NOW |
| VULN-002 | Multi-tenant IDOR — tenant isolation bypass | 🔴 Critical | 24 hrs | Engineering | 🔴 Open | Month 5+1d |
| VULN-001 | IAM admin user with long-lived keys | 🔴 Critical | 24 hrs | IT Manager | 🔴 Open | Month 5+1d |
| VULN-003 | RDS not encrypted at rest | 🔴 Critical | 7 days | IT Manager | 🟠 In Remediation | Month 5+7d |
| VULN-006 | GitHub Actions arbitrary code execution | 🟠 High | 7 days | Engineering | 🟠 Open | Month 5+7d |
| VULN-005 | Missing CSP headers | 🟠 High | 7 days | Engineering | 🟠 Open | Month 5+7d |
| VULN-007 | Auth0 MFA not enforced | 🟠 High | 30 days | IT + Legal | 🟠 Planning | Month 6 |
| VULN-011 | SSH open to internet | 🟡 Medium | 30 days | IT Manager | ⏳ Planned | Month 6 |
| VULN-010 | ECS privileged containers | 🟡 Medium | 30 days | Engineering | ⏳ Planned | Month 6 |
| VULN-013 | JWT tokens no expiry | 🟡 Medium | 30 days | Engineering | ⏳ Planned | Month 6 |
| VULN-008 | S3 access logging disabled | 🟡 Medium | 30 days | IT Manager | ⏳ Planned | Month 6 |
| VULN-009 | CloudTrail not in eu-west-1 | 🟡 Medium | 30 days | IT Manager | ⏳ Planned | Month 6 |
| VULN-014 | Verbose error messages | 🟡 Medium | 30 days | Engineering | ⏳ Planned | Month 6 |
| VULN-012 | Container images use `latest` tag | 🟡 Medium | 30 days | Engineering | ⏳ Planned | Month 6 |
| VULN-015 | No SBOM generated | 🟡 Medium | 30 days | Engineering | ⏳ Planned | Month 6 |

---

### Remediation Verification Process

```
For each finding, after owner signals fix is complete:

1. GRC Analyst performs verification:
   - Critical/High: Re-run the specific test that found it
   - Medium: Spot-check configuration or re-run tool scan

2. For VULN-002 (tenant isolation):
   - Reproduce original test: logged in as Tenant A, attempt to access Tenant B dashboard IDs
   - Confirm: 403 Forbidden or empty response
   - Confirm: Audit log records the attempt

3. For VULN-004 (hardcoded secret):
   - Run Gitleaks across full git history: `gitleaks detect --source . --log-opts HEAD`
   - Confirm: No secrets found
   - Confirm: New secret in AWS Secrets Manager
   - Confirm: CloudTrail shows no unauthorized usage of old key

4. Update vulnerability tracker:
   - Status → Resolved
   - Resolution date logged
   - Evidence of fix uploaded to Vanta

5. Inform CISO when all Critical/High findings are resolved
```

---

## Security Assessment Summary

### Findings Overview

| Severity | Count | Resolved | Open |
|----------|-------|----------|------|
| 🔴 Critical | 4 | 0 | 4 |
| 🟠 High | 3 | 0 | 3 |
| 🟡 Medium | 8 | 0 | 8 |
| 🟢 Low | 0 | — | — |
| **Total** | **15** | **0** | **15** |

### Risk Posture Assessment

**Overall rating: 🔴 High Risk — not suitable for SOC 2 audit until Critical findings resolved**

The assessment identified two findings (VULN-002 and VULN-004) that represent immediate, material risks to client data:

- VULN-002 (tenant isolation bypass) means any authenticated CloudPulse user can access any other client's data right now. This would be a catastrophic breach and an automatic SOC 2 audit failure.
- VULN-004 (hardcoded AWS key) must be treated as an active incident — the key has been in a public/shared repository for 11 months and may already be exploited.

**Recommendation: Pause the SOC 2 audit observation window until VULN-001, VULN-002, and VULN-004 are fully resolved and verified.**

### Positive Security Findings

- TLS 1.3 enforced on all client-facing endpoints ✅
- MFA enforced for all internal staff via Okta ✅
- GuardDuty enabled and configured ✅
- EDR deployed on all endpoints ✅
- CloudTrail enabled in us-east-1 ✅
- WAF deployed in front of application ✅
- Incident response plan exists (untested) ✅
- Dependency scanning via Dependabot active ✅

---

## SOC 2 Evidence Produced by This Assessment

| Evidence | Control | Where to Upload |
|----------|---------|----------------|
| Threat model document | CC3.2, CC3.4 | Vanta → CC3.2 → Evidence |
| Vulnerability scan reports (Tenable, Prowler, ZAP) | CC7.1 | Vanta → CC7.1 → Evidence |
| Pen test report (SecureStrike) | CC7.1, CC3.2 | Vanta → CC7.1 + CC3.2 |
| Remediation tracking log | CC7.4, CC4.2 | Vanta → CC4.2 → Evidence |
| Verification scan reports | CC7.1 | Vanta → CC7.1 → Evidence |
| VULN-004 incident record | CC7.4 | Vanta → CC7.4 → Evidence |

---

## Tools Used in This Assessment

| Tool | Purpose | Cost |
|------|---------|------|
| Tenable.io | Vuln scanning — network + cloud | Paid (free trial: tenable.com/products/nessus/nessus-essentials) |
| AWS Inspector v2 | EC2 + container image scanning | Pay-per-use (built into AWS) |
| Prowler | AWS security posture assessment | Free / open source (prowler.pro) |
| OWASP ZAP | Web app DAST scanning | Free / open source (zaproxy.org) |
| Trivy | Container image scanning | Free / open source (aquasecurity.github.io/trivy) |
| Gitleaks | Secrets scanning in git repos | Free / open source (gitleaks.io) |
| Burp Suite Community | Manual web app testing | Free (professional: ~$449/yr) |
| IAM Access Analyzer | AWS privilege escalation analysis | Free (built into AWS) |
