# Project Progress Checklist — Secure Coaching Content Portal

## How to use this sheet

Allowed status values:

- `[ ]` Not started
- `[-]` In progress
- `[!]` Blocked
- `[x]` Done

For every item moved to done, record:

- Owner:
- Acceptance evidence:
- Dependencies:
- Notes:

Overall project status: Not started  
Current gate: Gate 0 — requirements and architecture approval  
Last updated: 2026-10-16

## Confirmed decisions

- [x] DEC-001 — Use Next.js for the web application.
  - Owner: Product/Architecture
  - Acceptance evidence: Customer planning decision
  - Dependencies: None
  - Notes: Admin and student web journeys.
- [x] DEC-002 — Use Java 21 and Spring Boot 4.1 for the backend.
  - Owner: Product/Architecture
  - Acceptance evidence: Customer planning decision
  - Dependencies: None
  - Notes: Modular monolith. Pin the latest Spring Boot 4.1 patch when implementation starts.
- [x] DEC-003 — Use React Native/Expo for Android and iOS.
  - Owner: Product/Architecture
  - Acceptance evidence: Customer planning decision
  - Dependencies: None
  - Notes: Student-only mobile MVP.
- [x] DEC-004 — Serve one coaching institute initially.
  - Owner: Product
  - Acceptance evidence: Customer planning decision
  - Dependencies: None
  - Notes: Keep an organization ownership boundary for future evolution.
- [x] DEC-005 — Use server-rendered, watermarked page images/tiles.
  - Owner: Product/Security
  - Acceptance evidence: Customer planning decision
  - Dependencies: Viewer proof-of-concept
  - Notes: Original PDFs are not sent to student clients.
- [x] DEC-006 — Use AWS infrastructure.
  - Owner: Product/Architecture
  - Acceptance evidence: Customer planning decision
  - Dependencies: Cost approval
  - Notes: Private S3, RDS PostgreSQL, containers, SQS, and CloudFront.
- [x] DEC-007 — Core MVP supports admin and student roles.
  - Owner: Product
  - Acceptance evidence: Customer planning decision
  - Dependencies: Permission model
  - Notes: Additional roles must be addable later.
- [x] DEC-008 — Use Amazon Cognito with OIDC Authorization Code and PKCE.
  - Owner: Product/Architecture
  - Acceptance evidence: Customer planning decision
  - Dependencies: Cognito configuration and managed-login design
  - Notes: Spring Security validates identity; business roles and resource authorization remain local.
- [x] DEC-009 — Adopt the modular engineering instruction and quality-gate package.
  - Owner: Product/Engineering
  - Acceptance evidence: Customer selection on 2026-10-16
  - Dependencies: None
  - Notes: GitHub pull requests and GitHub Actions; rules A1–A8, C1–C7, Q1–Q8, and D1–D7; AI-provenance tagging excluded.

## Gate 0 — Requirements approval

Exit criterion: customer requirements, unresolved limits, policies, and acceptance criteria are signed off.

- [ ] G0-001 — Approve `implementation-plan-nishant-tution.md`.
- [ ] G0-002 — Confirm maximum PDF file size.
- [ ] G0-003 — Confirm maximum page count and unsupported PDF features.
- [ ] G0-004 — Confirm institute timezone.
- [ ] G0-005 — Confirm student password policy.
- [ ] G0-006 — Confirm web idle and absolute session durations.
- [ ] G0-007 — Confirm mobile access and refresh session durations.
- [ ] G0-008 — Approve watermark fields, opacity, density, and placement.
- [ ] G0-009 — Confirm behavior when students join or leave assigned batches.
- [ ] G0-010 — Approve original, derivative, account, and audit retention periods.
- [ ] G0-011 — Approve supported browser matrix.
- [ ] G0-012 — Approve minimum Android/iOS versions and physical test devices.
- [ ] G0-013 — Approve accessibility target.
- [ ] G0-014 — Approve availability target, RPO, and RTO.
- [ ] G0-015 — Select email provider and verify sender-domain ownership.
- [ ] G0-016 — Confirm mobile store-account ownership, privacy policy, and support contact.
- [ ] G0-017 — Supply logo, colors, icons, app names, and branding assets.
- [ ] G0-018 — Approve core MVP and post-MVP split.

