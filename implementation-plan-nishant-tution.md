# Customer Requirements — Secure Coaching Content Portal

## 1. Document purpose

This document records the agreed customer requirements for the secure coaching content portal. It describes what the product must do and the constraints it must respect. Technical implementation details are maintained separately in `HLD.md` and `LLD.md`.

The requirements below preserve the original requested capabilities. Delivery phases identify sequencing only; they do not remove a requirement.

## 2. Product objective

Provide a branded web and mobile platform through which a coaching institute can assign educational PDF content to named students for a controlled period. Students must be able to view assigned content without an ordinary download facility. Every view must be attributable to the signed-in student through visible watermarking and audit records.

## 3. Confirmed product scope

- Initial deployment serves one coaching institute.
- Supported users in the first release are administrators and students.
- The authorization design must allow additional roles in future without redesigning the core model.
- Administrators use the web application.
- Students use either the responsive web application or the Android/iOS mobile application.
- The initial target is up to 1,000 students and approximately 100 concurrent viewers.
- The portal must be branded for the coaching institute.
- The system must use AWS-hosted infrastructure.

## 4. User roles

### 4.1 Administrator

An administrator must be able to:

- Sign in securely with mandatory multi-factor authentication.
- Create, edit, activate, and deactivate student accounts.
- Import students in bulk using a validated CSV file.
- Create and manage batches.
- Add and remove students from batches.
- Create and manage subjects or categories.
- Upload PDF papers and monitor processing status.
- Assign a paper to a batch.
- Set when assigned content becomes available and when access expires.
- Grant, extend, revoke, or restore access for an individual student.
- Configure the watermark fields permitted by the product.
- Review basic paper-access and viewing audit records.
- Configure supported institute branding.

### 4.2 Student

A student must be able to:

- Sign in using an administrator-created account.
- Set or reset a password through a secure email flow.
- View assigned papers grouped as upcoming, active, or expired.
- Open active papers in the protected viewer.
- See clear reasons when content is not yet available, expired, or revoked.
- View basic profile and active-session information.
- Sign out from the current session and revoke other sessions where supported.
- Use the same core student journey on web, Android, and iOS.

## 5. Functional requirements

### CR-01 Named-user access

- Every student must have an individual identity and account.
- Shared anonymous access links are not permitted.
- Every content request must be authorized for the current student.
- Administrators must be able to deactivate and reactivate accounts.
- The system must record successful and failed authentication events.
- Administrator accounts must use multi-factor authentication.

### CR-02 Controlled document viewing

- Students must view papers inside the supplied web or mobile viewer.
- The product must not expose an ordinary PDF download, print, share, or save-as action.
- Original PDFs must remain in private storage and must not be delivered directly to students.
- Student clients must receive server-produced page imagery rather than the original PDF.
- Access must be checked for every protected content request.
- The product must not claim that any browser or mobile technology can make copying impossible.

### CR-03 Dynamic forensic watermark

- Every viewed page must contain a visible, student-specific watermark.
- The watermark must support student name, email, internal student identifier, and a session- or view-specific marker.
- The watermark must be repeated and positioned so that simple cropping does not remove all identifying information.
- It must remain readable in a typical screenshot while allowing the paper to be read.
- The watermark must be applied by trusted server-side processing before protected imagery reaches the client.
- Watermark configuration changes must be controlled by an administrator and audited.

### CR-04 Expiring access

- An administrator must be able to configure `available from` and `expires at` times for each assignment.
- A per-student override may extend, revoke, or restore access without changing the full batch.
- Expiry and revocation must be enforced at request time, not only by a scheduled job.
- Date and time displays must use the institute’s configured timezone while storing canonical timestamps.
- A student must receive a clear status without receiving sensitive administrative details.

### CR-05 Screenshot and copying deterrence

- Visible forensic watermarking is the primary screenshot deterrent.
- Web printing must produce no protected content.
- The web viewer may suppress obvious save, print, selection, and context-menu actions as usability deterrents.
- Android must use secure-window controls to deter screenshots and screen recording where the operating system supports them.
- iOS must detect capture or mirroring where supported and obscure or warn as designed.
- The customer must be informed that screenshots, rooted or jailbroken devices, and external cameras cannot be completely prevented.
- DevTools detection and keyboard blocking must not be treated as security controls.

### CR-06 Coaching-specific paper assignment

