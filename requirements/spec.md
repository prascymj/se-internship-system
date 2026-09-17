# Student Internship Workflow Tracking System (Internship Workflow Tracking System)

> The first document of this project — captured from the raw requirement received from the user on 2026-09-16.
> No other spec document existed before this in `01-spec/`, so the FR/NFR numbering starts from 01.

## 1. Introduction

This project aims to develop a system that supports the student internship process — from announcing/tracking
status by semester, submitting proposed host companies and requesting approval from the advisor, checking
eligibility before starting the internship, managing acceptance documents, the supervision process during the
4-month internship, through to post-internship documents and recording problem cases that may arise along the way.

**Important:** There is currently an "existing core internship system" that students use to log their daily tasks
during the internship, and that host companies use to view progress. The system planned in this document **does not
replace** that system but works alongside it, focusing on the document workflow, approvals, supervision, and the
overall status of each student. The integration with the existing system in this document is still limited to having
students self-confirm (see Assumption 3 and FR-22–FR-23).

## 2. Scope

### In scope
- Tracking the status of each student's internship process by semester (this picture starts from the "semester 2" context)
- Submitting proposed host companies, scheduling and recording the results of the proposal presentation with the advisor, and iterating when it does not pass
- Checking eligibility with respect to attending pre-internship training and uploading evidence (certificate)
- Uploading and tracking the 3 internship acceptance documents (Request Letter / Acceptance Letter / Referral (Placement) Letter)
- The supervision process during the 4-month internship: pinning the host company on Google Map, grouping supervision
  routes and assigning a Supervising Instructor **1 per company** according to the route group they are responsible for
  (updated 2026-09-16 — see Section 9), scoring per the scoring form/rubric and interview form, where each supervision
  round can be specified as being **online or on-site**
- Confirming that data has been recorded in the existing core internship system (self-declare) and updating the related status
- Post-internship documents (Thank-you Letter to the host company, no signature)
- Recording problem cases: returned/dismissed from the internship, and cases of students at risk of not passing

### Out of scope (of this document)
- Logging daily tasks during the internship and host companies viewing progress — these are the responsibility of the
  existing core internship system already in place; they are not duplicated.
- Digital signing/e-signature — the Thank-you Letter to the host company that the system generates has no signature.
- Paying compensation/benefits to intern students
- Defining any tech stack — pending the decision in _technology stack (to be decided)_ per project convention.

## 3. Roles

| Role | Main responsibilities in this system |
|---|---|
| Student | Submit host company, upload documents/certificate, pin on Google Map, confirm recording in the existing core internship system |
| Academic Advisor / internship approver | Schedule the presentation date, record the pass/fail result of the host company the student proposes |
| Supervising Instructor (1 per company, according to the assigned route group — updated 2026-09-16) | Responsible for supervising the companies in their route group (online/on-site), scoring per the scoring form/rubric, and recording the interview results during supervision |
| Internship Coordinator | Verify documents/eligibility, record problem cases, view the overall status for the whole semester |

> Note: The role names above are an interpretation of the raw requirement, not yet confirmed against the actual
> permission structure of the university/school. If additional roles exist (e.g., head of school, committee members),
> they must be revised later.

## 4. Assumptions not yet confirmed with the user (must be reviewed before proceeding to the next design stage)

The raw requirement has several points that can be interpreted in more than one way. This document chooses the most
reasonable interpretation for now so that work does not stall, but **every point below must be confirmed by the actual
user before being carried forward to the design stage**:

1. **Approver of the host company presentation result (FR-04–FR-05):** Assumed to be "a single Academic Advisor"
   per student (single approver). If in practice it is a committee of several people who must vote jointly, FR-05
   must be adjusted to support aggregating results from multiple people.
2. **Linkage with the existing core internship system (FR-22–FR-23):** Assumed to be only a "self-declare"
   confirmation by the student, not a real API/data integration with the existing system, because there is not yet
   any information about the access rights/technology stack of the existing system. If a real integration is later
   required, a new requirement must be opened separately once the details of the existing system are known.
3. **Number of training sessions (FR-08):** Assumed that "5 sessions" is a default value that staff can change per
   semester, not a permanently hardcoded constant.
