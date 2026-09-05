# 🛡️ VulnOps Automation Suite (Vuln-Pilot)
### *Next-Generation Vulnerability Ingestion, Intelligence & Automated Remediation Framework*

---

## 🌟 The Origin Story: The Genesis of VulnOps Automation

In enterprise security operations, Infrastructure Vulnerability Management (IVM) teams face an overwhelming weekly operational hurdle: **fragmented scan data, massive spreadsheets, disparate cloud inventories, and manual correlation bottlenecks.**

```
       [ MANUAL ENTERPRISE CHALLENGES ]
  ┌────────────────────────────────────────┐
  │  Qualys Server Raw Report (100k+ rows) │
  │  Qualys Network Raw Report (+Tags)     │──┐
  │  AWS & Azure Multi-Cloud Inventories   │  │
  │  Complex CMDB Mapping (IP/Code/Host)   │  ├─► Manual Excel Chaos (Hours lost)
  │  Lost Exception Approvals & Dates      │  │   VLOOKUP Failures & Formula Lag
  │  Human Error in SLA & Asset Tracking   │  │   Delayed Remediation & Escalation
  └────────────────────────────────────────┘──┘
```

### The Problem Statement
1. **Dual Report Silos**: Raw vulnerability exports are split across **Server** reports (system vulnerabilities) and **Network** reports (network findings with `Associated Tags`). Merging them manually without losing tags was error-prone and caused Excel memory crashes.
2. **The Cloud Disconnect**: Cloud assets frequently change state (`stopped`, `deallocated`). Standard reporting often dropped non-running assets, causing visibility blind spots for compliance reporting like IASP.
3. **Correlation Bottlenecks**: Mapping findings to Application Owners, APM IDs, and IF/PCI classifications via CMDB required multi-pass matching (IP address, 5-digit account correlation codes, and hostnames).
4. **Exception Handling Gaps**: Approved risk exceptions lacked pre-processing, causing accepted vulnerabilities to be erroneously escalated as past-due SLAs.
5. **Operational Fatigue**: Crafting individual follow-up emails for dozens of application owners took hours every week.

### The Innovation: Building the VulnOps 3-Tool Ecosystem
To resolve these challenges once and for all, this automation suite was architected as a **100% client-side, privacy-first, zero-infrastructure vulnerability operations ecosystem** comprising three interconnected platforms designed to execute in complete harmony.

---

## 🏗️ The 3 Core Platforms & Their Enterprise Usage

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│                            VULNOPS AUTOMATION SUITE                              │
├──────────────────────────┬──────────────────────────┬────────────────────────────┤
│   VulnOps Reporting      │    SecureMetrics Hub     │      Mail Automation       │
│         Engine           │                          │                            │
│  ──────────────────────  │  ──────────────────────  │  ────────────────────────  │
│  • Dual Raw Ingestion    │  • Executive KPI Matrix  │  • SLA Threshold Escalator │
│  • Sev 1 & 2 Auto-Filter │  • TruRisk / QDS Engine  │  • Dynamic Email Templates │
│  • 3-Tier CMDB Engine    │  • Weekly Trend Deltas   │  • IST Timezone Precision  │
│  • 54-Col IASP / PowerBI │  • Age Distribution      │  • Batch Follow-up Engine  │
└──────────────────────────┴──────────────────────────┴────────────────────────────┘
```

### 1. ⚙️ VulnOps Reporting Engine (`VulnOps_Reporting_Engine.html`)
*The Core Ingestion, Normalization & Correlation Engine*
- **Dual Raw Ingestion (Server + Network)**: Ingests both Qualys Server and Network raw exports, concatenates datasets seamlessly, and preserves `Associated Tags` and `Associated Malware`.
- **Automated Severity Filtering**: Automatically strips out low-risk noise (Severity 1 & 2), focusing remediation solely on actionable risk (Severities 3, 4, and 5).
- **Multi-Cloud Asset State Retention**: Retains and matches all AWS (EC2/VPC) and Azure (VM/Subscriptions) assets, ensuring stopped and deallocated machines remain properly mapped for IASP compliance.
- **3-Tier Fallback CMDB Matcher**:
  1. *Priority 1*: Direct IP Address match.
  2. *Priority 2*: 5-digit cloud account/subscription correlation code extraction.
  3. *Priority 3*: Hostname / NetBIOS fallback.
- **Exception Approval Pre-Processor**: Configures APM ID and vulnerability acceptance rules before generation, auto-stamping `Exception Approved` status with `Exception Start Date` and `Exception End Date`.
- **Dual-Mode Output Packages**:
  - **IASP Outcome Report**: Exact 54-column compliance format ready for direct portal ingestion.
  - **PowerBI Relational Model**: Star-schema workbook (`Fact_Vulnerabilities`, `Dim_Applications`, `Dim_Cloud_Assets`, `Measures_SLA_Summary`, `Fact_Exceptions`).

### 2. 📊 SecureMetrics Hub (`SecureMetrics_Hub.html`)
*The Executive Security Telemetry & SLA Analytics Portal*
- **Executive Security Dashboard**: High-level visual telemetry over total vulnerability volume, remediated items, and SLA breach rates.
- **Asset Criticality & Compliance**: Segmented risk distribution across **IF (Internet Facing)**, **PCI (Payment Card Industry)**, and internal assets.
- **Vulnerability Aging Spectrum**: Deep breakdown of vulnerability age buckets (`0-7d`, `8-30d`, `31-60d`, `61-90d`, `90d+`) to track aging technical debt.
- **Week-over-Week Trend Tracker**: Delta comparison evaluating new findings vs. remediated/closed findings.

### 3. 📬 Mail Automation (`Mail_Automation.html`)
*The Automated SLA Remediation & Application Owner Escalation Engine*
- **Automated Follow-Up Generation**: Automatically clusters findings by Application Owner and APM ID to draft personalized, professional remediation emails.
- **SLA Breach Threshold Indicators**: Highlights Critical and Past-Due SLA findings with urgency tags.
- **IST Timezone Localization**: All timestamps and follow-up schedules are stamped in Indian Standard Time (IST) for synchronized operations.
- **Interactive Template Customization**: Allows security analysts to tweak templates, insert custom action items, and preview live email drafts before dispatching.

---

## 🎯 The S.P.E.C.T.R.A. Framework Alignment

This suite was architected around the enterprise **SPECTRA** lifecycle model to guarantee end-to-end vulnerability governance:

| Letter | SPECTRA Phase | Enterprise Automation Capability |
| :---: | :--- | :--- |
| **S** | **Scan & Ingest** | Ingests disparate scanner reports (Server & Network raw Qualys reports) with automated column alias resolution. |
| **P** | **Prioritize & Filter** | Filters out Severity 1 & 2 noise; classifies risk tiers (5 - Critical, 4 - High, 3 - Medium) and TruRisk scores. |
| **E** | **Evaluate & Except** | Pre-processes formalized risk exception approvals with validity date ranges (`Exception Start/End Dates`). |
| **C** | **Correlate & Enrich** | Multi-pass CMDB correlation (IP $\rightarrow$ 5-digit code $\rightarrow$ Hostname) and AWS/Azure cloud asset tagging. |
| **T** | **Track & SLA Matrix** | Computes precise SLA deadlines based on asset exposure (IF, PCI, Internal) and vulnerability age. |
| **R** | **Remediate & Escalate** | Generates automated, formatted email communications with target remediation tables for App Owners. |
| **A** | **Audit & Export** | Maintains local browser audit trails, week-over-week deltas, and dual export models (54-col IASP & PowerBI Star Schema). |

---

## 🚀 Quick Start Guide

### 1. Local Execution (Zero-Install)
All tools run completely in modern web browsers (Chrome, Edge, Safari, Firefox) with no backend server or Node.js runtime required.

```bash
# Clone the repository
git clone https://github.com/buildxtechs/Vuln-Pilot.git

