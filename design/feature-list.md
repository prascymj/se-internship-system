# Feature List — Student Internship Process Tracking System

Groups the FR/NFR from the [backlog](../requirements/backlog.md) into features that are meaningful to real users. Always refer to the full details in the [source spec](../requirements/spec.md).

> Grouping rationale: The A–I groups in the spec document are used as the starting point, but group E (the supervision process) is split into 2 features (5 and 6) because they are genuinely handled by users in different roles on different screens (pinning/route planning versus scoring/on-site interviewing) — this is not an ambiguous case that requires asking the user, but a first-time re-grouping of the whole file to make it easier to read for the design/development team.

## Summary table of all features

| # | Feature | Short description (1 line) | MoSCoW | FR/NFR codes | User roles |
|---|---|---|---|---|---|
| 1 | Track the internship process status | Show individual status and a whole-semester overview in a filterable table | Must have | FR-01, FR-02, NFR-02 | Student, Academic Advisor, Internship Coordinator |
| 2 | Submit a host company proposal and request approval | Student submits a host company, schedules a proposal presentation, and repeats until the advisor approves | Must have | FR-03, FR-04, FR-05, FR-06, FR-07, NFR-02 | Student, Academic Advisor |
| 3 | Verify training eligibility | Check the number of training sessions, upload certificates, and confirm completeness before starting the internship | Must have | FR-08, FR-09, FR-10, NFR-01, NFR-06 | Student, Internship Coordinator |
| 4 | Manage the 3 internship acceptance documents | Upload/track the completeness of the Request Letter, the Acceptance Letter, and the Referral (Placement) Letter | Must have | FR-11, FR-12, FR-13, FR-14, FR-15, NFR-01, NFR-06 | Student, Internship Coordinator |
| 5 | Pin host companies, plan routes, and assign Supervising Instructors | Pin locations on Google Map, help group routes, assign 1 Supervising Instructor per route group/company, with confirmation required before replacing an existing assignment | Must have | FR-16, FR-17, FR-32, FR-34, NFR-04, NFR-02 | Student, Supervising Instructor, Internship Coordinator |
| 6 | Score and record interview results during supervision | 1 Supervising Instructor per company sets the online/on-site mode, then records scores per the rubric and the interview results | Must have | FR-18, FR-19, FR-20, FR-33, NFR-03, NFR-07 | Supervising Instructor |
| 7 | Confirm data entry with the existing core internship system | The student self-declares that they have recorded their tasks in the existing system, and the system updates the status | Must have | FR-22, FR-23, NFR-02 | Student, Internship Coordinator |
| 8 | End the internship and the thank-you letter to the host company | Change the status when the term is complete and auto-generate a thank-you letter from a template | Must have | FR-24, FR-25, NFR-02, NFR-05 | Internship Coordinator, Student |
| 9 | Record and track problem cases during the internship | Record cases of being returned/dismissed or at risk of not passing, with a per-student history timeline | Must have | FR-26, FR-27, FR-28, NFR-02 | Internship Coordinator, Supervising Instructor |
| 10 | Notify about presentation and supervision schedules | Notify the Academic Advisor/Supervising Instructor when a schedule is approaching, per a configurable lead-time policy | Should have | FR-29, FR-31 | Academic Advisor, Supervising Instructor |

## 1. Track the internship process status

The student views their own current status in the internship process, while advisors/staff view an overview of the status of all students in the same semester in a table, with filtering by status (e.g., host company not yet submitted / awaiting presentation / approved / awaiting complete acceptance documents / interning / returned/dismissed from the internship / internship ended).

- Related codes: [FR-01, FR-02](../requirements/spec.md), [NFR-02](../requirements/spec.md)
- User roles: Student (views own status), Academic Advisor/Internship Coordinator (views the overview dashboard)
- Priority (MoSCoW): Must have

## 2. Submit a host company proposal and request approval

The student records the information of the host company they want to intern at, schedules a presentation date with the Academic Advisor, and awaits the decision. If it is not approved, they must submit a new host company and schedule a new presentation, repeating until approved. Once approved, the system changes the student's status to "ready to apply for an internship at this host company".

- Related codes: [FR-03, FR-04, FR-05, FR-06, FR-07](../requirements/spec.md), [NFR-02](../requirements/spec.md)
- User roles: Student, Academic Advisor/internship approver
- Priority (MoSCoW): Must have

## 3. Verify training eligibility

The system verifies that the student has attended the required number of preparation training sessions (default 5, configurable). The student uploads a certificate each time as evidence, and the staff/system confirms completeness before allowing the next step (submitting the internship application documents). Uploaded certificate files must be of type PDF/JPG/PNG and no larger than 10MB per file; otherwise the system rejects the upload immediately with a message explaining the reason to fix (it does not accept the file first and report the problem later).

- Related codes: [FR-08, FR-09, FR-10](../requirements/spec.md), [NFR-01, NFR-06](../requirements/spec.md)
- User roles: Student, Internship Coordinator
- Priority (MoSCoW): Must have

## 4. Manage the 3 internship acceptance documents

