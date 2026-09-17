# Acceptance Criteria — Student Internship Process Tracking System

Acceptance criteria (Given-When-Then) for every FR/NFR, grouped under exactly the same
feature headings as [feature-list](../design/feature-list.md) so the two can be read side by
side. Behavioral details always reference [spec](../requirements/spec.md). The priority
(High/Medium/Low) appended after each code is taken directly from
[backlog](../requirements/backlog.md).

> Note: Some NFRs (e.g., NFR-01, NFR-02) are referenced repeatedly across several features per
> [feature-list](../design/feature-list.md). This document therefore writes ACs separately
> according to the context of each feature (e.g., the audit trail of status changes as distinct
> events) instead of repeating the same content, so that testing covers the real situations of
> each feature.

## 1. Track Internship Process Status

Reference: [Track internship process status](../design/feature-list.md)

#### FR-01 (High) — [Display each student's internship process status](../requirements/spec.md)

- **AC-1 (happy path):** Given the student is in the current semester's internship process (e.g.,
  has just had a host company approved), When the student opens the "My Status" page, Then the
  system displays the current status matching actual progress from the defined status set (not yet
  submitted a host company / awaiting presentation / approved / awaiting complete acceptance
  documents / interning / returned/dismissed from the internship / internship ended).
- **AC-2 (edge — initial status):** Given a student who has not taken any action at all this
  semester, When the student opens the "My Status" page for the first time, Then the system shows
  the initial status "not yet submitted a host company".

#### FR-02 (High) — [Semester-wide status overview dashboard](../requirements/spec.md)

- **AC-1:** Given an Academic Advisor or Internship Coordinator logs into the system, When they
  open the overview dashboard, Then the system displays a table listing all students in the same
  semester together with each one's current status.
- **AC-2 (status filter):** Given the user is on the overview dashboard where students of various
  statuses are mixed together, When they select one status filter value (e.g., "interning"), Then
  the table shows only students whose status matches the filtered value and hides all other rows.

#### NFR-02 (High) — [Audit — context of status changes shown on the dashboard](../requirements/spec.md)

- **AC-1:** Given a student's status has been changed at least once before, When an authorized user
  opens that student's status history from the dashboard, Then the system displays the name of the
  person who performed each status change and the date-time of the action for every past change.

## 2. Propose a Host Company and Request Approval

Reference: [Propose a host company and request approval](../design/feature-list.md)

#### FR-03 (High) — [Submit the host company where the student wishes to intern](../requirements/spec.md)

- **AC-1:** Given the student has the status "not yet submitted a host company" or "must find a new
  internship placement", When the student fills in the host company details (name, address, contact,
  position to intern in) completely and clicks save, Then the system records the proposed host
  company with that student and changes the status to "awaiting presentation".

#### FR-04 (High) — [Schedule a proposal presentation date with the advisor](../requirements/spec.md)

- **AC-1:** Given the student has a host company already submitted in the "awaiting presentation"
  status, When the student or Academic Advisor records the presentation appointment date, Then the
  system records the appointed date with that host company's data and shows the same appointment
  date on both the student's and the advisor's side.

#### FR-05 (High) — [Record the proposal presentation result (pass/fail)](../requirements/spec.md)

- **AC-1 (pass):** Given the recorded presentation appointment date has arrived, When the Academic
  Advisor records the presentation result as "pass" together with accompanying comments, Then the
  system records the result and comments, and forwards it to the status-change process per FR-07.
- **AC-2 (fail):** Given the recorded presentation appointment date has arrived, When the Academic
  Advisor records the presentation result as "fail" together with accompanying comments, Then the
  system records the result and comments, and forwards it to the re-submission process per FR-06.

#### FR-06 (High) — [Loop back to submit a new host company on failure](../requirements/spec.md)

- **AC-1:** Given the student's presentation result was recorded as "fail" (FR-05), When the student
  goes back to submit new host company details, Then the system allows submitting a new host company
  and scheduling a new presentation date, repeatable an unlimited number of times until a pass.

