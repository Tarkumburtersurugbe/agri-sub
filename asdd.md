ASMS — Updated Architecture & Database Design Page 5
l blockchain_outbox rows are created in the same PostgreSQL transaction as the approved business action, then
processed asynchronously.
Use generic reference_type/reference_id links only if the application enforces referential integrity in service logic. For
stronger relational integrity, add nullable foreign keys such as programme_id, allocation_id, application_decision_id and
distribution_batch_id to blockchain_anchors, or use separate typed link tables. Do not rely on an unconstrained text
reference for critical audit relationships.
5.2 Important indexes and constraints
l Unique constraint on (network_id, tx_hash) when tx_hash is present.
l Unique constraint on (network_id, contract_address) for active deployment records, as appropriate.
l Unique constraint on (network_id, contract_id, reference_type, reference_id, record_version) for each anchor version.
l Indexes on transaction status, submitted_at, block_number, reference_type/reference_id and event name.
l Store transaction hashes and addresses in normalized lowercase form for consistent lookup.
l Store monetary amounts as integer smallest units or PostgreSQL NUMERIC with an explicit currency and scale; never
use floating-point arithmetic for money.
6. End-to-end workflows
6.1 Programme approval
l Authorised officer prepares programme; LGA/State approval workflow is completed in PostgreSQL.
l Backend validates the approval authority, programme status and required approvals.
l Within one database transaction, save the decision, status history, audit log and blockchain_outbox item with a
canonical data hash.
l Background worker submits the anchor transaction to Polygon using the approved relayer.
l Worker waits for the configured confirmation policy, saves tx hash/block/status and processes the contract event.
l ASMS displays the programme as approved in its business workflow and shows blockchain verification as pending,
confirmed or failed.
6.2 Beneficiary approval
l Officer review and LGA Administrator final decision remain the ASMS approval process.
l Create the beneficiary record in PostgreSQL only after the authorised final decision.
l Create a hash from a minimal, versioned approval evidence payload; do not include personal data.
l Queue and submit the approval anchor to Polygon.
l Link the returned transaction and event to the application decision and show a verification reference to authorised
users.
6.3 Distribution confirmation
l An authorised officer records the distribution batch, items, quantities and evidence in PostgreSQL.
l A separate authorised reviewer confirms the batch where the programme requires two-person review.
l The backend anchors the completed batch evidence hash to Polygon.
l Corrections are appended as new records linked to the original batch; do not attempt to delete the original blockchain
record.
l Reports distinguish between recorded distribution, reviewed distribution and blockchain-anchored distribution.
ASMS — Updated Architecture & Database Design Page 6
Important: A blockchain transaction proves that a specific declaration was submitted and included on-chain. It does not
independently prove that physical goods reached farmers. Field verification, receipts, beneficiary acknowledgement and
independent inspections remain necessary.
7. Blockchain transaction lifecycle and reliability
Status Meaning
PENDING Business action is approved and queued; no transaction has been submitted yet.
SUBMITTED Transaction hash received from the RPC provider.
CONFIRMING Transaction is included in a block; waiting for the configured confirmation/finality policy.
CONFIRMED Transaction has met the application's confirmation policy and expected event was validated.
FAILED Transaction reverted, was rejected or failed validation.
RETRY_REQUIRED Transient issue occurred; retry is allowed after checking nonce and prior transaction state.
REORG_REVIEW A previously observed block/transaction changed due to a chain reorganisation and needs reconciliation.
l Use an outbox pattern: save the approved business record and its pending blockchain job atomically in PostgreSQL.
l Process blockchain jobs asynchronously; do not make farmer registration or routine browsing wait for chain
confirmation.
l Use idempotency keys and unique business references to prevent duplicate anchors during retries.
l Track nonce, transaction hash, receipt, block number, event log index and failure details.
l Reconcile periodically against Polygon RPC and re-check critical transactions before marking them final in reports.
l Do not silently treat a failed blockchain transaction as a successful anchor. Keep the business record and show its
blockchain status separately.
8. Updated API design
Endpoint Purpose
GET /api/v1/blockchain/networks Lists configured networks available to the application.
GET /api/v1/blockchain/contracts Lists active contract deployments for authorised administrators.
GET /api/v1/blockchain/transactions/:id Returns transaction lifecycle and explorer reference.
GET /api/v1/blockchain/verify/:referenceType/:referenceId Checks an ASMS record against its stored anchor.
POST /api/v1/blockchain/anchors/:id/verify Runs an authorised verification check and stores the result.
GET /api/v1/blockchain/health Returns RPC connectivity, indexer lag and queue health for administrators.
These routes are examples. Protect operational endpoints with role-based permissions and jurisdiction checks. Public
verification endpoints should expose only deliberately public, non-sensitive information.
9. Security, privacy and governance
l Keep private keys out of source code, frontend bundles, ordinary environment files and PostgreSQL. Use a managed
secret/key service or hardware-backed signer for production.
l Use a dedicated relayer account with limited funds and narrowly scoped contract permissions; monitor balances and
unusual activity.
ASMS — Updated Architecture & Database Design Page 7
l Separate human approval from transaction submission. A relayer should not be able to invent an approval that the
ASMS workflow has not authorised.
l Use role-based access control in NestJS and contract-level access control on Polygon. These are complementary, not
substitutes.
l Apply rate limits, input validation, secure session/token handling, HTTPS, audit logging, backups and security
monitoring.
l Perform independent Solidity review, automated tests, static analysis and testnet pilot before production.
l Define data retention, correction, dispute and complaint processes. Blockchain immutability does not remove the need
to correct inaccurate source data.
l Publish only aggregate programme information or deliberately approved verification data; do not expose individual
farmer participation.
10. Recommended technology stack
Area Technology
Web frontend React + Vite + TypeScript
Mobile (later phase) React Native + Expo
Backend Node.js + NestJS + TypeScript
Database / ORM PostgreSQL + Prisma
Smart contracts Solidity + OpenZeppelin contracts
Contract development Hardhat; automated unit and integration tests
Blockchain connection Ethers.js + Polygon-compatible RPC provider
Development network Polygon Amoy testnet
Production network candidate Polygon PoS mainnet, subject to cost, security, governance and operational review
API documentation Swagger / OpenAPI
Maps OpenStreetMap
Private documents Private object storage with access controls
11. Development roadmap
Phase Work Completion evidence
1. Foundation Keep existing ASMS modules and database as the base; add
blockchain tables and configuration.
Database migrations, network config and
documented data-hash format.
2. Contract MVP Implement core registry, roles, programme anchors and distribution
anchors in Solidity.
Unit tests, access-control tests and deployment to
Polygon Amoy.
3. Backend integration Add blockchain service, transaction outbox, worker, event indexer and
verification endpoints.
Successful testnet transactions and
retry/reconciliation tests.
4. Workflow integration Connect programme approval, allocation approval, beneficiary approval
and distribution completion.
End-to-end tests showing DB record ↔ hash ↔
transaction ↔ event.
5. Pilot and review Run a controlled pilot, review gas costs, key management, privacy and
governance.
Security review, operational runbook and go/no-go
approval.
6. Production Deploy contracts and backend integrations to approved production
infrastructure.
Production monitoring, key custody, incident plan
and audit sign-off.
ASMS — Updated Architecture & Database Design Page 8
12. Testing and acceptance criteria
l An approved programme can be anchored on Polygon Amoy and independently verified against its PostgreSQL
record.
l A modified off-chain record fails hash comparison against its earlier anchor.
l Unauthorised roles cannot call privileged smart-contract functions.
l Beneficiary anchors do not reveal names, phone numbers, NIN or other personal information.
l A distribution batch can be anchored, queried and corrected through an append-only correction event.
l A failed or delayed RPC transaction remains visible as pending/failed and can be safely retried without creating
duplicate business records.
l The system can reconcile stored transaction references with contract events and report mismatches.
l The farmer and staff workflows remain usable when the blockchain provider is temporarily unavailable; blockchain jobs
queue and resume safely.
13. Key decisions still required before production
l Who legally controls the Polygon contract roles: State Government, a designated programme authority, or a governed
multi-signature group?
l Which actions require one approval versus two-person approval before an on-chain anchor is submitted?
l Which allocation figures and distribution summaries are approved for public visibility?
l What confirmation/finality policy will the system use before displaying an anchor as confirmed?
l Who pays for Polygon transaction fees and manages the relayer account?
l What is the contract upgrade, pause, incident response and key-recovery policy?
l Which privacy and public-record rules apply to farmer and subsidy programme data?
14. Final architecture recommendation
Proceed with a hybrid design. PostgreSQL remains the source of truth for ASMS operational data, while Polygon provides
a verifiable record of selected high-impact approvals and distribution declarations. Solidity smart contracts enforce limited,
explicit on-chain permissions and emit events for audit and verification. Start on Polygon Amoy, complete a controlled pilot
and security review, then decide whether to deploy to Polygon PoS mainnet.
Do not promise that blockchain prevents all fraud. It can make later alteration of anchored evidence detectable and
improve auditability, but it cannot guarantee that the original information was truthful or that physical subsidy goods were
delivered. Human verification, good governance and secure application controls remain essential.
