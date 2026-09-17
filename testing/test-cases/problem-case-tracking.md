# Test Cases — Recording and Tracking Problem Cases During the Internship

Step-by-step test cases for the feature [9. Recording and Tracking Problem Cases During the Internship](../../design/feature-list.md), referencing the acceptance criteria in [acceptance-criteria](../acceptance-criteria.md) and the flow in [user-journey](../../design/user-journey.md).

| ID | Test case name | Precondition | Steps | Expected result | AC tested | FR/NFR code | Priority |
|---|---|---|---|---|---|---|---|
| TC-09-01 | Record a case of being returned/dismissed from the internship | The Student is currently on the internship (status "internship in progress") | 1. Log in with an Internship Coordinator/Supervising Instructor account<br>2. Open the problem-case recording page for that Student<br>3. Record the case of being returned/dismissed, with the date and reason | The system saves the case along with the name of the person who recorded it, and changes the Student's status to "must find a new internship placement" | [FR-26 AC-1](../acceptance-criteria.md) | FR-26 | High |
| TC-09-02 | A Student who was returned/dismissed can submit a new host company | The Student has been changed to the status "must find a new internship placement" (continuing from TC-09-01) | 1. Log in with that Student's account<br>2. Open the new host company submission page<br>3. Fill in the new host company information and save | The system allows submitting new host company information the same as the normal process (equivalent to FR-03) | [FR-26 AC-2](../acceptance-criteria.md) | FR-26 | High |
| TC-09-03 | Record a case of a Student at risk of not passing, with the remedial measures | A Student has internship results that trend toward being at risk of not passing | 1. Log in with a Supervising Instructor/Internship Coordinator account<br>2. Open the problem-case recording page for that Student<br>3. Record the at-risk-of-not-passing case, with details of the remedial measures taken | The system saves that case with that Student along with the complete remedial details | [FR-27 AC-1](../acceptance-criteria.md) | FR-27 | High |
| TC-09-04 | Display a timeline of multiple problem cases | A Student has had problem cases recorded more than once (e.g. both a returned/dismissed case and an at-risk-of-not-passing case, continuing from TC-09-01 and TC-09-03) | 1. Open the problem-case history for that Student | The system displays all problem cases ordered chronologically as a single timeline | [FR-28 AC-1](../acceptance-criteria.md) | FR-28 | Medium |
| TC-09-05 | Check the audit trail for recording a problem case | A problem case has been recorded for a Student (continuing from TC-09-01 or TC-09-03) | 1. Open the details of a problem case in that Student's timeline | The system shows the name of the person who recorded it and the date and time it was recorded as part of the audit trail in the timeline | [NFR-02 AC-1](../acceptance-criteria.md) | NFR-02 | High |

## Related documents

- [Acceptance criteria — 9. Recording and Tracking Problem Cases During the Internship](../acceptance-criteria.md)
- [Feature list — 9. Recording and Tracking Problem Cases During the Internship](../../design/feature-list.md)
- [User journey](../../design/user-journey.md)
- [Test plan](../test-plan.md)
