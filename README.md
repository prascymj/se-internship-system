# Internship Management System — Documentation

🇹🇭 **[อ่านฉบับภาษาไทย](th/)**

A software requirements and design documentation set for the **Internship Management System**, developed to support and track the student internship process at **University of Phayao**.

This site collects the English documentation so students can understand the internship workflow, the roles involved, and how each stage is handled by the system.

> This system complements the school's **existing core internship system** (where students log daily tasks and host companies review them). It focuses on the surrounding workflow: proposing a company, presenting to an advisor, checking eligibility, managing documents, supervision visits, and post-internship paperwork.

---

## The internship process at a glance

1. **Track status** — each student sees their current stage in the internship process for the semester.
2. **Propose a host company & present** — the student proposes a company and books a presentation with their academic advisor. If not approved, they find a new company and present again.
3. **Check training eligibility** — the student must complete the required training sessions and upload a certificate for each.
4. **Upload acceptance documents** — three letters: the Request Letter, the Acceptance Letter, and the Referral (Placement) Letter.
5. **On-site supervision (3 months)** — the student pins the host company on Google Map; the Internship Coordinator assigns one Supervising Instructor per company by route group; supervision can be **online or on-site**; instructors score using a form/rubric and an interview.
6. **Confirm with the core system** — the student confirms they have logged their tasks in the existing core internship system.
7. **Completion & thank-you letter** — when the internship ends, a Thank-you Letter to the host company is generated. When the host company's evaluation of the student is recorded as complete, the student is notified.
8. **Problem handling** — if a student is returned/dismissed mid-internship, it is recorded and they find a new placement; at-risk cases are tracked with the actions taken.

---

## Documentation map

### Requirements
- **[Requirements Specification](requirements/spec.md)** — the full functional (FR) and non-functional (NFR) requirements, with the supervision scoring form, rubric, and interview questions in the appendix.
- **[Backlog](requirements/backlog.md)** — all FR/NFR items summarized by priority.

### Design
- **[Feature List](design/feature-list.md)** — requirements grouped into user-facing features with MoSCoW priority.
- **[User Journeys](design/user-journey.md)** — the flow of the system by role (Student, Academic Advisor, Internship Coordinator, Supervising Instructor), each with a flowchart.

### Testing
- **[Test Plan](testing/test-plan.md)** — overall testing strategy, scope, and entry/exit criteria.
- **[Acceptance Criteria](testing/acceptance-criteria.md)** — Given-When-Then criteria for every requirement.
- **[Test Cases](testing/test-cases/)** — step-by-step test cases per feature.

---

## Roles

| Role | Responsibility |
|---|---|
| **Student** | Proposes a company, uploads documents, pins the location, confirms task logging |
| **Academic Advisor** | Reviews and approves the company proposal presentation |
| **Internship Coordinator** | Checks eligibility/documents, assigns supervising instructors, generates letters, handles problem cases |
| **Supervising Instructor** | Conducts the supervision visit (online/on-site) and scores the student (one per company) |

---

*Source documentation is maintained in Thai; this is the English edition prepared for student communication. Requirement codes (FR-xx / NFR-xx) are kept identical across both editions for traceability.*
