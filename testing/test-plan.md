# Test Plan — Student Internship Process Tracking System

A document summarizing the project's overall testing strategy (one file per project), referencing
[feature-list](../design/feature-list.md), [user-journey](../design/user-journey.md),
[backlog](../requirements/backlog.md), and [acceptance-criteria](./acceptance-criteria.md) as
sources of truth. This project is still at the requirements/design stage **with no source code
yet**, so this test plan is written in advance to prepare before real development begins, without
being tied to any tech stack.

## 1. Scope

### In scope

Test all 10 features per [feature-list](../design/feature-list.md), every feature (features 1–9 =
Must have, feature 10 = Should have):

| # | Feature | MoSCoW |
|---|---|---|
| 1 | [Track internship process status](../design/feature-list.md) | Must have |
| 2 | [Propose a host company and request approval](../design/feature-list.md) | Must have |
| 3 | [Verify training eligibility](../design/feature-list.md) | Must have |
| 4 | [Manage the three internship acceptance documents](../design/feature-list.md) | Must have |
| 5 | [Pin host companies, plan routes, and assign supervising instructors](../design/feature-list.md) | Must have |
| 6 | [Score and record interview results during supervision](../design/feature-list.md) | Must have |
| 7 | [Confirm data entry with the existing core internship system](../design/feature-list.md) | Must have |
| 8 | [Internship completion and thank-you letter to the host company](../design/feature-list.md) | Must have |
| 9 | [Record and track problem cases during the internship](../design/feature-list.md) | Must have |
| 10 | [Notify proposal presentation and supervision schedules](../design/feature-list.md) | Should have |

This covers all of FR-01–FR-20, FR-22–FR-29, FR-31–FR-35 and NFR-01–NFR-07 (FR-21, FR-30 =
Deprecated since 2026-09-16, so they are no longer in the test scope — see details in
[backlog](../requirements/backlog.md)).

### Out of scope (per [spec, Section 2](../requirements/spec.md))

- Recording daily tasks during the internship, and host companies viewing progress — these are the
  responsibility of the existing "core internship system" **and are not tested in this plan** (this
  system only tests the self-declare integration point per FR-22–FR-23).
- Digital document signing / e-signature.
- Payment of compensation/benefits to intern students.
- Real API integration with the existing core internship system (still an unconfirmed assumption —
  see [Assumption 2](../requirements/spec.md)).

## 2. Types of Testing

### 2.1 Functional Testing (per FR group)

| FR group (per spec) | Related features | Type of testing |
|---|---|---|
| Group A (FR-01–FR-02) | Feature 1 | Functional Testing — status display/dashboard, filtering |
| Group B (FR-03–FR-07) | Feature 2 | Functional Testing — approval/loop workflow (state transition) |
| Group C (FR-08–FR-10) | Feature 3 | Functional Testing — criterion checking/file upload |
| Group D (FR-11–FR-15) | Feature 4 | Functional Testing — document upload/notification |
| Group E (FR-16–FR-20, FR-32–FR-34; FR-21, FR-30 = Deprecated) | Features 5, 6 | Functional Testing — map / 1:1 supervising instructor assignment by route group (FR-32) / confirm before replacing an existing assignment (FR-34) / setting the online–on-site supervision mode per session (FR-33) / scoring and interview |
| Group F (FR-22–FR-23) | Feature 7 | Functional Testing — self-declare confirmation |
| Group G (FR-24–FR-25, FR-35) | Feature 8 | Functional Testing — automatic status change / document generation from a template / notify the student when the host company evaluation is completed (FR-35 — a parallel milestone that does not block the status change) |
| Group H (FR-26–FR-28) | Feature 9 | Functional Testing — problem-case recording / timeline |
| Group I (FR-29, FR-31) | Feature 10 | Functional Testing — scheduled notifications / configurable advance lead-time policy |

### 2.2 Non-Functional Testing (per NFR)

| Code | Area | Type of testing |
|---|---|---|
| [NFR-01](./acceptance-criteria.md) | Security/data access rights | Security Testing — test access rights to documents/files by role (access control / authorization) |
| [NFR-02](./acceptance-criteria.md) | Audit | Audit/Traceability Testing — test that every significant status change records the actor and time completely |
| [NFR-03](./acceptance-criteria.md) | Field use | Usability/Reliability Testing (Field & Offline Conditions) — test data entry via mobile device under an unstable internet signal |
| [NFR-04](./acceptance-criteria.md) | Map rendering performance | Performance Testing — test map rendering latency when there are many pins |
| [NFR-05](./acceptance-criteria.md) | Correctness of auto-generated documents | Output/Document Verification Testing — test the correctness of the data and format of documents the system generates automatically |
| [NFR-06](./acceptance-criteria.md) | Uploaded file validity (File Validation) | Security/Input Validation Testing — test the immediate rejection of wrong-type/oversized/corrupted files at every upload point (certificate, the three acceptance documents) |
| [NFR-07](./acceptance-criteria.md) | Offline operation and data sync (Offline Draft & Auto-Sync) | Reliability/Offline Testing — test storing local drafts indefinitely, auto-retry when the signal returns, and the pending-sync notification banner |

## 3. Environment

