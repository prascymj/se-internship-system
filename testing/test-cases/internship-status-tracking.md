# Test Cases — Tracking the Internship Process Status

Step-by-step test cases for the feature [1. Tracking the Internship Process Status](../../design/feature-list.md), referencing the acceptance criteria in [acceptance-criteria](../acceptance-criteria.md) and the flow in [user-journey](../../design/user-journey.md).

| ID | Test case name | Precondition | Steps | Expected result | AC tested | FR/NFR code | Priority |
|---|---|---|---|---|---|---|---|
| TC-01-01 | Student views their own current status | The Student has an account in the system and is currently in the status "approved" (has passed the host company proposal presentation) | 1. Log in with a Student account<br>2. Open the "My Status" page | The system shows the current status "approved", matching the Student's real progress | [FR-01 AC-1](../acceptance-criteria.md) | FR-01 | High |
| TC-01-02 | A new Student sees the initial status | The Student has not taken any action yet in this semester | 1. Log in with a Student account that has just started the semester<br>2. Open the "My Status" page for the first time | The system shows the initial status "host company not yet submitted" | [FR-01 AC-2](../acceptance-criteria.md) | FR-01 | High |
| TC-01-03 | An Academic Advisor/Internship Coordinator views the overview dashboard | Several Students in the same semester have different statuses | 1. Log in with an Academic Advisor or Internship Coordinator account<br>2. Open the overview dashboard page | The system shows a table listing all Students in the same semester with each one's current status | [FR-02 AC-1](../acceptance-criteria.md) | FR-02 | High |
| TC-01-04 | Filter the dashboard by status | On the overview dashboard with Students of several mixed statuses (continuing from TC-01-03) | 1. On the overview dashboard page<br>2. Select the status filter "internship in progress" | The table shows only Students with the status "internship in progress"; other rows are hidden | [FR-02 AC-2](../acceptance-criteria.md) | FR-02 | High |
| TC-01-05 | Check the audit trail for a status change from the dashboard | A Student has had their status changed at least once before (e.g. from "awaiting proposal presentation" to "approved") | 1. Log in with an authorized account (Academic Advisor/Internship Coordinator)<br>2. Open the status history/details for that Student from the dashboard | The system shows the name of the person who performed the status change and the date and time of the action for every past change | [NFR-02 AC-1](../acceptance-criteria.md) | NFR-02 | High |

## Related documents

- [Acceptance criteria — 1. Tracking the Internship Process Status](../acceptance-criteria.md)
- [Feature list — 1. Tracking the Internship Process Status](../../design/feature-list.md)
- [User journey](../../design/user-journey.md)
- [Test plan](../test-plan.md)
