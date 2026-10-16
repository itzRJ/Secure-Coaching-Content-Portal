# Development Standards

## 1. Scope

These standards apply to product code, tests, scripts, configuration,
infrastructure definitions, and technical documentation. They adapt the
selected portable guidance from the AIAssistants repository to this project's
Java 21, Spring Boot, Next.js, React Native/Expo, PostgreSQL, and AWS design.

The approved requirements, HLD, LLD, ADRs, and OpenAPI contracts take
precedence when they define a more specific rule.

## 2. General engineering rules

- Apply DRY, KISS, YAGNI, SOLID, and separation of concerns pragmatically.
- Use descriptive names and focused modules, classes, functions, and files.
- Keep comments minimal. Explain non-obvious intent, constraints, protocols,
  or trade-offs; do not narrate code or preserve change history in comments.
- Remove dead and commented-out code.
- Validate all data at trust boundaries. Client validation is for usability;
  server validation is authoritative.
- Prefer explicit, typed contracts over maps, unbounded JSON, or stringly
  typed behavior.
- Use UTC instants for persistence and domain calculations. Convert to the
  approved institute IANA timezone only at presentation boundaries.
- Keep dependencies pinned through canonical manifests and lockfiles. Add a
  dependency only when the standard library or existing dependencies do not
  meet the need safely.

## 3. Repository and architecture boundaries

- Follow the monorepo and package-by-feature layout in `LLD.md`.
- Keep clients presentation-focused. Authentication validation, business
  authorization, access decisions, and storage access remain in the backend.
- Controllers do not access repositories directly.
- Persistence entities are not API response models.
- Cross-module backend calls use application interfaces; do not reach into
  another module's persistence implementation.
- Domain policies do not depend on HTTP, S3, queues, or framework classes.
- All organization-owned records and resource checks preserve the
  organization boundary even while only one institute is deployed.
- OpenAPI is the canonical REST contract. Generated clients are not hand
  edited.
- Database migrations are immutable after release and use
  expand/migrate/contract for destructive evolution.

## 4. Java and Spring

- Use Java 21 and the approved Spring Boot 4.1 patch.
- Use UTF-8 and LF line endings. Apply the project formatter.
- Use explicit imports; wildcard and unused imports are prohibited.
- Use standard Java naming: PascalCase types, camelCase methods and variables,
  UPPER_SNAKE_CASE constants, and lowercase packages.
- Prefer constructor injection and immutable dependencies.
- Keep transaction boundaries in application services. Avoid remote calls
  while holding database transactions unless explicitly designed.
- Use try-with-resources for closeable resources.
- Use bounded executors, queues, retries, caches, and telemetry payloads.
- Clean thread-local or request-scoped context in `finally`.
- Do not catch `NullPointerException` as control flow or swallow exceptions.
- Map failures once at the appropriate boundary. Do not both log and rethrow
  the same failure at every layer.
- Use structured logs with correlation ID, safe internal identifiers, outcome,
  and duration. Never log secrets, tokens, document content, or unnecessary
  personal data.
- Use parameterized queries or safe repository APIs. Validate filesystem paths
  against an allowed base. Never build shell commands from untrusted input.
- Write concise Javadoc for public contracts when the signature and type
  system do not fully express behavior, failure, or security constraints.

## 5. REST and API behavior

- Use `/api/v1`, camelCase JSON, UTF-8, and ISO-8601 UTC timestamps as defined
  by `LLD.md`.
- Return appropriate HTTP status codes and the standard safe error envelope.
- Do not expose stack traces, internal exception text, storage keys, signed
  URLs, authorization internals, or another user's resource existence.
- Apply authentication, permission, organization, and object-level checks to
  every endpoint.
- Support idempotency for mutations that retries could duplicate.
- Use cursor pagination for growing collections.
- Add optional response fields compatibly. Breaking changes require a new API
  version or a reviewed migration-compatible rollout.
- Update OpenAPI, generated clients, contract tests, and examples together.

## 6. TypeScript, Next.js, and React Native

- Enable TypeScript strict mode. Avoid `any`; any unavoidable use requires a
  narrow boundary and justification.
- Run ESLint, Prettier, and type checking before merge.
- Use `const` by default, strict equality, explicit conversions, and ES
  modules.
- Validate external API and deep-link payloads before use.
- Handle promise failures at the boundary that can add context or recover.
  Do not add empty catches or catches that merely hide failures.
- Run independent asynchronous work concurrently only when ordering and load
  limits permit it.
- Keep React components and hooks pure during render. Side effects belong in
  event handlers or correctly scoped effects.
- Follow the Rules of Hooks. Treat props, state, hook inputs, and cached query
  data as immutable.
- Prefer function components and typed props. Do not add PropTypes alongside
  TypeScript.
- Clean up timers, subscriptions, listeners, and in-flight work.
- Keep secrets and privileged decisions out of browser and mobile bundles.
- Do not render unsanitized HTML. Apply an approved Content Security Policy on
  the web.
- Preserve keyboard, screen-reader, focus, contrast, reduced-motion, and touch
  accessibility appropriate to the platform.
- Do not persist protected page imagery to user-accessible storage.
- Keep mobile refresh credentials in Keychain/Keystore and access tokens in
  memory as defined by `LLD.md`.

## 7. Shell and automation

- Use Bash only for small wrappers and command orchestration. Use a structured
  language when control flow or data processing becomes substantial.
- Start executable scripts with `#!/usr/bin/env bash` and
  `set -euo pipefail`.
- Quote expansions, use arrays for argument lists, and never use `eval`.
- Validate inputs and required tools before performing work.
- Send diagnostics to stderr and return meaningful non-zero exit codes.
- Provide `--help` and `--dry-run` for user-facing or destructive utilities
  where applicable.
- New and materially changed scripts must pass ShellCheck without unexplained
  warnings.

## 8. Documentation

- Use Markdown and Mermaid where diagrams materially improve understanding.
- Write to teach: one idea per sentence, point first, details second, and
  acronyms expanded on first use.
- State each decision once and cross-reference it elsewhere.
- HLDs describe system shape, decisions, boundaries, and risks without
  source-level detail.
- LLDs own modules, schemas, APIs, algorithms, failure behavior, and
  verification detail.
- Update documentation and runbooks in the same pull request as the behavior
  they describe.