`docs/02-design/02-technical/technology-stack.md` **does not yet exist / is still empty** as of the
date this plan was written (2026-09-16) — **pending the tech stack decision first** — so the
technical environment (e.g., browser/OS versions, test database, CI pipeline) cannot yet be
specified at this time. Once the tech stack is decided, return to update this section to specify:
- Environment at the dev/staging/production level (if any)
- Devices that must be tested for real for NFR-03 (mobile/tablet in the field, with simulation of an
  unstable internet signal — required only for **on-site** supervision rounds per FR-33; **online**
  supervision rounds are tested with normal devices/internet instead, without simulating an unstable
  signal)
- Test accounts for each role (Student, Academic Advisor, Supervising Instructor, Internship
  Coordinator)
- Sample data (seed data) covering every status in the internship student lifecycle

## 4. Entry Criteria

- Source code/features developed and completed per the scope specified in the
  detailed design of that feature (to be created when real development begins)
- The relevant test cases in `test-cases/{feature-slug}.md` are complete and have been reviewed
- The environment is ready as specified in Section 3 (pending tech stack)
- Test accounts exist for every role relevant to that feature

## 5. Exit Criteria

- All test cases of features with "High" priority (MVP) must pass 100%
- Test cases of "Medium"/"Low" features pass at least per the criteria the team agrees on before
  going live (defects found must be prioritized and have a fix plan before closing the test round)
- No Critical/Blocker-level defects remain in Must-have features
- Non-functional test results (Security, Audit, Field/Offline, Performance, Document Accuracy) pass
  per the criteria defined in [acceptance-criteria](./acceptance-criteria.md) for each NFR

## 6. Tester Roles

Test according to the system's real user roles (reference
[spec, Section 3](../requirements/spec.md) and [user-journey](../design/user-journey.md)):

| Role | Primary testing scope |
|---|---|
| Student | Submit host company, upload certificate/documents, pin on Google Map, self-declare with the existing core internship system, view own status |
| Academic Advisor / internship approver | Schedule presentation date, record pass/fail results, view overview dashboard, receive notifications |
| Supervising Instructor (one per company, per the assigned route group — revised 2026-09-16) | View pin locations/plan routes, set the online/on-site supervision mode per session, record scores/interview results (via mobile device for on-site cases only), record problem cases |
| Internship Coordinator | Verify eligibility/documents, view overview dashboard, record/track problem cases, generate thank-you letters |

## 7. Summary Table: Feature ↔ Test Case File ↔ Number of ACs Covered

| # | Feature | Test case file | Number of ACs covered |
|---|---|---|---|
| 1 | Track internship process status | [internship-status-tracking](./test-cases/internship-status-tracking.md) | 5 (FR-01 ×2, FR-02 ×2, NFR-02 ×1) |
| 2 | Propose a host company and request approval | [company-proposal-approval](./test-cases/company-proposal-approval.md) | 7 (FR-03, FR-04, FR-05 ×2, FR-06, FR-07, NFR-02) |
| 3 | Verify training eligibility | [training-qualification](./test-cases/training-qualification.md) | 10 (FR-08 ×2, FR-09, FR-10 ×2, NFR-01, NFR-06 ×4) |
| 4 | Manage the three internship acceptance documents | [acceptance-documents](./test-cases/acceptance-documents.md) | 10 (FR-11, FR-12, FR-13, FR-14 ×2, FR-15, NFR-01, NFR-06 ×3) |
| 5 | Pin host companies, plan routes, and assign supervising instructors | [company-map-pinning](./test-cases/company-map-pinning.md) | 11 (FR-16 ×2, FR-17, FR-32 ×2, FR-34 ×4, NFR-02 ×1, NFR-04) |
| 6 | Score and record interview results during supervision | [supervision-scoring](./test-cases/supervision-scoring.md) | 13 (FR-18 ×2, FR-19 ×2, FR-20 ×2, FR-33 ×3, NFR-03, NFR-07 ×3; FR-21/FR-30 = Deprecated, not counted) |
| 7 | Confirm data entry with the existing core internship system | [main-system-confirmation](./test-cases/main-system-confirmation.md) | 3 (FR-22, FR-23, NFR-02) |
| 8 | Internship completion and thank-you letter to the host company | [internship-completion](./test-cases/internship-completion.md) | 6 (FR-24, FR-25, FR-35 ×2, NFR-02, NFR-05) |
| 9 | Record and track problem cases during the internship | [problem-case-tracking](./test-cases/problem-case-tracking.md) | 5 (FR-26 ×2, FR-27, FR-28, NFR-02) |
| 10 | Notify proposal presentation and supervision schedules | [schedule-notifications](./test-cases/schedule-notifications.md) | 4 (FR-29 ×2, FR-31 ×2) |

A total of 74 ACs cover FR-01–FR-20, FR-22–FR-29, FR-31–FR-35 and NFR-01–NFR-07, every active code
(FR-21, FR-30 = Deprecated since 2026-09-16, no longer counted in this total — see *(Deprecated —
FR-21/FR-30, removed from scope)*). (For the details of each AC, see
[acceptance-criteria](./acceptance-criteria.md).)

## Related Documents

- [feature-list](../design/feature-list.md) — the full feature list with MoSCoW
- [user-journey](../design/user-journey.md) — real usage flows by role
- [backlog](../requirements/backlog.md) — summary of all FR/NFR with priorities
- [acceptance-criteria](./acceptance-criteria.md) — acceptance criteria per code
- [spec](../requirements/spec.md) — the source spec document
