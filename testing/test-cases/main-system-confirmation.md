# Test Cases — Confirming Data Recording with the Existing Core Internship System

Step-by-step test cases for the feature [7. Confirming Data Recording with the Existing Core Internship System](../../design/feature-list.md), referencing the acceptance criteria in [acceptance-criteria](../acceptance-criteria.md) and the flow in [user-journey](../../design/user-journey.md).

| ID | Test case name | Precondition | Steps | Expected result | AC tested | FR/NFR code | Priority |
|---|---|---|---|---|---|---|---|
| TC-07-01 | Student self-declares that they have recorded data in the core system | The Student has finished recording their daily task/data in the existing core internship system (outside this system) | 1. Log in with a Student account<br>2. Open the data-recording confirmation page<br>3. Click confirm (self-declare) | The system saves that confirmation with that Student | [FR-22 AC-1](../acceptance-criteria.md) | FR-22 | High |
| TC-07-02 | The system updates the overview status upon receiving the confirmation | The Student has just self-declared successfully (continuing from TC-07-01) | 1. Open that Student's overview status (from the Student's own status page or the dashboard) | That Student's overview status now reflects this confirmation | [FR-23 AC-1](../acceptance-criteria.md) | FR-23 | High |
| TC-07-03 | Check the audit trail of the confirmation | The Student has self-declared successfully (continuing from TC-07-01) | 1. The Internship Coordinator opens the confirmation history for that Student | The system shows the time the Student confirmed as part of an audit trail that can be reviewed retrospectively | [NFR-02 AC-1](../acceptance-criteria.md) | NFR-02 | High |

## Related documents

- [Acceptance criteria — 7. Confirming Data Recording with the Existing Core Internship System](../acceptance-criteria.md)
- [Feature list — 7. Confirming Data Recording with the Existing Core Internship System](../../design/feature-list.md)
- [User journey](../../design/user-journey.md)
- [Test plan](../test-plan.md)
