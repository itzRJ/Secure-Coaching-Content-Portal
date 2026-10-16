# Agent Instructions — Secure Coaching Content Portal

## Purpose and authority

These instructions apply to every human or AI-assisted change in this
repository. Read the following documents before planning or changing the
system:

1. `implementation-plan-nishant-tution.md` — product requirements.
2. `HLD.md` — proposed architecture and system boundaries.
3. `LLD.md` — proposed detailed design and contracts.
4. `project-progress-checklist.md` — current gate, approvals, risks, and
   evidence.
5. `docs/engineering/` — development, testing, review, and delivery rules.

When documents disagree, stop and report the conflict. Requirements and
recorded decisions outrank design assumptions. Implemented behavior outranks
stale commentary, but drift must be reported and corrected through review.

## Hard delivery gates

- Do not implement product code, infrastructure, prototypes, or benchmarks
  until the current project gate and the user explicitly authorize that work.
- Requirements approval precedes architecture approval. Approved HLD and LLD
  precede implementation planning. An approved task plan precedes coding.
- Do not silently treat a recommendation, proposed value, or unchecked
  checklist item as approved.
- Work only on the approved task. Ask before destructive operations, material
  scope changes, public-contract changes, or security-policy changes.
- Never bypass a failing quality gate by weakening, excluding, or disabling
  the check without documented approval.

## Evidence-first behavior

- Inspect relevant source, configuration, migrations, tests, and documentation
  before making behavioral claims.
- Separate confirmed facts, reasonable inferences, and unresolved assumptions.
- Cite repository paths and exact evidence in plans, reviews, and handoffs.
- Reproduce failures and identify the root cause before proposing a fix.
- If required evidence is unavailable, say what could not be verified.

## Change discipline

- Prefer the smallest coherent change that satisfies approved acceptance
  criteria.
- Search for an existing implementation before adding a helper, abstraction,
  API, schema type, or dependency.
- Avoid speculative refactors and unrelated cleanup.
- Preserve backward compatibility unless a reviewed change explicitly permits
  a break and defines migration and rollback.
- Update tests, API contracts, documentation, observability, and runbooks in
  the same change when behavior changes.
- Do not hand-edit generated OpenAPI clients, build output, coverage output, or
  generated infrastructure artifacts. Change the canonical source and
  regenerate them.

## Security and privacy

- Treat browsers, mobile devices, uploaded PDFs, identifiers, and request data
  as untrusted.
- Enforce authentication, organization ownership, permission, and
  object-relationship checks in the backend.
- Never commit or expose passwords, tokens, session identifiers, private keys,
  signed URLs, protected document bytes, or production data.
- Do not log authentication secrets, protected content, raw sensitive
  payloads, or unnecessary personally identifiable information.
- Use parameterized persistence, validated paths and commands, least
  privilege, secure secret storage, and safe failure responses.
- Do not claim that screenshots or copying can be completely prevented.

## Task handoff and completion

Every implementation task must identify:

- linked requirement and acceptance criteria;
- approved scope and dependencies;
- affected components and contracts;
- authorization, privacy, migration, accessibility, observability, and
  rollback impact;
- required tests and quality evidence.

A task is complete only when applicable formatting, linting, type checking,
tests, builds, security scans, coverage, documentation, and review gates pass.
Report commands run, results, known limitations, and remaining risks.

## Mandatory quality baseline

- At least 80% overall test coverage and 90% coverage on new production code
  for each testable deployable.
- No new blocker or critical Sonar findings.
- Code duplication at or below 3%.
- At least one peer approval before merge.
- No unresolved release-blocking security, correctness, privacy,
  accessibility, migration, or recovery finding.

Generated code and declarative/configuration files may be excluded from
coverage only through a reviewed, documented exclusion.

## Detailed standards

- `docs/engineering/development-standards.md`
- `docs/engineering/testing-quality-gates.md`
- `docs/engineering/github-cicd.md`

Scoped Cursor rules under `.cursor/rules/` summarize these standards for the
relevant files. The engineering documents remain the canonical source.
