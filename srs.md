ASMS | Ushongo LGA, Benue State Page 2
Document control
Item Value
Product Agricultural Subsidy Management System (ASMS)
Initial jurisdiction Ushongo LGA, Benue State, Nigeria
Release target MVP / functional prototype
Status Initial requirements baseline
Related document ASMS Product Requirements Document (PRD)
Requirement IDs use stable prefixes (FR, NFR, BR, UC and AC) to support implementation, testing and change
tracking.
1. Introduction
1.1 Purpose
This Software Requirements Specification (SRS) defines the functional and non-functional requirements for the ASMS
MVP. It provides a shared reference for product owners, designers, developers, testers and reviewers.
1.2 Scope
The MVP is a web-first system with a mobile application planned as part of the product delivery. It supports farmer
registration, identity and farm verification records, programme management, applications, two-level review, beneficiary
management, basic distribution records, notifications and auditability for the Ushongo LGA pilot.
1.3 Definitions
Term Meaning
ASMS Agricultural Subsidy Management System
LGA Local Government Area
Farmer ID Unique identifier assigned by ASMS to a farmer
Programme A defined government agricultural subsidy initiative
Beneficiary Farmer approved to receive support under a programme
RBAC Role-based access control
OTP One-time password used for confirmation
MVP Minimum Viable Product
1.4 Assumptions and dependencies
• The initial pilot jurisdiction is Ushongo LGA, Benue State.
• Government roles and approval authority will be formally designated before production use.
• Official NIN verification is not assumed to be available until an authorized service is contracted or approved.
• SMS delivery depends on an external provider and network coverage.
• Payment execution is outside the MVP unless separately authorized and integrated.
• The prototype may use synthetic or consented test data.
ASMS | Ushongo LGA, Benue State Page 6
• FR-NOT-004: Failed notifications shall be visible to authorized support users and shall not reverse the underlying
application decision.
• FR-NOT-005: Email notification support shall be designed for a later phase.
3.11 Dashboards and reports
• FR-REP-001: Farmers shall see their profile completion, verification status, applications and notifications.
• FR-REP-002: Officers shall see assigned verification tasks and application review queues.
• FR-REP-003: LGA Administrators shall see farmer totals, verification summaries, programme applications, approval
totals and basic distribution records for their LGA.
• FR-REP-004: State Administrators shall see authorized aggregate statistics across participating LGAs.
• FR-REP-005: Reports shall be filterable by programme, status and date where applicable.
• FR-REP-006: Exports shall be permission-controlled and shall minimize personal data.
3.12 Audit logging
• FR-AUD-001: The system shall record sensitive actions including account and role changes, verification decisions,
programme publication, application decisions and distribution record changes.
• FR-AUD-002: Each audit entry shall include actor, action, affected record, timestamp and relevant before/after values
where appropriate.
• FR-AUD-003: Ordinary users shall not be able to modify or delete audit entries.
• FR-AUD-004: Access to audit records shall be restricted to authorized roles.
3.13 Future-phase requirements
The following capabilities are recognized but are not acceptance requirements for the first MVP release: detailed budget
authorization and expenditure management; financial payment processing; full physical inventory and distribution centre
management; dual officer/farmer confirmation; offline field capture and synchronization; email notifications; public
transparency portal; anonymous complaints and fraud investigations; advanced analytics; multi-LGA onboarding. These
shall be specified in a later SRS revision before implementation.
4. External Interface Requirements
4.1 User interfaces
• The web interface shall be responsive for desktop, tablet and mobile browser widths.
• The farmer interface shall use clear language, visible status labels and guided forms.
• Administrative screens shall expose only actions permitted to the signed-in role.
• Forms shall show validation errors next to the relevant fields and preserve entered data where safe.
4.2 Software interfaces
• Web and mobile clients shall communicate with the backend through authenticated REST APIs over HTTPS.
• The backend shall use PostgreSQL as the authoritative relational data store.
• File uploads shall use controlled storage with authorization checks.
• SMS integration shall use a provider adapter so the provider can be changed without rewriting business logic.
4.3 Hardware interfaces
No specialized hardware is required for the MVP. Users need an internet-capable phone, tablet or computer. Optional
printers or scanners may be considered later.
ASMS | Ushongo LGA, Benue State Page 7
5. Data Requirements
5.1 Core data entities
Entity Purpose / key relationships
User Login identity, status and assigned role(s).
Role and Permission Defines allowed operations and access scope.
Jurisdiction State and LGA hierarchy; scopes staff and programme access.
Farmer Farmer profile and unique Farmer ID; may link to one user account.
Farm Farm location, size, crops and farming details; belongs to a farmer.
Verification Verification type, result, evidence reference, officer and timestamp.
Programme Subsidy programme, eligibility rules, dates, category and capacity.
Application Farmer's request for a programme; has status and review history.
Review / Decision Officer recommendation and LGA final decision.
Beneficiary Approved entitlement associated with application and programme.
Distribution Record Basic record of support delivered or recorded.
Notification Message event, channel, recipient and delivery status.
Audit Log Append-only record of sensitive actions.
5.2 Data integrity
• Primary keys shall be unique and stable.
• Farmer ID and application reference shall be unique.
• Foreign keys shall preserve relationships between farmers, applications, programmes and decisions.
• Amounts and quantities shall use appropriate decimal or integer representations and explicit units.
• Programme dates shall be validated so closing date is not earlier than opening date.
• Records with historical or financial significance should be archived or status-changed rather than hard-deleted.
5.3 Sensitive data
NIN, contact details, farm coordinates and any financial identifiers must be treated as sensitive. Store only what is
necessary, restrict access, encrypt in transit and at rest where supported, mask values in routine interfaces and define
retention and deletion rules before production use.
6. Non-Functional Requirements
6.1 Security
• NFR-SEC-001: All production traffic shall use HTTPS.
• NFR-SEC-002: Passwords, if used, shall be stored using a modern adaptive password hash; plaintext passwords shall
never be stored.
• NFR-SEC-003: Authorization shall be enforced server-side for every protected operation.
• NFR-SEC-004: Sensitive data shall be encrypted at rest where supported by the hosting environment.
• NFR-SEC-005: The system shall apply rate limits to authentication and OTP-related endpoints.
• NFR-SEC-006: Uploaded files shall be type- and size-validated and access-controlled.
ASMS | Ushongo LGA, Benue State Page 8
• NFR-SEC-007: Administrative and sensitive actions shall be auditable.
6.2 Performance
• NFR-PER-001: Common dashboard and list views should load within 3 seconds under the agreed pilot test load,
excluding slow external services.
• NFR-PER-002: Paginated list endpoints shall avoid returning unbounded datasets.
• NFR-PER-003: Long-running exports and notification jobs should run asynchronously.
6.3 Availability and recovery
• NFR-REL-001: The production service should target 99.5% monthly availability after operational hosting is established.
• NFR-REL-002: Database backups shall be scheduled and restoration tested before pilot launch.
• NFR-REL-003: Failed external notifications shall be retried according to a bounded retry policy.
6.4 Usability and accessibility
• NFR-USE-001: Core farmer workflows shall be usable on common Android phone screen sizes.
• NFR-USE-002: Forms shall provide clear labels, instructions and actionable validation messages.
• NFR-USE-003: Color shall not be the only way to communicate status.
• NFR-USE-004: Interfaces should follow accessible contrast, keyboard and screen-reader practices.
6.5 Scalability and maintainability
• NFR-SCL-001: Data models shall include jurisdiction references to support future LGAs.
• NFR-SCL-002: Business rules shall be implemented in the backend rather than duplicated across clients.
• NFR-MNT-001: The API shall be versioned and documented.
• NFR-MNT-002: Automated tests shall cover authorization, application workflow and key validation rules.
7. Business Rules
• BR-001: A farmer must have a unique Farmer ID within the ASMS platform.
• BR-002: A farmer can only access their own private profile and application records.
• BR-003: An application must relate to an active programme and an eligible farmer.
• BR-004: An Agricultural Officer reviews and recommends; the LGA Administrator makes the final LGA application
decision.
• BR-005: State Administrators authorize budgets and approve LGA allocations; detailed budget workflows are planned
beyond the initial MVP.
• BR-006: Programme-specific eligibility and repeat-benefit rules take precedence over generic defaults.
• BR-007: No user may approve their own request where separation of duties is required.
• BR-008: A record of an administrative decision must include actor, timestamp and reason where applicable.
• BR-009: Public-facing data must be aggregated and must not expose private farmer identifiers.
• BR-010: A manual verification record must not be represented as a successful live NIN verification.
8. Key Use Cases
UC-01: Farmer self-registration
Primary actor: Farmer. Preconditions: Registration is open. Main flow: Farmer opens registration, enters required
information, verifies contact if configured, submits the form, and receives a Farmer ID. Alternative flow: Suspected
duplicate is flagged for staff review. Postcondition: Farmer record exists with an initial verification status.
ASMS | Ushongo LGA, Benue State Page 10
• AC-012: In-app notifications are created for key application status changes; SMS delivery status is recorded when
integration is enabled.
• AC-013: Sensitive administrative actions generate audit entries.
• AC-014: Unauthorized requests are rejected by the backend even if a user attempts to call an API directly.
10. Testing Requirements
• Unit tests: validation, eligibility evaluation, Farmer ID generation and status transitions.
• Integration tests: authentication, database transactions, notification adapter and API permissions.
• Workflow tests: registration through approval and beneficiary creation.
• Security tests: role escalation attempts, cross-LGA access, direct API access and sensitive data exposure.
• Usability tests: farmer registration and application flows on common Android devices.
• Recovery tests: database backup restoration and notification retry behavior.
• User acceptance testing: representatives of farmers, officers and administrators review the pilot workflows using test
data.
11. Deployment and Operational Requirements
• Separate development, test/staging and production environments should be maintained.
• Secrets and API keys must be stored in environment configuration or a managed secrets service, not committed to
source control.
• Production database access must be restricted.
• Monitoring should cover API health, errors, database health and notification failures.
• Backups and restoration procedures must be documented.
• Before a real pilot, the project must obtain an identified operational owner, approved data collection purpose, user
notices, support process and required government authorizations.
12. Out of Scope for Initial MVP
• Live NIN database verification without an authorized provider agreement.
• Actual government fund transfer or payment execution.
• Full inventory management for warehouses and distribution centres.
• OTP-based farmer confirmation of physical delivery.
• Offline data capture and synchronization.
• Public transparency portal and downloadable public reports.
• Anonymous fraud reporting and full investigation case management.
• Multi-LGA production onboarding.
• Automated government eligibility decisions without human review.
13. Open Decisions to Resolve Before Production
• Who is the formally designated product owner and operational authority?
• What exact farmer data is necessary, and what is the lawful basis and retention period?
• Which identity verification provider, if any, is authorized?
• Which SMS provider and sender identity will be used?
• What are the final programme-specific eligibility rules and appeals process?
ASMS | Ushongo LGA, Benue State Page 11
• Who is authorized to record distribution and who reconciles financial transactions?
• What hosting region, backup retention and incident response arrangements are required?
• What local languages and accessibility support are needed?
• What formal approvals are required from the relevant government departments?
14. Traceability to PRD
This SRS translates the PRD's MVP scope into testable requirements. Features identified in the PRD as later-phase
capabilities are explicitly kept out of MVP acceptance criteria unless separately approved through change control. Any
change to scope, roles, eligibility rules, data collection or integrations should be documented, reviewed and versioned.
⋮⋮
⋮⋮