# Navigate to the folder
cd Vuln-Pilot

# Open the central suite portal
open index.html   # On macOS
# or start on Windows: start index.html
```

### 2. Recommended Operational Workflow
1. Open **`index.html`** and launch the **VulnOps Reporting Engine**.
2. Select your pipeline mode (**IASP** or **PowerBI**).
3. Upload raw reports in **Ingestion Hub**:
   - Qualys Server Raw Report & Qualys Network Raw Report
   - AWS Inventory & Azure Inventory
   - CMDB Asset Repository
   - Previous Week's Final Outcome *(Optional, for Week-over-Week Fixed tracking)*
4. Configure any active risk waivers in **Rule Engine & CMDB $\rightarrow$ Exception Approvals**.
5. Click **Generate Final Report** in **Process & Run**.
6. Export the processed workbook (`.xlsx`) or flat table (`.csv`) in **Export Packages**.
7. Switch to **Mail Automation** to dispatch automated remediation notifications to application owners.
8. Review metrics and executive trends in **SecureMetrics Hub**.

---

## 📋 IASP 54-Column Outcome Schema Specification

The IASP export package strictly adheres to the following 54 enterprise column headers:

```tsv
1. IP                     19. Date Last Fixed          37. ARS
2. DNS                    20. First Reopened           38. ACS
3. NetBIOS                21. Last Reopened            39. TruRisk Score
4. Tracking Method        22. Times Reopened           40. IF or PCI
5. OS                     23. CVE ID                   41. Scan Type
6. IP Status              24. Vendor Reference         42. APM ID
7. Unique Id              25. Bugtraq ID               43. SLA
8. Vulnerability Name     26. Threat                   44. App Owner
9. Vulnerability Status   27. Impact                   45. Organization
10. Type                  28. Recommendation           46. Exception Start Date
11. Risk Rating           29. Exploitability           47. Exception End Date
12. Port                  30. Associated Malware       48. IF
13. Protocol              31. Results                  49. PCI
14. FQDN                  32. PCI Vuln                 50. CSP
15. SSL                   33. Ticket State             51. Cloud Account Name
16. First Detected        34. Instance                 52. Environment
17. Last Detected         35. Category                 53. Impacted Asset
18. Times Detected        36. QDS                      54. Vulnerability Category
```

---

## 🔒 Security & Privacy by Design

- **100% In-Browser Computation**: Client-side JavaScript execution via Web Workers & SheetJS. No sensitive asset inventory or vulnerability data is ever sent to external cloud APIs or remote servers.
- **Encrypted Local Storage**: User preferences, rule configurations, and audit trail records remain confined to the local browser context.
- **Deterministic & Auditable**: Every row transformation, exception override, and CMDB link is logged with exact traceability.

---

### 👨‍💻 Engineering Credits
Developed and maintained by the **IVM Operations & Cyber Engineering Team**.
*Designed for enterprise scale, auditor compliance, and operational excellence.*
