# Test Cases — Ending the Internship and the Thank-you Letter to the Host Company

Step-by-step test cases for the feature [8. Ending the Internship and the Thank-you Letter to the Host Company](../../design/feature-list.md), referencing the acceptance criteria in [acceptance-criteria](../acceptance-criteria.md) and the flow in [user-journey](../../design/user-journey.md).

| ID | Test case name | Precondition | Steps | Expected result | AC tested | FR/NFR code | Priority |
|---|---|---|---|---|---|---|---|
| TC-08-01 | The system changes the status to internship-ended after 4 months | The Student has completed the full 4-month internship period per the defined plan | 1. The plan's due date for that Student arrives (or simulate the due date)<br>2. Check that Student's status | The system changes that Student's status to "internship ended" automatically | [FR-24 AC-1](../acceptance-criteria.md) | FR-24 | High |
| TC-08-02 | The Internship Coordinator generates the Thank-you Letter to the host company | The Student has the status "internship ended" and complete Student/host company information exists in the system (continuing from TC-08-01) | 1. Log in with an Internship Coordinator account<br>2. Open the Thank-you Letter generation page for that Student<br>3. Instruct the system to generate the document | The system generates the document from a template, pulling in the saved Student and host company information without a signature | [FR-25 AC-1](../acceptance-criteria.md) | FR-25 | High |
| TC-08-03 | Check the audit trail for the internship-ended status change | The Student has just changed status to "internship ended" (continuing from TC-08-01) | 1. Open the status-change history for that Student | The system records the time of the status change as part of the audit trail | [NFR-02 AC-1](../acceptance-criteria.md) | NFR-02 | High |
| TC-08-04 | Verify the correctness of the auto-generated document | The system has generated the Thank-you Letter to the host company (continuing from TC-08-02) | 1. Open and inspect the generated document<br>2. Compare the Student/host company information in the document against the information saved in the system, field by field<br>3. Compare the document's format/structure against the official format of the university/school | The document's format/structure matches the official format, and every field in the document matches the information saved in the system | [NFR-05 AC-1](../acceptance-criteria.md) | NFR-05 | High |

## Related documents

- [Acceptance criteria — 8. Ending the Internship and the Thank-you Letter to the Host Company](../acceptance-criteria.md)
- [Feature list — 8. Ending the Internship and the Thank-you Letter to the Host Company](../../design/feature-list.md)
- [User journey](../../design/user-journey.md)
- [Test plan](../test-plan.md)