#### FR-07 (High) — [Change status upon approval](../requirements/spec.md)

- **AC-1:** Given the student's presentation result was recorded as "pass" (FR-05), When the result
  is recorded successfully, Then the system automatically changes the student's status to "ready to
  apply for the internship at this host company".

#### NFR-02 (High) — [Audit — context of the host company proposal presentation result](../requirements/spec.md)

- **AC-1:** Given the Academic Advisor records a student's presentation result (pass or fail), When
  the recording succeeds, Then the system records the name of the advisor who recorded the result
  and the date-time of recording as part of an audit trail that can be reviewed later.

## 3. Verify Training Eligibility

Reference: [Verify training eligibility](../design/feature-list.md)

#### FR-08 (High) — [Check the number of training sessions attended](../requirements/spec.md)

- **AC-1 (default value):** Given the Internship Coordinator has not yet adjusted the training
  session count for this semester, When the system checks the number of sessions the student has
  attended, Then the system uses the default of 5 sessions as the criterion for checking completeness.
- **AC-2 (adjustable):** Given the Internship Coordinator adjusts this semester's training session
  count criterion to another value (e.g., 6 sessions), When the system checks the number of sessions
  the student has attended, Then the system uses the latest value adjusted by the coordinator as the
  criterion, not the default of 5 sessions.

#### FR-09 (High) — [Upload training certificates](../requirements/spec.md)

- **AC-1:** Given the student has completed one preparatory training session, When the student
  uploads that session's certificate into the system, Then the system records that certificate with
  the student and counts it as one session with complete evidence.

#### FR-10 (High) — [Confirm eligibility completeness](../requirements/spec.md)

- **AC-1 (complete):** Given the student has uploaded certificates complete per the defined criterion
  count (FR-08), When the Internship Coordinator reviews and confirms completeness, Then the system
  allows the student to proceed to the next step (uploading internship application documents).
- **AC-2 (incomplete):** Given the student has not uploaded certificates complete per the defined
  criterion count, When the Internship Coordinator reviews, Then the system does not allow proceeding
  to the next step and shows the student how many sessions are still missing.

#### NFR-01 (High) — [Security/data access rights — context of training certificates](../requirements/spec.md)

- **AC-1:** Given a certificate uploaded by a student, When a user who is not the owning student, a
  related advisor, or an authorized coordinator tries to access that file, Then the system denies
  access and does not display the file's content.

#### NFR-06 (High) — [Uploaded file validity (File Validation) — context of training certificates](../requirements/spec.md)

- **AC-1 (invalid file type):** Given the student selects a certificate file that is not of type
  PDF/JPG/PNG (e.g., .docx or .zip), When the student clicks upload, Then the system rejects the
  upload immediately with a message explaining that the file type is invalid, and does not save that
  file with the student.
- **AC-2 (file size exceeds limit):** Given the student selects a certificate file of a valid type
  but larger than 10MB, When the student clicks upload, Then the system rejects the upload immediately
  with a message explaining that the file exceeds the size limit, and does not save the file.
- **AC-3 (corrupted file):** Given the student selects a certificate file with a valid extension per
  the conditions but whose content is corrupted/unreadable, When the student clicks upload, Then the
  system detects the file anomaly and rejects the upload immediately with an explanatory message (it
  does not accept the file first and report later).
- **AC-4 (happy path):** Given the student selects a certificate file of type PDF/JPG/PNG no larger
  than 10MB and not corrupted, When the student clicks upload, Then the system accepts and saves the
  file successfully per FR-09 immediately.

## 4. Manage the Three Internship Acceptance Documents

Reference: [Manage the three internship acceptance documents](../design/feature-list.md)

#### FR-11 (High) — [Upload the Request Letter](../requirements/spec.md)

- **AC-1:** Given the student has the status "ready to apply for the internship at this host company"
  (via FR-10), When the student uploads the Request Letter, Then the system records that file as
  document No. 1 of that student.

