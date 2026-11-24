ASMS | Ushongo LGA, Benue State Page 1
ASMS
PRODUCT REQUIREMENTS
DOCUMENT
Agricultural Subsidy Management System
Project location: Ushongo Local Government Area, Benue State, Nigeria
Project type: Government-oriented agricultural technology platform
Document: Product Requirements Document (PRD)
Delivery approach: Functional MVP, designed for future expansion
Prepared as a project planning document. Government adoption, official identity verification, payment services and production
deployment require the relevant authorizations and agreements.
ASMS | Ushongo LGA, Benue State Page 3
• Review applications and recommend decisions.
• Record field activities and, in later phases, distribution events.
Local Government Administrators
• Manage officers and farmer records within their jurisdiction.
• Review and approve applications.
• Propose subsidy allocations and manage approved allocations.
• Monitor beneficiaries and distribution.
• Handle routine complaints and produce reports.
State Administrators
• Manage participating LGAs and state programmes.
• Authorize budgets and approve LGA allocations.
• Monitor programme and LGA performance.
• Manage state-level permissions and escalated complaints.
Public Users
• View published programmes and aggregated public statistics.
• Access approved reports without seeing private farmer or government records.
5. Subsidy Categories
• Fertilizer subsidy.
• Improved seeds subsidy.
• Farming equipment support.
• Financial support.
Administrators should be able to configure individual programmes for one or more permitted subsidy categories.
6. Farmer Registration and Identification
The platform will support self-registration and assisted registration by authorized officers. Each farmer will receive a
unique system-generated Farmer ID, for example ASMS-USH-000001.
• Capture name and contact details.
• Capture residential community and LGA.
• Capture farm location, farm size, farming type and crops cultivated.
• Capture NIN only where required and through an approved process.
• Support duplicate detection and review.
• Protect personal and identity information.
7. Farmer Verification
The proposed verification model combines NIN identity verification, physical farm verification and community verification.
The MVP may record verification outcomes and supporting references; live NIN verification requires an authorized
integration.
• Not verified.
• Pending verification.
ASMS | Ushongo LGA, Benue State Page 4
• Partially verified.
• Verified.
• Rejected.
8. Subsidy Programme Management
Authorized administrators can create programmes with a name, description, category, geographic coverage, dates,
eligibility rules, available budget or resources, beneficiary limits, distribution method and status.
Programme statuses: Draft, Pending Authorization, Published, Active, Closed, Suspended and Completed.
9. Subsidy Application Management
Farmers can view eligible programmes and submit applications. Agricultural officers review applications and the Local
Government Administrator makes the final local approval decision.
Application statuses: Draft, Submitted, Under Review, Returned for Correction, Approved, Rejected, Waitlisted and
Withdrawn. Decisions should include a reason where applicable.
10. Beneficiary Selection
Selection is eligibility-based and may use programme-defined prioritization. Criteria can include verified farmer status,
location, farm size, crop type, programme rules and previous benefits where relevant. Rules must be published or
otherwise communicated clearly and decisions must be traceable.
11. Administrative Hierarchy
State administrators oversee state programmes, budgets and participating LGAs. Local Government Administrators
manage their jurisdiction, officers, applications and approved allocations. Agricultural Officers carry out assigned field and
review activities. Access must be restricted by role and jurisdiction.
12. Budget Management
State Administrators authorize programme budgets. Local Government Administrators submit allocation proposals and
manage approved allocations. The system must distinguish authorized budget, proposed allocation, approved allocation,
committed amount, actual disbursement and remaining balance.
13. Subsidy Distribution
The long-term product supports financial assistance and physical agricultural input distribution. Records should identify
the beneficiary, programme, amount or input type and quantity, date, location, responsible officer, status and payment
reference where applicable.
A later phase will introduce dual confirmation: an officer records delivery and the farmer confirms receipt using an OTP or
another approved method. Disputed records must be flagged rather than treated as confirmed.
14. Notifications
The product is intended to support SMS, email and in-app notifications for registration, verification, programme
announcements, application decisions, beneficiary selection, distribution and complaint updates. The MVP prioritizes
in-app and SMS notifications; email is planned for a later phase.
ASMS | Ushongo LGA, Benue State Page 5
15. Public Transparency Portal
A later phase will provide published programme information, budgets, aggregated beneficiary statistics, distribution
statistics, budget utilization, performance comparisons and downloadable reports. It must not expose names where not
authorized, NINs, phone numbers, bank details or confidential records.
16. Complaints and Fraud Reporting
A later phase will support complaints, anonymous reports, evidence attachments, classification, investigator assignment,
investigation records, resolution tracking and notifications. Routine complaints are handled locally; complaints involving
LGA administrators or serious misconduct are escalated to state investigators. Conflicts of interest must be managed.
17. MVP Scope
• Farmer registration, authentication and profile management.
• Unique Farmer ID generation and duplicate checks.
• Farm information management.
• Officer and administrator accounts.
• Farmer verification records.
• Subsidy programme creation and eligibility rules.
• Subsidy applications and officer review.
• Local Government Administrator final approval.
• Beneficiary management.
• Basic distribution records.
• In-app notifications and SMS integration.
• Basic dashboards and audit logs.
• Role-based access control.
Advanced payment processing, full distribution confirmation, advanced budget reporting, offline field operations, email
notifications, public transparency, advanced complaint investigations, analytics and multi-LGA rollout are planned for later
phases. The architecture should anticipate these capabilities.
18. Non-Functional Requirements
Security and privacy
• Secure authentication and role-based access control.
• Protected personal information and encrypted communication.
• Secure file handling and audit trails for sensitive actions.
• Compliance planning for applicable Nigerian data protection requirements.
Performance and reliability
• Responsive interfaces and efficient database queries.
• Consistent application records, backups and error handling.
• Reliable notification processing and recoverable failures.
Usability and scalability
• Mobile-responsive web experience and simple workflows.
ASMS | Ushongo LGA, Benue State Page 6
• Assisted registration for farmers who need help.
• Architecture that supports additional LGAs and states.
19. Proposed Technical Direction
Component Proposed technology
Web frontend React, Vite, TypeScript
Mobile app React Native, Expo
Backend Node.js, NestJS
Database PostgreSQL
Storage Supabase Storage or equivalent
API REST API
Maps OpenStreetMap
Web deployment Vercel
Backend hosting Suitable cloud hosting provider
Final technology and hosting choices will be confirmed during technical architecture design.
20. Success Criteria
• Farmers can register and receive unique Farmer IDs.
• Officers can record verification outcomes.
• Administrators can create subsidy programmes.
• Farmers can submit applications.
• Officers can review applications and LGA administrators can make final decisions.
• Beneficiaries can be identified and managed.
• Basic distribution records can be maintained.
• Farmers receive application notifications.
• Sensitive actions are audited and unauthorized access is blocked.
21. Risks and Dependencies
• Limited internet connectivity and digital literacy.
• Inaccurate registration information and duplicate applications.
• Unauthorized access to sensitive records.
• Government approvals and operational ownership.
• Programme funding and availability of inputs.
• Dependence on SMS, identity verification and payment providers.
• Official integrations require authorization and agreements.
22. Implementation Roadmap
• Requirements: finalize PRD and SRS, roles and workflows.
• Design: architecture, database, API and UI/UX.
ASMS | Ushongo LGA, Benue State Page 7
• Backend: authentication, farmers, verification, programmes and applications.
• Frontend: farmer, officer, LGA and state interfaces.
• Mobile: farmer and officer workflows with API integration.
• Testing: functional, security, database and user acceptance testing.
• Prototype deployment: deploy web, backend and database using test data.
• Expansion: distribution, budget management, transparency, complaints, offline support and multi-LGA deployment.
23. Expected Outcomes and Conclusion
ASMS aims to improve farmer registration and identification, subsidy application management, beneficiary selection,
distribution records, programme monitoring and accountability. Its first implementation will focus on Ushongo LGA while
preserving a scalable foundation for future government agricultural programmes.
⋮⋮
⋮⋮
