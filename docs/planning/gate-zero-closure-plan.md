# Gate 0 Closure Plan

## Current status

The project remains at Gate 0. No product code, infrastructure, prototype, or
benchmark has been implemented.

Approved decisions:

1. Next.js and TypeScript for the administrator and student web application.
2. Java 21 and Spring Boot 4.1 modular-monolith backend.
3. React Native/Expo and TypeScript for student Android and iOS applications.
4. One institute initially, with organization ownership boundaries retained.
5. Server-watermarked page images or tiles; original PDFs never reach
   students.
6. AWS infrastructure.
7. Admin and student MVP roles with an extensible permission model.
8. Amazon Cognito using OIDC Authorization Code with PKCE; business
   authorization remains local.

The requirements document, HLD, and LLD are not approved as whole documents.
All G0-001 through G0-018 checklist items remain unresolved.

## Proposed Gate 0 baseline

These values are recommendations until the appropriate owner approves them:

- PDF: 50 MiB and 300 pages; reject encrypted/password-protected, package,
  attachment, JavaScript/action, XFA, 3D/multimedia, malformed, and
  resource-limit-exceeding files.
- Timezone: UTC persistence plus an institute IANA timezone; use
  `Asia/Kolkata` only if confirmed.
- Passwords: Cognito-managed, minimum 12 characters, single-use expiring
  invitations/resets, and no routine expiry without a security event.
- Web sessions: admin 15-minute idle/8-hour absolute; student 30-minute
  idle/12-hour absolute.
- Mobile: 15-minute access tokens and rotating 30-day refresh credentials,
  revocable on disablement, password change, and global logout.
- Watermark: repeated diagonal full name, masked email, student reference, and
  short viewer marker; initial opacity range 12–18%, subject to visual testing.
- Batch membership: joining grants current active assignments; leaving removes
  access unless an explicit individual grant applies; audit history remains.
- Accessibility: WCAG 2.2 AA plus applicable mobile criteria.
- Service targets: 99.9% monthly availability, RPO at most 15 minutes, and RTO
  at most 4 hours.
- Compatibility: latest two stable major desktop browsers; proposed Android
  11+ and iOS 17+, subject to Expo and institute-device validation.
- Email: Amazon SES with an institute-owned verified sender domain.
- Store accounts: institute-owned Apple and Google accounts with privacy and
  support contacts.
- Scope: retain the documented Core MVP/post-MVP split.

Retention periods require legal/business review and must not be inferred.

## Closure sequence

1. Create a decision register for G0-002 through G0-018 with owner, proposed
   value, rationale, acceptance test, date, and evidence.
2. Review decisions in order: scope and batch behavior; content and watermark;
   identity and sessions; retention, service, and accessibility; compatibility,
   external ownership, and branding.
3. Reconcile two design inconsistencies:
   - Protected content requests must preserve synchronous revocation and expiry
     enforcement; bounded re-evaluation must not weaken that requirement.
   - Decide whether invitation/reset UI is Cognito managed login or an
     application-owned branded route.
4. Approve G0-001 and G0-018 last, after dependent decisions close.
5. Prepare Gate 1 ADR, threat-model, authorization-matrix, proof-of-concept,
   topology, cost, and Cognito review plans.

Do not execute Gate 1 prototypes, benchmarks, infrastructure, or product
implementation without separate explicit approval.

## Engineering governance decision

The selected mandatory baseline is recorded in `AGENTS.md` and
`docs/engineering/`:

- evidence-first agent and SDLC behavior;
- portable coding standards for Java/Spring and strict TypeScript/React;
- behavior-first testing and Definition of Done;
- at least 80% overall and 90% new-code coverage;
- no new blocker/critical Sonar findings and at most 3% duplication;
- GitHub pull requests and GitHub Actions;
- peer review, secure CI, immutable artifact promotion, environment isolation,
  and rollback evidence.

Nokia/NCC corporate headers, Gerrit/Jenkins, telecom-specific conventions,
legacy React rules, and AI-provenance tags were explicitly excluded.