4. **Supervision form/rubric/interview questions (Appendix, Section 7):** The user asked to draft the content in this
   document. The drafted content is **only a preliminary example**, not yet the official form of the school; the user
   must review/adjust the scoring criteria and questions before actual use.
5. **Grouping/planning supervision routes from the pinned locations (FR-17):** It is not yet clear whether full
   automation is required (the system groups/recommends routes automatically) or merely displaying locations on the
   map for staff to plan themselves. This document sets it at the "Medium" level (not MVP) for now, with only FR-16
   (pinning) defined as MVP.
6. **Lead time for notifications (FR-31, which extends FR-15/FR-29):** When asked how many days in advance the
   notification should be sent before the due date, the user answered "not sure," so the recommended default of
   **7 days** is used (adjustable by staff, following the same approach as FR-08). This value is **not yet a final
   conclusion**; the user must confirm/adjust it again before it is used in actual design/development.
> **Note (2026-09-16, after confirmation):** The former Assumption 7 (the status of FR-21/FR-30 after adjusting FR-18
> to "1 Supervising Instructor per company") has been answered by the user: to **cancel both FR-21 and FR-30**. It is
> therefore removed from the list of assumptions to review — see the full decision details at
> _(Deprecated — FR-21/FR-30, removed from scope)_ and Section 9 below.

## 5. Functional Requirements

### Group A: Status tracking by semester (FR-01–FR-02)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-01 | Display the internship process status of each student | The system must display each student's current status in the internship process for the semester (e.g., host company not yet submitted / awaiting presentation / approved / awaiting all acceptance documents / interning / returned-dismissed / internship ended) | High |
| FR-02 | Dashboard overview of status for the whole semester | Staff/instructors must be able to view an overview of the status of all students in the same semester in a table, with the ability to filter by status | High |

### Group B: Submitting proposed host companies and the presentation (FR-03–FR-07)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-03 | Submit the host company data for the desired internship | The student records host company data (name, address, contact person, position to be interned) through the system | High |
| FR-04 | Schedule the presentation date with the instructor | The system allows recording/scheduling the presentation date of the chosen host company with the Academic Advisor | High |
| FR-05 | Record the presentation result (pass/fail) | The Academic Advisor records the review result along with accompanying comments after the presentation date (see Assumption 1 regarding the approver) | High |
| FR-06 | Loop back to submit a new host company when it does not pass | If the result is fail, the system must allow the student to submit a new host company and schedule a new presentation date (repeatable until it passes) | High |
| FR-07 | Change status when approved | When the result passes, the system changes the student's status to "ready to apply for the internship at this host company" | High |

### Group C: Checking training eligibility (FR-08–FR-10)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-08 | Check the number of training sessions attended | The system checks whether the student has attended the required number of preparation training sessions (default 5 sessions, adjustable by staff — see Assumption 3) | High |
| FR-09 | Upload the training certificate | The student uploads evidence/certificate of attending each training session | High |
| FR-10 | Confirm completeness of eligibility | Staff/the system confirms pass/fail on training eligibility before allowing the next step (submitting the internship application documents) | High |

### Group D: Internship acceptance documents (FR-11–FR-15)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-11 | Upload the Request Letter | The student uploads the Request Letter asking the company to accept the student for an internship | High |
| FR-12 | Upload the Acceptance Letter | The student uploads the internship Acceptance Letter from the host company | High |
| FR-13 | Upload the Referral (Placement) Letter | The student uploads the Referral (Placement) Letter sending the student to the internship | High |
| FR-14 | Track the completeness of all 3 documents | The system displays the status of whether all 3 documents are complete, and which one is still missing | High |
| FR-15 | Notify about missing documents | The system notifies the student/staff when documents are still incomplete and the due date is approaching | Medium |

