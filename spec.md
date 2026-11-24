# ASMS — Agricultural Subsidy Management System
## Software Development Specification (`spec.md`)

**Project:** Agricultural Subsidy Management System (ASMS)  
**Initial Deployment:** Ushongo Local Government Area, Benue State, Nigeria  
**Project Type:** Government Agricultural Subsidy Management Platform  
**Architecture:** Full-stack application with hybrid blockchain integration  
**Document Version:** 1.0  
**Status:** Development Specification

---

# 1. Project Overview

## 1.1 Introduction

The Agricultural Subsidy Management System (ASMS) is a digital platform designed to improve the management, monitoring, distribution and accountability of government agricultural subsidies.

The system will enable government agricultural departments to register farmers, manage agricultural programmes, receive subsidy applications, verify eligibility, approve beneficiaries, manage subsidy allocations, record distributions and monitor programme performance.

The platform will initially serve Ushongo Local Government Area in Benue State, Nigeria, with an architecture that supports future expansion to other LGAs and state-level administration.

ASMS will incorporate blockchain technology through Polygon and Solidity smart contracts to provide an additional layer of transparency, accountability and verification.

## 1.2 Problem Statement

Traditional agricultural subsidy management can experience challenges including:

- Inaccurate or duplicated farmer registration.
- Lack of reliable farmer records.
- Unclear beneficiary selection processes.
- Poor monitoring of subsidy distribution.
- Inadequate accountability for government allocations.
- Difficulty identifying fraudulent applications.
- Limited access to reliable programme information.
- Difficulty auditing historical programme activities.

ASMS addresses these challenges through a centralized digital management platform supported by blockchain-based verification of selected critical records.

## 1.3 Project Objectives

The system aims to:

1. Create a centralized database of registered farmers.
2. Digitize agricultural subsidy programmes.
3. Provide transparent application and approval workflows.
4. Improve beneficiary identification and verification.
5. Manage agricultural subsidy allocations.
6. Record and monitor subsidy distributions.
7. Improve government accountability.
8. Provide reliable reports and analytics.
9. Support complaints and fraud investigations.
10. Use blockchain technology to make selected records independently verifiable.
11. Support future expansion across multiple LGAs.

---

# 2. Project Scope

## 2.1 Included Features

The system will include:

- Farmer registration and management.
- Farm registration and management.
- Farmer verification.
- Government user and role management.
- Agricultural programme management.
- Subsidy category and item management.
- Farmer subsidy applications.
- Eligibility assessment.
- Application review and approval.
- Beneficiary management.
- Budget and allocation management.
- Distribution batch management.
- Distribution confirmation.
- Notifications.
- Complaints and investigation management.
- Reports and analytics.
- Audit logging.
- Blockchain integration.
- Smart contract verification.
- Blockchain transaction monitoring.

## 2.2 Initial Deployment Scope

The initial implementation will support:

- One state-level administrative authority.
- Multiple Local Government Areas.
- Ushongo LGA as the initial pilot.
- Farmers within registered communities.
- Authorized agricultural officers.
- LGA administrators.
- State administrators.
- Auditors and investigators.

## 2.3 Excluded from the Initial MVP

The following are not required for the first release:

- Direct bank payment processing.
- Cryptocurrency payments to farmers.
- Fully automated identity verification without an authorized provider.
- Advanced offline synchronization.
- Complete mobile application deployment.
- Automated agricultural insurance.
- Automated agricultural market pricing.
- Advanced AI-based fraud detection.
- Public disclosure of individual farmer records.

These can be introduced in later development phases.

---

# 3. Technology Stack

## 3.1 Frontend

| Technology | Purpose |
|---|---|
| React | User interface |
| Vite | Frontend development and build |
| TypeScript | Type safety |
| Tailwind CSS | Styling |
| shadcn/ui | Reusable interface components |
| React Router | Application navigation |
| TanStack Query | Server-state management |
| React Hook Form | Form management |
| Zod | Form validation |
| Recharts | Dashboard analytics |
| Lucide React | Icons |

## 3.2 Backend

| Technology | Purpose |
|---|---|
| Node.js | Runtime |
| NestJS | Backend framework |
| TypeScript | Programming language |
| PostgreSQL | Main relational database |
| Prisma ORM | Database access |
| JWT | Authentication |
| Argon2id | Password hashing |
| Class Validator | Request validation |
| Swagger | API documentation |

