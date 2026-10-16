# GitHub Review and CI/CD Standards

## 1. Branches and pull requests

- Protect the default and production branches. Do not push directly to them.
- Use short-lived branches and narrowly scoped pull requests.
- Link every pull request to approved requirements, a checklist item, or an
  issue with testable acceptance criteria.
- Update the branch from its target before merge and rerun all checks after
  resolving conflicts.
- Require at least one peer approval and dismissal of stale approvals after
  material changes.
- Require CODEOWNERS approval for security, identity, authorization, database,
  infrastructure, and deployment paths once owners are defined.
- Do not merge with unresolved review threads or failing required checks.

Commit and pull-request text should state what changed and why. Keep history
factual and avoid design-document repetition. AI-provenance tags are not
required by this project.

## 2. Required GitHub Actions checks

The exact workflow split may evolve, but branch protection must require all
applicable checks:

1. Repository policy and generated-file freshness.
2. Formatting and linting.
3. TypeScript strict type checking.
4. Java compilation and static analysis.
5. Unit tests and coverage.
6. PostgreSQL repository integration tests.
7. API/OpenAPI contract checks and client-generation freshness.
8. Web and mobile component tests.
9. Production builds for API, worker, web, and mobile packages.
10. Database migration validation against a clean database and upgrade path.
11. Secret scanning.
12. Dependency and software-composition analysis.
13. Container and infrastructure-as-code scanning.
14. Sonar quality gate.
15. License-policy checks.

End-to-end, accessibility, physical-device, performance, security, and
recovery suites may run in staged workflows, but the checklist defines when
their evidence is required before promotion.

## 3. CI safety

- Use GitHub OpenID Connect and short-lived AWS credentials. Do not store
  long-lived AWS keys in GitHub.
- Scope workflow permissions explicitly and minimally.
- Pin third-party actions to reviewed immutable commit SHAs.
- Keep production environments protected by named reviewers.
- Do not expose secrets to untrusted pull-request workflows.
- Sanitize logs and uploaded artifacts. Do not retain protected document
  samples, tokens, signed URLs, or production data.
- Set timeouts and concurrency controls for every workflow.
- Cancel obsolete runs where safe without cancelling an active production
  deployment.

## 4. Dependencies and generated output

- Pin Java, Node, package-manager, action, container-base, and tool versions in
  canonical manifests.
- Commit approved lockfiles.
- Automated dependency updates require the same tests, scans, and review as
  other changes.
- Generate OpenAPI clients and other derived sources in CI and fail when the
  committed result is stale.
- Do not publish artifacts from a pull request originating from an untrusted
  fork.

## 5. Build artifacts

- Build deployable artifacts once from an approved commit.
- Give every artifact an immutable version tied to the commit SHA and release
  identifier.
- Produce a software bill of materials and provenance where supported.
- Scan artifacts before promotion.
- Promote the same verified artifact through staging and production; do not
  rebuild for each environment.
- Retain checksums, image digests, release notes, migration version, and scan
  evidence with the release.

## 6. Environments and deployment

- Keep development, staging, and production accounts, data, identities,
  secrets, and access boundaries isolated.
- Never copy production credentials or protected content into lower
  environments.
- Manage infrastructure through reviewed infrastructure-as-code.
- Rehearse database migrations, document processing, and rollback in staging.
- Require manual approval for production deployment.
- Run pre-deployment readiness and post-deployment smoke checks.
- Stop or roll back when health, error rate, access-denial behavior, migration,
  or viewer checks violate release criteria.
- Prefer a forward fix only when it is safer than rollback and has explicit
  approval.

## 7. Release and rollback evidence

Every production release records:

- approved commit and immutable artifact digests;
- database and infrastructure change set;
- completed required checks and approvals;
- backup/readiness status;
- deployment and verification timestamps;
- dashboard and alarm status;
- rollback criteria and tested procedure;
- release owner and support handoff;
- known limitations and follow-up issues.

## 8. Exceptions

A required check or policy exception must identify its rationale, risk, owner,
compensating control, tracking issue, and expiry date. Exceptions require
security or architecture approval when they affect trust boundaries, data,
identity, deployment, or quality thresholds.