### Group E: Supervision process during the 4-month internship (FR-16–FR-20, FR-32–FR-34; FR-21, FR-30 = Deprecated)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-16 | Pin the host company on Google Map | The student pins the location of the internship host company on Google Map for use in supervision planning (used mainly to support route planning for **on-site** supervision per FR-33 — **online** supervision does not need to reference this location) | High |
| FR-17 | Help group/plan supervision routes | The system helps group host companies by nearby areas to support supervision route planning, and serves as the basis for assigning Supervising Instructors by route group in FR-32 (see Assumption 5 regarding the automation level) | Medium |
| FR-18 | One Supervising Instructor per company (updated 2026-09-16) | The system requires each host company/student to have only **1** responsible Supervising Instructor throughout the internship round (no longer supporting multiple co-supervisors simultaneously). The assignment references the route grouping arranged in FR-17/FR-32 _(formerly: "supports multiple Supervising Instructors per round" — revised per the new requirement 2026-09-16)_ | High |
| FR-19 | Record scores per the scoring form/rubric | The Supervising Instructor records the scoring result per the scoring form/criteria (rubric) through the system after each supervision, whether online or on-site (see FR-33, Appendix Section 7) | High |
| FR-20 | Record interview results | The Supervising Instructor records the student interview results per the defined question set, whether supervising online or on-site (see FR-33, Appendix Section 7) | High |
| ~~FR-21~~ | ~~Summarize the total score from multiple Supervising Instructors~~ | **Deprecated (cancelled 2026-09-16)** — formerly: "when there is more than 1 Supervising Instructor in the same round, the system aggregates/summarizes the scores into a summary score per supervision round." Cancelled because FR-18 changed to 1 Supervising Instructor per company, so there is no longer a multi-instructor use case (confirmed by the user). This code is reserved and will not be reused — see the original content and full rationale at _(Deprecated — FR-21/FR-30, removed from scope)_ | ~~Medium~~ |
| ~~FR-30~~ | ~~Set a summary score manually (manual override) when there are multiple Supervising Instructors~~ | **Deprecated (cancelled 2026-09-16)** — formerly extended FR-21 (manual override of the score by staff/the lead instructor when there are multiple Supervising Instructors). Cancelled for the same reason as FR-21 (confirmed by the user). This code is reserved and will not be reused — see the original content and full rationale at _(Deprecated — FR-21/FR-30, removed from scope)_ | ~~Medium~~ |
| FR-32 | Assign Supervising Instructors by route group (new 2026-09-16) | Staff assigns 1 Supervising Instructor to be responsible for one route group/area (referencing the grouping from FR-17). All host companies in the same group are assigned to the same instructor (a 1:1 relationship between Supervising Instructor and company per FR-18). It supports manual assignment even without the full automation of FR-17 | High |
| FR-33 | Specify the supervision mode (Online/On-site) per round (new 2026-09-16) | The system allows specifying the mode of each supervision round as **online** or **on-site**, tied to the score/interview recording of that round (FR-19/FR-20). The on-site case must reference the pinned location of the host company (FR-16) and meets the field-use/offline conditions (NFR-03/NFR-07). The online case does not require coordinates/route and does not need to support NFR-03/NFR-07 | High |
| FR-34 | Confirm before replacing the existing Supervising Instructor assignment (new 2026-09-16) | When staff assigns a Supervising Instructor (FR-32) to a host company that already has a responsible Supervising Instructor (conflicting with the 1:1 rule of FR-18), the system **must not reject immediately and must not replace automatically**, but must display the existing assignment information (the name of the existing Supervising Instructor) and have the staff (authorized user) **confirm the cancellation/replacement of the existing assignment first** before the new instructor's assignment can be recorded. The system must record the history of the change of responsible person (old instructor → new instructor, who performed the action, time) for audit purposes per NFR-02 | High |

### Group F: Confirmation with the existing core internship system (FR-22–FR-23)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-22 | Confirm data recording in the existing core internship system | The student self-declares that they have recorded their daily tasks/data in the existing core internship system (see Assumption 2) | High |
| FR-23 | Update status upon confirmation | The system updates the student's overall status when the confirmation per FR-22 is received | High |

### Group G: Ending and post-internship (FR-24–FR-25)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-24 | Change status when the internship ends | The system changes the student's status to "internship ended" when the 4-month period is complete per plan | High |
| FR-25 | Generate the Thank-you Letter to the host company | The system generates the Thank-you Letter to the host company (no signature) from a template, pulling the student/host company data recorded in the system, after the internship is finished | High |

### Group H: Problem cases during the internship (FR-26–FR-28)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-26 | Record the case of being returned/dismissed during the internship | The system records the date, reason, and recorder for the case of a student being returned/dismissed during the internship, and changes the status to "must find a new internship placement," from which the student can start the host company submission process again (returning to Group B) | High |
| FR-27 | Record the case of a student at risk of not passing | The system records the details of a student whose internship result is at risk of not passing, along with a record of how the instructor/staff has provided assistance | High |
| FR-28 | Display the history/timeline of problem cases | The system displays the history of each student's problem cases in chronological order for continuous follow-up | Medium |

