# Business Continuity and Disaster Recovery Plan

## Northbridge Skills Institute: Flood and Power-Failure Scenario
[![Course](https://img.shields.io/badge/Course-GRC205-17365D)](#document-information)
[![Domain](https://img.shields.io/badge/Domain-BC%2FDR-8B1E3F)](#executive-summary)
[![NIST](https://img.shields.io/badge/NIST-SP%20800--34%20Rev.%201-2E7D32)](#references)
[![ISO](https://img.shields.io/badge/ISO-22301%3A2019-005A9C)](#references)
[![Status](https://img.shields.io/badge/Status-Academic%20Submission-6F42C1)](#document-information)

> An evidence-led business continuity and disaster recovery plan addressing a 72-hour site outage caused by flooding and power failure.

## Document Information

| Field | Detail |
|---|---|
| **Student Name** | Mohammed Nazir |
| **Student ID** | 2025/GRC/2512799 |
| **Institution** | International Cybersecurity and Digital Forensics Academy |
| **Course** | GRC205 — Incident Management and Business Continuity |
| **Assessment** | Business Continuity and Disaster Recovery Assignment |
| **Scenario** | Flood and power failure at Northbridge Skills Institute |
| **Submission date** | 23 October 2026 |

## Repository Summary

This repository-ready document covers business impact analysis, recovery objectives, backup design, strategy selection, continuity procedures, a disaster recovery runbook, recovery scheduling, tabletop testing, governance, and performance measurement for five critical institutional functions.

### Key Findings

- Estimated no-recovery impact: **NGN 1,200,000 after eight hours** and **NGN 3,360,000 after 24 hours**.
- The warm-site schedule restores LMS assessment service at **11:45 WAT**, 45 minutes after the examination start.
- Recommended annual option: **Warm Site + Protected Backups + Training/Testing** at **NGN 2,100,000**, leaving **NGN 900,000** within budget.
- The option does not meet every RTO and RPO, requiring approved workarounds, risk treatment, or faster capability.

## Table of Contents

- [Executive Summary](#executive-summary)
- [Scope and Assumptions](#scope-and-assumptions)
- [Task 1 — Business Impact Analysis](#task-1--business-impact-analysis)
- [Task 2 — Recovery Objectives and Backup Design](#task-2--recovery-objectives-and-backup-design)
- [Task 3 — Recovery Strategy and Budget](#task-3--recovery-strategy-and-budget)
- [Task 4 — Coordinated BC/DR Plan](#task-4--coordinated-bcdr-plan)
- [Task 5 — Recovery Schedule and Tabletop](#task-5--recovery-schedule-and-tabletop)
- [Task 6 — Governance and Performance Measures](#task-6--governance-and-performance-measures)
- [Conclusion](#conclusion)
- [References](#references)

> [!IMPORTANT]
> This is an academic scenario, not a production continuity plan or a claim of ISO 22301 certification. Recovery objectives, supplier capability, checkpoint integrity, alternate-site capacity, restore duration, and residual risk require approval and operational testing.

---

## Executive Summary

At 08:00 WAT on Monday (Day 0), flooding and power failure make Northbridge Skills Institute’s main site and local systems unavailable for an estimated 72 hours. No cyberattack is confirmed. The institute has 1,800 learners, 90 staff, two disaster-recovery technicians, Microsoft 365 identity/email through mobile internet, and alternate facility with 25 workstations from 10:00. Of 120 learners due to sit an 11:00 examination, 40 require centre workstations and 80 can use their own devices.

The no-recovery cost estimate is NGN 1,200,000 for eight hours and NGN 3,360,000 for 24 hours, including the one-off NGN 120,000 examination rescheduling trigger. The modelled warm-site schedule restores LMS assessment service at 11:45 and all five functions by 12:45. A continuity workaround is therefore required before 11:00. The recommended annual option is Warm plus protected independent backups and training/testing at NGN 2,100,000. It fits the NGN 3,000,000 limit but does not meet every proposed RTO/RPO; residual risk must be accepted by leadership or mitigated through faster capabilities and continuity procedures.

## Scope and Assumptions

Functions are F1 teaching/assessment (LMS01, DB01), F2 fees/finance (FIN01, DB01), F3 admissions/registration (REG01, DB01), F4 payroll (HR01, DB01), and F5 records/certificates (FS01). F1–F4 depend on network, AUTH01, DB01 and their application; F5 depends on network, AUTH01 and FS01. All require available staff, secure access and communication. The assignment says the baseline checkpoint pass integrity check; the tabletop later challenges this assumption. A function is not recovered merely because a server starts: application, data, identity, security and business-owner checks must pass.

## Task 1 — Business Impact Analysis 

### 1.1 BIA

| **Function / owner** | **Users and resources** | **Impact / deadline** | **Minimum acceptable service** | **Priority** |
|----|----|----|----|----|
| F1 Teaching/assessment — Academic/Examinations Lead | 120 exam candidates; LMS01, DB01, network, AUTH01, exam content, accessible devices, invigilators, safe alternate room. | Exam 11:00; failure to provide acceptable assessment triggers NGN 120,000 one-off cost. Integrity and fairness matter. | Approved secure exam route, identity checks, invigilation, auditable submissions and accessibility support. | 1 immediate |
| F2 Fees/finance — Finance Manager | Finance staff, learners; FIN01, DB01, network, AUTH01, payment provider and transaction reports. | Fee confirmation due 16:00 Day 0; NGN 40,000/hour. | Restricted transaction register with provider reference, timestamp, amount, two-person review and no duplicate payment instructions. | 2 same day |
| F3 Admissions — Admissions Manager | Applicants; REG01, DB01, network, AUTH01, secure intake and staff. | Admissions close 18:00 Day 0; NGN 20,000/hour. | Timestamped intake queue, unique case ID, acknowledgement, privacy controls and later verified entry. | 3 before 18:00 |
| F4 Payroll — HR/Payroll Lead | 90 staff; HR01, DB01, network, AUTH01, approved payroll file and bank channel. | Bank submission due 12:00 Day 1; errors/duplicates can harm staff; NGN 10,000/hour. | Last approved payroll source, separation of preparation/approval, validated changes and duplicate checks. | 4 before bank deadline |
| F5 Records/certificates — Registrar/Records Manager | Learners, graduates, employers; FS01, network, AUTH01, permissions and protected records. | 48-hour internal service commitment; NGN 5,000/hour; integrity/confidentiality essential. | Verify requester; log request; issue only from verified records or explain delay. | 5 within 48h |

**People, premises, suppliers and information:** F1 needs safe facilities, sufficient invigilators, device/connectivity check and learner communication. F2 depend on provider report; F4 on the bank submission channel; all depend on trained staff and safe access. Facilities must confirm alternate-site power, network, accessibility, privacy and safe occupancy before use. The 25 workstations cannot seat all 40 centre-dependent candidates simultaneously.

### 1.2 Worked cost calculations

Hourly rates are treated as separate, non-overlapping incremental costs for the first 8 and 24 hours. Since the no-recovery assumption means acceptable assessment service is not available by 11:00, add the NGN 120,000 rescheduling cost once at both horizons.

| **Function** | **Rate/hour** | **8-hour calculation** | **8h cost** | **24-hour calculation** | **24h cost** |
|----|----|----|----|----|----|
| F1 | 60,000 | 60,000×8 + 120,000 | 600,000 | 60,000×24 + 120,000 | 1,560,000 |
| F2 | 40,000 | 40,000×8 | 320,000 | 40,000×24 | 960,000 |
| F3 | 20,000 | 20,000×8 | 160,000 | 20,000×24 | 480,000 |
| F4 | 10,000 | 10,000×8 | 80,000 | 10,000×24 | 240,000 |
| F5 | 5,000 | 5,000×8 | 40,000 | 5,000×24 | 120,000 |
| TOTAL | 135,000/hour | 1,080,000 + 120,000 | 1,200,000 | 3,240,000 + 120,000 | 3,360,000 |

**Limitations:** these are exercise estimates that assume linear cost and do not account for real revenue, overtime, restoration expense, penalties or duration-specific effects. They omit learner welfare, unfair assessment, reputation, confidentiality, data integrity and long-term trust. Financial impact is therefore only one part of business impact.

### 1.3 Priorities and dependencies

F1 come first because 11:00 is the earliest hard deadline. F2 and F3 follow because of 16:00 and 18:00 deadlines; F4 must be ready for the Day 1 noon bank deadline; F5 has a 48-hour commitment, with urgent requests escalated. Business priority differs from technical order: network → AUTH01 → security/backup checks → DB01 → dependent applications. FS01 can be restored after AUTH01 and security/backup check. Risk include DB01 being a single dependency for four functions; AUTH01 blocking authenticated access; two-technician capacity creating a queue; corrupt backups; and unverified alternate-site/provider capacity.

## Task 2 — Recovery Objectives and Backup Design

### 2.1 RTO, RPO and MTD

RTO is the target time to restore required service.

RPO is the maximum acceptable age of recoverable data.

MTD is the outer limit of tolerable disruption.

Declare recovery only after technical, security, data and business checks. MTD leaves a buffer beyond RTO for validation, communications and contingency decisions.

| **Function** | **Proposed RTO** | **Proposed RPO** | **Proposed MTD** | **Reason / caveat** |
|----|----|----|----|----|
| F1 | 1h acceptable assessment route; LMS technical target 4h | 15 min | 4h | Protects 11:00 start; warm technical schedule alone cannot meet service target. |
| F2 | 6h | 1h | 12h | Fee confirmation by 16:00; controlled manual records bridge outage. |
| F3 | 8h | 1h | 12h | Admissions close 18:00; timestamped intake queue. |
| F4 | 16h | 1h | 24h | Leaves buffer before Day 1 noon payroll deadline. |
| F5 | 24h | 4h | 48h | Align with 48-hour service commitment; integrity before speed. |

These are proposed commitments, not proven capabilities. F1’s one-hour objective mean an acceptable service route, not that LMS01 itself is technically restored within one hour.

### 2.2 Checkpoint ages and gaps

| **System** | **Latest checkpoint and dependency** | **Age at 08:00** | **Affected functions / comparison** |
|----|----|----|----|
| DB01 | B02 incremental at 07:00 Day 0; requires B01 full at 23:00 Day −1 plus every required incremental through 07:00. | 1 hour | F1–F4. F1 RPO 15 min misses by 45 min; F2–F4 1h targets are met only if the full chain is complete and validated. |
| AUTH01 | B03 snapshot at 00:00 Day 0. | 8 hours | All functions depend on local identity/configuration; 8h exceeds every proposed RPO. |
| FS01 | B04 full backup at 23:00 Day −1. | 9 hours | F5 RPO 4h misses by 5h; later changes cannot be assumed recoverable. |
| Disconnected full | 17:00 Day −3. | About 39 hours | Independent fallback candidate but too old for proposed RPOs; must be validated. |

Temporary payment-provider report, admissions intake forms and payroll approval can support reconciliation but do not prove every missing database transaction can be reconstructed. Never invent missing records. A missing/corrupt DB01 incremental invalidates the claimed 07:00 recovery point.

### 2.3 Backup design

1.  DB01: nightly full plus hourly incrementals; retain at least 35 days subject to approved records retention. Consider a daily differential if restore testing shows it reduces chain risk.

2.  AUTH01: daily snapshot/full export and additional versioned configuration/state exports after material changes; keep recovery credentials separate from production identity.

3.  FS01: daily full plus incrementals at least every four hours to target the proposed four-hour RPO, with permissions and version history preserved.

4.  Apply 3-2-1: production plus two backup copies, two media/storage types and one geographically separate copy. Add offline or immutable backup inaccessible to production administrators.

5.  Separate production and backup admin identities; use named accounts, least privilege, MFA, monitoring, dual control for destructive actions, encryption in transit/at rest and separately held recovery keys.

6.  Test monthly sample restore for critical system and quarterly integrated service recovery. Record checksum, chain completeness, access independence, elapsed time, transaction tests, permission and business-owner acceptance.

**Offsite storage alone does not prove recoverability**: access controls may be weak, keys unavailable, data corrupt or restore throughput inadequate. A live replica may copy ransomware or logical corruption. Use clean-room restore, integrity and malware checks, database consistency checks, sample transactions, permissions tests and business acceptance. Provider access independence and actual restore times remain unverified assumptions.

## Task 3 — Recovery strategy and budget 

| **Package** | **Base** | **Backup add-on** | **Training/tests** | **Annual total** | **Capability / trade-off** |
|----|----|----|----|----|----|
| Cold | 600,000 | 400,000 | 200,000 | 1,200,000 | 24–48h; up to 24h data loss; affordable but too slow for urgent deadlines. |
| Warm | 1,500,000 | 400,000 | 200,000 | 2,100,000 | 3–5h first critical service; 1–6h data-loss window; balanced cost but misses F1 one-hour service target and some RPOs. |
| Hot | 2,400,000 | 400,000 | 200,000 | 3,000,000 | About 1h; up to 15min data loss; at budget ceiling, no contingency and supplier claims need testing. |

**Calculation:**

**Cold** = 600,000 + 400,000 + 200,000 = NGN 1,200,000.

**Warm** = 1,500,000 + 400,000 + 200,000 = NGN 2,100,000.

**Hot** = 2,400,000 + 400,000 + 200,000 = NGN 3,000,000. All fit the cap; Hot uses all of it.

Recommend Warm plus protected backups and training/testing. Because it costs NGN 2.1m and leaves NGN 900,000 headroom, subject to procurement approval. It is materially faster than Cold and more affordable than Hot. It does not meet F1’s one-hour service target or every RPO; leadership must accept those risks explicitly or fund faster capability. A single-outage estimate cannot prove annual ROI because it excludes incident probability, outage distributions, multiple events, non-financial harm, implementation costs and control effectiveness. Before approval, demand witnessed restore tests, actual RTO/RPO evidence, backup access-independence proof, service-level commitments, support escalation, security evidence, data-export/exit terms and full pricing. Executive leadership accepts residual business risk; technical owners document the gaps.

## Task 4 — Coordinated BC/DR plan 

### 4.1 Activation and command

Activate when the site or critical service cannot operate safely, a deadline is threatened, or projected outage exceeds an RTO. The 08:00 site closure meets the threshold. Executive Sponsor/Principal is accountable for declaring a major event; Deputy Principal/Operations Director is deputy. BC/DR Coordinator manage the plan and log; Incident Commander direct priorities; DR Lead coordinate technicians; Facilities confirm site safety; business coordinators run temporary services. Unauthorised access, suspicious changes, malware or backup tampering triggers Security/Incident Response involvement.

Use M365 only while availability and trust are confirmed; mobile calls/SMS and a pre-agreed contact tree are alternatives. Keep an offline contact list/runbook. Issue situation reports every 30 minutes during the first four hours, recording impact, decisions, owners, risks, next actions and next update.

### 4.2 RACI

| **Activity** | **Responsible** | **Accountable** | **Consulted / informed** |
|----|----|----|----|
| Activate BC/DR | BC/DR Coordinator | Executive Sponsor | Facilities, business leads / all staff |
| Temporary assessment | Academic Coordinator | Academic Director | Security, learner support / learners |
| Validate backups | DR Lead | BC/DR Coordinator | Security, system owners / Executive Sponsor |
| Restore systems | DR Technicians | DR Lead | Security/IR, application owners / business leads |
| Approve manual business controls | Relevant business lead | Executive Sponsor | Finance/HR/Admissions/Legal / affected users |
| Stakeholder communications | Communications Lead | Executive Sponsor | Business leads, Legal / learners and staff |
| Accept restored service | Business Service Owner | Executive Sponsor | DR Lead, Security / users |
| Return to primary site | Facilities Lead | Executive Sponsor | DR Lead, business/security leads / all staff |

## 

### 4.3 Temporary Procedures for a 72-Hour Outage

1.  **F1:** verify room safety, power, network, accessibility, invigilators and device readiness. Since 25 seats cannot serve 40 centre-dependent candidates at once, the Academic Director approves fair cohorts or formal rescheduling. Verify identity, supervise, restrict exam material, log exceptions and preserve submissions.

2.  **F2**: use provider transaction references as evidence. Log ID, amount, time and staff member in a restricted register; require second-person review. Do not resend payment instructions because local records are absent; reconcile to provider reports after restoration.

3.  **F3:** accept applications through approved secure channels or numbered forms; timestamp, issue acknowledgement, assign case ID and restrict access. Preserve original submission time and use two-person checks when entering restored REG01.

4.  **F4**: use last approved payroll file, signed change log, separated preparation/approval and duplicate checks. Compare final bank file with approved version and escalate deadline risk.

5.  **F5:** verify requester and authority; log requests; disclose only from verified source with Records Manager approval. Defer unsafe requests and communicate expected timing.

Minimum roles include two DR technicians, BC/DR Coordinator, Academic Coordinator/invigilators, Finance, Admissions, Payroll and Records leads, Facilities, Communications and Security/IR on call. Equipment includes tested workstations, secure connectivity, power protection, locked storage, approved forms and learner-support channel. Confirm alternate-site capacity and provider support.

### 4.4 Disaster Recovery Runbook

| **Step / owner** | **Prerequisite** | **Completion check** | **If it fails** |
|----|----|----|----|
| 1\. Declare/assess — BC Coordinator + Facilities | Site outage; safety check | Scope, safety, functions and log recorded | Keep staff away from unsafe site; use alternate communications. |
| 2\. Network — DR Lead/Tech 1 | Recovery environment and power available | Connectivity, segmentation, time and admin access checked | Escalate provider issue; continue manual service. |
| 3\. AUTH01 — Tech 1 | Network validated; approved B03 selected | Directory health, configuration, privileged access and test login pass | Stop if identity trust/integrity fails; choose clean point. |
| 4\. Security/backup checks — Security + Tech 2 | AUTH01 restored | Backup chain, dates, integrity, keys and independence checked | Do not restore suspect data; use validated fallback and recalculate objectives. |
| 5\. DB01 — Tech 1 | Checks pass; B01 and all increments available | Restore B01 then increments through 07:00; consistency and sample transactions pass | Stop at last validated point; log actual RPO and obtain business approval. |
| 6\. Applications/files — DR team | DB01 passes for F1–F4; AUTH01/checks pass for FS01 | Restore LMS01, FIN01, REG01, HR01 and FS01; workflow/permission tests pass | Prioritise deadline services; maintain manual procedures. |
| 7\. Security/business acceptance — Security + owners | Technical restore complete | No unresolved compromise; data, access, workflow and accessibility validated | Keep isolated/read-only or roll back to clean state. |
| 8\. Return — Facilities + BC Coordinator | Site cleared; primary systems checked | Controlled transfer, reconciliation, dual sign-off and executive approval | Keep alternate service until safe and validated; prevent split-brain records. |

### 4.5 Communications and initial learner notice

| **Audience** | **Owner / timing** | **Channel and message** |
|----|----|----|
| Learners | Communications/Academic lead; immediately, then every 30–60 min during exam | Verified channels/SMS; service status, assessment instructions, accessibility support and next update. |
| Staff/business leads | BC Coordinator; immediate and each situation report | Phone tree/SMS/M365 if trusted; roles, safe access and manual controls. |
| Executive leadership | Incident Commander; immediate, then 30-min reports | Impact, decisions, deadlines, risks, costs and forecast. |
| Payment provider/bank | Finance Lead as needed | Verified contact/secure portal; transaction report, reconciliation and payroll timing. |
| Regulators/insurer/media | Legal/Privacy + Communications when triggered | Approved channel, verified facts, legal timeline; no speculation. |

**Learner Notice**

Northbridge Skills Institute is temporarily unable to operate from its main site following flooding and power failure this morning. We are working to maintain essential learning and assessment services while the site is assessed for safety. The 11:00 examination is being reviewed urgently because the disruption affect access to our local learning systems. Please do not travel to the main site until further notice confirm that it is safe to do so. Check the institute’s verified channels for the next update. We recognise that not everyone has a suitable device, reliable internet access or accessibility support; contact Learner Support through the published route if you need assistance. Do not submit personal or payment information through unofficial links or social media messages. We will provide confirmed assessment instructions and the next update as soon as approved. Thank you for your patience.

Return only after Facilities confirms safety, Security approves the system risk, business owners validate workflows and the Executive Sponsor signs off. Transfer temporary records using controlled encrypted methods, reconcile counts/totals, obtain dual sign-off and archive the log.

## Task 5 — Recovery schedule and tabletop 

### 5.1 Feasible modelled baseline schedule

Each action occupies one technician for the full duration and cannot be split. Schedule starts at 08:00; parallel work begins only after prerequisites complete.

| **Action** | **Technician** | **Start** | **Finish** | **Prerequisite** |
|----|----|----|----|----|
| Recovery network | 1 | 08:00 | 08:30 | None |
| AUTH01 restoration | 1 | 08:30 | 09:00 | Network |
| Security and backup checks | 1 | 09:00 | 09:30 | AUTH01 |
| FS01 restoration | 2 | 09:30 | 10:30 | AUTH01 + checks |
| DB01 restoration | 1 | 09:30 | 11:00 | Checks; complete B01/incremental chain |
| LMS01 restoration | 1 | 11:00 | 11:45 | DB01 |
| FIN01 restoration | 2 | 11:00 | 11:30 | DB01 |
| REG01 restoration | 2 | 11:30 | 12:00 | DB01 |
| HR01 restoration | 2 | 12:00 | 12:45 | DB01 |

**Assessment critical path** = network 30 + AUTH01 30 + security/backup checks 30 + DB01 90 + LMS01 45 = 225 minutes. Earliest LMS service is 11:45, 45 minutes after the examination starts. FS01 finishes 10:30, FIN01 11:30, REG01 12:00, HR01 12:45. All five functions finish by 12:45. This is a modelled baseline, not a live test.

### 5.2 Objective comparison

| Function | Elapsed time | RTO / MTD and RPO result | Continuity need |
|----|----|----|----|
| F1 | 3h45 | Misses 1h service RTO; LMS technical target 4h met. DB01 age 1h misses 15-min RPO by 45 min. | Approved workaround or fair reschedule before 11:00. |
| F2 | 3h30 | 6h RTO met; DB01 1h checkpoint meets 1h RPO at boundary if chain valid. | Manual payment register until reconciliation. |
| F3 | 4h | 8h RTO met; DB01 1h checkpoint meets 1h RPO if valid. | Timestamped intake queue before 18:00. |
| F4 | 4h45 | 16h RTO met; DB01 1h checkpoint meets 1h RPO if valid. | Approved payroll validation before Day 1 noon. |
| F5 | 2h30 | 24h RTO met; FS01 9h age misses 4h RPO by 5h; AUTH01 age 8h. | Verify permissions and records; queue unverified requests. |

MTDs are not permission to ignore earlier deadlines. F2 16:00 and F3 18:00 remain operational constraints even when RTO is met.

### 5.3 45-minute tabletop exercise

| **Time / inject** | **Decision and revised action** | **Owner** | **Rationale / effect** |
|----|----|----|----|
| 0–10: baseline, site closed 72h; exam at 11 | Activate plan, log event, confirm safe alternate site, issue learner update and start manual controls. | Incident Commander / BC Coordinator | Establish command; verify capacity and connectivity. |
| Minute 10: closure becomes five days | Extend facility, shifts, supplies and temporary-service arrangements; reassess costs and supplier capacity; update communications. | Facilities Lead / BC Coordinator | Longer outage needs sustainable resources and updated forecast. |
| Minute 20: only 15 workstations | Re-plan the 40 centre-dependent candidates using approved fair cohorts or rescheduling; confirm accessibility, invigilation and exam security. | Academic Director | Do not exceed safe capacity or disadvantage learners. |
| Minute 30: DB01 incremental fails integrity; unexpected backup admin logon | Stop chain restore; preserve logs, investigate privileged activity, isolate backup administration, find last known-good checkpoint, recalculate RPO and obtain business approval. | Security/IR Lead + DR Lead | Integrity before speed; 07:00 data cannot be assumed recoverable. |
| Minute 40: provider payments missing from restored finance | Freeze duplicate payment instructions; compare provider references, amounts and timestamps; use dual-approved reconciliation register; investigate sync or access issue. | Finance Lead | Avoid duplicate payments and distinguish stale data from compromise. |

### 5.4 Corrective actions

| **Priority / action** | **Owner** | **Target** | **Evidence of completion** |
|----|----|----|----|
| P1 Separate production and backup admin identities; MFA/least privilege. | Security Lead / IT Manager | 30 days | Access review signed; test proves production admin cannot delete immutable/offline copy. |
| P1 Prove DB01 chain and last-good fallback. | DR Lead | 30 days | Witnessed restore with checksums, transaction tests, duration and measured RPO. |
| P1 Approve exam continuity/capacity design. | Academic Director | 14 days | Walkthrough demonstrates fair, accessible route for 40 centre-dependent learners. |
| P2 Increase AUTH01/FS01 checkpoint frequency. | System owners | 60 days | Restore test shows checkpoint age within approved RPO. |
| P2 Create controlled manual forms for F2–F5. | Business leads | 21 days | Version-controlled forms and reconciliation/dual approval tested. |
| P2 Validate warm-site SLA, power, network, capacity and timings. | BC/DR Coordinator | 60 days | Supplier review and witnessed test report actual dependencies/timing. |
| P3 Run integrated BC/DR exercise and track findings. | BC/DR Program Manager | 90 days | Exercise report and evidence-based closure of findings. |

## Task 6 — Governance and performance measures 

### 6.1 Ownership, testing and framework mapping

The BC/DR Program Manager owns the plan and maintenance calendar. The Executive Sponsor approves policy, objectives, budget, activation and residual-risk acceptance. Business owners approve minimum service and data reconciliation. The DR Lead owns technical runbooks and restore evidence; Security/IR owns investigation and integrity criteria; Facilities owns site safety.

Testing calendar: monthly sample restore for DB01/AUTH01/FS01; quarterly tabletop for flood, power, cyber, supplier and staff-loss scenarios; semi-annual walkthrough of manual processes and contact trees; annual integrated warm-site test. A full interruption test is only performed if risk-assessed and authorised. Re-test after major system, supplier, backup, staffing or site changes and after incidents. Train role-holders annually and new staff on joining. Version-control every plan with owner, approver, date, change log, next review and offline controlled copies.

| Assignment output | NIST SP 800-34 step | ISO 22301 theme from slides |
|----|----|----|
| Policy, roles, approval | Step 1: contingency planning policy | Leadership (Clause 5), support (Clause 7) |
| BIA, impact calculations, RTO/RPO/MTD | Step 2: BIA | Context (4), planning (6), operation (8) |
| Protected backups and alternate site | Steps 3–4: preventive controls and strategies | Planning (6), operation (8) |
| Activation, RACI, runbook, communications | Step 5: contingency plan | Support/communication (7), operation (8) |
| Tabletop, restore tests and KPIs | Step 6: testing, training and exercises | Performance (9), improvement (10) |
| Corrective actions and annual review | Step 7: maintenance | Improvement (10), PDCA cycle |

This is an educational alignment, not a claim of certification. Flood/climate planning should consider local flood history, drainage, site elevation, safe routes, alternate-site geography, power resilience, moisture protection and whether the alternate facility shares the same flood or utility risk. Consider the ISO 22301:2019 climate-action amendment when assessing organizational context.

### 6.2 Performance dashboard

| **KPI and method** | **Source** | **Target** | **Frequency / owner** |
|----|----|----|----|
| Recovery performance: elapsed time to business acceptance compared with each RTO | DR logs and owner sign-off | ≥90% of critical services meet approved RTO in tests; F1 workaround before exam deadline | After tests/quarterly; BC/DR Program Manager |
| Restore-test coverage: critical systems tested ÷ critical systems scheduled ×100 | Test plans and reports | 100% critical systems tested annually; DB01/AUTH01/FS01 sampled monthly | Monthly; DR Lead |
| Corrective action closure: actions closed with evidence by due date ÷ actions due ×100 | Improvement register | ≥90% on time; no overdue P1 without signed risk acceptance | Monthly; BC/DR Program Manager |
| Training completion: trained assigned staff ÷ assigned staff ×100 | Training records | ≥95% annually; every key role has a deputy | Quarterly; HR/BCDR Manager |
| RPO achievement: tested systems within RPO ÷ systems tested ×100 | Backup catalogue and restore logs | 100% critical systems in successful tests or logged exception/risk treatment | Each restore test; DR Lead/data owners |
| Plan freshness: plans reviewed by due date ÷ plans due ×100 | Document register | 100% annually and after material changes | Quarterly; BC/DR Program Manager |

**Provisional current maturity**:

Level 2 — Developing (Repeatable). Some checkpoints and drill timings exist, but shared administrator identity, undocumented offsite access independence, RPO gaps and unproven integrated recovery show that repeatable, measured performance is not yet established.

Target Level 3 — Defined (Standardized) within 12 months: approved plans for all critical functions, clear governance, regular tests, evidenced RTO/RPO results and a tracked corrective-action register.

## Conclusion

Northbridge should coordinate business continuity and disaster recovery because restoring technology is only one part of sustaining acceptable services. F1’s 11:00 deadline drives the first decision; the modelled warm-site schedule restores LMS01 at 11:45, so an approved workaround is essential. Warm plus protected backups and testing is affordable at NGN 2.1 million but leaves explicit RTO/RPO gaps. Independent backups, validated restore chains, disciplined manual controls, clear accountability and regular exercises are necessary to make the plan operational.