## Gate 1 — Architecture and security approval

Exit criterion: HLD, LLD, threat model, proof-of-concept results, AWS topology, and costs are approved.

- [ ] G1-001 — Review and approve `HLD.md`.
- [ ] G1-002 — Review and approve `LLD.md`.
- [ ] G1-003 — Record the framework and runtime version ADR, including the selected Spring Boot 4.1 patch.
- [ ] G1-004 — Record ECS Fargate/App Runner deployment ADR.
- [ ] G1-005 — Record Next.js hosting and same-origin routing ADR.
- [ ] G1-006 — Complete data-flow diagram and trust-boundary threat model.
- [ ] G1-007 — Complete object-level authorization matrix.
- [ ] G1-008 — Prototype safe PDF validation and rasterization.
- [ ] G1-009 — Benchmark watermark/tile generation quality, CPU, memory, and latency.
- [ ] G1-010 — Validate Android secure-window behavior on physical devices.
- [ ] G1-011 — Validate iOS capture and app-switcher behavior on physical devices.
- [ ] G1-012 — Select PDF parser/rasterizer, malware scanner, and image encoder.
- [ ] G1-013 — Select IaC tool and repository workflow.
- [ ] G1-014 — Produce AWS staging and production topology.
- [ ] G1-015 — Produce AWS monthly cost estimate and budget alerts.
- [ ] G1-016 — Approve backup, restore, incident-response, and secret-rotation designs.
- [ ] G1-017 — Approve logging/privacy redaction policy.
- [ ] G1-018 — Approve API versioning and OpenAPI workflow.
- [ ] G1-019 — Approve Cognito user pool, app clients, scopes, claims, MFA, managed-login branding, and recovery configuration.
- [ ] G1-020 — Approve Cognito/local-user provisioning, disablement, reconciliation, and failure handling.

## Gate 2 — Engineering foundation

Exit criterion: repositories, environments, CI, core data platform, observability, identity, and authorization are working in staging.

- [ ] G2-001 — Initialize monorepo and ownership rules.
- [ ] G2-002 — Create Java API and worker projects.
- [ ] G2-003 — Create Next.js web project.
- [ ] G2-004 — Create React Native Expo project and development builds.
- [ ] G2-005 — Create shared OpenAPI client generation.
- [ ] G2-006 — Add formatting, linting, tests, and build pipelines.
- [ ] G2-007 — Add dependency, container, license, and secret scanning.
- [ ] G2-008 — Provision isolated development, staging, and production foundations.
- [ ] G2-009 — Configure DNS, TLS, WAF, routing, and private networking.
- [ ] G2-010 — Provision RDS PostgreSQL and migration pipeline.
- [ ] G2-011 — Provision private S3 storage and lifecycle policies.
- [ ] G2-012 — Provision SQS and dead-letter queue.
- [ ] G2-013 — Configure secrets and least-privilege IAM roles.
- [ ] G2-014 — Configure structured logs, metrics, alerts, and correlation IDs.
- [ ] G2-015 — Implement organization, user, role, and permission schema.
- [ ] G2-016 — Provision Cognito user pool, separate web/mobile app clients, exact redirect allowlists, scopes, claims, and managed-login branding.
- [ ] G2-017 — Implement Spring Security OIDC login, encrypted authorized-client storage, opaque web sessions, and CSRF protection.
- [ ] G2-018 — Implement Spring Security resource-server token validation and immutable Cognito-subject mapping.
- [ ] G2-019 — Implement mobile OIDC Authorization Code with PKCE, Cognito refresh rotation, and Keychain/Keystore storage.
- [ ] G2-020 — Configure mandatory administrator TOTP MFA plus local assurance and permission enforcement.
- [ ] G2-021 — Configure Cognito invitations, password reset, password policy, token revocation, and global sign-out.
- [ ] G2-022 — Implement local/Cognito user provisioning, disablement, compensation, and reconciliation.
- [ ] G2-023 — Verify OIDC state/nonce/PKCE, token validation, redirect allowlists, revocation, disabled-account enforcement, and account-enumeration resistance.

## Gate 3 — Administration and coaching structure

Exit criterion: administrators can securely manage students, batches, subjects, and branding.

