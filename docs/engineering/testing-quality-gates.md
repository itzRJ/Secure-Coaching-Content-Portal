# Testing and Quality Gates

## 1. Principles

- Tests verify observable behavior, contracts, authorization, and failure
  handling. Do not write assertion-free tests to increase coverage.
- Every meaningful behavior includes positive, negative, boundary, and error
  cases as applicable.
- Tests are deterministic, isolated, repeatable, and independent of execution
  order.
- Use controlled clocks and UTC for time logic. Do not use real sleeps.
- Create and clean up test data within the test boundary.
- Parameterize cases that differ only by input and expected output. Keep
  distinct behavior and setup in distinct tests.
- Mock external boundaries, not the behavior under test.

## 2. Required test layers

Apply every relevant layer to a change:

### Backend and worker

- Domain unit tests for access policy, state machines, time boundaries, and
  override precedence.
- Application tests for permissions, transactions, idempotency, audit
  creation, and compensation.
- PostgreSQL repository integration tests.
- S3, SQS, Cognito, and email adapter contract tests.
- API/OpenAPI contract and object-level authorization tests.
- Worker tests using benign, malformed, encrypted, oversized, complex, and
  malicious PDF samples.

Use JUnit 5 and modern Mockito. Prefer strict stubbing and scoped mocks. Restore
modified static/global state after every test. Verify Java coverage with
JaCoCo rather than estimating it.

### Web

- Component, hook, accessibility, and API-client tests.
- End-to-end administrator and student journeys.
- Direct-navigation, object-identifier tampering, CSRF, print, cache, and
  session-expiry tests.
- Supported-browser responsive tests.

### Mobile

- Component, navigation, lifecycle, and API-client tests.
- Secure-storage, refresh rotation, revocation, logout, and user-switch tests.
- Offline, interrupted-network, upgrade, and expired-session tests.
- Physical-device Android capture/recording checks.
- Physical-device iOS capture, mirroring, and app-switcher checks.
- Internal Android and TestFlight acceptance tests.

### Cross-cutting

- Threat-model and broken-object-authorization verification.
- Upload/parser abuse, secret, dependency, container, and static analysis.
- Accessibility verification against the approved target.
- Load, endurance, watermark CPU/memory, and worker-backlog tests.
- RDS/S3 restore, dead-letter replay, rollback, and forward-fix rehearsals.

## 3. Test suppression policy

Do not disable, quarantine, weaken, or exclude a test to bypass:

- a compilation or type error;
- a visibility, stubbing, fixture, or environment problem that can be fixed;
- flakiness;
- a product defect;
- a quality threshold.

A genuinely environment-only test may be skipped only with a documented
reason, owner, tracking issue, and expiry/review date. Release-critical
behavior must still have an executable test in the appropriate environment.

## 4. Mandatory thresholds

For each testable deployable:

- overall production-code coverage is at least 80%;
- new production-code coverage is at least 90%;
- meaningful decision branches and security denial paths are covered;
- duplicated code is at or below 3%;
- no new blocker or critical Sonar finding is permitted.

Coverage is a floor, not a substitute for behavior verification. Generated
OpenAPI clients, generated framework code, database migrations, declarative
configuration, and infrastructure definitions may be excluded only through a
reviewed and documented configuration. Do not exclude difficult business
logic, authorization, or error handling.

## 5. Pull-request quality evidence

CI must publish or link:

- unit, integration, contract, component, and end-to-end results;
- line and branch coverage reports;
- Sonar quality-gate results;
- formatting, linting, type-check, and build results;
- dependency, secret, static, and container scan results;
- migration validation when schemas change;
- accessibility, performance, security, device, or recovery evidence when
  applicable.

The pull request must state the commands run locally, tests added or changed,
verified coverage, known limitations, and any approved exception.

## 6. Review gate

At least one peer approval is required. Reviewers assess:

- requirements and acceptance traceability;
- correctness and backward compatibility;
- authentication, authorization, privacy, and abuse cases;
- concurrency, idempotency, transactions, retries, and data migration;
- accessibility and supported-client behavior;
- performance, resource bounds, and cost-sensitive hot paths;
- observability, supportability, recovery, and rollback;
- test quality rather than coverage alone.

A change cannot merge with an unresolved release-blocking correctness,
security, privacy, accessibility, migration, data-loss, or recovery finding.

## 7. Definition of Done

A feature is done only when:

- approved acceptance criteria are met and linked;
- API and UI behavior are documented;
- organization and object-level authorization are tested;
- happy, denial, expiry, failure, and retry behavior is covered;
- applicable quality gates pass;
- audit and observability behavior is included;
- accessibility is verified;
- migrations and rollback are rehearsed where applicable;
- operational and support impacts are documented;
- acceptance evidence is recorded in `project-progress-checklist.md`.