## 3.3 Blockchain

| Technology | Purpose |
|---|---|
| Polygon | Blockchain network |
| Polygon Amoy | Development and testing network |
| Polygon PoS | Proposed production network |
| Solidity | Smart contract development |
| Hardhat | Smart contract development and testing |
| OpenZeppelin | Smart contract security libraries |
| Ethers.js | Backend blockchain interaction |
| Polygon RPC | Blockchain connectivity |

## 3.4 Additional Services

- OpenStreetMap for geographical mapping.
- SMS provider for farmer and staff notifications.
- Private object storage for documents and evidence.
- GitHub for source-code management.
- Vercel or equivalent for frontend hosting.
- Managed cloud hosting for the backend.
- Supabase PostgreSQL or another managed PostgreSQL provider.

**Architecture decision:** PostgreSQL remains the primary operational database. Polygon is an additional verification and smart-contract execution layer.

---

# 4. System Architecture

## 4.1 Architecture Overview

The system will follow a modular monolithic architecture initially.

Main architecture:

```text
ASMS SYSTEM
│
├── FRONTEND
│   ├── React Web Application
│   ├── Farmer Portal
│   ├── Officer Dashboard
│   ├── LGA Administration
│   └── State Administration
│
├── BACKEND
│   ├── NestJS API
│   ├── Authentication
│   ├── Farmer Management
│   ├── Programme Management
│   ├── Application Management
│   ├── Approval Management
│   ├── Distribution Management
│   ├── Budget Management
│   ├── Complaint Management
│   ├── Reporting
│   └── Blockchain Integration
│
├── DATABASE
│   └── PostgreSQL
│
├── FILE STORAGE
│   └── Private Object Storage
│
└── BLOCKCHAIN
    ├── Polygon Network
    ├── Solidity Smart Contracts
    ├── Ethers.js
    └── Blockchain Event Indexer
```

## 4.2 Main Architecture Responsibilities

### Frontend

The frontend will provide interfaces for farmers, agricultural officers, administrators, auditors and investigators.

### Backend

The backend will handle business logic, authentication, authorization, database operations, application workflows and blockchain integration.

### PostgreSQL

PostgreSQL will store all operational application information.

### Polygon

Polygon will store selected cryptographic record fingerprints and blockchain events.

### Smart Contracts

Smart contracts will enforce authorized blockchain operations and maintain verifiable records of selected programme activities.

---

# 5. User Roles and Permissions

The system must implement role-based access control (RBAC).

## 5.1 Farmer

Permissions:

- Register an account.
- Create and update an allowed farmer profile.
- Register farm information.
- Submit subsidy applications.
- Upload required documents.
- View application status.
- View approved subsidy information.
- View personal distribution history.
- Submit complaints.
- Receive notifications.

Farmers must only access their own personal records.

## 5.2 Agricultural Officer

Permissions:

- Register farmers on their behalf.
- Review farmer information.
- Conduct farm verification.
- Review subsidy applications.
- Recommend approval or rejection.
- Record distribution activities.
- Submit reports.
- View records within their assigned jurisdiction.

Agricultural officers must not make final decisions reserved for LGA administrators.

## 5.3 LGA Administrator

Permissions:

- Manage LGA officers.
- Manage communities within the LGA.
- Review officer recommendations.
- Make final LGA-level application decisions.
- Manage LGA programme activities.
- Monitor subsidy distribution.
- View LGA reports.
- Assign routine complaints.
- Escalate serious complaints.
- Authorize permitted LGA blockchain operations.

## 5.4 State Administrator

Permissions:

- Manage state-level administrators.
- Manage LGAs.
- Create or authorize state programmes.
- Approve programme budgets.
- Allocate funds to LGAs.
- Monitor LGA activities.
- View state-wide reports.
- Investigate escalated complaints.
- Manage approved blockchain governance responsibilities.

## 5.5 Auditor

Permissions:

- View authorized programme records.
- Review allocation records.
- Review beneficiary decisions.
- Review distribution records.
- Inspect audit logs.
- Verify blockchain anchors.
- Generate audit reports.

Auditors must not modify the records they are auditing.

## 5.6 Investigator

Permissions:

- Receive assigned complaints.
- Review supporting evidence.
- Record investigation actions.
- Request additional information.
- Submit investigation findings.
- Recommend corrective actions.
- Escalate investigations when necessary.