### Group I: Notifications (FR-29, FR-31)

| Code | Requirement | Details | Priority |
|---|---|---|---|
| FR-29 | Notify about the presentation/supervision due date | The system notifies the Academic Advisor/Supervising Instructor when the host company presentation date or a supervision schedule is approaching (for the definition of "approaching," see FR-31) | Medium |
| FR-31 | Policy for the notification lead time (adjustable) | The system notifies the relevant people **7 days** in advance of the due date (a default value staff can adjust, following the same approach as FR-08). Used together with FR-15 (here "due date" means the planned internship start date) and FR-29 (here "due date" means the presentation/supervision date). **Important note: the 7-day value is only a recommended default; the user has not yet confirmed the final value (see Assumption 6) and it must be reviewed again before being used in actual design/development** | Medium |

## 6. Non-Functional Requirements

| Code | Area | Requirement |
|---|---|---|
| NFR-01 | Security/data access rights | Uploaded documents (certificate, Acceptance Letter, Referral (Placement) Letter) must be accessible only to the student who owns the data, the relevant instructors, and authorized staff. |
| NFR-02 | Audit | Every important status change (pass/fail of the presentation, returned/dismissed, internship ended) must record who performed the action and the time it was performed. |
| NFR-03 | Field use | The Supervising Instructor must be able to record scores/interview results via a mobile device while at the host company, where the internet signal may be unstable **(applies only to on-site supervision per FR-33 — online supervision is not subject to this condition, as it is used via normal devices/internet)**. |
| NFR-04 | Map rendering performance | Displaying the pinned host company locations of a whole cohort on the map must not lag, even with a large number of pins. |
| NFR-05 | Correctness of auto-generated documents | The Thank-you Letter to the host company that the system generates must conform to the official format of the university/school. |
| NFR-06 | Correctness of uploaded files (File Validation) | Every point in the system that allows file upload (training certificate FR-09, Request Letter/Acceptance Letter/Referral (Placement) Letter FR-11–FR-13) must accept only PDF and image (JPG/PNG) files, no larger than 10MB per file. If the user uploads a wrong file type, an oversized file, or a corrupt file, the system must **reject the upload immediately** and display a clear message explaining the reason for the user to fix (it must not accept the file first and notify later). |
| NFR-07 | Offline operation and data sync (Offline Draft & Auto-Sync) | Extends NFR-03: when there is no internet signal while recording scores/interview results in the field (only for **on-site** supervision per FR-33), the system must keep the data as a local draft on the device **with no time limit** until it syncs successfully with the server, with automatic auto-retry when the signal returns, and displaying a message/banner notifying the user throughout the period there is still unsynced data. It must never delete the draft data automatically, no matter how long it remains pending. |

## 7. Appendix: Draft supervision and interview forms (Draft — not yet confirmed)

> This draft was prepared to fulfill the "form and questions" request in the raw requirement. It is only a preliminary
> example, referencing the general format of internship supervision evaluation forms. **The user must review, adjust the
> scoring criteria, and adjust the questions to match the official form of the school before actual use** (related to
> FR-19, FR-20).

### 7.1 General information of the supervision
- Student name / student ID
- Host company name / address
- Supervision date / supervision round number
- Name of the Supervising Instructor (may be more than 1 person)

### 7.2 Scoring criteria (example rubric, 5 points per item)

| Aspect evaluated | Description | Full score |
|---|---|---|
| Professional knowledge and skills applied in actual work | How appropriately the student applies the knowledge they learned to the assigned work | 5 |
| Responsibility and punctuality | Punctual attendance, responsibility for the assigned work | 5 |
| Working with others/communication | Adapting to the organizational culture, communicating with the mentor/team | 5 |
| Problem-solving and initiative | Ability to solve immediate problems and propose new ideas | 5 |
| Personality and professional ethics | Dress, manners, work ethics | 5 |
| Work progress compared to the plan | Work completed compared to the plan agreed upon at the outset | 5 |
| **Total** | | **30** |

