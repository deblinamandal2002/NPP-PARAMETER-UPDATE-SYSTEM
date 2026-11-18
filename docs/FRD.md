# Functional Requirements Document (FRD)
## NPP Parameter Update System

| Document field | Value |
|---|---|
| Document type | Functional Requirements Document |
| Project | NPP Parameter Update System |
| Version | 1.0 – Draft for validation |
| Related document | `BRD.md` |
| Status | Draft – validate against source code and running application |

---

## 1. Purpose

This document translates the business intent in the BRD into functional behaviours that can be reviewed and tested. It describes expected system interactions for parameter information management.

**Implementation note:** This FRD is a requirements baseline, not proof that every listed feature is already present. Requirements marked **Conditional / verify** must be checked against the repository and running application before being described as implemented.

## 2. System overview

The project is described as a web-based interface for managing NPP parameter information. The available project context identifies HTML, CSS, JavaScript and SQL as technologies used. The exact backend framework, database engine, API design, authentication mechanism and deployment topology are not confirmed here.

### 2.1 High-level interaction

1. A user opens the application.
2. The application displays the available parameter-management interface.
3. The user views parameter information and, if supported, enters or edits a record.
4. The application validates submitted input according to configured rules.
5. If persistence is implemented, the application sends the data to the configured data layer.
6. The application communicates the outcome to the user.

This is a logical workflow. Actual screen names, endpoints and sequence must be aligned with the code.

## 3. User roles

The following roles are logical actors, not confirmed configured accounts:

| Actor | Expected interaction |
|---|---|
| Data entry user | Views parameter information and enters or edits data where permitted |
| Reviewer / supervisor | Reviews submitted information if a review workflow exists |
| Administrator | Manages users or configuration only if such functionality exists |

Authentication and authorization requirements are **not assumed to be implemented**.

## 4. Functional requirements

### 4.1 Application access and navigation

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-01 | The application shall load the parameter-management interface when opened through its configured entry point. | Must | Open the application in a supported browser |
| FR-02 | The interface shall provide navigation to the parameter-related views that are included in the build. | Should | Navigate to each available view |
| FR-03 | The interface shall display a clear message when a requested view or operation cannot be completed, where error handling is implemented. | Should | Trigger a controlled error condition |

### 4.2 Parameter information display

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-04 | The application shall display available parameter records in a readable format. | Must | Load a known test dataset and compare displayed values |
| FR-05 | Each displayed record shall show the fields defined in the approved parameter data specification. | Must – validate | Compare the screen with the approved field list |
| FR-06 | If record search or filtering is implemented, the application shall display only records matching the supplied criteria. | Conditional / verify | Search for a known value and verify the result set |
| FR-07 | If no matching record is available, the application shall show an appropriate empty-state message. | Should | Search for a value known not to exist |

### 4.3 Parameter entry and update

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-08 | If record creation is implemented, the application shall provide input controls for the approved parameter fields. | Must – validate | Inspect the form and compare fields with the data specification |
| FR-09 | If record update is implemented, the application shall allow an authorized user to select an existing record and edit permitted fields. | Must – validate | Edit a test record and verify the displayed result |
| FR-10 | The application shall identify missing mandatory fields before accepting a submission, where client- or server-side validation exists. | Must | Submit a form with a required field omitted |
| FR-11 | The application shall validate field formats and permitted values against confirmed business rules. | Must – validate | Test valid, invalid and boundary values |
| FR-12 | The application shall provide feedback after a submission attempt. | Should | Verify success and failure messages |
| FR-13 | If a save operation fails, the application shall not display a false success confirmation. | Must | Simulate or safely test a persistence failure |

### 4.4 Review / approval workflow

The existence of an approval workflow has not been confirmed. Apply the following requirements only if the code contains review states and related actions.

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-14 | The application shall display the current review state of a record if workflow states are implemented. | Conditional | Inspect records in each available state |
| FR-15 | A reviewer shall be able to perform only the review actions permitted by the defined workflow and access rules. | Conditional | Test each permitted and prohibited action |
| FR-16 | The application shall display the result of a review action to the user. | Conditional | Complete a test review action |

Do not invent state names such as Pending, Approved or Rejected unless those exact values exist in the implementation.

### 4.5 Data persistence

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-17 | If database persistence is implemented, a successfully saved record shall be retrievable from the configured data store. | Must – validate | Save a test record, reload and retrieve it |
| FR-18 | The application shall handle a failed data operation without reporting it as successful. | Must | Test a controlled database or service failure |
| FR-19 | The application shall preserve the approved data types and formats when storing and retrieving parameter values. | Must – validate | Compare submitted and retrieved values |

### 4.6 User access and audit information

These requirements are security-sensitive and must be confirmed before they are treated as implemented.

| ID | Requirement | Priority | Verification |
|---|---|---|---|
| FR-20 | If authentication exists, the application shall restrict access to authenticated users. | Conditional | Test signed-in and signed-out access |
| FR-21 | If role-based permissions exist, the application shall restrict actions according to the assigned role. | Conditional | Test each role against the permission matrix |
| FR-22 | If audit logging exists, the application shall record the defined change details for parameter updates. | Conditional | Inspect audit records after a test update |