Investigators must not investigate matters where they have a conflict of interest.

## 5.7 Super Administrator

The Super Administrator manages technical platform configuration.

Permissions:

- Manage system configuration.
- Manage technical user access.
- Monitor system health.
- Manage integrations.
- Monitor blockchain transactions.
- Manage technical permissions.

Technical administration must not automatically grant authority to approve agricultural subsidy applications or government budget allocations.

---

# 6. Functional Requirements

## 6.1 Authentication and Authorization

The system must support:

- User registration.
- User login.
- Secure logout.
- Password reset.
- Password hashing.
- Access and refresh token handling.
- Role-based access control.
- Jurisdiction-based access control.
- Account activation and suspension.
- Session management.

Authentication and authorization must be enforced by the backend.

Hiding a frontend button is not sufficient security.

## 6.2 Farmer Management

The system must allow farmers to register through:

1. Self-registration.
2. Officer-assisted registration.

Each farmer must receive a unique identification number.

Example:

```text
ASMS-USH-000001
ASMS-USH-000002
ASMS-USH-000003
```

Farmer records should contain:

- Farmer ID.
- Full name.
- Contact information.
- Community.
- LGA.
- State.
- Gender where legitimately required.
- Date of birth where legitimately required.
- Farming experience.
- Agricultural interests.
- Verification status.
- Registration date.

Sensitive information must be collected only when necessary and protected appropriately.

## 6.3 Farm Management

The system must support multiple farms belonging to one farmer.

Farm information should include:

- Farm ID.
- Farmer ID.
- Farm name or description.
- Community.
- Location.
- Farm size.
- Land ownership or usage information.
- Main crops.
- Farm verification status.
- Registration date.

OpenStreetMap will support farm location display.

## 6.4 Farmer Verification

The system must support:

- Officer-based verification.
- Document verification.
- Farm verification.
- Community verification where approved.
- Verification rejection.
- Verification history.

Verification records must include:

- Farmer ID.
- Verifying officer.
- Verification type.
- Verification status.
- Verification date.
- Supporting evidence references.
- Rejection reason where applicable.

External identity verification must only be enabled through an authorized provider.

## 6.5 Agricultural Programme Management

Authorized administrators must be able to create and manage agricultural subsidy programmes.

Programme information:

- Programme ID.
- Programme name.
- Description.
- Programme category.
- Responsible authority.
- Target LGA or LGAs.
- Start date.
- Closing date.
- Eligibility conditions.
- Subsidy items.
- Programme budget.
- Programme status.

Programme statuses:

- Draft.
- Pending Approval.
- Approved.
- Published.
- Active.
- Suspended.
- Completed.
- Cancelled.

## 6.6 Subsidy Categories

The system must support:

- Fertilizer.
- Improved seeds.
- Agricultural equipment.
- Financial support.
- Other approved agricultural assistance.

Administrators should be able to create additional categories.

## 6.7 Application Management

Farmers must be able to apply for available programmes.

Application information:

- Application ID.
- Farmer ID.
- Programme ID.
- Requested subsidy item.
- Requested quantity.
- Application date.
- Supporting documents.
- Application status.

Application statuses:

- Draft.
- Submitted.
- Under Review.
- Verification Required.
- Recommended.
- Approved.
- Rejected.
- Withdrawn.

The system must prevent duplicate applications where programme rules prohibit them.

## 6.8 Application Review and Approval

Approval workflow:

```text
Farmer submits application
          |
          v
Application received
          |
          v
Agricultural Officer reviews
          |
          v
Eligibility and verification checks
          |
          v
Officer recommendation
          |
          v
LGA Administrator reviews
          |
          v
Final decision
      /       \
     /         \
 Approved     Rejected
    |
    v
Beneficiary record created
    |
    v
Distribution eligibility
```

The system must:

- Record each review.
- Record reviewer identity.
- Record timestamps.
- Require a decision reason where applicable.
- Maintain application status history.
- Prevent unauthorized approval.
- Create a beneficiary record after final approval.

## 6.9 Beneficiary Management

The system must automatically create a beneficiary record after successful final approval.

Beneficiary information:

- Beneficiary ID.
- Farmer ID.
- Programme ID.
- Application ID.
- Approval reference.
- Approval date.
- Beneficiary status.

The system must prevent duplicate beneficiary creation for the same approved application.

## 6.10 Budget and Allocation Management