### 7.3 Interview form (example open-ended questions)
1. Does the assigned work align with the field of study, and how?
2. What obstacles or problems were encountered during the internship, and how were they solved?
3. What additional things were learned beyond the classroom?
4. The mentor's/supervisor's opinion of the student's performance (ask the host company side)
5. Is there a wish to continue working with this host company after graduation?

### 7.4 Supervision result summary
- Total score / evaluation result level
- Recommendations from the Supervising Instructor
- Signature of the Supervising Instructor (in the system, not an actual handwritten signature on paper)

## 8. Extension: Gaps found while writing Test Cases (added 2026-09-16)

While the `test-writer` subagent was writing acceptance criteria/test cases from this document, 4 points were found where
the original spec (FR-01–FR-29, NFR-01–NFR-05) had never defined the behavior, making it impossible to write
deterministic test cases. The user (the instructor) answered all 4 policy questions on the same day, so new codes were
added following FR-29/NFR-05 as follows (full details are in the tables of the relevant groups above):

| New code | Extends | Summary of the user's answer |
|---|---|---|
| NFR-06 | FR-09, FR-11–FR-13 | Accept only PDF/JPG/PNG no larger than 10MB/file; reject immediately with a message explaining the reason when the conditions are not met |
| FR-30 | FR-21 | The summary score is a manual override by staff/the lead instructor, not computed automatically; must record who set it + the reference scores of each person |
| FR-31 | FR-15, FR-29 | Notify 7 days in advance (an adjustable default — **not yet firmly confirmed**; the user answered "not sure") |
| NFR-07 | NFR-03 | Keep the local draft with no time limit + auto-retry + notification banner; do not delete automatically |

## 9. Extension: One Supervising Instructor per company and the Online/On-site supervision mode (added 2026-09-16)

The user made an additional update to the supervision requirement (raw text: "adjust the supervising instructor to 1
person per company, dividing supervision according to the route grouping; supervision has online and on-site modes").
Summary of the changes in this round:

| Change | Details |
|---|---|
| Revise FR-18 | From "supports multiple Supervising Instructors per round" to "1 Supervising Instructor per company" (still High priority) |
| Add FR-32 (new) | Assign Supervising Instructors by route group (building on FR-17) — High |
| Add FR-33 (new) | Specify the online/on-site supervision mode per round — High — affects FR-16 (on-site uses coordinates), NFR-03/NFR-07 (apply only to on-site) |
| Reword NFR-03, NFR-07 | Clearly specify that they apply only to the on-site supervision case |
| FR-21, FR-30 | **Cancelled (Deprecated, confirmed by the user on 2026-09-16)** — because FR-18 changed to 1 Supervising Instructor per company, there is no longer a multi-instructor-per-round use case. The original content was moved to _(Deprecated — FR-21/FR-30, removed from scope)_. In the Group E table, the codes are kept with strikethrough (~~Deprecated~~) for traceability; the codes will not be reused |
| Reword | The introduction (scope) and the roles table (Supervising Instructor) to reflect "1 per company" and online/on-site |

**The decision (confirmed by the user via the UI on 2026-09-16):** FR-21 and FR-30 have been **cancelled (Deprecated)**
and moved to `docs/00-archived/20260916-fr21-fr30-multi-supervisor-scoring-deprecated.md`. Both codes are permanently
reserved and will not be reused in any document of this project.

## 10. Extension: Edge case of reassigning a Supervising Instructor to the same company (added 2026-09-16)

While the `test-writer` subagent was writing test cases for FR-32, an edge case was found that the original spec had not
yet defined: the case where staff attempts to assign a "second" Supervising Instructor to a company that already has 1
responsible Supervising Instructor (conflicting with the 1:1 rule of FR-18). The user (the instructor) decided via the UI
that the system must have the authorized user confirm/cancel the existing assignment first before the new instructor can
be assigned (not rejecting immediately, and not replacing automatically). Therefore **FR-34** was added, building on
FR-18/FR-32 in Group E (full details are in the Group E table above), linked to NFR-02 (audit) for recording the history
of the change of responsible person.

## Related documents

- [Backlog](./backlog.md) — summary of all FR/NFR of the project
- _(Deprecated — FR-21/FR-30, removed from scope)_ — the original content and the rationale for cancelling FR-21/FR-30