- Papers must be organized by subject or category.
- Administrators must be able to assign a paper to an entire batch.
- Students added to a batch must receive access according to the documented assignment-membership rule.
- Individual access overrides must be supported.
- Future release dates must be supported.
- Assignment changes must be auditable.

### CR-07 Branded portal

- The login and student experiences must display the institute name and logo.
- Supported primary and secondary colors, favicon, and basic footer text must be configurable.
- Branding must apply consistently to the web application.
- Mobile applications must use the institute’s approved app name, icons, splash treatment, and theme.
- No third-party “Powered by” label is required in the student experience.

### CR-08 Paper management

- Administrators must be able to upload PDF files subject to configured size and page limits.
- Uploads must be validated as genuine, supported PDFs and malware-scanned.
- The system must show processing states such as uploaded, scanning, converting, ready, and failed.
- A file integrity hash must be recorded.
- Failed processing must not expose partial or unprotected output.
- Deletion and retention must follow the approved retention policy and preserve required audit evidence.

### CR-09 Student dashboard

- Students must see only papers assigned to them.
- Papers must be separated into upcoming, active, and expired states.
- Subject, title, availability, and expiry information must be shown.
- The dashboard must work on supported web and mobile devices.

### CR-10 Audit and basic reporting

- The system must record administrator changes to users, batches, papers, assignments, access overrides, branding, and security settings.
- Protected viewing must record student, paper, assignment, session/view identifier, timestamp, client type, and relevant request metadata.
- Audit records must be append-only from normal application workflows.
- Administrators must be able to search or filter basic access records.
- Sensitive values, passwords, authentication secrets, and full tokens must never appear in logs.

### CR-11 Web application

- The web application must provide the complete administrator experience.
- It must also provide the complete student MVP experience.
- It must be responsive and support current approved desktop and mobile browsers.
- Authentication and protected application traffic must use HTTPS.

### CR-12 Mobile applications

- One React Native application must target Android and iOS.
- The mobile MVP is student-only.
- It must provide sign-in, assigned-paper dashboard, upcoming/active/expired states, protected viewing, profile, and session/logout controls.
- The application must not offer offline paper downloads.
- Authentication secrets must use operating-system secure storage.
- Protected page imagery must not be intentionally persisted to user-accessible storage.
- The application must handle interrupted networks, expired sessions, revoked access, processing failures, and application upgrades safely.
- Release candidates must be tested on real Android and iOS devices before store submission.

### CR-13 Account recovery and sessions

- Students must have a secure email-based password reset process.
- Reset and invitation links must be single-use and expire.
- Administrators must be able to revoke student sessions.
- Password changes and account deactivation must revoke applicable sessions.
- Mobile refresh credentials must be rotating and revocable.
- Web sessions must use secure, HttpOnly cookies and appropriate cross-site request protections.

### CR-14 Notifications

- Assignment alerts and expiry reminders remain required product capabilities.
- They are planned after the core MVP unless promoted through change control.
- Email is the initial notification channel.

### CR-15 Analytics and export

- Administrative analytics, CSV export, and enhanced paper statistics remain required product capabilities.
- They are planned after the core MVP unless promoted through change control.

## 6. Core business rules

### BR-01 Access decision

Access to a paper is allowed only when all conditions are true:

1. The user and organization context are valid and active.
2. The paper is ready for viewing.
3. A relevant assignment and effective student grant exist.
4. The assignment is active.
5. The current time is at or after `available from`.
6. The current time is before `expires at`.
7. No applicable student override or account state revokes access.

The backend is the authority for this decision. Web and mobile clients must not infer access from display state alone.

### BR-02 Batch membership

The final behavior for students joining or leaving a batch after an assignment is created must be selected and recorded before implementation. The recommended default is:

- Active batch membership grants access to active batch assignments.
- Removing membership removes access unless an explicit individual grant exists.
- Historical audit records remain unchanged.

### BR-03 Effective expiry

When both assignment and per-student expiry values exist, the explicit override governs only when it was created through an authorized override action. Every override must retain actor, reason, and timestamp.

### BR-04 Paper readiness

A paper is viewable only after validation, malware scanning, conversion, integrity recording, and publication have completed successfully.

### BR-05 Audit time

All persisted timestamps use UTC. User interfaces render them using the configured institute timezone.

## 7. Security and privacy requirements