#### FR-12 (High) — [Upload the Acceptance Letter](../requirements/spec.md)

- **AC-1:** Given the student has received the Acceptance Letter from the host company, When the
  student uploads the Acceptance Letter, Then the system records that file as document No. 2 of that
  student.

#### FR-13 (High) — [Upload the Referral (Placement) Letter](../requirements/spec.md)

- **AC-1:** Given the student has received the Referral (Placement) Letter, When the student uploads
  the Referral (Placement) Letter, Then the system records that file as document No. 3 of that
  student.

#### FR-14 (High) — [Track completeness of all three documents](../requirements/spec.md)

- **AC-1 (complete):** Given the student has uploaded all three documents (FR-11–FR-13), When the
  coordinator or student checks the document status, Then the system shows the status "documents
  complete".
- **AC-2 (incomplete):** Given the student has uploaded only 1 or 2 of the 3 documents, When the
  document status is checked, Then the system shows the status "documents incomplete" and clearly
  specifies which document is still missing.

#### FR-15 (Medium) — [Notify about missing documents](../requirements/spec.md)

- **AC-1:** Given the student's documents are not yet complete (all three) and the current date meets
  the "approaching deadline" criterion per the advance-notification lead-time policy the coordinator
  has set in the system (counted from the planned internship start date — see
  [FR-31](./acceptance-criteria.md)), When the time arrives at which the system detects the criterion
  is met, Then the system notifies both the student and the coordinator which document(s) are still
  missing.

#### NFR-01 (High) — [Security/data access rights — context of internship acceptance documents](../requirements/spec.md)

- **AC-1:** Given acceptance documents (Request Letter/Acceptance Letter/Referral (Placement) Letter)
  uploaded by a student, When a user without related rights to that student tries to open the
  documents, Then the system denies access.

#### NFR-06 (High) — [Uploaded file validity (File Validation) — context of the three internship acceptance documents](../requirements/spec.md)

- **AC-1 (invalid file type):** Given the student selects one of the three documents (Request
  Letter/Acceptance Letter/Referral (Placement) Letter) that is not of type PDF/JPG/PNG, When the
  student clicks upload, Then the system rejects the upload immediately with a message explaining
  that the file type is invalid, and does not count it as that document.
- **AC-2 (file size exceeds limit / corrupted file):** Given one of the documents is larger than 10MB
  or its content is corrupted/unreadable, When the student clicks upload, Then the system rejects the
  upload immediately with a message matching that problem.
- **AC-3 (happy path):** Given one of the documents is of type PDF/JPG/PNG no larger than 10MB and not
  corrupted, When the student clicks upload, Then the system accepts and saves the file as that
  document successfully (per FR-11/FR-12/FR-13 depending on the document).

## 5. Pin Host Companies, Plan Routes, and Assign Supervising Instructors

Reference: [Pin host companies, plan routes, and assign supervising instructors](../design/feature-list.md)

#### FR-16 (High) — [Pin the host company on Google Map](../requirements/spec.md)

- **AC-1:** Given the student has the status "ready to apply for the internship" or is preparing to
  start the internship, When the student pins their host company's location on Google Map in the
  system, Then the system records the location coordinates with that student's internship data and
  shows that pin to the Supervising Instructor/coordinator on the combined map.
- **AC-2 (on-site uses these coordinates primarily, online does not require them — revised
  2026-09-16):** Given the student has already pinned the host company location (AC-1) and that host
  company has a supervision round with a defined mode (see [FR-33](./acceptance-criteria.md)), When
  that supervision round is set as **on-site**, Then the system uses the pinned coordinates to help
  plan the supervision route for that round — but if the supervision round is set as **online**, the
  system does not require referencing these pinned coordinates at all.

#### FR-17 (Medium) — [Assist grouping/planning of supervision routes](../requirements/spec.md)