The student uploads 3 documents (Request Letter / Acceptance Letter / Referral (Placement) Letter). The system shows the status of whether the documents are complete, which one is still missing, and notifies the student/staff when they are still incomplete as the deadline approaches (per the configurable lead-time policy, see Feature 10). All 3 uploaded files must be of type PDF/JPG/PNG and no larger than 10MB per file, the same as the training certificates; otherwise the system rejects the upload immediately with a message explaining the reason.

- Related codes: [FR-11, FR-12, FR-13, FR-14, FR-15](../requirements/spec.md), [NFR-01, NFR-06](../requirements/spec.md)
- User roles: Student, Internship Coordinator
- Priority (MoSCoW): Must have

## 5. Pin host companies, plan routes, and assign Supervising Instructors

The student pins the location of the host company where they will intern on Google Map. The system helps group host companies by nearby areas to support supervision route planning (the level of automation of the route planning is still an assumption to be confirmed with users, see spec section 4 item 5). The staff then assign a Supervising Instructor **1 per route group** to be responsible, whereby all host companies in the same group are assigned to the same instructor (a 1:1 relationship between the Supervising Instructor and the company per FR-18 — updated 2026-09-16). Manual assignment is supported even without the full automation of route grouping. If the staff attempt to assign a Supervising Instructor to a host company that already has a responsible instructor (violating the 1:1 rule above), the system must not reject immediately and must not replace automatically, but must show the existing assignment information and have the staff confirm the cancellation/replacement first before the new instructor can be saved, while recording the history of the change of responsible instructor (previous instructor → new instructor, who performed the action, timestamp) for auditability.

- Related codes: [FR-16, FR-17, FR-32, FR-34](../requirements/spec.md), [NFR-04, NFR-02](../requirements/spec.md)
- User roles: Student (pinning), Internship Coordinator (route grouping/assigning Supervising Instructors/confirming replacement of an existing assignment), Supervising Instructor (receiving assignments per route group)
- Priority (MoSCoW): Must have

## 6. Score and record interview results during supervision

The Supervising Instructor **1 per company** (updated 2026-09-16) sets the mode of each supervision as **online or on-site** before recording scores per the scoring form/rubric and the student interview results. Whichever mode it is, in the **on-site** case the recording must be done through a mobile device at the host company (even when the internet signal is unstable): when there is no signal while recording, the system keeps the data as a local draft on the device with no time limit until it syncs with the server successfully, with automatic auto-retry when the signal returns, and shows a message/banner notification throughout the period there is data still pending sync (the draft must never be auto-deleted no matter how long it is pending). In the **online** case, the field/offline conditions above are not enforced, since it is used through a normal device/internet (see the draft scoring form/rubric/sample interview questions in the spec appendix, section 7 — not yet the official version).

- Related codes: [FR-18, FR-19, FR-20, FR-33](../requirements/spec.md), [NFR-03, NFR-07](../requirements/spec.md)
- User roles: Supervising Instructor (1 per company)
- Priority (MoSCoW): Must have

## 7. Confirm data entry with the existing core internship system

The student self-declares that they have recorded their daily tasks/data in the existing core internship system (this system does not connect via API to the existing system in reality, it is only a self-declaration — see assumption item 2 in the spec). The system updates the overall status of the student once the confirmation is received.

- Related codes: [FR-22, FR-23](../requirements/spec.md), [NFR-02](../requirements/spec.md)
- User roles: Student, Internship Coordinator
- Priority (MoSCoW): Must have

## 8. End the internship and the thank-you letter to the host company

The system changes the student's status to "internship ended" when the planned 4-month period is complete, and generates a thank-you letter to the host company (unsigned) from a template, pulling the student/host company information recorded in the system. The generated document must conform to the official format of the university/school.

- Related codes: [FR-24, FR-25](../requirements/spec.md), [NFR-02, NFR-05](../requirements/spec.md)
- User roles: Internship Coordinator (generates the document), Student (whose status changes)
- Priority (MoSCoW): Must have

## 9. Record and track problem cases during the internship

The system records the date, reason, and recorder for cases where a student is returned/dismissed during the internship (changing the status to "must find a new internship placement" and allowing them to go back to submit a new host company), as well as recording cases of students at risk of not passing along with the assistance measures taken, and displays the problem-case history/timeline of each student in chronological order for continuous follow-up.

- Related codes: [FR-26, FR-27, FR-28](../requirements/spec.md), [NFR-02](../requirements/spec.md)
- User roles: Internship Coordinator, Supervising Instructor
- Priority (MoSCoW): Must have

## 10. Notify about presentation and supervision schedules

The system notifies the Academic Advisor/Supervising Instructor when the host company presentation date, or the supervision schedule, of a student they oversee is approaching, per a lead-time notification policy that the staff can configure (the recommended default is 7 days — **not yet a fixed conclusion**; the user answered "not sure" when asked about the number of days, so it must be confirmed/adjusted again before actual design/development). The same policy is also used for the notification of still-missing documents in Feature 4.

- Related codes: [FR-29, FR-31](../requirements/spec.md)
- User roles: Academic Advisor, Supervising Instructor
- Priority (MoSCoW): Should have

## Related documents

- [backlog](../requirements/backlog.md) — summary of all FR/NFR in the project
- [source spec](../requirements/spec.md) — the source spec document
- [user-journey](./user-journey.md) — maps these features into real usage flows by role