The system must support:

- Programme budget creation.
- State-level budget approval.
- LGA allocation.
- Allocation tracking.
- Allocation history.
- Budget reports.
- Allocation status monitoring.

Budget information:

- Budget ID.
- Programme ID.
- Total approved budget.
- Currency.
- Financial year.
- Approving authority.
- Approval date.
- Status.

LGA allocation information:

- Allocation ID.
- Programme ID.
- LGA ID.
- Allocated amount.
- Allocation date.
- Approval reference.
- Status.

Actual bank transfers and direct payments are outside the initial MVP.

## 6.11 Distribution Management

The system must support recording physical subsidy distributions.

Distribution information:

- Distribution ID.
- Distribution batch.
- Programme.
- Beneficiary.
- Subsidy item.
- Quantity.
- Distribution location.
- Distribution officer.
- Distribution date.
- Confirmation status.
- Supporting evidence.

Distribution statuses:

- Planned.
- In Progress.
- Completed.
- Partially Completed.
- Cancelled.
- Under Investigation.

The system must support distribution verification and corrections.

Blockchain confirmation must not be treated as proof that physical goods were delivered.

## 6.12 Notifications

The system should support:

- In-app notifications.
- SMS notifications.
- Application status updates.
- Approval notifications.
- Rejection notifications.
- Programme announcements.
- Distribution announcements.
- Complaint updates.

## 6.13 Complaint Management

Farmers and authorized users must be able to submit complaints.

Complaint categories may include:

- Missing subsidy.
- Unfair selection.
- Officer misconduct.
- Fraud allegations.
- Incorrect farmer records.
- Distribution problems.
- Other programme-related complaints.

Investigation workflow:

```text
Complaint Submitted
        |
        v
Complaint Reviewed
        |
        v
Conflict-of-interest check
        |
        v
Assigned Investigator
        |
        v
Investigation
        |
        v
Investigation Findings
        |
        v
Resolution or Escalation
```

Routine complaints should be investigated at LGA level.

Complaints involving LGA administrators or serious misconduct must be escalated to state-level investigators.

## 6.14 Reports and Analytics

The system should provide:

- Total registered farmers.
- Verified farmers.
- Total agricultural programmes.
- Total applications.
- Approved applications.
- Rejected applications.
- Total beneficiaries.
- Budget allocations.
- Distribution records.
- Programme completion statistics.
- LGA comparisons.
- Complaint statistics.
- Blockchain verification statistics.

Reports must respect the user's jurisdiction and permissions.

---

# 7. Blockchain and Smart Contract Requirements

## 7.1 Blockchain Integration Model

ASMS will use a hybrid blockchain architecture.

PostgreSQL stores operational information.

Polygon stores selected cryptographic fingerprints and blockchain transaction evidence.

Solidity smart contracts enforce permitted blockchain operations.

## 7.2 Network

Development network:

```text
Polygon Amoy Testnet
```

Proposed production network:

```text
Polygon PoS Mainnet
```

Production deployment must follow a security, cost and governance review.

## 7.3 Main Blockchain Objectives

Blockchain integration must support:

1. Programme transparency.
2. Budget allocation accountability.
3. Beneficiary approval verification.
4. Subsidy distribution verification.
5. Tamper-evident audit evidence.
6. Smart contract authorization.
7. Independent record verification.

## 7.4 Smart Contract Components

The initial smart contract architecture should support the following responsibilities.

### ASMS Registry

Manages system-level contract configuration and approved contract references where needed.

### Programme Registry

Records:

- Programme references.
- Programme versions.
- Approval evidence hashes.
- Timestamps.
- Authorized recording roles.

### Allocation Registry

Records:

- Allocation references.
- Programme references.
- Approved allocation evidence.
- Amount and currency representation where approved for disclosure.
- Transaction references.

### Beneficiary Approval Registry

Records:

- Pseudonymous application references.
- Programme references.
- Approval evidence hashes.
- Approval timestamps.

It must not store farmer personal information.

### Distribution Registry

Records:

- Distribution batch references.
- Programme references.
- Distribution evidence hashes.
- Completion declarations.
- Correction references.

## 7.5 Smart Contract Security

Contracts must:

- Use established access-control patterns.
- Restrict privileged functions.
- Prevent unauthorized updates.
- Prevent accidental duplicate operations.
- Emit events for important operations.
- Support append-only correction records.
- Include emergency pause functionality where justified.
- Be tested before deployment.

