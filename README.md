# TECHNICAL DUE DILIGENCE REPORT

Need a Technical Due Diligence report? [Book a free no-commitment chat today.](https://bogatell.io?utm_source=github)

**Target Asset:** Project Apex (SaaS - Field Service Management)  
**Date:** December 18, 2025

1. Executive Summary
2. Codebase Quality & Architecture
3. IP & Licensing Fortress
4. Bus Factor & Team
5. Infrastructure, Security & Scalability
6. Data Integrity & Analytics
7. Integration Readiness
8. Remediation Budget

---

### 1. Executive Summary
**Overall Risk Rating:** 🟡 **YELLOW** (Remediation Required)

The platform is built on a standard, hireable tech stack (Python/Django & React) and is capable of supporting the buyer’s 24-month growth plan. However, we identified specific risks regarding Intellectual Property ownership and key-person dependency that must be addressed prior to closing.

**Primary Deal Risks:**
* **IP Ownership:** A critical PDF generation library is licensed under GPL v3. This requires immediate replacement to avoid "copyleft" legal exposure.
* **Founder Dependency:** The core scheduling algorithm is undocumented and deployment keys reside solely on the CTO's local machine.
* **Data Integrity:** Marketing attribution logic is flawed, leading to a 15% discrepancy between reported leads and actual database records.

**Recommendation:** Proceed to close subject to the "Conditions Precedent" outlined in the Remediation Budget.

---

### 2. Codebase Quality & Architecture
**Objective:** Assess maintainability, technical debt, and rewrite risk.

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **Core Stack:** Python (Django 4.2), React, PostgreSQL. | **Low Risk.** These are industry-standard technologies. Recruiting new developers will be fast and affordable. | None required (Asset). |
| **Legacy Code:** "Invoicing Module" uses Python 2.7 syntax wrapped in compatibility layers. | **Medium Risk.** The billing system is fragile. Modifying pricing tiers will be expensive and prone to breaking. | Budget $15k to rewrite this module in Year 1. |
| **Test Coverage:** High backend coverage (85%), but zero frontend tests. | **Medium Risk.** New features will likely break the User Interface (UI), frustrating customers. | Implement basic automated browser testing (Cypress) post-close. |

**Tools & Methodology:**
* **SonarCloud:** Utilized to map "Cyclomatic Complexity." Identified 3 specific "God Classes" in the billing module that exceed maintainability thresholds.
* **Manual Review:** Spot-checked 5 critical pull requests to assess code review rigour.

---

### 3. IP & Licensing Fortress
**Objective:** Verify ownership and identify "poison pill" open-source licenses.

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **License Audit:** 98% of libraries are MIT / Apache 2.0. | **Low Risk.** These licenses allow you to sell the software for profit without restriction. | None required. |
| **Critical Flag:** `lib-gpl-report-gen` (PDF tool) is **GPL v3**. | **CRITICAL RISK.** GPL v3 is a "viral" license. Legally, you may be forced to open-source your entire proprietary code. | **Mandatory:** Swap for a commercial alternative (e.g., ReportLab) *before* signing. |

**Tools & Methodology:**
* **Snyk (Team Plan):** Automated deep scan of `requirements.txt` and `package.json`. Cross-referenced dependencies against the NVD (National Vulnerability Database).
* **FOSSA:** Verification scan to confirm license compatibility across the dependency tree.

---

### 4. Bus Factor & Team
**Objective:** Determine if the platform survives the founder's departure.

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **Tribal Knowledge:** "Schedule Engine" logic is undocumented. | **High Risk.** If the CTO leaves or gets sick, no one can fix bugs in the core product. | CTO must record a "Code Walkthrough" video series before exit. |
| **Security:** AWS Root keys shared via email; no MFA on Database. | **High Risk.** A disgruntled ex-employee or hacker could delete the entire business data. | Enable Multi-Factor Authentication (MFA) immediately. |
| **Deployment:** Manual release process from CTO’s laptop. | **Medium Risk.** The team cannot release updates/fixes without the CTO physically present. | Build an automated deployment pipeline (GitHub Actions). |

**Tools & Methodology:**
* **Git Analysis:** Reviewed commit logs to identify modules touched exclusively by a single contributor.
* **Stakeholder Interview:** Structured technical interview with the CTO to map "knowledge silos."

---

### 5. Infrastructure, Security & Scalability
**Objective:** Verify costs, security posture, and ability to handle 10x growth.

**Visual Architecture Map:**
> *(Figure 1: Current AWS Architecture auto-generated via Cloudcraft live-scan)*

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **Architecture:** Cloud-native (AWS) with async queues (Celery). | **Low Risk.** The system successfully handled 5x peak load. It will support your growth plan. | None required (Asset). |
| **Storage:** DB logs growing linearly; no retention policy. | **Financial Risk.** Hosting costs will double in 12 months if waste is not cleaned up. | Configure auto-deletion for logs older than 90 days. |
| **PII Data:** Customer addresses stored in plain text. | **Legal Risk.** Violation of GDPR. A data breach would result in maximum fines. | Encrypt the database "at rest" immediately. |

**Tools & Methodology:**
* **Cloudcraft:** Live-scan of AWS environment to generate the architecture diagram above and inventory all active resources.
* **Prowler:** Audited AWS account against CIS Benchmarks. Flagged 3 critical failures regarding S3 bucket permissions and Root User MFA.
* **AWS Trusted Advisor:** Checked for idle resources and service limit warnings.

---

### 6. Data Integrity & Analytics
**Objective:** Validate that the metrics in the Investment Deck are technically accurate.

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **Revenue Match:** Stripe webhooks match Database exactly. | **Verified.** The financial history in the CIM is accurate and trustworthy. | None required. |
| **Bot Traffic:** ~8% of visitors are AWS Data Center bots. | **Commercial Insight.** Top-of-funnel marketing traffic is slightly inflated. | Adjust marketing conversion models to exclude this traffic. |
| **Tracking Error:** GTM triggers on "Click" not "Success". | **Metric Inflation.** Lead volume is overstated by ~15% (errors count as leads). | Fix Google Tag Manager triggers to fire only on form confirmation. |

**Tools & Methodology:**
* **Google Tag Assistant:** Verified the firing triggers for key conversion events.
* **Segment Inspector:** Audited the raw JSON payload of events to ensure consistent user identification across marketing and product tools.
* **SQL Analysis:** Direct queries on the PostgreSQL replica to compare raw row counts against dashboard KPIs.

---

### 7. Integration Readiness
**Objective:** Assess the difficulty of merging this asset with the Buyer’s existing tech stack.

| Technical Finding | Business Significance | Remedy |
| :--- | :--- | :--- |
| **API Limits:** REST API is "Read-Only." | **Operational Friction.** You cannot automatically push leads from your CRM into this product. | Engineer must build "Write" endpoints (approx. 2 weeks work). |
| **No Webhooks:** System cannot notify external tools of updates. | **Latency.** Syncing data will be slow and inefficient (polling vs real-time). | Build a webhook system post-close. |
| **Data Export:** No automated ETL pipeline. | **Blind Spots.** You cannot easily pull historical data into your corporate Data Warehouse. | Write custom SQL scripts to migrate history one-time. |

**Tools & Methodology:**
* **Postman:** Tested API endpoints for response structure and latency.
* **SchemaSpy:** Generated a visual diagram of the database schema to assess complexity for migration.

---

### 8. Remediation Budget
The following costs should be factored into the final purchase price or set aside as a post-close working capital requirement.

| Severity | Issue | Remediation Action | Est. Cost | Timeline |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | **IP Violation (GPL)** | Replace PDF library | $2,500 | Pre-Close |
| **Critical** | **Security Gap** | Encrypt PII & enable MFA | $1,500 | Days 1-7 |
| **High** | **Deployment Risk** | Implement CI/CD pipeline | $5,000 | Days 1-30 |
| **Medium** | **Tracking Error** | Fix GTM triggers | $1,000 | Days 30-60 |
| **Medium** | **Integration** | Build Write-API endpoints | $8,000 | Days 30-90 |
| | | **TOTAL TECH DEBT** | **~$18,000** | |

***

Need a Technical Due Diligence report? [Book a free no-commitment chat today.](https://bogatell.io?utm_source=github)