- **AC-1:** Given several students have already pinned their host company locations in the same
  semester, When the Supervising Instructor or coordinator activates the supervision-route
  grouping/planning function, Then the system groups host companies located near one another together
  to support planning (the automation level of this function is still an unconfirmed assumption not
  yet validated with users, see [Assumption 5](../requirements/spec.md)). The result of this grouping
  serves as a basis for the coordinator to assign supervising instructors per route group per
  [FR-32](./acceptance-criteria.md).

#### FR-32 (High) — [Assign supervising instructors by route group (new 2026-09-16)](../requirements/spec.md)

- **AC-1 (assign one instructor per route group):** Given the coordinator has at least one group of
  host companies grouped by nearby area (FR-17), When the coordinator assigns one Supervising
  Instructor to be responsible for that route group, Then the system records the assignment and
  requires that all host companies in the same group be assigned to the same instructor (1:1
  relationship between Supervising Instructor and company per [FR-18](./acceptance-criteria.md)).
- **AC-2 (manual assignment possible even without full automation):** Given the automatic grouping
  function (FR-17) does not yet cover every case per assumption 5 of the spec, When the coordinator
  manually selects a host company and Supervising Instructor and clicks assign (without going through
  the automatic grouping result), Then the system accepts the manual assignment and records it just
  like AC-1.

> Note (updated 2026-09-16): The case where the coordinator tries to assign a second Supervising
> Instructor to a host company that already has a responsible Supervising Instructor (conflicting
> with the 1:1 relationship of FR-18) — previously an edge case whose behavior the spec had not
> specified — is now defined by the new requirement
> [FR-34](./acceptance-criteria.md). See FR-34's ACs below for the full desired behavior in every
> case (with/without an existing responsible instructor, confirm/cancel).

#### FR-34 (High) — [Confirm before replacing an existing supervising instructor assignment (new 2026-09-16)](../requirements/spec.md)

- **AC-1 (no existing responsible instructor — save immediately):** Given the host company the
  coordinator is about to assign a Supervising Instructor to has no responsible Supervising Instructor
  beforehand (not conflicting with the 1:1 relationship of [FR-18](./acceptance-criteria.md)), When
  the coordinator selects a Supervising Instructor and clicks assign
  ([FR-32](./acceptance-criteria.md)), Then the system records the assignment immediately without
  showing any confirmation box or extra step.