OpenZeppelin libraries should be preferred over implementing common security mechanisms from scratch.

## 7.6 Blockchain Data Privacy

The following information must never be stored directly on the public blockchain:

- Farmer names.
- Phone numbers.
- NIN.
- Residential addresses.
- Identity documents.
- Precise farm coordinates.
- Private investigation records.
- Personal photographs.

Only approved, minimal, non-sensitive references and cryptographic evidence hashes should be recorded.

## 7.7 Blockchain Transaction Lifecycle

Every blockchain operation must have a tracked status.

```text
PENDING
   |
   v
SUBMITTED
   |
   v
CONFIRMING
   |
   v
CONFIRMED
```

Failure path:

```text
PENDING / SUBMITTED
         |
         v
       FAILED
         |
         v
   RETRY REQUIRED
```

The system must store:

- Transaction hash.
- Network.
- Contract address.
- Operation type.
- Referenced ASMS record.
- Payload hash.
- Submission date.
- Block number.
- Gas used.
- Confirmation status.
- Failure information.

A failed blockchain transaction must not be silently treated as successful.

## 7.8 Blockchain Verification

The system must provide an API that allows authorized users to verify whether a stored ASMS record matches its blockchain anchor.

Verification process:

1. Retrieve the relevant record.
2. Recreate its canonical evidence representation.
3. Calculate its cryptographic hash.
4. Retrieve the corresponding on-chain anchor.
5. Compare the hashes.
6. Return the verification result.

Possible results:

- Verified.
- Mismatch.
- Anchor Not Found.
- Transaction Pending.
- Transaction Failed.
- Verification Unavailable.

A hash mismatch should trigger an audit review rather than automatically changing or deleting the record.

## 7.9 Blockchain Reliability

The backend must implement:

- Asynchronous transaction processing.
- Transaction retry management.
- Idempotency protection.
- Event indexing.
- Transaction reconciliation.
- RPC availability monitoring.
- Transaction failure logging.

The application must remain usable when the blockchain provider is temporarily unavailable. Blockchain jobs should be queued and processed when connectivity returns.

---

# 8. Database Requirements

## 8.1 Database

PostgreSQL will serve as the main database.

Prisma ORM will manage schema definitions, migrations and database access.

## 8.2 Core Database Tables

### Authentication and Administration

- users
- roles
- user_roles
- staff_assignments
- refresh_tokens

### Geography

- states
- lgas
- communities

### Farmer Management

- farmers
- farms
- farmer_documents
- farmer_verifications

### Programme Management

- programmes
- subsidy_items
- programme_eligibility

### Applications and Approvals

- applications
- application_reviews
- application_decisions
- application_status_history
- beneficiaries

### Budget Management

- budgets
- lga_allocations
- budget_transactions

### Distribution

- distribution_batches
- distributions

### Complaints

- complaints
- complaint_assignments
- complaint_actions

### Notifications and Audit

- notifications
- audit_logs

### Blockchain

- blockchain_networks
- smart_contracts
- blockchain_transactions
- blockchain_anchors
- blockchain_events
- blockchain_outbox
- blockchain_verification_checks

## 8.3 Database Relationship Requirements

- One state can contain multiple LGAs.
- One LGA can contain multiple communities.
- One community can contain multiple farmers.
- One farmer can have multiple farms.
- One farmer can submit multiple applications.
- One programme can receive multiple applications.
- One application can have multiple reviews.
- One application has a final decision according to the approval workflow.
- One approved application can create one beneficiary record.
- One programme can have multiple subsidy items.
- One programme can have multiple LGA allocations.
- One distribution batch can contain multiple distribution records.
- One complaint can have multiple investigation actions.
- One ASMS record can have multiple blockchain anchors across different versions or events.
- One blockchain transaction can produce multiple indexed events.

## 8.4 Database Integrity

The system must implement:

- Primary keys.
- Foreign keys.
- Unique constraints.
- Required field validation.
- Appropriate indexes.
- Transaction management.
- Database migrations.
- Backup and recovery procedures.

Financial values must not use floating-point storage or calculations.

---

# 9. API Specification

The backend will expose a versioned REST API.

Base URL:

```text
/api/v1
```

## 9.1 Authentication

```http
POST /auth/register
POST /auth/login
POST /auth/logout
POST /auth/refresh
POST /auth/forgot-password
POST /auth/reset-password
GET  /auth/me
```