- [ ] G3-001 — Build administrator application shell and navigation.
- [ ] G3-002 — Build student create/edit/activate/deactivate workflows.
- [ ] G3-003 — Build validated CSV student import and result reporting.
- [ ] G3-004 — Build batch CRUD.
- [ ] G3-005 — Build batch membership management.
- [ ] G3-006 — Build subject/category management.
- [ ] G3-007 — Build basic branding configuration.
- [ ] G3-008 — Add permissions and object-ownership checks for every endpoint.
- [ ] G3-009 — Add append-only audit events for administrative mutations.
- [ ] G3-010 — Complete accessibility and end-to-end tests for admin workflows.

## Gate 4 — Secure content pipeline

Exit criterion: valid PDFs process into private derivatives safely, observably, and repeatably.

- [ ] G4-001 — Build paper metadata creation and upload initialization.
- [ ] G4-002 — Enforce upload type, size, ownership, and object-key constraints.
- [ ] G4-003 — Implement quarantine and malware scanning.
- [ ] G4-004 — Implement PDF structure, page, dimension, and complexity validation.
- [ ] G4-005 — Implement SHA-256 integrity recording.
- [ ] G4-006 — Implement idempotent page rasterization and tiling.
- [ ] G4-007 — Generate and verify private page manifests.
- [ ] G4-008 — Implement processing state and safe error reporting.
- [ ] G4-009 — Implement retries, dead-letter handling, and authorized replay.
- [ ] G4-010 — Prevent publication of partial or failed output.
- [ ] G4-011 — Implement paper archive/deletion and retention behavior.
- [ ] G4-012 — Test benign, malformed, encrypted, oversized, and malicious samples.
- [ ] G4-013 — Document processing operations and recovery runbook.

## Gate 5 — Assignment and access

Exit criterion: batch assignments, time windows, and individual overrides are correctly enforced.

- [ ] G5-001 — Implement assignment create/list/detail/update.
- [ ] G5-002 — Implement future availability and expiry.
- [ ] G5-003 — Implement individual grant/extend/revoke/restore overrides.
- [ ] G5-004 — Implement deterministic access-policy service.
- [ ] G5-005 — Enforce access synchronously on protected requests.
- [ ] G5-006 — Implement safe student-facing denial reasons.
- [ ] G5-007 — Implement active/upcoming/expired student queries.
- [ ] G5-008 — Cover batch join/leave behavior with policy tests.
- [ ] G5-009 — Cover time-boundary and timezone behavior with tests.
- [ ] G5-010 — Complete broken-object-authorization test matrix.

## Gate 6 — Protected viewer

Exit criterion: authorized students progressively view only server-watermarked imagery, and revocation is effective.

- [ ] G6-001 — Implement short-lived viewer-session creation.
- [ ] G6-002 — Implement manifest endpoint without storage identifiers.
- [ ] G6-003 — Implement validated page/tile endpoint.
- [ ] G6-004 — Implement dynamic server-side watermarking.
- [ ] G6-005 — Prevent shared caching and cross-user leakage.
- [ ] G6-006 — Implement bounded view telemetry and audit events.
- [ ] G6-007 — Recheck expiry, revocation, account, assignment, and paper state.
- [ ] G6-008 — Implement web progressive viewer.
- [ ] G6-009 — Add web print blanking and approved interaction deterrents.
- [ ] G6-010 — Verify original PDFs and unwatermarked derivatives never reach student clients.
- [ ] G6-011 — Load test 100 concurrent viewers.
- [ ] G6-012 — Security test identifier tampering, replay, caching, and revoked sessions.

## Gate 7 — Student web experience

Exit criterion: the complete student MVP works accessibly in supported browsers.

- [ ] G7-001 — Build branded login, invitation, and reset screens.
- [ ] G7-002 — Build active/upcoming/expired paper dashboard.
- [ ] G7-003 — Build paper details and access-status states.
- [ ] G7-004 — Integrate protected web viewer.
- [ ] G7-005 — Build profile and session management.
- [ ] G7-006 — Handle loading, empty, offline, retry, forbidden, expired, revoked, and processing states.
- [ ] G7-007 — Complete responsive-browser testing.
- [ ] G7-008 — Complete accessibility verification.
- [ ] G7-009 — Complete student web end-to-end tests.

## Gate 8 — Android and iOS student application

Exit criterion: the complete student MVP is accepted on physical Android/iOS devices and beta channels.

