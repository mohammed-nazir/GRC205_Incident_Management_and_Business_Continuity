---
Title: "Incident Response Planning: Suspected Ransomware Incident at Northbridge Skills Institute"
Author: "Mohammed Nazir"
Student_id: "2025/GRC/2512799"
Course: "GRC105 — Incident Management and Business Continuity"
Institution: "International Cybersecurity and Digital Forensics Academy"
Assessment: "Week 20"
Submission_date: "20 October 2026"
---

# Incident Response Planning

## Suspected Ransomware Incident at Northbridge Skills Institute

[![Course](https://img.shields.io/badge/Course-GRC205-1F4E79)](#document-information)
[![Domain](https://img.shields.io/badge/Domain-GRC%20%7C%20Incident%20Response-8B1E3F)](#executive-summary)
[![Framework](https://img.shields.io/badge/Framework-NIST%20SP%20800--61%20Rev.%203-2E7D32)](#references)
[![Status](https://img.shields.io/badge/Status-Academic%20Submission-6F42C1)](#document-information)

> A comprehensive, evidence-led incident response plan covering classification, governance, containment, forensic preservation, recovery, communications, tabletop exercising, and continuous improvement.

## Document information

| Field | Detail |
|---|---|
| **Student** | Mohammed Nazir |
| **Student ID** | 2025/GRC/2512799 |
| **Institution** | International Cybersecurity and Digital Forensics Academy |
| **Course** | GRC105 — Incident Management and Business Continuity |
| **Assessment** | Week 20 Incident Response Planning Assignment |
| **Case** | Suspected ransomware incident at Northbridge Skills Institute |
| **Submission date** | 20 October 2026 |

## Contents

- [Executive summary](#executive-summary)
- [Scope, assumptions, and evidence discipline](#scope-assumptions-and-evidence-discipline)
- [Task 1 — Incident classification and initial assessment](#task-1--incident-classification-and-initial-assessment)
- [Task 2 — Incident response plan and team responsibilities](#task-2--incident-response-plan-and-team-responsibilities)
- [Task 3 — Response playbook and evidence preservation](#task-3--response-playbook-and-evidence-preservation)
- [Task 4 — Communication and escalation](#task-4--communication-and-escalation)
- [Task 5 — Tabletop exercise and improvement plan](#task-5--tabletop-exercise-and-improvement-plan)
- [Task 6 — Case study analysis and critical reflection](#task-6--case-study-analysis-and-critical-reflection)
- [Conclusion](#conclusion)
- [References](#references)

> [!IMPORTANT]
> This is an academic incident-response scenario. Proposed collections and actions are plans, not claims that evidence has already been acquired. No malware family, attacker identity, data theft, forensic hash, or breach conclusion should be treated as confirmed unless supported by evidence.

---


## Executive summary

At 08:45 WAT on Monday (Day 0), Northbridge Skills Institute must respond to suspected ransomware incident that is affecting finance workstation (FIN-PC07), shared file server (FS01), and learning portal availability. Evidence indicate that a suspicious payroll attachment was opened, an unfamiliar Microsoft 365 sign-in occurred, the backup service account made unusual privileged logons, 1.2 GB was uploaded to unfamiliar cloud storage, and encrypted-looking files and a ransom note were found. These observations support declaring a Critical incident because shared files are encrypted, an examination for 100 learners is scheduled for 11:00, and the integrity of backups and possible exposure of learner/finance information are uncertain. The evidence does not yet prove the malware family, attacker identity, or theft of personal data.

The response will prioritise life-safety-neutral but business-critical containment, preservation of evidence, protection of backup systems, and a safe decision about the examination. The Institute will use an incident command structure, an out-of-band staff-phone channel, a documented evidence register, and a controlled recovery testing. The portal will not be reopened merely to meet the examination time: the Incident Manager and IT lead must demonstrate that the selected recovery point is clean, that dependencies are safe, and that the business owner approves service restoration. Therefore, this plan follows the assignment's four teaching stages and aligns incident response with risk management practices described by NIST SP 800-61 Rev. 3 and the CISA StopRansomware Guide (NIST, 2025; CISA et al., 2023).

## Scope, assumptions, and evidence discipline

This report use the Northbridge scenario and the supplied evidence IDs E01–E08. All proposed collections and actions are plans, not claims that evidence has already been acquired. No hash values, forensic findings, breach conclusions, or real contact details are invented. Times are West Africa Time (WAT).

1.  Confirmed observation means the scenario explicitly records the event; it does not necessarily prove the event's cause or full meaning.

2.  Working hypothesis means a plausible explanation to test, not a conclusion.

3.  Unresolved question means the evidence pack does not answer it.

4.  All contact names, telephone numbers, and email addresses used below are fictional placeholders. Replace them with approved internal contacts before operational use.

5.  The teaching deck presents four stages for teaching: Preparation; Detection and Analysis; Containment, Eradication and Recovery; and Post-Incident Activity. NIST SP 800-61 Rev. 3 aligns incident response with CSF 2.0 Detect, Respond, and Recover, supported by Govern, Identify, and Protect; the four teaching stages are used here as the assignment's organising structure, not attributed as NIST Rev. 3's exact lifecycle.

## Task 1 — Incident classification and initial assessment

### 1.1 Evidence-linked timeline

| **Time (WAT)** | **Evidence** | **Confirmed observation** | **Hypothesis / uncertainty** | **Next validation** |
|:---|:---|:---|:---|:---|
| Day −1, 16:40 | E01 | A finance officer opened an unexpected payroll attachment on FIN-PC07. Code execution is not verified. | Possible phishing/malware entry; attachment may have been benign or blocked. | Email headers, attachment hash, endpoint process tree, user interview. |
| Day 0, 01:15 | E02 | Finance account signed in from an unfamiliar IP and new device; MFA and user involvement unknown. | Possible stolen credentials, legitimate travel/device, VPN/proxy, or attacker session. | Entra/M365 sign-in and audit logs, MFA result, device details, user confirmation, and IP reputation. |
| Day 0, 01:35 | E03 | Svc_backup made out-of-schedule remote administrator logons to FS01 and BAK01. | Possible compromised privileged credential or authorised but undocumented maintenance. | Windows logon events, service logs, scheduled jobs, change tickets, administrator interview. |
| Day 0, 01:50 | E04 | FIN-PC07 uploaded 1.2 GB via HTTPS to unfamiliar cloud storage; content unknown. | Possible data exfiltration; alternatively legitimate sync, backup, or other transfer requiring verification. | Proxy/DNS/firewall logs, destination details, endpoint network/process telemetry, cloud audit if available. |
| Day 0, 02:00 | E05 | Backup jobs for FS01 and LMS01 reported success; recoverability and cleanliness unproven. | Backup data may be clean, partially corrupted, or compromised; successful job status is not a restore test. | Backup catalog, job logs, snapshot metadata, access logs, and isolated test restore. |
| Day 0, 08:30 | E06 | EDR/helpdesk recorded mass file changes on FIN-PC07; FS01 shares contain .locked files and ransom note. | Ransomware activity is strongly indicated; exact family, start time, scope, and data theft remain unknown. | Disk/memory capture where feasible, ransom note, and file samples, EDR timeline, server logs. |
| Day 0, 08:40 | E07 | LMS login page loads, but learners cannot open materials or submit assessments. | Portal dependency on FS01 may be disrupted; LMS01 compromise itself is unconfirmed. | LMS/application logs, health checks, dependency tests, file access logs. |
| Day 0, 08:45 | E08 | Incident contact list on FS01 inaccessible; staff phones available; corporate email trust unverified. | Normal incident coordination is impaired; email could be unavailable or untrustworthy. | Use phone tree; validate contacts independently; preserve email logs before relying on them. |

### 1.2 Incident type and severity

Incident type: suspected ransomware/malware with possible credential compromise, privileged-account misuse, service disruption, and possible data exfiltration. The incident is declared Critical at 08:45 WAT because the file server is encrypted or otherwise rendered unusable, the learner portal's core functions are unavailable, an examination is due at 11:00, suspicious privileged access reached the backup repository, and a 1.2 GB outbound transfer raises a credible but unconfirmed confidentiality risk (E03–E07).

| **Severity** | **Decision criteria** | **Example response** |
|:---|:---|:---|
| Critical | Confirmed or strongly indicated a compromise of critical systems; widespread/critical service outage; credible data exposure; backup compromise; or urgent business/safety impact. | Activate full CSIRT immediately; notify executive sponsor; out-of-band coordination; immediate containment; legal/privacy assessment. |
| High | Significant system or data impact, but critical services remain available or containment is likely to be prompt; scope is limited but material. | Rapid response within one hour; management notification; dedicated investigation and frequent updates. |
| Medium | Limited affected assets, no current evidence of sensitive-data exposure, critical services remain operational, and containment is straightforward. | Standard incident workflow, documented owner and tracked remediation. |
| Low | Low-impact policy violation or blocked event with no evidence of compromise and negligible operational impact. | Log, investigate proportionately, and close with rationale. |

**CIA Assessment:**

1.  Confidentiality: Potentially affected. E04 records a 1.2 GB upload to unfamiliar cloud storage, but transferred content is unknown. E02 raises identity risk. Do not state that learner data was stolen until evidence supports that conclusion.

2.  Integrity: Strongly at risk. E06 records mass file changes and .locked files on FS01; malicious changes to files, backup catalogues, or identities must be investigated.

3.  Availability: Confirmed material impact. FS01 shared folders are affected and learners cannot access materials or submit assessments through LMS01 (E06–E07).

Assets confirmed affected or involved Includes FIN-PC07 (suspicious attachment, mass changes, outbound transfer); FS01 (locked files/ransom note); LMS01 service availability (functional impact; underlying compromise unknown). Potentially affected are BAK01 (unusual svc_backup logon), Microsoft 365/finance identity, other endpoints or servers reachable using privileged credentials, learner and finance data, and backups. The scenario does not establish that all these assets are compromised.

### 1.3 Response priorities

1.  **Stop active encryption and lateral movement**: isolate FIN-PC07 and affected FS01 network paths, using the least disruptive action that achieves containment. If active spread is observed, isolate immediately even if some volatile evidence may be lost; document the action and rationale.

2.  **Protect BAK01 and backup credentials:** restrict network access and disable/rotate compromised privileged access after preserving necessary authentication evidence. Do not connect backups to potentially infected systems.

3.  **Preserve evidence and establish scope:** capture relevant endpoint/server/cloud logs, ransom note, file metadata, sign-in records, and proxy data using trained staff or external support.

4.  **Decide examination arrangements before 11:00:** communicate a holding notice that the examination status is under review. Do not restore from an unverified backup simply to meet the scheduled time.

5.  **Assess data exposure and reporting obligations:** legal/privacy adviser to determine what data might be affected, applicable jurisdiction, recipients, and any deadlines.

6.  **Plan safe recovery:** validate backup cleanliness and readability in an isolated environment; prioritise the dependencies required for LMS service and learner materials.

7.  

### 1.4 Priority investigation questions

| **Question** | **Evidence/check to obtain** | **Finding that changes scope/severity** |
|:---|:---|:---|
| Was the payroll attachment the initial entry point? | Collect email headers/attachment, endpoint process tree and EDR telemetry; interview finance officer; compare timestamps. | Confirmed malicious execution increases confidence in phishing entry; evidence of blocked/no execution may shift initial-access hypothesis. |
| Was the finance account or svc_backup compromised? | M365 sign-in/MFA/audit logs; Windows Security logs on FS01/BAK01; credential changes, service account use, admin interviews. | Unrecognized successful sign-ins, token abuse, or malicious privilege use expands identity scope and keeps Critical severity. |
| What was transferred in the 1.2 GB upload? | Proxy/firewall/DNS logs, endpoint process and connection telemetry, destination ownership, cloud audit records where available. | Evidence of learner/finance data leaving the organization triggers formal breach assessment and likely broader notification; benign verified transfer may narrow confidentiality concern. |
| Are BAK01 and available backups safe and recoverable? | Backup access/audit logs, snapshot metadata, offline backup inventory, isolated restore and malware/integrity checks. | Deletion, encryption, suspicious backup modification, or failed restoration expands recovery impact and extends outage. |
| Is LMS01 itself compromised or only blocked by FS01? | LMS application/system logs, configuration comparison, dependency tests in isolation, EDR/AV scan. | Evidence of persistence or direct compromise on LMS01 requires rebuild and wider scope; clean LMS with dependency failure may permit staged recovery. |
| Did the attacker move to other assets? | EDR/network logs, domain/authentication logs, privileged account use, endpoint inventory, threat hunting for indicators and persistence. | Additional encrypted systems or lateral movement confirms wider outbreak and may require subnet-level isolation. |

## 

## Task 2 — Incident response plan and team responsibilities

### 2.1 Policy and plan outline

**Mission:** To protect learners, staff, institutional information, and essential training services by coordinating a timely, evidence-led response that limits harm, meets applicable obligations, and restores trustworthy operations.

**Objectives:** (1) To detect, validate, classify, and document incidents; (2) To contain threats without avoidable evidence loss; (3) To preserve evidence and chain of custody; (4) To assess confidentiality, integrity, availability, and business impact; (5) coordinate clear, accurate communications; (6) To recover from verified clean sources; and (7) To learn and improve after closure.

**Scope:** All Northbridge-managed systems, identities, endpoints, networks, cloud services, backups, third-party services, and data. The plan will cover all employees, learners, contractors, and service providers when they support affected systems.

**Declaration and activation:** Any staff member may report a suspected incident using the published phone tree or service desk. The Incident Manager (IM) validates available evidence and may declare an incident. Critical criteria are ransomware on a critical server, credible data exfiltration, privileged/backup compromise, or major service outage. For this scenario, Critical status is declared at 08:45 WAT on Day 0 based on E03–E07.

**Authority and escalation:** the Incident Manager directs response coordination and may order immediate isolation of a suspected compromised endpoint/server where delay risks continued encryption or lateral movement. The IT Operations Lead implement network/account actions. If immediate isolation may disrupt essential services, the Incident Manager consults the business owner when time permits; consultation must not delay urgent containment. Only the executive sponsor approves major business decisions such as examination cancellation/rescheduling or exceptional expenditure. Legal/privacy adviser recommend regulatory and contractual notifications; the designated executive/data controller approves formal external statements.

**Documentation:** Maintain a timestamped incident log, decision log, evidence register, custody transfers, affected asset list, indicators of compromise, stakeholder notices, approvals, recovery tests, and closure report. Record WAT timestamps, collector, source, method, integrity check, storage location, and every access/transfer. Use least privilege and restricted encrypted storage.

**Plan review:** Review after every Critical/High incident and exercise; complete the formal lessons-learned review within 14 calendar days after incident closure. The plan owner tracks corrective actions to closure.

**Business continuity integration:** the incident plan handles cyber containment and trustworthy restoration; business continuity arrangements handle alternate delivery of learning, learner communications, examination postponement/rescheduling, staff workarounds, and prioritisation of essential services. Continuity workarounds must not reconnect unsafe systems or use unverified data.

### 2.2 CSIRT structure and roles

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 43%" />
<col style="width: 36%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Role</strong></th>
<th style="text-align: left;"><strong>Primary responsibilities</strong></th>
<th style="text-align: left;"><strong>Decision/authority</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">1. Incident Manager / IR Lead</td>
<td style="text-align: left;">Declare severity; coordinates CSIRT; maintains incident log; assigns actions; escalates to executive sponsor; chairs briefings.</td>
<td style="text-align: left;"><p>May order urgent containment;</p>
<p>Coordinates all response work.</p></td>
</tr>
<tr>
<td style="text-align: left;">2. Security Analyst / SOC Lead</td>
<td style="text-align: left;">Triage alerts; correlate EDR, endpoint, identity, proxy and server logs; hunt for lateral movement; maintain indicators.</td>
<td style="text-align: left;">Recommend scope/severity; performs analysis within approved access.</td>
</tr>
<tr>
<td style="text-align: left;">3. Forensics Lead</td>
<td style="text-align: left;"><p>Plan and perform evidence acquisition;</p>
<p>Preserve volatile data where feasible; hashes copies; maintain chain of custody; produces findings.</p></td>
<td style="text-align: left;">Control forensic method and evidence register; advises before destructive action when time allow.</td>
</tr>
<tr>
<td style="text-align: left;"><p>4. IT Operations</p>
<p>Lead</p></td>
<td style="text-align: left;"><p>Isolate endpoints/servers, disables</p>
<p>Sessions/accounts, manages network controls, patches/rebuilds systems and tests</p>
<p>dependencies.</p></td>
<td style="text-align: left;">Executes containment and technical recovery under IM authority.</td>
</tr>
<tr>
<td style="text-align: left;"><p>5. Business</p>
<p>Continuity / LMS</p>
<p>Owner</p></td>
<td style="text-align: left;"><p>Assesses learner/examination impact; defines</p>
<p>minimum service; proposes alternate</p>
<p>arrangements; validates business functionality.</p></td>
<td style="text-align: left;"><p>Own business acceptance criteria; recommends exam reschedule or</p>
<p>service return.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>6. Legal / Privacy</p>
<p>Adviser</p></td>
<td style="text-align: left;"><p>Assesse data categories, jurisdiction,</p>
<p>legal/contractual duties, notification recipients</p>
<p>and deadlines; preserves privilege where</p>
<p>applicable.</p></td>
<td style="text-align: left;">Advise on notification obligations and legal risks; does not infer a breach without evidence.</td>
</tr>
<tr>
<td style="text-align: left;"><p>7. Communications</p>
<p>Lead</p></td>
<td style="text-align: left;"><p>Maintain approved messages; manages learner/staff notices, media enquiries and</p>
<p>update schedule; corrects misinformation.</p></td>
<td style="text-align: left;"><p>Published only approved statements</p>
<p>through safe channels.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>8. Executive</p>
<p>Sponsor / Director</p></td>
<td style="text-align: left;">Approve major business decisions, resources, external commitments and risk acceptance; receives critical updates.</td>
<td style="text-align: left;">Accountable for exceptional business risk decisions and exam decision.</td>
</tr>
<tr>
<td style="text-align: left;"><p>9. Microsoft 365 /</p>
<p>Identity</p>
<p>Administrator</p></td>
<td style="text-align: left;">Review sign-ins, MFA, audit logs, sessions, OAuth/app consent and account controls; revokes sessions and resets credentials as directed.</td>
<td style="text-align: left;">Executes identity containment; records all changes.</td>
</tr>
<tr>
<td style="text-align: left;"><p>10. External IR /</p>
<p>Managed Security</p>
<p>Provider</p></td>
<td style="text-align: left;">Provide surge forensics, malware analysis, threat hunting and recovery validation if internal capacity is exceeded.</td>
<td style="text-align: left;"><p>Works under written scope and IM</p>
<p>coordination.</p></td>
</tr>
</tbody>
</table>

**Small-team resourcing:** Northbridge has only three IT staff and one security analyst. The Incident Manager should request pre-approved external incident-response support, if server forensics, malware analysis, identity investigation, or 24-hour monitoring exceeds internal capacity. Preserve independence by separating evidence collection/review from the person rebuilding a system where staffing permits. Record vendor authorisation, access scope, confidentiality terms, and all actions.

### 2.3 RACI matrix

R = Responsible (does the work); A = Accountable (one role answerable for the result); C = Consulted (provides input); I = Informed (kept updated). Each activity below has exactly one accountable role and at least one responsible role.

| **Activity** | Incident Manager | **Security analyst** | **Forensics** | **IT Ops** | **Business/LMS owner** | **Legal/privacy** | **Communications lead** | **Executive sponsor** |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| Detection and alert triage | I | A/R | C | I | I | I | I | I |
| Incident analysis and severity | A | R | C | C | C | C | I | I |
| Containment / isolation | A | C | C | R | C | I | I | I |
| Evidence handling and custody | A | C | R | C | I | C | I | I |
| Stakeholder communications | C | I | I | I | C | C | A/R | I |
| Assess reporting obligations | C | C | C | I | I | A/R | C | I |
| Restoration approval | C | C | C | R | A | C | I | I |
| Incident closure and lessons learned | A/R | C | C | C | C | C | C | I |
| Exam postponement/rescheduling | C | I | I | C | R | C | C | A |
| Credential/session containment | A | C | C | R | I | C | I | I |

The matrix uses combined A/R where one role both performs and owns the result. For examination rescheduling, the executive sponsor is the single accountable role; the business/LMS owner is responsible for proposing and implementing the academic arrangement.

### 2.4 Readiness improvement checklist

<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 16%" />
<col style="width: 33%" />
<col style="width: 24%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Improvement</strong></th>
<th style="text-align: left;"><strong>Owner</strong></th>
<th style="text-align: left;"><strong>Resources needed</strong></th>
<th style="text-align: left;"><p><strong>Readiness check /</strong></p>
<p><strong>evidence</strong></p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;"><p>Create tested</p>
<p>offline/immutable backup</p>
<p>copies; separate backup</p>
<p>admin identities; document restore priorities.</p></td>
<td style="text-align: left;"><p>IT Operations</p>
<p>Lead</p></td>
<td style="text-align: left;"><p>Offline/immutable storage, separate</p>
<p>credentials, backup monitoring,</p>
<p>budget.</p></td>
<td style="text-align: left;"><p>Quarterly isolated restore test; documented</p>
<p>RTO/RPO; prove restored sample is readable and</p>
<p>malware-checked.</p></td>
</tr>
<tr>
<td style="text-align: left;">Maintain incident contact list outside FS01 and corporate email.</td>
<td style="text-align: left;">Communications Lead</td>
<td style="text-align: left;"><p>Printed sealed copy, encrypted offline copy, staff phone tree, named</p>
<p>alternates.</p></td>
<td style="text-align: left;"><p>Quarterly call-tree test;</p>
<p>contact success rate ≥95%; update after staff changes.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Extend EDR/logging to</p>
<p>servers and centralize</p>
<p>identity, proxy, server and</p>
<p>backup logs.</p></td>
<td style="text-align: left;">Security Analyst</td>
<td style="text-align: left;"><p>Server EDR licences, SIEM/log</p>
<p>storage, alert rules, and retention.</p></td>
<td style="text-align: left;"><p>Monthly coverage report;</p>
<p>test alert for suspicious</p>
<p>admin logon and mass file changes.</p></td>
</tr>
<tr>
<td style="text-align: left;">Create secure out-of-band response channels.</td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;"><p>Approved phone bridge, emergency</p>
<p>messaging group, and alternate</p>
<p>meeting details.</p></td>
<td style="text-align: left;"><p>Tabletop confirms every</p>
<p>role can join within 15</p>
<p>minutes without corporate email.</p></td>
</tr>
<tr>
<td style="text-align: left;">Document ransomware and identity-compromise playbooks.</td>
<td style="text-align: left;">Incident Manager + IT Lead</td>
<td style="text-align: left;"><p>Runbooks, access-control diagrams,</p>
<p>vendor contacts, change templates.</p></td>
<td style="text-align: left;"><p>Semi-annual tabletop;</p>
<p>actions have owner,</p>
<p>timestamp, approval and</p>
<p>completion evidence.</p></td>
</tr>
<tr>
<td style="text-align: left;">Train staff on phishing and reporting; conduct role-based CSIRT drills.</td>
<td style="text-align: left;">HR/Training + Security Analyst</td>
<td style="text-align: left;"><p>Short learning modules, simulated</p>
<p>phishing, exercise time.</p></td>
<td style="text-align: left;">Completion ≥95%; measure report rate and time from suspicious activity to escalation.</td>
</tr>
<tr>
<td style="text-align: left;">Arrange external IR retainer or on-call support.</td>
<td style="text-align: left;">Executive Sponsor</td>
<td style="text-align: left;"><p>Contract, service scope, contact</p>
<p>details, secure evidence transfer</p>
<p>terms.</p></td>
<td style="text-align: left;">Annual call-out test; confirm response SLA and access prerequisites.</td>
</tr>
<tr>
<td style="text-align: left;">Inventory system dependencies and recovery order.</td>
<td style="text-align: left;">LMS Owner + IT Lead</td>
<td style="text-align: left;">Asset inventory, dependency map, recovery checklist.</td>
<td style="text-align: left;">Annual validation; tabletop demonstrates LMS dependencies and owner sign-off.</td>
</tr>
</tbody>
</table>

## Task 3 — Response playbook and evidence preservation 

### 3.1 Ordered response playbook

The first 60 minutes run from 08:45 to 09:45 WAT on Day 0. Times are target stages, not claims that actions have already occurred. Actions may run in parallel if personnel are available, but containment and evidence integrity must be coordinated.

<table>
<colgroup>
<col style="width: 10%" />
<col style="width: 24%" />
<col style="width: 9%" />
<col style="width: 20%" />
<col style="width: 17%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Time / stage</strong></th>
<th style="text-align: left;"><strong>Action</strong></th>
<th style="text-align: left;"><strong>Owner</strong></th>
<th style="text-align: left;"><strong>Approval</strong></th>
<th style="text-align: left;"><strong>Evidence to retain</strong></th>
<th style="text-align: left;"><strong>Completion check</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">08:45–08:50</td>
<td style="text-align: left;"><p>Declare Critical incident; appoint IM; open incident log; start staff-</p>
<p>phone bridge; tell staff not to use FS01 incident contact list or</p>
<p>unverified email.</p></td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;">Executive sponsor informed; urgent isolation does not wait for approval.</td>
<td style="text-align: left;"><p>E01–E08 references, initial reports,</p>
<p>timestamps,</p>
<p>participants, decisions.</p></td>
<td style="text-align: left;">Incident ID assigned; call bridge operating; first status note saved offline.</td>
</tr>
<tr>
<td style="text-align: left;">08:45–08:55</td>
<td style="text-align: left;"><p>Isolate FIN-PC07 from</p>
<p>wired/wireless network; do not</p>
<p>ower it off unless necessary to stop</p>
<p>immediate harm. Photograph</p>
<p>screen/ransom note and not</p>
<p>logged-in user.</p></td>
<td style="text-align: left;">IT Ops + Forensics</td>
<td style="text-align: left;"><p>IM authorises; immediate</p>
<p>isolation allowed to stop</p>
<p>active encryption.</p></td>
<td style="text-align: left;"><p>Endpoint identifiers,</p>
<p>screen photos, EDR</p>
<p>alert export, volatile</p>
<p>data plan.</p></td>
<td style="text-align: left;"><p>Network isolation</p>
<p>confirmed;</p>
<p>action/time/operator documented.</p></td>
</tr>
<tr>
<td style="text-align: left;">08:48–09:00</td>
<td style="text-align: left;"><p>Restrict FS01 network access or</p>
<p>isolate affected shares/server if</p>
<p>active encryption continues;</p>
<p>preserve logs and coordinate</p>
<p>impact to LMS01.</p></td>
<td style="text-align: left;">IT Ops</td>
<td style="text-align: left;"><p>IM; consult LMS owner if</p>
<p>delay is safe.</p></td>
<td style="text-align: left;"><p>FS01 security/system</p>
<p>logs, share state,</p>
<p>ransom note, file</p>
<p>metadata, network</p>
<p>configuration.</p></td>
<td style="text-align: left;">New file changes stop or are bounded; LMS impact recorded.</td>
</tr>
<tr>
<td style="text-align: left;">08:50–09:05</td>
<td style="text-align: left;"><p>Protect BAK01: restrict</p>
<p>inbound/outbound access,</p>
<p>suspend svc_backup</p>
<p>interactive/remote access, and</p>
<p>preserve its authentication logs</p>
<p>before credential changes where</p>
<p>feasible.</p></td>
<td style="text-align: left;">IT Ops + Identity Admin</td>
<td style="text-align: left;"><p>IM; emergency restriction</p>
<p>authorised.</p></td>
<td style="text-align: left;"><p>BAK01 logs,</p>
<p>svc_backup logons,</p>
<p>backup job/catalogue logs, policy changes.</p></td>
<td style="text-align: left;"><p>Backup repository is isolated from infected systems; no</p>
<p>restoration started.</p></td>
</tr>
<tr>
<td style="text-align: left;">08:50–09:10</td>
<td style="text-align: left;"><p>Use Microsoft 365 audit/sign-in</p>
<p>logs to assess finance account</p>
<p>activity; revoke sessions and reset credentials if unauthorised activity is indicated. Check privileged</p>
<p>accounts and MFA.</p></td>
<td style="text-align: left;">Identity Admin + Analyst</td>
<td style="text-align: left;"><p>IM approves account</p>
<p>containment; emergency</p>
<p>revocation may be</p>
<p>immediate.</p></td>
<td style="text-align: left;"><p>Sign-in/audit logs, MFA details, session IDs,</p>
<p>account change record.</p></td>
<td style="text-align: left;"><p>Known sessions</p>
<p>revoked as</p>
<p>appropriate; account owner contacted by</p>
<p>phone.</p></td>
</tr>
<tr>
<td style="text-align: left;">08:55–09:15</td>
<td style="text-align: left;"><p>Collect proxy, DNS, firewall, EDR</p>
<p>and endpoint telemetry related to</p>
<p>1.2 GB transfer; identify destination</p>
<p>and process; block destination if</p>
<p>malicious confidence is sufficient.</p></td>
<td style="text-align: left;">Analyst + Forensics</td>
<td style="text-align: left;"><p>IM/IT change approval;</p>
<p>preserve rule before/after</p>
<p>state.</p></td>
<td style="text-align: left;"><p>Proxy records,</p>
<p>destination domain/IP, process and network</p>
<p>telemetry, block rule.</p></td>
<td style="text-align: left;"><p>Transfer scope</p>
<p>assessed; any block</p>
<p>and potential side</p>
<p>effects logged.</p></td>
</tr>
<tr>
<td style="text-align: left;">09:00–09:20</td>
<td style="text-align: left;"><p>Preserve evidence: collect logs and forensic images/memory where</p>
<p>feasible; capture ransom note and</p>
<p>representative encrypted files;</p>
<p>hash forensic copies.</p></td>
<td style="text-align: left;">Forensics Lead</td>
<td style="text-align: left;"><p>IM authorises; trained</p>
<p>collector only.</p></td>
<td style="text-align: left;"><p>Evidence register items EV-01 onward;</p>
<p>tool/version, timestamps, hashes</p>
<p>after collection.</p></td>
<td style="text-align: left;"><p>Evidence stored read-only/restricted;</p>
<p>custody record</p>
<p>completed.</p></td>
</tr>
<tr>
<td style="text-align: left;">09:00–09:25</td>
<td style="text-align: left;"><p>Hunt for broader compromise</p>
<p>across endpoints, FS01, BAK01,</p>
<p>LMS01, Microsoft 365, admin</p>
<p>accounts and network logs; search for common indicators and unusual remote logons.</p></td>
<td style="text-align: left;">Security Analyst</td>
<td style="text-align: left;"><p>IM authorises read-only</p>
<p>investigation; coordinate any active containment.</p></td>
<td style="text-align: left;"><p>EDR alerts, Windows</p>
<p>events, M365 audit,</p>
<p>network flows,</p>
<p>scheduled tasks/services.</p></td>
<td style="text-align: left;">Asset scope updated; no unreview system declared clean.</td>
</tr>
<tr>
<td style="text-align: left;">09:05–09:25</td>
<td style="text-align: left;">Send approved holding message to staff and learners using verified phone/SMS/portal-independent channel; state exam status is under urgent review, not that data was stolen.</td>
<td style="text-align: left;">Comms Lead</td>
<td style="text-align: left;">Executive sponsor approves external notice; legal/privacy consulted if available.</td>
<td style="text-align: left;"><p>Final message,</p>
<p>recipients, channel,</p>
<p>delivery timestamp,</p>
<p>approval.</p></td>
<td style="text-align: left;">Message is consistent across channels; next update time stated.</td>
</tr>
<tr>
<td style="text-align: left;">09:15–09:35</td>
<td style="text-align: left;"><p>Convene decision group on the</p>
<p>11:00 exam; assess dependency</p>
<p>and safe alternatives. Do not</p>
<p>reopen portal from unverified</p>
<p>backup.</p></td>
<td style="text-align: left;">LMS Owner + Executive Sponsor</td>
<td style="text-align: left;">Executive sponsor approves reschedule/alternate format.</td>
<td style="text-align: left;"><p>Decision record, LMS dependency test plan, learner impact</p>
<p>estimate.</p></td>
<td style="text-align: left;"><p>Exam decision</p>
<p>communicated by</p>
<p>target 10:00 or earlier if decision is clear.</p></td>
</tr>
<tr>
<td style="text-align: left;">09:25–09:45</td>
<td style="text-align: left;">Create incident action plan for remaining 24 hours: containment, forensic scope, identity recovery, isolated backup validation, external support and update cadence.</td>
<td style="text-align: left;">IM</td>
<td style="text-align: left;"><p>Executive sponsor approves resources and external</p>
<p>support.</p></td>
<td style="text-align: left;"><p>Action list, owners, deadlines, risk</p>
<p>decisions.</p></td>
<td style="text-align: left;"><p>All critical actions have owner and target time; next briefing</p>
<p>scheduled.</p></td>
</tr>
</tbody>
</table>

### 3.2 Remainder of first 24 hours

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 37%" />
<col style="width: 21%" />
<col style="width: 29%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><p><strong>Stage /</strong></p>
<p><strong>target</strong></p></th>
<th style="text-align: left;"><strong>Action</strong></th>
<th style="text-align: left;"><strong>Owner and approval</strong></th>
<th style="text-align: left;"><strong>Evidence / completion check</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">09:45–12:00</td>
<td style="text-align: left;">Continue threat hunting; map assets and dependencies; confirm whether LMS01 is directly compromised or unavailable because FS01 is affected. Request external IR support if required.</td>
<td style="text-align: left;"><p>Analyst/Forensics; IM</p>
<p>coordinates.</p></td>
<td style="text-align: left;">Scope map, log exports, support request; affected asset list updated.</td>
</tr>
<tr>
<td style="text-align: left;">By 12:00</td>
<td style="text-align: left;">Complete initial data exposure assessment using proxy, endpoint, cloud and identity logs. Do not infer data theft solely from upload volume.</td>
<td style="text-align: left;">Analyst + Legal/Privacy.</td>
<td style="text-align: left;">Evidence-based preliminary finding with confidence level and gaps.</td>
</tr>
<tr>
<td style="text-align: left;">By 14:00</td>
<td style="text-align: left;">Examine backup logs and copies without connecting them to production. Run a test restore in isolated recovery environment; if latest network backup fails, preserve failure details and test the disconnected Day −3 backup.</td>
<td style="text-align: left;">IT Ops + Forensics; IM approval.</td>
<td style="text-align: left;">Backup catalogue, snapshot error, malware/integrity scan, restore test report.</td>
</tr>
<tr>
<td style="text-align: left;">By 16:00</td>
<td style="text-align: left;">Determine persistence and initial-access hypotheses; remove persistence only after evidence capture when feasible. Rebuild affected systems from known-good images rather than relying on untrusted cleanup alone.</td>
<td style="text-align: left;"><p>Forensics advises; IT</p>
<p>Ops executes.</p></td>
<td style="text-align: left;"><p>Image baseline,</p>
<p>patch/configuration list, persistence findings, change log.</p></td>
</tr>
<tr>
<td style="text-align: left;">By 18:00</td>
<td style="text-align: left;">Rotate credentials and revoke sessions for affected finance and privileged identities; reset svc_backup with separate least-privilege backup identity and MFA where supported. Check application secrets and tokens.</td>
<td style="text-align: left;"><p>Identity Admin; IM</p>
<p>approval.</p></td>
<td style="text-align: left;">Credential reset/session revocation log; validation of least privilege.</td>
</tr>
<tr>
<td style="text-align: left;">By 20:00</td>
<td style="text-align: left;">Approve recovery plan and priorities based on clean restore validation and business impact. If no safe backup is validated, continue containment and use continuity alternatives.</td>
<td style="text-align: left;"><p>IM + LMS Owner;</p>
<p>executive sponsor</p>
<p>approves business risk.</p></td>
<td style="text-align: left;"><p>Recovery decision, risk</p>
<p>acceptance/rejection, RTO/RPO</p>
<p>proposal.</p></td>
</tr>
<tr>
<td style="text-align: left;">By 24 hours</td>
<td style="text-align: left;">Issue status update; maintain enhanced monitoring; preserve all decisions and notify relevant authorities/affected parties only as legal/privacy advice and verified facts require.</td>
<td style="text-align: left;"><p>Comms + Legal/Privacy;</p>
<p>executive approval for external statements.</p></td>
<td style="text-align: left;"><p>Update log, notifications,</p>
<p>monitoring plan, next review time.</p></td>
</tr>
</tbody>
</table>

### 

### 3.3 Difficult decisions and trade-offs

**Decision A**: **Containment versus evidence preservation.** The preferred sequence is to preserve volatile evidence quickly where it is safe and feasible, then isolate. However, if the active encryption or lateral movement is continuing, immediate isolation takes priority because each minute may increase damage. The responder record the exact time, interface or control used, system state observed, approval or emergency authority, and any evidence that could not be collected. CISA recommends isolating impacted systems and preserving system images, memory, logs, and relevant artifacts where possible (CISA et al., 2023).

**Decision B:** **Restoring examination access while backup safety is uncertain**. Do not reopen the portal from a backup that has not been validated, even under management pressure. A restored service could reintroduce malware, expose learner information, or corrupt assessment records. The LMS owner should assess safe alternatives (postponement, rescheduling, or a separately approved clean environment) and the executive sponsor should decide the academic arrangement. Restore only after an isolated test demonstrates readability, integrity, malware checks, dependency safety, and monitoring readiness.

Immediate isolation is necessary when active encryption, suspicious lateral movement, command-and-control activity, or imminent backup destruction is observed. If an isolation action removes volatile evidence or interrupts service, the log must record the reason, approver, time, system affected, likely evidence loss, business impact, and follow-up collection method.

### 3.4 Evidence register and custody

<table>
<colgroup>
<col style="width: 10%" />
<col style="width: 9%" />
<col style="width: 21%" />
<col style="width: 9%" />
<col style="width: 11%" />
<col style="width: 12%" />
<col style="width: 13%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Evidence ID</strong></th>
<th style="text-align: left;"><strong>Source</strong></th>
<th style="text-align: left;"><p><strong>Proposed collection</strong></p>
<p><strong>method</strong></p></th>
<th style="text-align: left;"><strong>Collector</strong></th>
<th style="text-align: left;"><strong>Date/time (WAT)</strong></th>
<th style="text-align: left;"><p><strong>Integrity</strong></p>
<p><strong>check</strong></p></th>
<th style="text-align: left;"><strong>Secure storage</strong></th>
<th style="text-align: left;"><p><strong>Custody</strong></p>
<p><strong>transfers</strong></p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">EV-01</td>
<td style="text-align: left;">FIN-PC07 endpoint; E01/E06</td>
<td style="text-align: left;"><p>Planned: photograph</p>
<p>screen/note; collect EDR</p>
<p>telemetry; forensic image</p>
<p>and memory capture if</p>
<p>feasible using approved</p>
<p>tools.</p></td>
<td style="text-align: left;">Forensics Lead</td>
<td style="text-align: left;">Day 0, after 08:45 WAT; exact time to be recorded at collection.</td>
<td style="text-align: left;"><p>Hash acquired image/copy with approved algorithm; record tool/version. Not yet</p>
<p>collected.</p></td>
<td style="text-align: left;"><p>Restricted encrypted evidence repository; read-only master; working copy</p>
<p>separate.</p></td>
<td style="text-align: left;">Collector Forensics custodian; every transfer signed/time-stamped.</td>
</tr>
<tr>
<td style="text-align: left;">EV-02</td>
<td style="text-align: left;">Email and attachment; E01</td>
<td style="text-align: left;"><p>Planned: export original</p>
<p>message with headers</p>
<p>and attachment; preserve</p>
<p>mailbox audit and</p>
<p>attachment metadata.</p></td>
<td style="text-align: left;">M365 Admin with Forensics oversight</td>
<td style="text-align: left;">Day 0; exact collection time to be recorded.</td>
<td style="text-align: left;">Hash attachment and exported message package after acquisition; no hash asserted now.</td>
<td style="text-align: left;">Restricted evidence repository; access limited to IR/legal as needed.</td>
<td style="text-align: left;"><p>Collector → Forensics custodian; log any legal</p>
<p>review.</p></td>
</tr>
<tr>
<td style="text-align: left;">EV-03</td>
<td style="text-align: left;">Microsoft 365 sign-in/audit logs; E02</td>
<td style="text-align: left;"><p>Planned: export relevant</p>
<p>sign-in, MFA, audit,</p>
<p>device and session</p>
<p>records for the finance</p>
<p>account and privileged</p>
<p>users.</p></td>
<td style="text-align: left;">Identity Admin / Analyst</td>
<td style="text-align: left;">Day 0; preserve retention-sensitive logs promptly.</td>
<td style="text-align: left;">Record export query, time range, source tenant, export time, and hash of export.</td>
<td style="text-align: left;">Restricted encrypted repository; audit access.</td>
<td style="text-align: left;">Identity Admin → Forensics custodian; transfer logged.</td>
</tr>
<tr>
<td style="text-align: left;">EV-04</td>
<td style="text-align: left;">Windows logs on FS01/BAK01; E03/E06</td>
<td style="text-align: left;"><p>Planned: export</p>
<p>Security/System logs and</p>
<p>relevant service/backup</p>
<p>logs; preserve original</p>
<p>timestamps and time</p>
<p>zone context.</p></td>
<td style="text-align: left;">Forensics Lead with IT Ops</td>
<td style="text-align: left;">Day 0; before log rollover or rebuild.</td>
<td style="text-align: left;"><p>Hash exported files; document system clock/time offset and</p>
<p>export method.</p></td>
<td style="text-align: left;">Restricted repository; read-only master copy.</td>
<td style="text-align: left;">IT Ops/collector → Forensics custodian.</td>
</tr>
<tr>
<td style="text-align: left;">EV-05</td>
<td style="text-align: left;">Proxy/firewall/DNS records; E04</td>
<td style="text-align: left;"><p>Planned: export</p>
<p>connection records for</p>
<p>FIN-PC07 and unfamiliar</p>
<p>destination, including</p>
<p>volume and timestamps.</p></td>
<td style="text-align: left;">Network/IT Ops + Analyst</td>
<td style="text-align: left;">Day 0; priority due to possible retention limits.</td>
<td style="text-align: left;"><p>Hash export; record query/filter and system</p>
<p>source.</p></td>
<td style="text-align: left;"><p>Restricted repository; do</p>
<p>not send</p>
<p>sensitive logs</p>
<p>through unapproved email.</p></td>
<td style="text-align: left;">Network administrator → Forensics custodian.</td>
</tr>
<tr>
<td style="text-align: left;">EV-06</td>
<td style="text-align: left;">Ransom note and sample .locked files; E06</td>
<td style="text-align: left;"><p>Planned: photograph</p>
<p>note, copy note and</p>
<p>representative files to</p>
<p>isolated media; do not</p>
<p>execute samples.</p></td>
<td style="text-align: left;">Forensics Lead</td>
<td style="text-align: left;">Day 0, before cleanup.</td>
<td style="text-align: left;"><p>Hash each acquired file; retain original path and</p>
<p>timestamps.</p></td>
<td style="text-align: left;"><p>Malware/evidence quarantine with restricted</p>
<p>access.</p></td>
<td style="text-align: left;">Collector → Forensics custodian; record all analysis copies.</td>
</tr>
<tr>
<td style="text-align: left;">EV-07</td>
<td style="text-align: left;"><p>Backup catalogue, job</p>
<p>Reports</p>
<p>and snapshot error; E05</p></td>
<td style="text-align: left;"><p>Planned: export backup</p>
<p>job status, access/audit</p>
<p>logs, catalogue and test</p>
<p>restore error; isolate</p>
<p>copies from production.</p></td>
<td style="text-align: left;">Backup Administrator with Forensics oversight</td>
<td style="text-align: left;">Day 0, before restore or retention changes.</td>
<td style="text-align: left;"><p>Hash exports; record backup IDs,</p>
<p>timestamps, test environment and outcome.</p></td>
<td style="text-align: left;"><p>Restricted recovery/evidence repository; no production</p>
<p>restore without approval.</p></td>
<td style="text-align: left;">Backup admin → Forensics custodian.</td>
</tr>
</tbody>
</table>

**Access and custody rules:** only named CSIRT, legal/privacy, and authorised external responders may access evidence on a need-to-know basis. Store master evidence encrypted and read-only; perform analysis on working copies. Use unique evidence IDs, tamper-evident packaging where physical media is used, and a custody log with date/time, sender, receiver, purpose, seal/hash verification, and signatures. Preserve original timestamps and record clock offsets. Any failed collection, missing log, or custody exception must be documented.

### 3.5 Eradication, recovery order, and acceptance criteria

1.  **Eradication plan:** identify the initial access vector by reviewing the payroll email and endpoint execution chain; remove malicious files, services, scheduled tasks, autoruns, remote tools and other persistence only after relevant evidence is preserved. Patch the exploited weakness if identified, disable exposed services, remove unauthorised rules and tokens, and rebuild compromised endpoints/servers from known-good images when confidence in cleaning is insufficient. Rotate potentially compromised credentials and revoke sessions, including privileged and service accounts. Confirm least privilege, MFA for privileged/cloud identities, and separate backup credentials.

2.  **Scope checks:** compare endpoint EDR findings with central logs; review successful/failed logons, new accounts, privileged group changes, remote service creation, scheduled tasks, suspicious PowerShell/process activity, new OAuth/app consent, mailbox forwarding rules, unusual cloud storage access, and network traffic to suspicious destinations. Expand containment if additional systems show related indicators.

3.  **Recommended restoration order:** (1) identity and administrative control plane from known-good state; (2) backup management and clean recovery environment; (3) FS01 data after validation, because LMS depends on it; (4) LMS01 application and its content; (5) FIN-PC07 rebuilt as a clean workstation; (6) other services after scope review. This order is conditional on dependency testing and the business owner’s priorities.

4.  **Recovery targets:** critical identity and backup-control functions target recovery within 8 hours after a clean environment is available; minimum learning portal service target within 24 hours after a clean restore is validated; full service target within 72 hours if backups and application dependencies pass. These are planning targets, not guarantees. Proposed RPO: up to 3 days of data loss may be possible if the only confirmed disconnected backup is from Day −3 at 17:00; the actual acceptable loss must be approved by management and academic/finance owners. No loss of assessment submissions after the last verified checkpoint should be accepted without explicit business approval and learner communication.

5.  **Backup selection and validation:** do not trust a 'success' job report alone (E05). Inventory the disconnected Day −3 backup and network backups; review access history for compromise; restore each candidate in an isolated network; verify file readability, expected counts and timestamps, malware scan results, system integrity, application dependencies, and sample learner/finance records against trusted references. The unreadable snapshot in the tabletop scenario must be preserved as evidence and treated as a failed candidate until independently validated.

6.  **Recovery acceptance criteria:** (1) selected restore point is documented and approved; (2) no unresolved critical indicators remain on the recovery environment; (3) endpoint/server/identity logs and security monitoring are enabled; (4) privileged credentials and sessions are secured; (5) file integrity and application functions pass owner-defined tests; (6) LMS owner tests access to materials and a non-production assessment submission; (7) backup is protected from production compromise; (8) enhanced monitoring runs for at least 24 hours without recurrence; and (9) business owner and IM sign a return-

## Task 4 — Communication and escalation 

### 4.1 Communication matrix

<table>
<colgroup>
<col style="width: 14%" />
<col style="width: 19%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Stakeholder</strong></th>
<th style="text-align: left;"><strong>Trigger</strong></th>
<th style="text-align: left;"><strong>Message owner</strong></th>
<th style="text-align: left;"><strong>Channel / alternative</strong></th>
<th style="text-align: left;"><strong>Approver</strong></th>
<th style="text-align: left;"><strong>Frequency</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;"><p>Executive sponsor /</p>
<p>management</p></td>
<td style="text-align: left;"><p>Critical declaration; every major decision; material scope</p>
<p>change.</p></td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;">Phone bridge / direct call; secure approved channel after verification.</td>
<td style="text-align: left;"><p>Executive sponsor for business</p>
<p>decisions; IM for</p>
<p>internal status.</p></td>
<td style="text-align: left;"><p>Every 30 minutes during first 2</p>
<p>hours; then at</p>
<p>east every 2 hours</p>
<p>or on material</p>
<p>change.</p></td>
</tr>
<tr>
<td style="text-align: left;">IT and security team</td>
<td style="text-align: left;"><p>Immediate activation; containment changes; new indicators;</p>
<p>recovery actions.</p></td>
<td style="text-align: left;">Incident Manager / Security Analyst</td>
<td style="text-align: left;"><p>Staff phones and verified out-of</p>
<p>band bridge;</p>
<p>ticket/log stored</p>
<p>offline if needed.</p></td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;"><p>Continuous coordination; written action log</p>
<p>after each major</p>
<p>action.</p></td>
</tr>
<tr>
<td style="text-align: left;">Learners (1,800)</td>
<td style="text-align: left;"><p>Exam status decision; portal/material access changes; verified</p>
<p>impact requiring user action.</p></td>
<td style="text-align: left;">Communications Lead</td>
<td style="text-align: left;"><p>SMS, verified</p>
<p>official social</p>
<p>channel,</p>
<p>telephone/website banner only if</p>
<p>trusted; alternative to email.</p></td>
<td style="text-align: left;"><p>Executive sponsor; legal/privacy consulted for</p>
<p>breach-related wording.</p></td>
<td style="text-align: left;"><p>Initial holding</p>
<p>notice promptly;</p>
<p>update by 10:00</p>
<p>WAT, then at each decision or at least every 2 hours.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Staff and</p>
<p>faculty</p></td>
<td style="text-align: left;">Do not use affected file shares; reporting instructions; exam/teaching workarounds.</td>
<td style="text-align: left;">Communications Lead</td>
<td style="text-align: left;"><p>Staff phones/SMS</p>
<p>and verified</p>
<p>briefing; avoid</p>
<p>corporate email</p>
<p>until trusted.</p></td>
<td style="text-align: left;"><p>Incident Manager for operational</p>
<p>directions; executive sponsor for policy</p>
<p>statements.</p></td>
<td style="text-align: left;"><p>At activation and</p>
<p>every 60 minutes during first phase.</p></td>
</tr>
<tr>
<td style="text-align: left;">Legal/privacy adviser</td>
<td style="text-align: left;"><p>Possible data</p>
<p>exfiltration, identity</p>
<p>compromise, external</p>
<p>threat claim, or</p>
<p>evidence of affected</p>
<p>personal data.</p></td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;"><p>Phone call using</p>
<p>verified number;</p>
<p>secure approved</p>
<p>channel for</p>
<p>documents.</p></td>
<td style="text-align: left;">Legal/privacy lead advises; executive sponsor approves formal notifications.</td>
<td style="text-align: left;"><p>Immediate initial</p>
<p>consult; updates</p>
<p>as evidence</p>
<p>changes and</p>
<p>before external</p>
<p>notification.</p></td>
</tr>
<tr>
<td style="text-align: left;">Cloud/email/IT service provider</td>
<td style="text-align: left;"><p>Evidence indicates</p>
<p>Compromised</p>
<p>identity/cloud tenant,</p>
<p>suspicious upload, or</p>
<p>need for forensic</p>
<p>assistance.</p></td>
<td style="text-align: left;"><p>IT Operations</p>
<p>Lead</p></td>
<td style="text-align: left;"><p>Verified provider</p>
<p>emergency portal/phone number; secure</p>
<p>evidence transfer.</p></td>
<td style="text-align: left;"><p>Incident Manager approves</p>
<p>technical request; legal/privacy reviews data</p>
<p>sharing</p>
<p>implications.</p></td>
<td style="text-align: left;"><p>At initial</p>
<p>assessment;</p>
<p>updates at</p>
<p>material findings</p>
<p>and provider</p>
<p>milestones.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Law enforcement /</p>
<p>competent authority</p></td>
<td style="text-align: left;"><p>Credible criminal</p>
<p>activity, extortion,</p>
<p>significant</p>
<p>compromise, or legal</p>
<p>advice recommends</p>
<p>contact.</p></td>
<td style="text-align: left;">Legal/privacy adviser + Incident Manager</td>
<td style="text-align: left;"><p>Verified official</p>
<p>contact route;</p>
<p>preserve reference/case number.</p></td>
<td style="text-align: left;">Executive sponsor with legal advice.</td>
<td style="text-align: left;"><p>As advised by</p>
<p>legal/privacy and</p>
<p>relevant jurisdiction; document time</p>
<p>and recipient.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Media / public</p>
<p>enquiries</p></td>
<td style="text-align: left;"><p>Journalist enquiry or</p>
<p>public misinformation; confirmed need for</p>
<p>public statement.</p></td>
<td style="text-align: left;">Communications Lead</td>
<td style="text-align: left;"><p>Approved spokesperson; single holding</p>
<p>statement; no staff speculation.</p></td>
<td style="text-align: left;"><p>Executive sponsor and legal/privacy</p>
<p>adviser.</p></td>
<td style="text-align: left;"><p>Acknowledge promptly through</p>
<p>spokesperson; update only when verified.</p></td>
</tr>
</tbody>
</table>

### 

### 4.2 Executive briefing 

At 08:45 WAT on Monday, Northbridge Skills Institute declared a Critical suspected ransomware incident. Confirmed observation include mass file changes on FIN-PC07, .locked files and a ransom note on FS01, unusual remote administrator logons by svc_backup to FS01 and BAK01, and a 1.2 GB HTTPS upload from FIN-PC07 to unfamiliar cloud storage (E03, E04, E06). Learners cannot access materials or submit assessments through the portal, and an online examination for 100 learners is scheduled for 11:00 (E07 and scenario context). The malware family, attacker identity, transferred content, and extent of any personal-data exposure remain unconfirmed. Backup job report show success, but backup integrity and recoverability have not been tested; the last disconnected backup is from Day −3 at 17:00 (E05 and scenario context).

The CSIRT isolated affected systems, restricting backup access, preserving endpoint, identity, server and network evidence, and investigating whether credentials or additional systems are compromised. Corporate email is not yet trusted; coordination is using verified staff-phone channels. Approval is requested to engage external incident-response support and to postpone or reschedule the examination if a clean, validated service cannot be demonstrated. No unverified backup will be restored solely to meet the examination time. Legal/privacy advisers are assessing applicable notification duties. Next management update: 09:15 WAT, or immediately if scope materially changes.

### 4.3 Learner notice 

Northbridge Skills Institute is investigating a cybersecurity incident affecting access to learning materials and assessment submission through the learning portal. The online examination scheduled for 11:00 WAT is under urgent review; please do not assume it will proceed until you receive a confirmed update through an official Institute channel. We are working to protect our systems and validate safe recovery options. At this stage, the Institute has not confirmed that learner personal information was accessed or stolen. Please do not open unexpected attachments claiming to be examination updates, share passwords or verification codes, or circulate unverified screenshots and claims. Keep your contact details available and follow only messages published by the authorised Institute communications team. If you cannot access learning materials, record the issue and wait for further instructions rather than repeatedly attempting to upload work. The next update will be issued by 10:00 WAT, or sooner if a decision is made.

### 4.4 Escalation and notification obligations

1.  Critical incident: immediate phone escalation to IM and executive sponsor; full CSIRT activation; notify legal/privacy adviser as soon as possible.

2.  Escalate to broader containment if encryption spreads, BAK01 is altered, privileged accounts are compromised, or new systems show related indicators.

3.  Escalate to legal/privacy if logs suggest personal data access/exfiltration, if an extortion actor claims possession of records, or if contractual/regulatory duties may apply.

4.  Operational notices (service disruption, exam status, password-reset instruction) are not the same as formal breach notifications. Formal notifications must be based on verified facts and legal analysis.

The scenario does not explicitly identify the governing jurisdiction or establish that personal data was breached. Legal/privacy advisers should confirm the data controller, locations of affected individuals, relevant Nigerian data-protection requirements and any other applicable law, contractual terms, sector rules, and regulator/individual notification thresholds and deadlines. They should document the legal basis, trigger date, required recipient, deadline, content, approval and proof of delivery. No fixed statutory deadline is asserted here because jurisdiction and the legal trigger must first be verified.

## Task 5 — Tabletop exercise and improvement plan 

### 5.1 Exercise design

**Exercise title:** Northbridge ransomware tabletop.

**Duration:** 60 minutes.

**Format:** facilitated discussion; no live systems are changed.

**Objectives:** (1) To validate escalation and out-of-band communications; (2) To test the balance between containment and evidence preservation; (3) To make a defensible examination and recovery decision under pressure; (4) To assess response to a possible data-extortion claim; and (5) To convert gaps into owned, measurable improvements.

**Participants/roles:** Incident Manager, Security Analyst, Forensics Lead, IT Operations Lead, LMS/Business Owner, Legal/Privacy Adviser, Communications Lead, Executive Sponsor. The individual simulation records each role's viewpoint and the final decision.

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 42%" />
<col style="width: 48%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Minute</strong></th>
<th style="text-align: left;"><strong>Agenda / inject</strong></th>
<th style="text-align: left;"><strong>Expected action and decision owner</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">0–5</td>
<td style="text-align: left;">Brief scenario, objectives, rules, roles and initial evidence E01–E08.</td>
<td style="text-align: left;">Incident Manager confirm Critical classification, evidence limitations, staff-phone bridge and incident log.</td>
</tr>
<tr>
<td style="text-align: left;">5–10</td>
<td style="text-align: left;">Initial response: identify first containment actions and evidence priorities.</td>
<td style="text-align: left;">IT Ops isolates FIN-PC07/affected FS01 paths; Forensics prioritises volatile and retention-limited evidence.</td>
</tr>
<tr>
<td style="text-align: left;">10–20</td>
<td style="text-align: left;">Inject 1: management asks to reopen portal before 11:00 even if latest backup is unverified.</td>
<td style="text-align: left;"><p>Executive sponsor/LMS owner decline unsafe</p>
<p>restoration; communicate exam under review and assess alternatives.</p></td>
</tr>
<tr>
<td style="text-align: left;">20–30</td>
<td style="text-align: left;">Inject 2: attacker claims all 1,800 learner records and threatens publication in 12 hours; screenshot authenticity unknown.</td>
<td style="text-align: left;"><p>Analyst validates indicators; Forensics preserves</p>
<p>screenshot and metadata; Legal/Privacy starts exposure assessment; Comms avoids confirming theft.</p></td>
</tr>
<tr>
<td style="text-align: left;">30–35</td>
<td style="text-align: left;">Inject 3: test restoration of latest network backup fails with unreadable snapshot error.</td>
<td style="text-align: left;">IT Ops records failure, preserves logs, stops using that candidate and tests disconnected backup in isolation.</td>
</tr>
<tr>
<td style="text-align: left;">35–45</td>
<td style="text-align: left;">Inject 4: social post claims exam cancelled; journalist asks whether learner information was exposed.</td>
<td style="text-align: left;">Comms issues approved correction/holding statement; legal/privacy reviews wording; next update time is clear.</td>
</tr>
<tr>
<td style="text-align: left;">45–52</td>
<td style="text-align: left;">Inject 5 (added): EDR finds a suspicious remote-admin logon on a second server using a privileged account shortly before the file encryption.</td>
<td style="text-align: left;">Analyst expands scope; IT Ops contains second server if needed; Identity Admin revokes sessions and rotates credentials; IM raises/maintains Critical.</td>
</tr>
<tr>
<td style="text-align: left;">52–57</td>
<td style="text-align: left;">Review decisions against success criteria; identify blockers and resource needs.</td>
<td style="text-align: left;">Incident Manager scores criteria and assigns corrective actions.</td>
</tr>
<tr>
<td style="text-align: left;">57–60</td>
<td style="text-align: left;">Hotwash, confirm owners, deadlines, and post-incident review date.</td>
<td style="text-align: left;">Incident Manager issues action log; formal review due within 14 days of incident closure.</td>
</tr>
</tbody>
</table>

### 

### 5.2 Measurable success criteria

| **Criterion** | **Target** | **Simulated result** |
|:---|:---|:---|
| Activation and escalation | Incident Manager and executive sponsor reached within 10 minutes; all CSIRT roles contacted within 15 minutes using phone/out-of-band channel. | Met in simulation: phone tree used; contact list must be maintained off FS01. |
| Containment decision | FIN-PC07 isolated within 10 minutes of activation; backup access restricted within 20 minutes. | Met as planned; requires tested authority and clear network runbook. |
| Evidence discipline | At least four evidence items registered with collector, WAT time, integrity method, restricted storage and custody log; no invented hashes. | Met in plan; acquisition remains planned until performed. |
| Safe recovery | No production restore until a candidate passes isolated restore, integrity and malware checks and receives business-owner approval. | Met: unreadable network snapshot rejected; disconnected backup requires validation. |
| Communications | Approved learner holding notice and next update time issued within 20 minutes; no unsupported claim that data was stolen. | Met in simulation; one spokesperson and out-of-band channel used. |
| Improvement ownership | At least five corrective actions have named owner, target date and measurable completion evidence. | Met in plan below. |

### 5.3 Decision log

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 20%" />
<col style="width: 16%" />
<col style="width: 15%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Inject / time</strong></th>
<th style="text-align: left;"><strong>Decision</strong></th>
<th style="text-align: left;"><strong>Decision owner</strong></th>
<th style="text-align: left;"><strong>Rationale</strong></th>
<th style="text-align: left;"><strong>Communication</strong></th>
<th style="text-align: left;"><strong>Effect</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;"><p>Minute 10 —</p>
<p>unverified backup pressure</p></td>
<td style="text-align: left;"><p>Do not reopen LMS from unverified backup;</p>
<p>Prepare</p>
<p>postponement/reschedule option.</p></td>
<td style="text-align: left;">Executive Sponsor, advised by IM and LMS Owner.</td>
<td style="text-align: left;"><p>Availability deadline does not</p>
<p>outweigh risk of</p>
<p>reinfection or</p>
<p>assessment-data corruption.</p></td>
<td style="text-align: left;">Comms Lead issues exam-under-review notice; next update by 10:00 WAT.</td>
<td style="text-align: left;"><p>Avoids unsafe</p>
<p>restoration; may</p>
<p>cause short-term</p>
<p>academic disruption.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Minute 20 —</p>
<p>extortion claim</p></td>
<td style="text-align: left;"><p>Treat claim as unverified but serious; preserve</p>
<p>screenshot and metadata; expand data exposure</p>
<p>investigation.</p></td>
<td style="text-align: left;">Incident Manager and Legal/Privacy Adviser.</td>
<td style="text-align: left;"><p>Threat actor may</p>
<p>bluff or use</p>
<p>old/public data;</p>
<p>confirmation requires log and</p>
<p>data evidence.</p></td>
<td style="text-align: left;">Executive sponsor briefed; no public confirmation of theft.</td>
<td style="text-align: left;"><p>Keeps severity</p>
<p>Critical and avoids</p>
<p>unsupported claims.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Minute 35 —</p>
<p>backup restore failure</p></td>
<td style="text-align: left;"><p>Quarantine the failed</p>
<p>network backup</p>
<p>candidate; preserve error logs; test disconnected</p>
<p>backup in isolated</p>
<p>environment.</p></td>
<td style="text-align: left;">IT Operations Lead.</td>
<td style="text-align: left;"><p>Unreadable snapshot is not a</p>
<p>dependable recovery source;</p>
<p>testing it in</p>
<p>production risks further harm.</p></td>
<td style="text-align: left;">IM and LMS owner informed; recovery ETA remains provisional.</td>
<td style="text-align: left;"><p>Extends recovery</p>
<p>planning but reduces reinfection/corruption risk.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Minute 45 — social</p>
<p>post and journalist</p></td>
<td style="text-align: left;"><p>Use single approved</p>
<p>holding statement;</p>
<p>confirm only service</p>
<p>disruption and that data exposure is under</p>
<p>investigation.</p></td>
<td style="text-align: left;">Communications Lead, approved by Executive Sponsor and Legal/Privacy.</td>
<td style="text-align: left;"><p>Avoid contradictory statements and</p>
<p>Protect</p>
<p>investigation integrity.</p></td>
<td style="text-align: left;">Correct misinformation through verified official channel; direct media to spokesperson.</td>
<td style="text-align: left;"><p>Reduces confusion</p>
<p>and limits</p>
<p>reputational harm.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Minute 48 — new</p>
<p>suspicious admin logon on second server</p></td>
<td style="text-align: left;"><p>Expand scope; isolate</p>
<p>second server if malicious activity is credible; revoke privileged sessions and</p>
<p>rotate credentials after</p>
<p>preserving relevant logs.</p></td>
<td style="text-align: left;">Incident Manager authorises; IT Ops and Identity Admin execute.</td>
<td style="text-align: left;"><p>New indicator</p>
<p>suggests possible lateral movement;</p>
<p>containment takes</p>
<p>priority over</p>
<p>convenience.</p></td>
<td style="text-align: left;"><p>Update management and</p>
<p>technical team;</p>
<p>learner notice only if service impact</p>
<p>changes.</p></td>
<td style="text-align: left;"><p>Wider investigation;</p>
<p>maintain Critical</p>
<p>classification.</p></td>
</tr>
<tr>
<td style="text-align: left;"><p>Minute 55 —</p>
<p>decision on service return</p></td>
<td style="text-align: left;"><p>Keep portal offline until</p>
<p>clean restore and</p>
<p>functional acceptance</p>
<p>criteria pass; activate</p>
<p>academic continuity</p>
<p>arrangements.</p></td>
<td style="text-align: left;"><p>LMS Owner</p>
<p>responsible; Executive Sponsor accountable.</p></td>
<td style="text-align: left;"><p>No validated</p>
<p>recovery point or</p>
<p>clean state yet.</p></td>
<td style="text-align: left;">Learners receive revised status and next update time.</td>
<td style="text-align: left;"><p>Protects integrity;</p>
<p>recovery timeline</p>
<p>may lengthen.</p></td>
</tr>
</tbody>
</table>

### 5.4 Evaluation and Improvement plan

The simulation shows that the strongest controls are clear authority to isolate, out-of-band communication, evidence discipline, and refusal to restore from an unverified backup. The main weaknesses are dependence on FS01 for contact details, incomplete server EDR coverage, untested backups, limited internal IT staffing, and uncertain recovery targets. These weaknesses are consistent with the evidence pack and should be addressed before a real incident.

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 28%" />
<col style="width: 16%" />
<col style="width: 17%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr>
<th style="text-align: left;"><strong>Priority</strong></th>
<th style="text-align: left;"><strong>Improvement/action</strong></th>
<th style="text-align: left;"><strong>Owner</strong></th>
<th style="text-align: left;"><strong>Target completion</strong></th>
<th style="text-align: left;"><strong>Measurable evidence</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: left;">P1 — Critical</td>
<td style="text-align: left;">Create offline/immutable backup tier and perform isolated restore test for FS01 and LMS01; separate backup credentials.</td>
<td style="text-align: left;">IT Operations Lead</td>
<td style="text-align: left;">Within 30 days</td>
<td style="text-align: left;"><p>Successful signed restore report; malware/integrity</p>
<p>results; documented</p>
<p>RTO/RPO; backup access</p>
<p>audit.</p></td>
</tr>
<tr>
<td style="text-align: left;">P1 — Critical</td>
<td style="text-align: left;">Publish contact list and call tree outside FS01/email; run contact test.</td>
<td style="text-align: left;">Communications Lead</td>
<td style="text-align: left;">Within 7 days</td>
<td style="text-align: left;">Printed/encrypted offline list approved; ≥95% of contacts reached in 15 minutes.</td>
</tr>
<tr>
<td style="text-align: left;">P1 — Critical</td>
<td style="text-align: left;">Review svc_backup permissions, remove interactive logon where not needed, rotate credentials and separate backup administration.</td>
<td style="text-align: left;">Identity Admin + IT Ops</td>
<td style="text-align: left;">Within 14 days</td>
<td style="text-align: left;"><p>Access review and test logs show least privilege;</p>
<p>emergency reset runbook</p>
<p>approved.</p></td>
</tr>
<tr>
<td style="text-align: left;">P1 — High</td>
<td style="text-align: left;"><p>Complete server EDR/logging</p>
<p>coverage for FS01, BAK01 and</p>
<p>LMS01; centralise identity, proxy and backup logs.</p></td>
<td style="text-align: left;">Security Analyst</td>
<td style="text-align: left;">Within 45 days</td>
<td style="text-align: left;">Coverage report ≥95% of in-scope servers; test alert for mass file changes and unusual admin logon.</td>
</tr>
<tr>
<td style="text-align: left;">P2 — High</td>
<td style="text-align: left;"><p>Contract or establish on-call</p>
<p>external incident-response support and test access path.</p></td>
<td style="text-align: left;">Executive Sponsor</td>
<td style="text-align: left;">Within 30 days</td>
<td style="text-align: left;"><p>Signed scope/SLA; call-out</p>
<p>exercise completed; evidence-transfer process documented.</p></td>
</tr>
<tr>
<td style="text-align: left;">P2 — High</td>
<td style="text-align: left;"><p>Create tested ransomware and</p>
<p>identity-compromise playbooks; train CSIRT in evidence collection and isolation.</p></td>
<td style="text-align: left;">Incident Manager</td>
<td style="text-align: left;">Within 45 days</td>
<td style="text-align: left;"><p>Tabletop completed; ≥90% of</p>
<p>assigned actions completed within exercise targets.</p></td>
</tr>
<tr>
<td style="text-align: left;">P2 — Medium</td>
<td style="text-align: left;"><p>Map LMS/FS01/identity/backup</p>
<p>dependencies and approve</p>
<p>business recovery priorities, RTO and RPO.</p></td>
<td style="text-align: left;">LMS Owner + IT Ops</td>
<td style="text-align: left;">Within 30 days</td>
<td style="text-align: left;"><p>Signed dependency map and business-approved recovery</p>
<p>targets.</p></td>
</tr>
<tr>
<td style="text-align: left;">P2 — Medium</td>
<td style="text-align: left;"><p>Run learner/staff phishing</p>
<p>awareness and incident reporting drill.</p></td>
<td style="text-align: left;">Training/HR + Security Analyst</td>
<td style="text-align: left;">Within 60 days</td>
<td style="text-align: left;">≥95% training completion; exercise records reporting rate and time to escalation.</td>
</tr>
</tbody>
</table>

**Post-incident review deadline:** within 14 calendar days after the real incident is formally closed, consistent with the teaching slides' lessons-learned guidance. The Incident Manager chairs the review; the executive sponsor approves the final report. Each action owner provides evidence of completion, while the IM tracks progress and closes actions only after verification. Unfinished high-priority actions remain on the risk register with an approved due date.

## Task 6 — Case study analysis and critical reflection 

### Healthcare ransomware case: analysis 

The teaching case describes a 2,500-employee healthcare organisation struck by a Ryuk ransomware variant after an employee opened a malicious phishing attachment. The malware established persistence and moved laterally for 72 hours before encryption. EDR alerts triggered response on Day 4; the team isolated network segments, quarantined affected systems and verified offline backups. Forensic analysis and malware removal followed, systems were rebuilt from clean backups, controls were strengthened, and service restoration was phased over Days 5–7. A review occurred on Day 14. The reported outcomes were no ransom payment, critical systems restored within 72 hours, no patient-data exfiltration confirmed, timely regulatory notifications, and seven days to full restoration (ICDFA, n.d.).

Three strengths stand out. Firstly, the team activated after EDR alerts and isolated affected network segments, limiting further spread. Secondly, offline backups were available and verified, enabling recovery without paying ransom. Thirdly, the organisation used forensic analysis, rebuilt system from clean backups, strengthened controls, and conducted a lessons-learned review. These actions reflect CISA guidance to isolate affected systems, preserve evidence, restore from clean backups, and improve the plan after an incident (CISA et al., 2023).

Two limitations or unresolved issues remain. The 72-hour period of stealthy lateral movement suggests that initial detection and threat hunting were not fast enough; the case does not explain why earlier telemetry failed to identify activity. Again, “no patient data exfiltration confirmed” is not proof that no data left the organisation. The case summary does not specify which egress logs, endpoint artifact, cloud record, or forensic analyses supported that conclusion, nor does it detail recovery-point loss or validation of all restored records.

I would transfer two changes to Northbridge. First, maintain offline or immutable backups and test restoration regularly; this is directly relevant because Northbridge's network backups are not immutable and neither backup route has been tested in 90 days (E05). Secondly, improve server monitoring and network segmentation, including alerting on unusual privileged logons and large outbound transfers; Northbridge has incomplete server EDR coverage and suspicious svc_backup access (E03). Critical systems restored within 72 hours means the most essential services became available within that period; therefore, full restoration over seven days means all affected services and supporting operations were not fully returned until Day 7. These are different milestones, not contradictory figures. Before claiming that no patient or learner data was stolen, investigators need correlated proxy/firewall/DNS logs, endpoint process and file-access telemetry, cloud destination records, identity logs, forensic review of relevant systems, as well as documented limits in visibility. After the tabletop, I would revise any assumed recovery promise: the portal must remain offline until a backup and clean environment pass validation, even if that requires a longer examination delay.

## Conclusion

Northbridge should treat the event as a Critical suspected ransomware incident, act rapidly to contain encryption and protect backups, preserve evidence, and communicate only what is supported by facts. The examination deadline is a major business concern but does not justify restoring from an unverified backup. A coordinated CSIRT, accessible contact list, tested recovery capability, out-of-band communications, and measurable post-incident actions will reduce the chance and impact of recurrence.

## References

8.  Cybersecurity and Infrastructure Security Agency, Multi-State Information Sharing and Analysis Center, National Security Agency, and Federal Bureau of Investigation. (2023). \#StopRansomware Guide. <https://www.cisa.gov/stopransomware/ransomware-guide>.

9.  International Cybersecurity and Digital Forensics Academy (ICDFA). (n.d.). Incident Response Planning: GRC105, Week 20 teaching deck (slides 1–18). Course material supplied with the assignment.

10. International Cybersecurity and Digital Forensics Academy (ICDFA). (n.d.). Incident Response Planning Assignment: GRC105 Incident Management and Business Continuity, Week 20. Assignment brief supplied by the course.

11. Nelson, A., Rekhi, S., Souppaya, M., & Scarfone, K. (2025). Incident Response Recommendations and Considerations for Cybersecurity Risk Management: A CSF 2.0 Community Profile (NIST SP 800-61 Rev. 3). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-61r3