## 9.2 Farmers

```http
POST   /farmers
GET    /farmers
GET    /farmers/:id
PATCH  /farmers/:id
GET    /farmers/me
```

## 9.3 Farms

```http
POST   /farms
GET    /farms
GET    /farms/:id
PATCH  /farms/:id
```

## 9.4 Verification

```http
POST /verifications
GET  /verifications
GET  /verifications/:id
PATCH /verifications/:id
```

## 9.5 Programmes

```http
POST  /programmes
GET   /programmes
GET   /programmes/:id
PATCH /programmes/:id
POST  /programmes/:id/approve
POST  /programmes/:id/publish
```

## 9.6 Applications

```http
POST /applications
GET  /applications
GET  /applications/:id
POST /applications/:id/reviews
POST /applications/:id/decisions
```

## 9.7 Beneficiaries

```http
GET /beneficiaries
GET /beneficiaries/:id
```

## 9.8 Budget and Allocations

```http
POST /budgets
GET  /budgets
POST /allocations
GET  /allocations
GET  /allocations/:id
```

## 9.9 Distribution

```http
POST /distribution-batches
GET  /distribution-batches
GET  /distribution-batches/:id
POST /distributions
GET  /distributions
POST /distribution-batches/:id/complete
```

## 9.10 Complaints

```http
POST  /complaints
GET   /complaints
GET   /complaints/:id
POST  /complaints/:id/assign
POST  /complaints/:id/actions
POST  /complaints/:id/escalate
```

## 9.11 Blockchain

```http
GET  /blockchain/networks
GET  /blockchain/contracts
GET  /blockchain/transactions/:id
GET  /blockchain/verify/:referenceType/:referenceId
POST /blockchain/anchors/:id/verify
GET  /blockchain/health
```

All endpoints must implement authentication, request validation and appropriate authorization.

---

# 10. Frontend Requirements

## 10.1 General Interface

The platform must have a professional government-management interface.

Design requirements:

- Responsive layout.
- Sidebar navigation.
- Top navigation bar.
- Dashboard cards.
- Data tables.
- Search and filtering.
- Pagination.
- Forms with validation.
- Loading states.
- Error states.
- Empty states.
- Confirmation dialogs.
- Notifications.
- Accessible controls.

The interface must work on desktop, tablet and mobile browsers.

## 10.2 Farmer Portal

Pages:

- Farmer Dashboard.
- Registration.
- Farmer Profile.
- Farm Management.
- Available Programmes.
- Application Form.
- My Applications.
- Beneficiary Status.
- Distribution History.
- Complaints.
- Notifications.

## 10.3 Officer Dashboard

Pages:

- Overview.
- Farmer Management.
- Farmer Verification.
- Farm Verification.
- Application Review.
- Recommended Applications.
- Distribution Management.
- Reports.
- Notifications.

## 10.4 LGA Administrator Dashboard

Pages:

- Overview.
- Officer Management.
- Community Management.
- Farmer Records.
- Programme Management.
- Application Decisions.
- Beneficiaries.
- Distribution Monitoring.
- LGA Allocations.
- Complaint Management.
- Reports.
- Blockchain Verification.

## 10.5 State Administrator Dashboard

Pages:

- State Overview.
- LGA Management.
- Programme Management.
- Budget Management.
- LGA Allocations.
- Beneficiary Statistics.
- Distribution Monitoring.
- Complaint Escalations.
- State Reports.
- Blockchain Monitoring.

## 10.6 Auditor Dashboard

Pages:

- Programme Audit.
- Budget Audit.
- Beneficiary Audit.
- Distribution Audit.
- Audit Logs.
- Blockchain Verification.
- Exportable Reports.

---

# 11. Security Requirements

The system must implement:

1. Argon2id password hashing.
2. Secure access and refresh token handling.
3. HTTPS for production communication.
4. Role-based authorization.
5. Jurisdiction-based authorization.
6. Input validation.
7. Rate limiting.
8. Secure document access.
9. Audit logging.
10. Database backups.
11. Error handling without leaking sensitive information.
12. Secure secret management.
13. Blockchain key protection.
14. Smart contract access control.
15. Security testing before production.

Private blockchain signing keys must never be embedded in frontend code or committed to GitHub.

---

# 12. Non-Functional Requirements

