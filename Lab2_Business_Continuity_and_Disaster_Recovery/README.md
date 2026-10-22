# Business Continuity and Disaster Recovery Plan

## Northbridge Skills Institute: Flood and Power-Failure Scenario

[![Course](https://img.shields.io/badge/Course-GRC205-17365D)](#project-information)
[![Focus](https://img.shields.io/badge/Focus-Business%20Continuity%20%26%20Disaster%20Recovery-8B1E3F)](#project-overview)
[![NIST](https://img.shields.io/badge/NIST-SP%20800--34%20Rev.%201-2E7D32)](#standards-alignment)
[![ISO](https://img.shields.io/badge/ISO-22301%3A2019-005A9C)](#standards-alignment)
[![Status](https://img.shields.io/badge/Status-Academic%20Project-6F42C1)](#academic-use-notice)

A structured Business Continuity and Disaster Recovery (BC/DR) project for a simulated 72-hour site outage caused by flooding and power failure at Northbridge Skills Institute. The analysis connects business impact, recovery objectives, backup integrity, continuity workarounds, technical recovery sequencing, governance, testing, and measurable improvement.

> [!IMPORTANT]
> This repository documents is an academic scenario. It is not a production continuity plan, evidence of tested supplier capability, or a claim of ISO 22301 certification.

## Project Information

| Field | Detail |
|---|---|
| **Author** | Mohammed Nazir |
| **Student ID** | 2025/GRC/2512799 |
| **Institution** | International Cybersecurity and Digital Forensics Academy |
| **Course** | GRC205: Incident Management and Business Continuity |
| **Assessment** | Business Continuity and Disaster Recovery Assignment |
| **Scenario** | Flood and power failure at Northbridge Skills Institute |
| **Submission date** | 23 October 2026 |

## Project Overview

At 08:00 WAT on Day 0, flooding and a power failure make the institute's main site and local systems unavailable for an estimated 72 hours. The scenario affects 1,800 learners, 90 staff, five critical business functions, and an 11:00 examination for 120 learners. Only two disaster-recovery technicians are available, while an alternate facility provides 25 workstations from 10:00.

The project assesses how the institute should maintain minimum acceptable services, validate recovery data, restore systems in dependency order, communicate with stakeholders, and govern residual risk.

## Business Functions in Scope

| ID | Business function | Critical deadline | Primary systems |
|---|---|---|---|
| **F1** | Teaching and assessment | Examination at 11:00 Day 0 | LMS01, DB01, AUTH01, network |
| **F2** | Fees and finance | Fee confirmation at 16:00 Day 0 | FIN01, DB01, AUTH01, network |
| **F3** | Admissions and registration | Admissions close at 18:00 Day 0 | REG01, DB01, AUTH01, network |
| **F4** | Payroll | Bank submission at 12:00 Day 1 | HR01, DB01, AUTH01, network |
| **F5** | Records and certificates | 48-hour service commitment | FS01, AUTH01, network |

## Key Findings

- **Estimated loss without recovery:** NGN 1,200,000 after eight hours and NGN 3,360,000 after 24 hours.
- **Immediate continuity concern:** 40 examination candidates require centre workstations, but the alternate facility has only 25.
- **Assessment critical path:** network, AUTH01, security and backup checks, DB01, then LMS01.
- **Earliest modelled LMS recovery:** 11:45 WAT, which is 45 minutes after the examination start.
- **Recommended annual strategy:** warm site, protected independent backups, and training/testing at NGN 2,100,000.
- **Available budget headroom:** NGN 900,000 within the NGN 3,000,000 ceiling.
- **Material limitation:** the warm option does not satisfy every proposed RTO and RPO. Workarounds, additional investment, or formal residual-risk acceptance are required.

## Recovery Objectives

| Function | Proposed RTO | Proposed RPO | Proposed MTD | Assessment |
|---|---:|---:|---:|---|
| **F1** | 1 hour for an acceptable assessment route; 4 hours technical LMS target | 15 minutes | 4 hours | Requires a continuity workaround because the baseline LMS recovery finishes at 11:45 |
| **F2** | 6 hours | 1 hour | 12 hours | Achievable if the DB01 backup chain is complete and valid |
| **F3** | 8 hours | 1 hour | 12 hours | Achievable with a controlled intake queue during disruption |
| **F4** | 16 hours | 1 hour | 24 hours | Leaves a buffer before the Day 1 payroll deadline |
| **F5** | 24 hours | 4 hours | 48 hours | RTO is achievable, but the available FS01 checkpoint misses the RPO |

## Backup and Recovery Gaps

| System | Latest checkpoint at 08:00 | Checkpoint age | Key issue |
|---|---|---:|---|
| **DB01** | 07:00 Day 0 incremental | 1 hour | Misses F1's 15-minute RPO and depends on a complete backup chain |
| **AUTH01** | 00:00 Day 0 snapshot | 8 hours | Exceeds every proposed RPO |
| **FS01** | 23:00 Day -1 full backup | 9 hours | Misses the four-hour RPO by five hours |
| **Disconnected full backup** | 17:00 Day -3 | About 39 hours | Independent fallback, but too old for the proposed RPOs |

The recommended design applies the **3-2-1 backup principle**, separates production and backup administrator identities, introduces offline or immutable protection, and requires witnessed restore testing. Offsite storage alone is not proof of recoverability. Recovery evidence must include chain completeness, integrity checks, access independence, measured restore time, permissions testing, transaction validation, and business-owner acceptance.

## Strategy Comparison

| Strategy | Base cost | Protected backups | Training and tests | Annual total | Trade-off |
|---|---:|---:|---:|---:|---|
| **Cold** | NGN 600,000 | NGN 400,000 | NGN 200,000 | **NGN 1,200,000** | Affordable, but 24–48-hour recovery is too slow for urgent deadlines |
| **Warm** | NGN 1,500,000 | NGN 400,000 | NGN 200,000 | **NGN 2,100,000** | Balanced option, but misses F1's one-hour service target and some RPOs |
| **Hot** | NGN 2,400,000 | NGN 400,000 | NGN 200,000 | **NGN 3,000,000** | Fastest option, but consumes the entire budget and leaves no contingency |

### Recommendation

Adopt the **warm-site strategy with protected independent backups and structured training/testing**. This option balances cost and recovery capability while preserving NGN 900,000 of budget headroom. Approval should be conditional on:

1. Witnessed restore tests that measure actual RTO and RPO performance.
2. Proof that production administrators cannot delete or alter protected backups.
3. Validated alternate-site power, network, accessibility, security, and capacity.
4. Approved continuity procedures for the examination and other deadline-driven services.
5. Documented executive acceptance or treatment of residual recovery gaps.

## Modelled Recovery Schedule

| Action | Technician | Start | Finish | Dependency |
|---|---:|---:|---:|---|
| Recovery network | 1 | 08:00 | 08:30 | None |
| AUTH01 restoration | 1 | 08:30 | 09:00 | Network |
| Security and backup checks | 1 | 09:00 | 09:30 | AUTH01 |
| FS01 restoration | 2 | 09:30 | 10:30 | AUTH01 and checks |
| DB01 restoration | 1 | 09:30 | 11:00 | Validated backup chain |
| LMS01 restoration | 1 | 11:00 | 11:45 | DB01 |
| FIN01 restoration | 2 | 11:00 | 11:30 | DB01 |
| REG01 restoration | 2 | 11:30 | 12:00 | DB01 |
| HR01 restoration | 2 | 12:00 | 12:45 | DB01 |

The modelled assessment critical path is **225 minutes**. All five functions are restored by 12:45, but technical restoration alone does not constitute recovery. Security, data, workflow, accessibility, and business-owner acceptance checks must pass before service reopening.

## Continuity Controls

### Teaching and Assessment

- Confirm safe premises, power, connectivity, invigilation, device readiness, and accessibility.
- Use approved learner cohorts or formal rescheduling when workstation capacity is insufficient.
- Verify identity, protect examination material, log exceptions, and preserve submissions.

### Fees and Finance

- Maintain a restricted transaction register using provider references, timestamps, and amounts.
- Require two-person review.
- Do not repeat payment instructions solely because local records are unavailable.
- Reconcile temporary records against provider reports after restoration.

### Admissions

- Use approved secure channels or numbered forms.
- Timestamp submissions, issue acknowledgements, assign case identifiers, and restrict access.
- Apply two-person checks when records are entered into restored systems.

### Payroll

- Use the last approved payroll file and a signed change log.
- Separate preparation from approval.
- Validate changes and perform duplicate-payment checks before bank submission.

### Records and Certificates

- Verify the requester's identity and authority.
- Log every request.
- Issue records only from verified sources with Records Manager approval.
- Defer requests when integrity cannot be demonstrated.

## Governance and Accountability

| Role | Primary responsibility |
|---|---|
| **Executive Sponsor** | Policy approval, activation authority, budget approval, and residual-risk acceptance |
| **BC/DR Coordinator** | Plan activation, coordination, situation reporting, and decision logging |
| **Incident Commander** | Operational priorities and cross-functional direction |
| **DR Lead** | Technical recovery sequencing, backup validation, and restore evidence |
| **Security/IR Lead** | Integrity checks, investigation, privileged-access review, and compromise assessment |
| **Facilities Lead** | Site safety, alternate-site readiness, and return-to-site approval inputs |
| **Business Service Owners** | Minimum-service definition, workflow validation, reconciliation, and service acceptance |
| **Communications Lead** | Approved staff, learner, supplier, regulator, and media communications |

## Testing and Improvement Programme

- **Monthly:** sample restores for DB01, AUTH01, and FS01.
- **Quarterly:** tabletop exercises covering flood, power, cyber, supplier, and staff-loss scenarios.
- **Semi-annually:** walkthroughs of manual procedures and communication trees.
- **Annually:** integrated warm-site recovery test.
- **After material changes or incidents:** targeted review and retesting.

### Priority Corrective Actions

| Priority | Action | Owner | Target |
|---|---|---|---:|
| **P1** | Separate production and backup administrator identities; enforce MFA and least privilege | Security Lead / IT Manager | 30 days |
| **P1** | Prove the DB01 recovery chain and last-known-good fallback | DR Lead | 30 days |
| **P1** | Approve an accessible examination continuity and capacity design | Academic Director | 14 days |
| **P2** | Increase AUTH01 and FS01 checkpoint frequency | System owners | 60 days |
| **P2** | Create controlled manual forms and reconciliation procedures for F2–F5 | Business leads | 21 days |
| **P2** | Validate warm-site SLA, power, network, capacity, and recovery timing | BC/DR Coordinator | 60 days |
| **P3** | Conduct an integrated BC/DR exercise and track findings to evidence-based closure | BC/DR Programme Manager | 90 days |

## Performance Measures

The project proposes the following measurable controls:

- At least **90% of critical services** meet approved RTOs during tests.
- **100% of critical systems** are tested annually, with DB01, AUTH01, and FS01 sampled monthly.
- At least **90% of corrective actions** close by their due date.
- No overdue P1 action remains open without signed risk acceptance.
- At least **95% of assigned role-holders** complete annual training, with a deputy identified for every critical role.
- **100% of tested critical systems** meet RPO or have a documented exception and approved risk treatment.
- **100% of plans** are reviewed annually and after material changes.

The provisional maturity rating is **Level 2: Developing/Repeatable**, with a target of **Level 3: Defined/Standardised within 12 months**.

## Standards Alignment

This academic project aligns its structure with:

- **NIST SP 800-34 Rev. 1**, covering contingency planning policy, BIA, preventive controls, recovery strategies, contingency planning, testing/training/exercises, and maintenance.
- **ISO 22301:2019**, covering organisational context, leadership, planning, support, operations, performance evaluation, and improvement.
- **ISO 22301:2019/Amd 1:2024**, considered in relation to climate-related organisational context.

> [!NOTE]
> The standards mapping is for educational Purposes. Organisations should obtain qualified assurance before claiming conformity or certification.

## Repository Structure

```text
.
├── README.md
└── docs/
   └── GRC205_BCDR_Assignment_Mohammed_Nazir_2512799.docx
|__References

```

## Academic Use Notice

This work is provided for educational and portfolio purposes. The organisation, systems, costs, recovery times, and incident conditions are part of a simulated assignment scenario. Anyone adapting this material for operational use should validate legal obligations, supplier contracts, recovery capability, site risks, staffing, data protection controls, and executive approval requirements.

## Author

**Mohammed Nazir**  
ICDFA Trainee, GRC Engineering  
Student ID: 2025/GRC/2512799

## References

See [`references/SOURCES.md`](references/SOURCES.md) for the principal public guidance listed for the assignment.
