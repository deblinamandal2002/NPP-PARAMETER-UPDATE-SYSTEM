# Business Requirements Document (BRD)
## NPP Parameter Update System

| Document field | Value |
|---|---|
| Document type | Business Requirements Document |
| Project | NPP Parameter Update System |
| Version | 1.0 – Draft for validation |
| Prepared for | Project stakeholders / academic project review |
| Prepared by | Project team |
| Status | Draft – validate against the implemented application |

---

## 1. Purpose

This document describes the business context, objectives, scope, stakeholders, high-level requirements and success measures for the NPP Parameter Update System.

The system is documented as an application intended to support the recording, updating, viewing and review of nuclear power plant (NPP) operational parameter information. This BRD is based on the project description available for this repository. Details that cannot be confirmed from the available implementation evidence are explicitly identified as assumptions or items requiring stakeholder validation.

## 2. Business context and problem statement

Operational teams need parameter information to be recorded and made available in a structured and consistent manner. When parameter updates are handled through disconnected or manual records, users may face difficulty locating the latest information, understanding what has changed, and coordinating review of updates.

The project aims to provide a centralized application interface for managing parameter information and supporting operational visibility. The intended business value is better organization of parameter records and a more consistent update workflow.

**Important boundary:** This project documentation describes an information-management application/prototype. It does not establish that the application is connected to live plant instrumentation, distributed control systems, safety systems or production nuclear infrastructure. It must not be represented as controlling plant equipment or authorizing safety-critical operating changes unless separately verified and formally approved.

## 3. Business objectives

- Provide a structured interface for viewing and maintaining parameter information.
- Reduce dependence on scattered or manually maintained records where the application is used.
- Make parameter information easier for relevant users to locate and review.
- Support a consistent process for submitting and checking parameter updates, where those workflow features are implemented.
- Improve visibility of parameter records for operational coordination.

## 4. Stakeholders and user groups

The following are logical stakeholder groups for validating the requirements. Their existence as configured application roles must be confirmed against the code and project owner.

| Stakeholder / user group | Interest or responsibility |
|---|---|
| Parameter data entry user | Enters or proposes parameter information and corrections |
| Reviewer / supervisor | Reviews submitted information if a review workflow exists |
| System administrator | Maintains application configuration and user access if administration is implemented |
| Operations team | Uses relevant parameter information for operational awareness |
| Project owner / business representative | Confirms business rules, scope and acceptance criteria |
| Development / support team | Maintains the application and resolves defects |

## 5. Scope

### 5.1 In scope (business intent)

- Presenting NPP parameter information through an application interface.
- Supporting parameter entry or update operations to the extent implemented.
- Displaying stored parameter information.
- Applying basic input checks where implemented.
- Supporting review of parameter information where a review function exists.
- Providing a maintainable project structure and supporting documentation.

### 5.2 Out of scope unless separately demonstrated and approved

- Direct control of plant equipment or operational processes.
- Integration with live sensors, SCADA, DCS, PLCs or plant control networks.
- Safety-system decision-making, alarms or automatic protective actions.
- Predictive maintenance, AI-based recommendations or forecasting.
- Enterprise identity management, role-based authorization, encryption, audit trails, backups, high availability or disaster recovery beyond what the source code and deployment evidence demonstrate.
- Production deployment or certification for use in a nuclear facility.

## 6. High-level business requirements

| ID | Business requirement | Priority | Acceptance evidence |
|---|---|---|---|
| BR-01 | The application shall provide a clear interface for accessing NPP parameter information. | Must | Demonstration of the relevant screen and navigation |
| BR-02 | The application shall support creating or entering parameter information if this function is part of the implemented build. | Must – validate | Successful entry using an agreed test record |
| BR-03 | The application shall support updating an existing parameter record if update functionality is implemented. | Must – validate | Existing test record can be changed and the result displayed |
| BR-04 | The application shall present parameter information in a readable and organized format. | Must | Representative records are displayed correctly |
| BR-05 | The application shall check required inputs and reject invalid values according to confirmed business rules. | Should | Positive and negative input tests |
| BR-06 | The application shall make the outcome of a user action clear (for example, success or validation feedback) where implemented. | Should | Demonstration of feedback for success and failure |
| BR-07 | If a review or approval process exists, the application shall make the review state visible to the relevant users. | Conditional | Demonstration of each implemented state and transition |
| BR-08 | Parameter records shall be stored and retrieved consistently by the configured data layer. | Must – validate | Test evidence from the actual persistence implementation |

## 7. Business rules requiring confirmation

The following rules must be confirmed with the project owner or from the implemented code before they are treated as final:

1. Which parameter fields are mandatory?
2. What units, data types, permitted ranges and precision apply to each parameter?
3. Are duplicate parameter identifiers allowed?
4. Can users edit an existing record after submission?
5. Is a reviewer or approval step required?
6. Which user groups can create, view, edit or delete records?
7. Is deletion permitted, or should records be retained?
8. Is a timestamp, user identity or change history captured?
9. What should happen when a save operation fails or the database is unavailable?
10. Are any values restricted to read-only display because of operational or safety requirements?

No numeric operating limits or plant-specific thresholds are defined in this document.

## 8. Assumptions and dependencies

- The application is treated as a project-level information-management solution, not a certified plant-control system.
- The available project description identifies HTML, CSS, JavaScript and SQL among the technologies used. The exact division of frontend and backend responsibilities, database engine and deployed architecture must be checked against the repository.
- Access to the actual application, source code, database schema and test data is required to validate detailed requirements.
- Any plant-specific parameter definitions, permitted ranges and approval policies must be supplied by an authorized subject-matter expert.
- The application must use synthetic or approved non-production data for demonstrations unless formal authorization states otherwise.

## 9. Success measures

Success should be evaluated using observable project evidence rather than unverified claims. Suggested measures include:

- A user can locate and view a representative parameter record.
- A valid parameter entry or update is processed correctly, if implemented.
- Invalid or incomplete inputs receive understandable feedback, if validation is implemented.
- Stored information can be retrieved consistently.
- Demonstrated user workflows match the agreed requirements.

Any claimed percentage improvement, number of workstations, uptime figure or reduction in manual effort must be supported by a documented baseline, measurement method and test or operational evidence before inclusion in a final BRD.

## 10. Risks and constraints

| Risk / constraint | Potential impact | Suggested treatment |
|---|---|---|
| Unconfirmed parameter rules | Incorrect or inconsistent records | Obtain approved field definitions and validation rules |
| Unclear user permissions | Unauthorized or accidental changes | Define and test access rules before any real deployment |
| Missing change history | Difficulty tracing modifications | Confirm whether audit history is required and implemented |
| Database or network failure | Updates may not be saved | Define error handling and recovery expectations |
| Misinterpretation as a plant-control tool | Serious operational and compliance risk | Clearly label the system as a project prototype unless formally certified |
| Unverified performance claims | Misleading project reporting | Publish metrics only with reproducible evidence |

## 11. Acceptance and sign-off

The BRD should be reviewed by the project owner and relevant technical stakeholders. Approval should confirm:

- Business objectives and scope.
- User groups and responsibilities.
- Parameter definitions and business rules.
- Priorities and acceptance evidence.
- Explicit exclusions and deployment limitations.

| Role | Name | Approval / date |
|---|---|---|
| Business / project owner | To be confirmed | Pending |
| Technical reviewer | To be confirmed | Pending |
| Project representative | To be confirmed | Pending |

## 12. Change history

| Version | Date | Description |
|---|---|---|
| 1.0 | 18 November 2026 | Initial draft prepared for repository documentation; requires validation against implementation |