## 12.1 Performance

- Common dashboard pages should load efficiently.
- Database queries must be indexed appropriately.
- Large tables must support pagination.
- Blockchain requests must be asynchronous.
- Long-running tasks must not block ordinary user requests.

## 12.2 Scalability

The system must support future expansion to:

- Multiple LGAs.
- Multiple agricultural programmes.
- Increasing farmer registrations.
- Larger distribution records.
- State-wide administration.
- Additional subsidy categories.

## 12.3 Availability

The application should provide reliable access and graceful error handling.

Temporary failures of SMS, storage or blockchain providers must not corrupt core application records.

## 12.4 Maintainability

The project must use:

- Modular backend architecture.
- Reusable frontend components.
- TypeScript.
- Documented APIs.
- Database migrations.
- Automated tests.
- Consistent naming conventions.

---

# 13. Project Folder Structure

Recommended monorepo structure:

```text
asms/
│
├── apps/
│   ├── web/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   ├── layouts/
│   │   │   ├── pages/
│   │   │   ├── features/
│   │   │   ├── hooks/
│   │   │   ├── services/
│   │   │   ├── routes/
│   │   │   ├── types/
│   │   │   └── lib/
│   │   └── package.json
│   │
│   └── api/
│       ├── src/
│       │   ├── auth/
│       │   ├── users/
│       │   ├── farmers/
│       │   ├── farms/
│       │   ├── locations/
│       │   ├── verifications/
│       │   ├── programmes/
│       │   ├── applications/
│       │   ├── beneficiaries/
│       │   ├── budgets/
│       │   ├── distributions/
│       │   ├── complaints/
│       │   ├── notifications/
│       │   ├── reports/
│       │   ├── audit/
│       │   ├── blockchain/
│       │   └── prisma/
│       └── package.json
│
├── packages/
│   └── shared/
│
├── blockchain/
│   ├── contracts/
│   ├── scripts/
│   ├── test/
│   ├── ignition/
│   ├── hardhat.config.ts
│   └── package.json
│
├── docs/
│   ├── PRD.md
│   ├── SRS.md
│   ├── ARCHITECTURE.md
│   └── DATABASE.md
│
├── .gitignore
├── README.md
└── spec.md
```

The mobile application can be added under `apps/mobile` in a later phase.

---

# 14. Development Phases

## Phase 1: Project Foundation

- Initialize the project repository.
- Configure React and Vite.
- Configure NestJS.
- Connect PostgreSQL.
- Configure Prisma.
- Establish development environment variables.
- Create initial database migrations.

## Phase 2: Authentication and Administration

- Build registration and login.
- Implement roles and permissions.
- Implement jurisdiction restrictions.
- Build administrator dashboards.
- Implement audit logging.

## Phase 3: Farmer and Farm Management

- Farmer registration.
- Officer-assisted registration.
- Farmer profiles.
- Farm records.
- Farmer verification.
- Farm verification.

## Phase 4: Programme Management

- Programme creation.
- Subsidy categories.
- Eligibility rules.
- Programme publication.
- Programme administration.

## Phase 5: Applications and Approvals

- Application submission.
- Application review.
- Eligibility assessment.
- Officer recommendation.
- LGA final decisions.
- Beneficiary creation.

## Phase 6: Budget and Distribution

- Budget creation.
- State budget approval.
- LGA allocations.
- Distribution batches.
- Distribution recording.
- Distribution reporting.

## Phase 7: Blockchain Development

- Initialize Hardhat.
- Configure Solidity.
- Install OpenZeppelin.
- Build smart contracts.
- Write contract tests.
- Deploy to Polygon Amoy.
- Connect NestJS using Ethers.js.
- Implement blockchain transaction tracking.
- Implement blockchain event indexing.
- Implement verification APIs.

## Phase 8: Blockchain Workflow Integration

Connect smart contracts to:

- Programme approvals.
- Budget allocation approvals.
- Beneficiary approvals.
- Distribution confirmations.

Implement transaction retries, event reconciliation and verification status displays.

## Phase 9: Complaints and Reporting

- Complaint submission.
- Investigation assignment.
- Escalation.
- Investigation records.
- Dashboard analytics.
- Exportable reports.

## Phase 10: Testing and Deployment

- Frontend testing.
- Backend testing.
- Database testing.
- Smart contract testing.
- Security testing.
- Integration testing.
- User acceptance testing.
- Pilot deployment.
- Production readiness review.