- Apply least privilege to users, services, storage, queues, and database access.
- Enforce object-level authorization for every user, batch, assignment, paper, and tile request.
- Encrypt traffic in transit and managed data at rest.
- Keep original PDFs and unwatermarked derivatives private.
- Do not place durable credentials or protected object identifiers in public URLs.
- Rate-limit authentication, reset, upload, and protected viewing endpoints.
- Validate uploaded type, structure, size, and page count.
- Protect against common web and API risks, including injection, broken access control, CSRF, credential stuffing, unsafe file processing, and insecure direct object references.
- Maintain auditable secret rotation, backup, restore, incident response, and account recovery procedures.
- Establish approved retention periods for originals, derivatives, audit logs, and inactive user data before production.
- Complete a threat model and security test before production approval.

## 8. Non-functional requirements

### Performance and scale

- Support up to 1,000 registered students and approximately 100 concurrent viewers in the initial architecture.
- Define measurable latency targets during architecture validation.
- Page viewing must progressively load rather than wait for the entire paper.
- Conversion work must be asynchronous and must not block upload requests.

### Availability and recovery

- Production availability, recovery-point objective, and recovery-time objective must be approved before deployment.
- Database backups and restoration must be tested.
- Failed document jobs must be retryable and observable without producing duplicate publication.

### Accessibility and usability

- Web and mobile interfaces must define and test an agreed WCAG target.
- Viewer controls, status messages, authentication, and navigation must support assistive technologies as far as protected content permits.
- Empty, loading, offline, retry, forbidden, expired, and processing states must be explicitly designed.

### Compatibility

- A supported browser matrix and mobile OS/device matrix must be approved before implementation completion.
- The mobile app must define a minimum supported Android and iOS version.

### Observability

- Production must provide structured application logs, metrics, traces or correlation identifiers, job visibility, and actionable alerts.
- Web and mobile failures must be diagnosable without collecting protected document content or authentication secrets.

## 9. Delivery scope

### Core MVP

- Administrator and student authentication.
- Mandatory administrator MFA.
- User, batch, membership, and subject management.
- PDF upload, validation, scanning, conversion, and processing status.
- Batch assignment, availability, expiry, and individual override.
- Server-rendered watermarked protected viewer.
- Responsive student web dashboard and viewer.
- Android and iOS student application.
- Basic institute branding.
- Basic access and administrative audit records.
- Production deployment, monitoring, backups, and operating runbooks.

### Post-MVP requirements

- Email assignment alerts and expiry reminders.
- Advanced administrative analytics.
- CSV exports.
- Full branding editor.
- Additional staff roles such as instructor.
- Custom domains.
- Multi-tenant SaaS operation.
- Optional higher-scale infrastructure optimizations.

Moving an item between these groups requires documented change control; it does not silently remove the requirement.

## 10. Explicit exclusions for the core MVP

- Student uploads or submissions.
- Payments, subscriptions, and commerce.
- Live classes, chat, examinations, or grading.
- Offline access to protected papers.
- Administrator features in the mobile app.
- Guaranteed screenshot prevention.
- Multi-organization self-service onboarding.

## 11. Acceptance summary

The core MVP is acceptable when:

- An administrator can securely create students and batches, upload a valid paper, and assign it with a controlled availability window.
- An assigned student can sign in on web, Android, and iOS and view the paper only during authorized access.
- The original PDF is not delivered to the student client.
- Every delivered page is visibly watermarked for the current student and view.
- Revocation and expiry are enforced on subsequent protected requests.
- Unauthorized users cannot access paper metadata or imagery by changing identifiers.
- Required administrative and viewing events are auditable.
- The approved security, performance, accessibility, recovery, browser, and device tests pass.

## 12. Open items requiring sign-off

These details refine acceptance criteria without changing the requirements:

- Maximum PDF size, page count, and supported PDF features.
- Institute timezone.
- Password policy and student session durations.
- Watermark text, opacity range, density, and placement.
- Batch membership behavior confirmation.
- Data and audit retention periods.
- Supported browsers, Android versions, iOS versions, and test devices.
- Accessibility target.
- Availability, RPO, and RTO targets.
- Email provider and sender domain.
- Store developer-account ownership, privacy policy, and support contact.
- Branding assets and final application names.

## 13. Related documents

- `HLD.md` — approved high-level architecture and system boundaries.
- `LLD.md` — detailed components, data model, APIs, workflows, and security behavior.
- `project-progress-checklist.md` — delivery gates, status, evidence, dependencies, risks, and decisions.