- **AC-2 (existing responsible instructor — must request confirmation first):** Given that host
  company already has a responsible Supervising Instructor (conflicting with the 1:1 relationship of
  FR-18), When the coordinator tries to assign a new Supervising Instructor to this same host company,
  Then the system must not reject the assignment immediately and must not automatically overwrite the
  existing instructor, but must show the existing assignment information (the existing Supervising
  Instructor's name) together with a box for the coordinator to choose to confirm the
  cancellation/replacement or cancel this assignment, before the system proceeds.
- **AC-3 (confirm replacement — record anew with history):** Given the system has shown the box
  confirming replacement of the existing assignment (AC-2), When the coordinator clicks to confirm the
  cancellation/replacement of the existing assignment, Then the system records the new Supervising
  Instructor as responsible in place of the previous one for that host company, and records the
  history of the responsibility change (old instructor → new instructor, who performed the action,
  date-time of the action) for later auditing per [NFR-02](./acceptance-criteria.md).
- **AC-4 (cancel — keep the existing assignment):** Given the system has shown the box confirming
  replacement of the existing assignment (AC-2), When the coordinator clicks cancel instead of
  confirming, Then the system records no changes, the previously responsible Supervising Instructor
  remains responsible for that host company exactly as before this assignment attempt, and the system
  records no additional change history.

#### NFR-02 (High) — [Audit — context of replacing a supervising instructor assignment](../requirements/spec.md)

- **AC-1:** Given the coordinator has successfully confirmed replacing the existing Supervising
  Instructor assignment of a host company (FR-34 AC-3), When an authorized user opens the Supervising
  Instructor assignment history of that host company, Then the system displays the previous
  Supervising Instructor's name, the new Supervising Instructor's name, the name of the person who
  made the change, and the date-time of the action, for every time a replacement of the assignment has
  occurred.

#### NFR-04 (High) — [Map rendering performance](../requirements/spec.md)

- **AC-1:** Given pins of the entire cohort's host companies are displayed on the map simultaneously
  (a large number), When the user opens/pans the combined map, Then the map renders and responds
  without lag that disrupts normal use.

## 6. Score and Record Interview Results During Supervision

Reference: [Score and record interview results during supervision](../design/feature-list.md)

#### FR-18 (High) — [One supervising instructor per company (revised 2026-09-16)](../requirements/spec.md)

> **Revised 2026-09-16:** FR-18 was originally "support multiple supervising instructors per round";
> it was changed to "one supervising instructor per company" per the new requirement — the original
> ACs referencing multiple instructors per round have been entirely replaced by the ACs below
> (priority remains "High" per [backlog](../requirements/backlog.md)).

- **AC-1 (1:1 throughout the internship round):** Given a host company/student has been assigned a
  Supervising Instructor per [FR-32](./acceptance-criteria.md), When the responsible supervisor of
  that host company is checked throughout the 3-month internship round, Then the system shows only one
  responsible Supervising Instructor for that host company, with no other Supervising Instructor
  co-responsible at the same time in the same round.
- **AC-2 (restrict recording rights to the responsible instructor only):** Given a host company has
  an assigned responsible Supervising Instructor (FR-32), When another Supervising Instructor who is
  not the assigned one tries to record scores/interview results for that company's supervision round,
  Then the system rejects the recording and states it is not authorized, because they are not the
  responsible Supervising Instructor of this company.

#### FR-19 (High) — [Record scores per the scoring form/rubric](../requirements/spec.md)

- **AC-1 (on-site):** Given the Supervising Instructor has completed an **on-site** supervision visit
  to the student at the host company (see [FR-33](./acceptance-criteria.md)), When the Supervising
  Instructor fills in the scores per the scoring form/rubric across all assessed dimensions (see the
  draft example in [Appendix, Section 7](../requirements/spec.md)) and saves, Then the system records
  the Supervising Instructor's scores with that supervision round, also marking the mode as on-site.
- **AC-2 (online):** Given the Supervising Instructor has completed supervising the student via an
  **online** channel (FR-33), When the Supervising Instructor fills in the scores per the scoring
  form/rubric across all assessed dimensions and saves, Then the system records the Supervising
  Instructor's scores with that supervision round successfully just like the on-site case, also
  marking the mode as online (without needing to meet the field/offline conditions per NFR-03/NFR-07).

#### FR-20 (High) — [Record interview form results](../requirements/spec.md)

- **AC-1 (on-site):** Given the Supervising Instructor interviews the student at the host company
  **on-site** (FR-33), When the Supervising Instructor records the answers/results of the interview
  form per the defined question set (see the draft example in
  [Appendix, Section 7](../requirements/spec.md)), Then the system records the interview form results
  with that supervision round, also marking the mode as on-site.
- **AC-2 (online):** Given the Supervising Instructor interviews the student via an **online** channel
  (FR-33), When the Supervising Instructor records the answers/results of the interview form per the
  defined question set, Then the system records the interview form results with that supervision round
  successfully just like the on-site case, also marking the mode as online.

#### ~~FR-21~~ (Deprecated — removed on 2026-09-16) — Aggregate total score from multiple supervising instructors

> **Removed — no longer part of the active test scope.** Because FR-18 changed to "one supervising
> instructor per company", there is no longer a multiple-instructors-per-round use case. The original
> ACs of FR-21 have been removed from this file (not counted in this feature's AC total). For the
> original content and full rationale, see *(Deprecated — FR-21/FR-30, removed from scope)* — this
> code is permanently reserved and will not be reused.

#### ~~FR-30~~ (Deprecated — removed on 2026-09-16) — Manually set the summary score (manual override) when there are multiple supervising instructors

> **Removed — no longer part of the active test scope.** Same rationale as FR-21 above. The original
> ACs of FR-30 have been removed from this file (not counted in this feature's AC total). See
> *(Deprecated — FR-21/FR-30, removed from scope)* — this code is permanently reserved and will not
> be reused.

#### FR-33 (High) — [Set the supervision mode (Online/On-site) per session (new 2026-09-16)](../requirements/spec.md)

- **AC-1 (choose on-site):** Given the Supervising Instructor starts recording one supervision round
  for a company they are responsible for, When the Supervising Instructor chooses this session's
  supervision mode as **"on-site"**, Then the system binds that supervision round to the pinned
  coordinates of the host company ([FR-16](./acceptance-criteria.md)) and enables the field/offline
  conditions ([NFR-03](./acceptance-criteria.md)/[NFR-07](./acceptance-criteria.md)) for this round.
- **AC-2 (choose online):** Given the Supervising Instructor starts recording one supervision round
  for a company they are responsible for, When the Supervising Instructor chooses this session's
  supervision mode as **"online"**, Then the system does not require any coordinates/route and does
  not enter the NFR-03/NFR-07 conditions for this round (treated as using a normal device/internet).
- **AC-3 (recording scores/interview succeeds in both modes):** Given the supervision round has had
  its mode set, whether online or on-site (AC-1/AC-2), When the Supervising Instructor records scores
  per the rubric ([FR-19](./acceptance-criteria.md)) and the interview form results
  ([FR-20](./acceptance-criteria.md)) of that round, Then the system records the data successfully in
  both cases, with the chosen mode (online/on-site) always recorded alongside that supervision result.

#### NFR-03 (High) — [Field use (required for on-site only)](../requirements/spec.md)

- **AC-1:** Given the Supervising Instructor is recording scores/interview results via a mobile device
  at the host company in a supervision round whose mode is set as **on-site** (FR-33) and the internet
  signal is unstable, When the signal drops temporarily during data entry and reconnects before
  leaving the screen, Then the entered data must not be lost and must be saved to the system
  successfully once the signal returns.
  > Note: This condition applies only to on-site supervision rounds; online supervision rounds do not
  > fall under this condition (see FR-33). For cases of no signal for a long continuous period or
  > closing the app before the signal returns, see [NFR-07](./acceptance-criteria.md), which directly
  > extends this NFR-03.

#### NFR-07 (High) — [Offline operation and data sync (Offline Draft & Auto-Sync) (required for on-site only)](../requirements/spec.md)

- **AC-1 (store local draft indefinitely — on-site only):** Given the Supervising Instructor is
  recording scores/interview results via a mobile device in a supervision round whose mode is set as
  **on-site** (FR-33) with no internet signal at that moment, When the Supervising Instructor clicks
  save, Then the system stores the data as a local draft on the device immediately without any time
  limit on how long it is kept, and does not automatically delete the draft no matter how long it
  remains.
- **AC-2 (auto-retry when the signal returns):** Given there is an unsynced local draft of an on-site
  supervision round pending on the device (AC-1), When the internet signal becomes available again,
  Then the system auto-retries syncing the data to the server automatically without the user having to
  press sync, and when the sync succeeds the data is saved to the system just like the normal-signal
  case.
- **AC-3 (banner notifying pending-sync data):** Given there is an unsynced local draft of an on-site
  supervision round pending on the device (whether pending for a short or long time), When the user
  opens/uses the app while the sync has not yet succeeded, Then the system shows a message/banner
  notifying that there is pending-sync data throughout that period until the sync succeeds.
  > Note: This condition (AC-1 to AC-3) applies only to on-site supervision rounds; online supervision
  > rounds do not fall under NFR-07 (see FR-33).

## 7. Confirm Data Entry with the Existing Core Internship System

Reference: [Confirm data entry with the existing core internship system](../design/feature-list.md)

#### FR-22 (High) — [Confirm data entry in the existing core internship system](../requirements/spec.md)

- **AC-1:** Given the student has recorded their task/daily data in the existing core internship
  system (outside this system), When the student manually self-declares in this system that they have
  recorded it, Then the system records that confirmation with that student.

#### FR-23 (High) — [Update status upon confirmation](../requirements/spec.md)

- **AC-1:** Given the student self-declares that they have recorded data in the existing core
  internship system (FR-22), When the confirmation succeeds, Then the system updates that student's
  overall status to reflect this confirmation.

#### NFR-02 (High) — [Audit — context of self-declaration with the existing core internship system](../requirements/spec.md)

- **AC-1:** Given the student self-declares that they have recorded data in the existing core
  internship system, When the confirmation succeeds, Then the system records the time the student
  confirmed as part of an audit trail that can be reviewed later.

## 8. Internship Completion and Thank-you Letter to the Host Company

Reference: [Internship completion and thank-you letter to the host company](../design/feature-list.md)

#### FR-24 (High) — [Change status upon internship completion](../requirements/spec.md)

- **AC-1:** Given the student has interned for the full 3-month planned duration, When the planned
  completion date arrives, Then the system automatically changes that student's status to "internship
  ended".

#### FR-25 (High) — [Generate the thank-you letter to the host company](../requirements/spec.md)

- **AC-1:** Given the student has the status "internship ended" (FR-24) and complete
  student/host company data in the system, When the coordinator instructs the system to generate the
  thank-you letter to the host company, Then the system generates the document from a template by
  pulling the recorded student and host company data into the document, without a signature.

#### FR-35 (Medium) — [Notify the student when the host company evaluation is completed (new 2026-09-17)](../requirements/spec.md)

> **Note:** Per assumption 7 of the spec ([Assumption 7](../requirements/spec.md) — not yet confirmed
> with users), this document assumes the host company does not yet have an account in this system, so
> the Internship Coordinator/Academic Advisor records the "host company evaluation completed"
> milestone on the host company's behalf (analogous to the self-declare approach of FR-22/FR-23). The
> ACs below are therefore written referencing this "recording on behalf" as the milestone trigger,
> not the host company filling in a form itself. This milestone is a notification running in parallel
> with FR-24/FR-25, not a gate that blocks the internship-ended status change (see
> [Section 11](../requirements/spec.md)).

- **AC-1 (evaluation recorded as completed → notify the student):** Given the student has the status
  "internship ended" (FR-24) and no host company evaluation result for that student has been recorded
  in the system yet, When the Internship Coordinator/Academic Advisor records on the host company's
  behalf that the host company evaluation is completed (milestone: Workplace Evaluation Completed),
  Then the system immediately notifies that student that the host company evaluation is completed
  (Student Notified).
- **AC-2 (before recording — not yet notified):** Given the student has the status "internship ended"
  (FR-24) but no one has recorded any host company evaluation result for that student in the system
  yet, When the student opens their own status/notification list, Then the system must not show a
  notification that the host company evaluation is completed (the student is not notified until a
  recording per AC-1 occurs).

#### NFR-02 (High) — [Audit — context of internship completion](../requirements/spec.md)

- **AC-1:** Given the student's status changes to "internship ended" (FR-24), When the status change
  occurs, Then the system records the time of the status change as part of an audit trail.

#### NFR-05 (High) — [Correctness of auto-generated documents](../requirements/spec.md)

- **AC-1:** Given the system generates the thank-you letter to the host company from a template
  (FR-25), When the generated document is checked, Then the document's format/structure must match the
  official format of the university/school, and the student/host company data shown in the document
  must match the data recorded in the system in every field.

## 9. Record and Track Problem Cases During the Internship

Reference: [Record and track problem cases during the internship](../design/feature-list.md)

#### FR-26 (High) — [Record cases of being returned/dismissed during the internship](../requirements/spec.md)

- **AC-1:** Given the student is currently interning (status "interning"), When the
  coordinator/Supervising Instructor records a case of the student being returned/dismissed, together
  with the date and reason, Then the system records that case with the recorder's name and changes the
  student's status to "must find a new internship placement".
- **AC-2 (continuation):** Given the student's status was changed to "must find a new internship
  placement" (AC-1), When the student begins the process of submitting a new host company, Then the
  system allows submitting new host company details just like the normal process (FR-03).

#### FR-27 (High) — [Record cases of students at risk of not passing](../requirements/spec.md)

- **AC-1:** Given a student's internship results trend toward being at risk of not passing, When the
  Supervising Instructor/coordinator records this case together with details of the assistance
  measures taken, Then the system records that case with the student, complete with the assistance
  details.

#### FR-28 (Medium) — [Display problem-case history/timeline](../requirements/spec.md)

- **AC-1:** Given a student has problem cases recorded more than once (e.g., both a returned/dismissed
  case and an at-risk-of-not-passing case), When an authorized user opens that student's problem-case
  history, Then the system displays all problem cases ordered chronologically as a single timeline.

#### NFR-02 (High) — [Audit — context of recording problem cases](../requirements/spec.md)

- **AC-1:** Given a problem case (returned/dismissed, or at risk of not passing) of a student has been
  recorded, When the recording succeeds, Then the system records the recorder's name and the date-time
  recorded as part of an audit trail that also appears in the timeline.

## 10. Notify Proposal Presentation and Supervision Schedules

Reference: [Notify proposal presentation and supervision schedules](../design/feature-list.md)

#### FR-29 (Medium) — [Notify proposal presentation/supervision dates](../requirements/spec.md)

- **AC-1 (presentation):** Given the student has a recorded host company proposal presentation
  appointment date (FR-04) and the current date meets the "approaching deadline" criterion per the
  advance-notification lead-time policy set in the system (see [FR-31](./acceptance-criteria.md)),
  When the time arrives at which the system detects the criterion is met, Then the system notifies the
  relevant Academic Advisor.
- **AC-2 (supervision):** Given there is a supervision schedule for a student the Supervising
  Instructor oversees, and the current date meets the "approaching deadline" criterion per the
  advance-notification lead-time policy set in the same system (FR-31), When the time arrives at which
  the system detects the criterion is met, Then the system notifies the relevant Supervising
  Instructor.

#### FR-31 (Medium) — [Advance-notification lead-time policy (configurable)](../requirements/spec.md)

- **AC-1 (default value):** Given the coordinator has never adjusted this semester's
  advance-notification lead-time policy value, When the system checks whether the "approaching
  deadline" criterion is met (presentation date/supervision date per FR-29 or planned internship start
  date per FR-15), Then the system uses the default value set in the system (the recommended value is
  7 days) as the notification criterion.
- **AC-2 (adjustable):** Given the coordinator adjusts this semester's advance-notification lead-time
  policy value to another value (e.g., 10 days), When the system checks whether the "approaching
  deadline" criterion is met, Then the system uses the latest value adjusted by the coordinator as the
  criterion (not the original default) and uses this same value jointly for both FR-15 and FR-29.
  > Note: The numeric value "7 days" is only a recommended default, not yet a fixed conclusion per the
  > spec (assumption 6) — so every related AC in this document (FR-15, FR-29, FR-31) references "the
  > value set in the system" rather than hard-coding a fixed number of days, so that tests are not
  > brittle when the value is adjusted.

## Related Documents

- [feature-list](../design/feature-list.md) — the full feature list with MoSCoW
- [backlog](../requirements/backlog.md) — summary of all FR/NFR with priorities
- [spec](../requirements/spec.md) — the source spec document
- [user-journey](../design/user-journey.md) — real usage flows by role
- [test-plan](./test-plan.md) — testing strategy overview