- [ ] G8-001 — Build app bootstrap and signed-in/signed-out navigation.
- [ ] G8-002 — Build mobile login and password recovery.
- [ ] G8-003 — Integrate secure credential storage and serialized refresh.
- [ ] G8-004 — Build active/upcoming/expired paper dashboard.
- [ ] G8-005 — Build paper details and status states.
- [ ] G8-006 — Build protected mobile viewer.
- [ ] G8-007 — Enable Android secure-window behavior on protected screens.
- [ ] G8-008 — Implement iOS capture/mirroring response.
- [ ] G8-009 — Obscure protected app-switcher snapshots.
- [ ] G8-010 — Prevent intentional protected-image persistence and sharing.
- [ ] G8-011 — Build profile, logout, logout-all, and session controls.
- [ ] G8-012 — Handle offline, interrupted, expired, revoked, retry, and upgrade states.
- [ ] G8-013 — Configure redacted crash/error reporting.
- [ ] G8-014 — Complete accessibility and approved device-matrix tests.
- [ ] G8-015 — Complete internal Android release and TestFlight acceptance.
- [ ] G8-016 — Complete store metadata, privacy disclosures, signing, and submission readiness.

## Gate 9 — Production readiness

Exit criterion: security, recovery, performance, support, and release evidence are approved.

- [ ] G9-001 — Complete unit, integration, contract, and end-to-end suites.
- [ ] G9-002 — Complete static, dependency, container, and secret scans.
- [ ] G9-003 — Complete threat-model verification and security assessment.
- [ ] G9-004 — Resolve all release-blocking security findings.
- [ ] G9-005 — Complete load, endurance, and worker-backlog tests.
- [ ] G9-006 — Complete accessibility acceptance.
- [ ] G9-007 — Test RDS and required S3 restoration.
- [ ] G9-008 — Test dead-letter replay and document-processing recovery.
- [ ] G9-009 — Approve dashboards, alarms, on-call ownership, and runbooks.
- [ ] G9-010 — Approve data retention and scheduled cleanup.
- [ ] G9-011 — Complete administrator onboarding and support documentation.
- [ ] G9-012 — Run production deployment and rollback rehearsal.
- [ ] G9-013 — Complete pilot with approved administrator and student users.
- [ ] G9-014 — Record final web, Android, iOS, backend, and infrastructure release approval.

## Post-MVP backlog

- [ ] P-001 — Assignment and expiry email notifications.
- [ ] P-002 — Advanced analytics dashboard.
- [ ] P-003 — CSV exports for users, assignments, and audit/view records.
- [ ] P-004 — Full branding editor.
- [ ] P-005 — Instructor and additional staff roles.
- [ ] P-006 — Custom domains.
- [ ] P-007 — Multi-tenant onboarding and operations.
- [ ] P-008 — Push notifications.
- [ ] P-009 — Evaluate caching or Redis from production measurements.

## Active risks

- [!] RISK-001 — Screenshot prevention cannot be guaranteed.
  - Owner: Product/Security
  - Mitigation: Accurate messaging, server-side forensic watermarking, platform deterrents.
  - Review gate: Gate 1 and Gate 9
- [!] RISK-002 — Dynamic watermarking may exceed latency/cost targets.
  - Owner: Architecture
  - Mitigation: Early benchmark, progressive tiles, horizontal scaling, profile before caching.
  - Review gate: Gate 1 and Gate 6
- [!] RISK-003 — PDF processing handles hostile files.
  - Owner: Security/Backend
  - Mitigation: Quarantine, malware scan, parser limits, isolated worker, least privilege.
  - Review gate: Gate 1 and Gate 4
- [!] RISK-004 — iOS cannot universally block screen capture.
  - Owner: Product/Mobile
  - Mitigation: Detection/obscuring where supported and persistent visible watermark.
  - Review gate: Gate 1 and Gate 8
- [!] RISK-005 — Open requirements may change acceptance or cost.
  - Owner: Product
  - Mitigation: Close all Gate 0 items before coding affected features.
  - Review gate: Gate 0

## Change log

- 2026-10-16 — Added approved engineering instructions, quality gates, GitHub delivery standards, and transfer handoff.
- 2026-10-15 — Initial checklist created from approved planning direction.