---

# 15. Testing Requirements

## 15.1 Frontend Tests

Test:

- Authentication screens.
- Form validation.
- Navigation.
- Role-specific page access.
- Dashboard data.
- Error handling.
- Responsive layouts.

## 15.2 Backend Tests

Test:

- Authentication.
- Authorization.
- Farmer registration.
- Application submission.
- Approval workflows.
- Budget calculations.
- Distribution records.
- Complaint escalation.
- API validation.

## 15.3 Database Tests

Test:

- Foreign key constraints.
- Unique farmer IDs.
- Duplicate application prevention.
- Transaction integrity.
- Data consistency.
- Migration reliability.

## 15.4 Smart Contract Tests

Test:

- Contract deployment.
- Role authorization.
- Programme registration.
- Allocation registration.
- Beneficiary approval anchors.
- Distribution anchors.
- Duplicate reference protection.
- Correction events.
- Unauthorized transaction rejection.
- Pause and recovery behavior.

## 15.5 Blockchain Integration Tests

Test:

- Successful transaction submission.
- Transaction confirmation.
- Transaction failure.
- Retry handling.
- Duplicate prevention.
- Event processing.
- Hash verification.
- RPC interruption.
- Database-to-blockchain reconciliation.

---

# 16. MVP Acceptance Criteria

The initial ASMS MVP will be considered functionally complete when:

1. Farmers can register.
2. Authorized officers can register farmers.
3. Farmers can register farm information.
4. Officers can verify farmers and farms.
5. Administrators can create subsidy programmes.
6. Farmers can submit applications.
7. Officers can review applications.
8. LGA administrators can make final decisions.
9. Approved applications create beneficiary records.
10. Administrators can manage programme budgets and LGA allocations.
11. Officers can record distribution activities.
12. Authorized users can view relevant reports.
13. Farmers can receive notifications.
14. Users can submit complaints.
15. Complaints can be assigned and escalated according to authority.
16. Important activities are captured in audit logs.
17. Selected programme and approval records can be anchored on Polygon Amoy.
18. Distribution evidence can be anchored and independently verified.
19. Authorized users can inspect blockchain transaction statuses.
20. Personal farmer information is not exposed on the public blockchain.
21. The system enforces role and jurisdiction restrictions.
22. The application remains usable when blockchain services are temporarily unavailable.

---

# 17. Important Implementation Rules

Developers and AI coding assistants working on this project must follow these rules:

1. Do not rebuild an existing working module unnecessarily.
2. Follow the existing project structure where one already exists.
3. Do not create duplicate database tables or API endpoints.
4. Do not use mock data as a replacement for real backend integration in completed modules.
5. Use reusable frontend components.
6. Use TypeScript consistently.
7. Validate all incoming backend requests.
8. Enforce permissions on the backend.
9. Keep database credentials and blockchain keys out of source code.
10. Never store personal farmer information on Polygon.
11. Do not assume a blockchain transaction proves a physical distribution occurred.
12. Use database transactions for critical business workflows.
13. Use an outbox pattern for reliable blockchain submissions.
14. Do not mark a blockchain anchor as confirmed before the required transaction and event checks succeed.
15. Write tests for business logic and smart contracts.
16. Document major implementation decisions.
17. Preserve historical records and append corrections instead of silently overwriting important audit evidence.
18. Do not deploy production smart contracts without a security review.
19. Do not introduce real financial transfers or cryptocurrency payments unless explicitly added to the approved scope.
20. Keep the implementation aligned with this specification and record approved changes.

---

# 18. Final Technical Direction

ASMS will be developed as a full-stack agricultural subsidy management platform with a hybrid blockchain architecture.

The main operational system will use:

- React.
- TypeScript.
- NestJS.
- PostgreSQL.
- Prisma.

The blockchain layer will use:

- Polygon.
- Solidity.
- Hardhat.
- OpenZeppelin.
- Ethers.js.

The initial blockchain environment will be Polygon Amoy, followed by a controlled production deployment review for Polygon PoS.

The system will prioritize reliable farmer management, transparent programme administration, accountable subsidy distribution, secure government workflows and independently verifiable records.

**Final architectural principle:**

PostgreSQL manages the agricultural subsidy system. Polygon provides independent verification. Solidity enforces selected blockchain rules. ASMS connects all three into one coordinated platform.