## 5. Data requirements

The exact schema must be taken from the actual SQL scripts, database configuration or backend models. The following is a **conceptual field checklist**, not a claim about the current schema.

| Conceptual field | Description | Rule to confirm |
|---|---|---|
| Parameter identifier | Unique reference for a parameter record | Format and uniqueness |
| Parameter name | Human-readable parameter name | Required / allowed length |
| Parameter value | Recorded value | Data type, precision and permitted range |
| Unit | Unit associated with the value | Approved unit list |
| Description | Additional explanation, if required | Optional / maximum length |
| Record timestamp | Time the record is created or updated | Source and timezone |
| Record status | State of the record, if workflow exists | Allowed state values |

Do not add, rename or assume database columns based on this conceptual table. Replace it with the real schema after inspecting the repository.

## 6. Input validation and error handling

The implementation should be checked for the following behaviours:

- Required-field validation.
- Numeric and text format validation appropriate to each field.
- Range and precision validation based only on approved parameter rules.
- Duplicate identifier handling, if identifiers must be unique.
- Clear handling of failed saves, unavailable services and invalid requests.
- Preservation of user-entered data after a validation failure where practical.
- Safe handling of unexpected input.

No plant operating limits are specified in this document. Such limits must come from an authorized source and must not be guessed.

## 7. Non-functional considerations

These are quality requirements to consider and validate; they are not claims that the current implementation meets them.

| ID | Quality area | Requirement / consideration |
|---|---|---|
| NFR-01 | Usability | Labels, field instructions and feedback should be understandable to intended users. |
| NFR-02 | Reliability | The application should handle failed operations without silently losing or misreporting data. |
| NFR-03 | Performance | Response-time targets should be agreed and measured using a documented test environment. |
| NFR-04 | Security | Authentication, authorization, secure transport and input protection should be assessed before deployment. |
| NFR-05 | Data integrity | Data types, validation and persistence should prevent unintended corruption. |
| NFR-06 | Compatibility | Supported browsers and screen sizes should be documented and tested. |
| NFR-07 | Maintainability | Code, configuration and database setup should be documented sufficiently for another developer to run the project. |

## 8. External interfaces and dependencies

Confirm from the repository before documenting implementation specifics:

- Browser entry point and supported browsers.
- Frontend-to-backend communication method, if a backend exists.
- Database engine, schema and connection configuration.
- Any external services or integrations.
- Runtime, package and environment requirements.

No live plant-system integration is assumed.

## 9. Core test scenarios

| Test ID | Scenario | Expected result |
|---|---|---|
| TC-01 | Open the application | The configured application interface loads |
| TC-02 | View an existing test parameter | The correct record and values are displayed |
| TC-03 | Submit a valid parameter entry, if supported | The application confirms success only after a successful save |
| TC-04 | Submit a record with a mandatory field missing | The application identifies the missing input |
| TC-05 | Submit a value with an invalid format | The application rejects it with useful feedback |
| TC-06 | Update an existing test record, if supported | The updated value is displayed after saving |
| TC-07 | Retrieve a saved record after reload, if persistence exists | The saved values remain consistent |
| TC-08 | Trigger a controlled save failure | The application reports failure and does not show false success |
| TC-09 | Attempt a restricted action, if access control exists | The action is blocked for an unauthorized user |
| TC-10 | Use a search/filter feature, if present | The result set matches the entered criteria |

Use synthetic test records. Do not test against live plant systems or production operational data without formal authorization.

## 10. Traceability to the BRD

| Business requirement | Related functional requirements |
|---|---|
| BR-01 – Access parameter information | FR-01, FR-02, FR-04 |
| BR-02 – Enter parameter information | FR-08, FR-10, FR-11, FR-12 |
| BR-03 – Update existing information | FR-09, FR-10, FR-11, FR-12 |
| BR-04 – Organized display | FR-04, FR-05, FR-06, FR-07 |
| BR-05 – Validate inputs | FR-10, FR-11 |
| BR-06 – Communicate operation outcome | FR-12, FR-13, FR-18 |
| BR-07 – Show review state | FR-14, FR-15, FR-16 |
| BR-08 – Consistent persistence | FR-17, FR-18, FR-19 |

## 11. Open points for implementation verification

Before marking this FRD as final, inspect the repository and record:

1. Exact screens and navigation labels.
2. Actual form fields and their validation rules.
3. Actual SQL table and column names.
4. Backend language/framework and database engine, if applicable.
5. Whether create, update, delete, search and filtering are implemented.
6. Whether authentication, roles, approval states or audit logs exist.
7. Actual test evidence and known limitations.

## 12. Approval

| Role | Name | Approval / date |
|---|---|---|
| Project owner | To be confirmed | Pending |
| Technical reviewer | To be confirmed | Pending |
| Project representative | To be confirmed | Pending |

## 13. Change history

| Version | Date | Description |
|---|---|---|
| 1.0 | 18 November 2026 | Initial functional requirements draft; implementation details pending verification |
