# YouTube-Style Video Platform — QA Prompt — Volume 1

## Cross-Platform Functional Testing, API and Data Integrity, Media Playback, Security, Accessibility, and Performance

### 1. Mission and Implementation Scope

Implement the comprehensive **quality-assurance and automated-testing foundation** for the YouTube-style video platform.

The platform includes web and mobile applications, NestJS backend services, PostgreSQL, Redis, Kafka-compatible event streaming, BullMQ workers, OpenSearch, object storage, a video-processing pipeline, HLS/DASH delivery, realtime communication, creator workflows, monetization, recommendations, and moderation capabilities.

The global platform target is approximately 250 million registered users and 50 million daily active users. This milestone must establish repeatable, meaningful test coverage of the implemented application and its cross-component contracts while creating a reliable foundation for later scale, resilience, and release-certification testing.

This assignment covers:

- Backend, API, and data-integrity testing.
- Web and mobile functional testing.
- Cross-component contract and integration testing.
- Video playback and media-delivery testing.
- Database, event, queue, search, and recommendation testing.
- Authentication, authorization, security, and privacy testing.
- Accessibility and usability validation.
- Browser, device, codec, resolution, and bitrate compatibility matrices.
- Performance testing for individual workflows and critical application paths.
- Test infrastructure, reusable fixtures, reporting, and CI integration.

The objective is to implement real tests that validate actual system behavior—not merely produce a testing strategy, increase coverage percentages, or create passing tests that avoid meaningful assertions.

This prompt is independently executable in a fresh coding-agent conversation. Inspect the repository and test infrastructure actually available, reuse compatible frameworks, and define explicit contracts for missing dependencies. Do not assume other coding-agent conversations share files or execution state.

### 2. Technology and Testing Constraints

Use the established project technology direction:

- **Web:** Next.js, React, TypeScript, Tailwind, shadcn/ui, TanStack Query, and Zustand.
- **Mobile:** React Native, Expo, and TypeScript.
- **Backend:** Node.js, NestJS, and TypeScript.
- **Database:** PostgreSQL and Prisma.
- **Cache and distributed state:** Redis.
- **Events:** Kafka-compatible streaming.
- **Background jobs:** BullMQ.
- **Search:** OpenSearch/Elasticsearch-compatible infrastructure.
- **Media:** Object storage, CDN, FFmpeg, HLS, and DASH.
- **Realtime:** WebSockets or Socket.IO where established.
- **Infrastructure:** AWS, Docker, Kubernetes, Helm, and Terraform.
- **Observability:** OpenTelemetry, Prometheus, and Grafana.

Inspect the actual repository to identify the installed test runners, assertion libraries, API-test tools, browser automation frameworks, mobile testing libraries, infrastructure-test tools, and CI workflow definitions.

Prefer existing supported tooling. Introduce new dependencies only where they provide necessary coverage that cannot reasonably be achieved through the existing stack.

Examples of appropriate tooling categories include unit-test frameworks, Playwright-style browser automation, React Native component testing, API contract validators, schema validators, database integration tests, and controlled load-test tools. Select actual dependencies according to the repository rather than installing every possible framework.

### 3. Required Deliverables

Implement the following QA foundation:

1. A test architecture organized by application layer and responsibility.
2. Unit tests for important domain logic and state transitions.
3. Backend API and authorization tests.
4. Database and migration-integrity tests.
5. Event, queue, and asynchronous-processing tests.
6. Search and recommendation contract tests.
7. Web component, integration, and browser end-to-end tests.
8. Mobile component, navigation, and platform-behavior tests.
9. Video-player and media-delivery compatibility tests.
10. Cross-component contract and integration tests.
11. Security, privacy, and abuse-resistance tests.
12. Accessibility validation.
13. Performance-test scenarios and measurable acceptance criteria.
14. Browser, device, operating-system, resolution, bitrate, and network-condition test matrices.
15. CI test execution, reporting, and failure diagnostics.
16. Test-data management, environment isolation, and reusable fixtures.
17. Documentation and a factual completion report.

Implement meaningful coverage within these boundaries. Do not turn this milestone into an unbounded enterprise release-certification exercise; comprehensive high-concurrency, disaster-recovery, rights/moderation certification, and broader release-readiness exercises remain separate testing responsibilities.

### 4. Repository Inspection and Test Baseline

Before making changes, inspect:

- Existing application packages and module structure.
- Current automated tests and their execution commands.
- Existing unit, integration, browser, and mobile test frameworks.
- Backend API schemas and authentication boundaries.
- Database models and migrations.
- Event names, payload schemas, and queue definitions.
- Video upload, processing, and playback contracts.
- Search and recommendation interfaces.
- Frontend routes and component architecture.
- Mobile navigation and native dependencies.
- Infrastructure and CI configurations.
- Existing fixtures, factories, seeds, and test environments.
- Test reports and known failures that are discoverable in the environment.

Establish a factual baseline by running the relevant existing checks where feasible.

Classify existing failures separately from new failures. Do not silently rewrite existing tests to hide genuine product regressions or change production behavior merely to make tests pass.

Preserve compatible test infrastructure and avoid duplicating existing test suites without a concrete coverage gap.

### 5. Test Architecture and Test Boundaries

Organize tests by responsibility and execution cost.

Use the following conceptual layers, adapting their directory names to the existing repository:

- Unit tests for isolated logic.
- Component tests for web and mobile UI behavior.
- Integration tests for real module and service interactions.
- API and schema-contract tests.
- Database integration and migration tests.
- Event and queue tests.
- Browser and mobile end-to-end tests.
- Media compatibility tests.
- Security and privacy tests.
- Accessibility tests.
- Performance and workload tests.

Keep fast feedback tests separate from expensive integration or environment-dependent tests.

Define consistent commands for running tests at different scopes, such as:

- Unit tests.
- Backend and database integration tests.
- Web tests.
- Mobile tests.
- Contract tests.
- Security checks.
- Accessibility checks.
- Media compatibility checks.
- Performance tests.

Ensure CI can execute the appropriate subset without requiring production credentials or unrestricted production infrastructure.

Use explicit environmental prerequisites when an integration test requires external services, native tooling, media fixtures, or controlled infrastructure.

Do not treat a test skipped because of a missing dependency as a passing verification.

### 6. Test-Data and Fixture Management

Create a deterministic, maintainable approach to test data.

Provide appropriately typed factories, fixtures, builders, and seed helpers for relevant entities, such as:

- Users and account states.
- Authentication sessions and permissions.
- Channels and subscriptions.
- Videos and video lifecycle states.
- Upload sessions and media-processing jobs.
- Playlists and viewing history.
- Likes, comments, replies, and reports.
- Notifications and preferences.
- Search results and recommendation responses.
- Live streams and chat events.
- Creator analytics.
- Premium entitlements and memberships.
- Moderation and access-restriction states.

Only create fixtures for domains that are actually present or explicitly covered by this testing milestone.

Requirements:

- Make fixture generation deterministic where practical.
- Use stable identifiers and controlled timestamps.
- Avoid cross-test state leakage.
- Provide cleanup for created resources.
- Avoid reliance on the order in which tests execute.
- Avoid shared mutable singleton fixtures when isolation is required.
- Do not use production personal data.
- Separate synthetic media fixtures from actual user-owned media.
- Keep fixtures small enough for ordinary CI runs.
- Use representative large files only in explicitly designated media or performance suites.

Do not fabricate test-only application endpoints or persistence mechanisms that bypass the real domain logic.

### 7. Backend Unit and Domain Tests

Add unit tests for important business logic and state transitions in the implemented backend.

Cover relevant existing behavior across:

- Identity and session handling.
- Authorization and ownership checks.
- Channel and subscription rules.
- Video metadata validation.
- Upload lifecycle and publication transitions.
- Playback-access decisions.
- Playlist and viewing-history behavior.
- Likes, comments, replies, and reactions.
- Notifications and user preferences.
- Search request validation.
- Recommendation response handling.
- Creator analytics domain rules.
- Moderation and reporting rules.
- Membership and entitlement decisions.
- Live-stream lifecycle where implemented.

Do not assume all these areas exist as completed modules. Discover the actual implementation and test supported functionality.

Tests must exercise meaningful rules, including invalid inputs, boundary conditions, state transitions, and relevant failures.

Avoid tests that simply instantiate a service or assert that a method returns an unrestricted mocked response.

For asynchronous processing, test retryable and terminal failures, idempotency, and state transitions wherever the domain logic supports those behaviors.

### 8. API and Authorization Testing

Implement API tests for the actual backend endpoints and contract definitions present in the repository.

Cover the relevant combinations of:

- Successful request.
- Invalid payload.
- Missing or malformed authentication.
- Expired session.
- Insufficient authorization.
- Resource ownership mismatch.
- Missing resource.
- Deleted or unavailable content.
- Rate-limited request.
- Duplicate mutation.
- Conflicting state transition.
- Pagination boundaries.
- Malformed query parameters.
- Service dependency failure.
- Internal error handling.

Validate:

- HTTP methods and status codes.
- Request and response schemas.
- Required and optional fields.
- Identifier formats.
- Timestamp formats.
- Error response structure.
- Pagination behavior.
- Authentication requirements.
- Authorization rules.
- Idempotency behavior for applicable operations.

Ensure that private or restricted videos, creator operations, moderation endpoints, account settings, and other protected resources are not accessible merely by changing an identifier in a request.

Test that rejected unauthorized operations do not cause unintended data mutation.

Do not invent routes that are absent from the actual backend. When a required API contract is unavailable, document the testable contract dependency and avoid claiming that the corresponding endpoint has been validated.

### 9. Database and Migration Testing

Test the actual PostgreSQL and Prisma data layer where feasible.

Implement coverage for:

- Migration application to a clean database.
- Migration application to representative existing schema states where supported.
- Schema constraints and relationships.
- Unique and foreign-key constraints.
- Transaction behavior.
- Rollback behavior where applicable.
- Concurrent conflicting updates.
- Referential integrity.
- Soft deletion and hard deletion behavior where defined.
- Data retention and deletion rules.
- Query results and pagination consistency.
- Important index-dependent query paths.
- Safe migration ordering.

Test data access behavior rather than merely checking that a Prisma client can be instantiated.

Where concurrency matters, use controlled concurrent operations to verify uniqueness, idempotency, ownership, and state-transition invariants.

Do not use a lightweight substitute for PostgreSQL when the behavior under test depends on PostgreSQL-specific semantics.

Avoid running destructive migration or deletion tests against shared development or production databases.

### 10. Event Streaming and Queue Testing

Implement meaningful tests for the event and background-job systems that exist in the repository.

For Kafka-compatible event processing and other asynchronous events, validate applicable properties such as:

- Payload-schema compatibility.
- Required fields and identifiers.
- Event version handling.
- Producer serialization.
- Consumer deserialization.
- Idempotent processing.
- Duplicate delivery behavior.
- Retry semantics.
- Ordering assumptions where guaranteed.
- Invalid payload handling.
- Terminal failure or dead-letter behavior where configured.
- Consumer restart and recovery.
- Trace or correlation-context propagation where implemented.

For BullMQ and Redis-backed jobs, test:

- Job creation and payload validation.
- Retry and backoff behavior.
- Job deduplication where supported.
- Graceful worker interruption.
- Failed-job handling.
- Concurrency constraints.
- Queue state transitions.
- Prevention of duplicate external side effects where idempotency is required.

Use real or controlled test instances of the underlying technology when correctness depends on its semantics. Mocks are appropriate for isolated unit tests, but must not be the only evidence for queue delivery, event processing, or retry guarantees.

Do not claim exactly-once delivery unless the actual system provides and validates that guarantee. Test the real supported delivery model.

### 11. Search and Recommendation Testing

Test the existing search and recommendation interfaces.

For search, validate relevant behaviors such as:

- Query normalization and validation.
- Pagination and continuation.
- Result-schema consistency.
- Empty results.
- Invalid filters.
- Search-service unavailability.
- Access restrictions on indexed content.
- Deleted or newly restricted content.
- Indexing delays and stale results where relevant.

For recommendations, test:

- Request and response contracts.
- User or session context handling where supported.
- Stable response schemas.
- Candidate filtering and access restrictions.
- Empty or degraded results.
- Dependency failures.
- Timeouts and fallback behavior.
- Exclusion or restriction signals exposed by the actual contract.

Do not invent expected ranking scores or insist that an unspecified ranking algorithm return a particular ordering.

For deterministic algorithm tests, use rules actually defined by the implementation. For model- or ranking-dependent behavior, validate supported invariants, schema correctness, and safety constraints rather than asserting unstable exact rankings.

Ensure recommendation or search responses cannot reintroduce content that violates authoritative access restrictions.

### 12. Web Frontend Testing

Test the existing Next.js and React implementation using the established component and browser-testing frameworks.

Cover the actual implemented user journeys, including applicable flows such as:

- Authentication and account navigation.
- Home and discovery.
- Search.
- Video playback.
- Comments and engagement.
- Channel and subscription pages.
- Playlists and viewing history.
- Creator upload and video management.
- Notifications and settings.
- Live-stream viewing and chat.
- Premium offerings and membership experiences.
- Short-form browsing.
- Moderation or administration interfaces.

Do not assume every capability exists or is within the current functional scope. Discover implemented routes and distinguish present coverage from unavailable functionality.

Component tests should validate observable behavior, accessibility attributes, form validation, error handling, loading states, and important user actions.

Browser end-to-end tests should verify actual navigation and integration across the application's major implemented journeys.

Test:

- Deep links and direct navigation.
- Session restoration.
- Authorization-aware page access.
- Form errors.
- Pagination.
- Empty states.
- API failures.
- Network interruption.
- Browser refresh.
- Expired sessions.
- Cross-page state consistency.
- Critical responsive layouts.

Avoid tests that depend exclusively on internal component implementation details or arbitrary time delays.

Use deterministic test selectors and wait for meaningful application state instead of relying on fragile sleeps.

### 13. Mobile Application Testing

Test the React Native and Expo application through the available unit, component, simulator, and device workflows.

Cover relevant implemented mobile journeys across:

- Authentication and session restoration.
- Home, search, discovery, and subscription feeds.
- Video playback and player lifecycle.
- Comments and engagement.
- Channels, playlists, and viewer library.
- Notifications and account settings.
- Creator uploads and publishing.
- Live streams and chat.
- Purchases and entitlements.
- Short-form video playback.
- Offline downloads where implemented.

Validate platform-specific behavior where applicable:

- iOS and Android navigation.
- Back handling and navigation-state restoration.
- Keyboard and safe-area behavior.
- App foreground and background transitions.
- Network disconnection and restoration.
- Permission denial and recovery.
- Deep-link handling.
- Native player and camera resource release.
- Secure account-state isolation.
- Supported operating-system variations.

Use React Native component tests for deterministic UI behavior. Use simulators, emulators, or physical devices for native capabilities that cannot be reliably validated with JavaScript-only tests.

Do not claim a native behavior has been verified on a device when only a mocked component test was executed.

### 14. Video Playback and Media Compatibility Testing

Implement a structured media-compatibility test suite covering the platform's actual ingest, transcoding, packaging, CDN, and playback contracts.

The suite must exercise real test media and supported playback paths where test infrastructure permits.

#### 14.1 Test media corpus

Maintain a small, versioned corpus of synthetic or properly licensed media fixtures.

Where relevant, include representative combinations of:

- Supported video codecs.
- Supported audio codecs.
- Different resolutions.
- Different frame rates.
- Portrait and landscape orientation.
- Different bitrates.
- Different durations.
- Different audio configurations.
- Supported captions and subtitle formats.
- Valid and intentionally invalid media.

Include HLS and DASH fixtures only when those delivery formats are supported by the platform implementation.

Do not add unnecessarily large media assets to ordinary unit-test suites. Store larger fixtures in an approved test-artifact location or generate them reproducibly through controlled scripts.

Do not include copyrighted or private production video assets without permission.

#### 14.2 Media-processing and playback checks

Test applicable behavior for:

- Source-media validation.
- Media-probe metadata.
- Transcoding outputs.
- Adaptive-bitrate variants.
- HLS/DASH manifest validity.
- Segment availability.
- Thumbnail generation.
- Audio and video synchronization.
- Caption availability.
- Range requests where supported.
- Playback-source authorization.
- Media delivery errors.
- Incomplete or malformed output rejection.

Inspect real generated manifests and media outputs when practical. A successful HTTP status alone is not evidence that the delivered media can actually be played.

Where full media processing is too expensive for ordinary CI, create separate controlled integration jobs and document their execution requirements.

### 15. Bitrate, Resolution, Browser, and Device Matrices

Define a concrete compatibility matrix based on the media profiles and platforms the application actually supports.

Include relevant combinations of:

- Browser family and supported version.
- Desktop and mobile web where applicable.
- iOS and Android.
- Device or hardware capability classes.
- Supported operating-system versions.
- Video codec and profile.
- Resolution.
- Frame rate.
- Bitrate.
- HLS/DASH playback path.
- Audio configuration.
- Captions or subtitles where applicable.

Use a representative matrix for routine CI and a larger matrix for scheduled or release-oriented testing.

For example, use available low-, medium-, and high-resolution media profiles, plus a small number of realistic high-bitrate cases, rather than attempting every theoretical combination.

The matrix must reflect actual encoding ladders and supported player capabilities. Do not label an unsupported codec as supported merely because the test runner can download the file.

For each selected combination, test applicable outcomes such as:

- Successful source initialization.
- Playback start.
- Playback continuity.
- Audio availability.
- Adaptive-quality changes where observable.
- Failure and recovery.
- Unsupported-format handling.

Record device or browser details, test media identifiers, and the actual failure symptoms so a result can be reproduced.

### 16. Security and Privacy Testing

Implement automated security and privacy tests covering the actual application boundaries.

Test applicable risks including:

- Broken object-level authorization.
- Privilege escalation.
- Authentication bypass.
- Session misuse.
- Unauthorized access to private videos.
- Unauthorized creator actions.
- Cross-account data leakage.
- Input-validation bypass.
- Injection risks.
- Unsafe output rendering.
- Untrusted deep links.
- Insecure file-upload behavior.
- Media-access control failures.
- Sensitive values in application logs.
- Exposed credentials or configuration secrets.
- Insecure CORS or security-header configuration.
- Rate-limit bypass.
- Unsafe redirect behavior.
- Unintended personal-data retention.
- Account deletion and relevant data-removal behavior.

Use dependency scanners, secret scanners, and static application security testing when appropriate.

Run dynamic security tests only against explicitly authorized test environments.

Use adversarial inputs that validate actual security boundaries rather than merely confirming that security-related files exist.

Do not use production accounts, production user data, or unapproved destructive operations as test fixtures.

Report findings using a risk-based classification and include reproducible evidence and the affected component.

### 17. Accessibility Testing

Implement accessibility checks for important user-facing web and mobile journeys.

Cover applicable requirements including:

- Semantic structure.
- Accessible names and labels.
- Keyboard navigation on web.
- Focus management.
- Visible focus indicators.
- Screen-reader navigation.
- Form labeling and error association.
- Appropriate contrast.
- Text scaling.
- Accessible modal and dialog behavior.
- Video-player control accessibility.
- Caption availability and interaction.
- Accessible loading and error announcements.
- Touch-target usability.
- Non-gesture alternatives for important mobile actions.

Use automated accessibility tools where supported, but supplement automated checks with targeted manual or device-assisted verification for important workflows.

Do not claim full accessibility conformance based solely on a passing automated scanner. Document coverage and testing limitations.

### 18. Performance Testing and Acceptance Criteria

Implement repeatable performance tests for important user journeys and service boundaries.

Cover relevant client and backend paths, including:

- API request latency.
- Database-dependent request latency.
- Authentication workflows.
- Search responses.
- Feed retrieval and pagination.
- Video metadata and playback-source resolution.
- Playback startup where measured end to end.
- Media-processing completion latency.
- Queue backlog and processing throughput.
- Comment or engagement mutations.
- Realtime connection establishment where supported.
- Web page responsiveness.
- Mobile feed transitions and player initialization where measurable.

Define performance metrics, test conditions, and acceptance thresholds based on the actual product behavior and available environment.

Do not invent production performance measurements or claim global-scale capacity from a small local benchmark.

Separate:

- Unit-level performance checks.
- Component or endpoint benchmarks.
- Integration performance tests.
- Controlled load tests.
- Real-device or browser measurements.

Record request rate, concurrency, duration, payload characteristics, environment, and error rates for load tests.

Where no approved threshold exists, establish a documented provisional threshold with its rationale and explicitly distinguish it from a production SLO.

Do not run high-load tests against production or shared environments without explicit authorization and capacity controls.

### 19. Resilience and Failure-Path Testing

Test failure behavior across the system boundaries that can be validated in this milestone.

Cover relevant cases such as:

- Backend dependency timeout.
- Database connection failure.
- Redis outage or saturation.
- Event broker unavailable.
- Queue-worker failure.
- Search service timeout.
- Object-storage failure.
- Media CDN error.
- WebSocket disconnection.
- Mobile network loss.
- Duplicate asynchronous delivery.
- Interrupted uploads.
- Expired authorization.
- Stale cache entries.
- Partial responses.
- Malformed provider data.

Verify that the application handles failures safely and that it does not:

- Lose confirmed user data silently.
- Repeatedly submit destructive operations.
- Grant unauthorized access.
- Treat a failed request as successful.
- Leak secrets into error messages.
- Enter unbounded retry loops.
- Continue using stale state where authoritative revalidation is required.

Do not implement a full production chaos-testing program here. Provide deterministic component and integration failure tests, and reserve broader infrastructure-level fault injection and recovery certification for the dedicated operational QA scope.

### 20. Test Isolation, Parallelism, and CI Integration

Integrate the QA foundation into the project's actual CI system.

Define which suites execute:

- On every relevant change.
- Before merge.
- On a scheduled basis.
- Against an integration environment.
- On native device or emulator infrastructure where required.

Ensure test isolation supports parallel execution without cross-test mutation, resource collisions, or shared-data corruption.

Use isolated database schemas or disposable databases where appropriate.

Provide controlled lifecycle management for test services and external dependencies. Avoid a suite that leaves containers, browser sessions, test resources, or worker processes running indefinitely.

Make failures diagnosable through:

- Test result reports.
- Browser screenshots or traces where appropriate.
- Logs.
- Failed API request details with sensitive fields redacted.
- Media fixture identifiers.
- Relevant configuration and environment information.
- Reproducible commands.

Do not let ordinary CI depend on production credentials or production user data.

When device farms, native platform SDKs, browser versions, or media codecs are unavailable in a CI environment, separate those checks from the suites that can run there and document the required environment.

### 21. Test Quality and False-Positive Prevention

Maintain test quality as a first-class engineering concern.

Every meaningful test must:

- Exercise a defined behavior.
- Assert an observable result or invariant.
- Fail when the target behavior is broken.
- Avoid depending on unrelated implementation details.
- Clean up resources it creates.
- Provide useful failure diagnostics.
- Use controlled data.
- Avoid flaky timing assumptions where possible.

Do not:

- Replace meaningful assertions with snapshots alone.
- Mock every dependency in a test labeled end-to-end.
- Skip known failing tests without documenting the reason.
- Add blanket retries that hide real nondeterminism.
- Weaken validation just to obtain passing CI.
- Introduce arbitrary sleeps instead of condition-based synchronization.
- Claim test coverage proves correctness without meaningful assertions.

Report test counts and coverage data where available, but prioritize behavioral coverage and defect detection over raw percentages.

Document any known flaky tests, unavailable suites, exclusions, and mitigations.

### 22. Portable Test Contracts

Create portable contracts for integration tests that span independently implemented project components.

Document and validate the relevant:

- API request and response schemas.
- Authentication and authorization expectations.
- Error structures and status codes.
- Pagination and identifier formats.
- Database ownership and migration assumptions.
- Event schemas and versioning.
- Queue payloads and retry semantics.
- Upload and media-processing lifecycle.
- Realtime message contracts.
- Playback authorization and delivery behavior.
- Search and recommendation response schemas.
- Entitlement checks.
- Notification flows.
- Logging and trace-correlation conventions.

Use authoritative contract files where available.

When a required contract is missing, identify the precise dependency and define a proposed test contract only where useful. Clearly label the proposal and do not claim it validates a nonexistent endpoint or service.

Independent implementation parts must be testable against the same documented expectations without requiring hidden conversation history or an assumed shared filesystem.

### 23. Documentation and QA Reporting

Create or update documentation describing:

- QA architecture and test layers.
- Supported testing frameworks and versions.
- Required environment variables and secret references.
- Test data and fixture generation.
- Local setup and execution commands.
- CI test stages.
- API and domain-contract coverage.
- Media fixture generation and compatibility matrices.
- Browser and device coverage.
- Security and privacy tests.
- Accessibility checks.
- Performance-test scenarios and thresholds.
- Environment-dependent integration suites.
- Known flaky tests and test exclusions.
- Test-report interpretation.
- Troubleshooting and cleanup.
- Remaining test coverage gaps.

Include a clear distinction between tests implemented, tests executed, tests passed, tests failed, tests skipped, and tests not executable in the available environment.

### 24. Explicitly Out of Scope

Do not implement the following as new standalone systems in this milestone:

- New product features that belong to application implementation prompts.
- Replacement backend services or databases.
- A new media-processing pipeline.
- New recommendation algorithms.
- New search infrastructure.
- A replacement frontend or mobile architecture.
- Full global-scale load certification.
- Production disaster-recovery certification.
- Comprehensive chaos testing across production infrastructure.
- Final commercial launch approval.
- A new standalone integration or production-readiness prompt.

This milestone establishes broad functional, integration, compatibility, security, accessibility, and bounded performance testing. More extensive release certification, high-concurrency testing, disaster-recovery validation, and operational-readiness verification remain assigned to the dedicated subsequent QA scope.

### 25. Definition of Done

This milestone is complete only when all applicable conditions below are satisfied:

1. The repository has a documented and executable testing structure.
2. Meaningful automated tests cover implemented backend domain behavior and API contracts.
3. Database and migration tests validate relevant persistence behavior.
4. Event and queue tests cover actual supported delivery, retry, and failure semantics.
5. Search and recommendation interfaces are tested against established contracts.
6. Web component and browser tests cover important implemented user journeys.
7. Mobile tests cover important screens, state transitions, and available native behavior.
8. Media tests exercise supported playback, processing, delivery, and malformed-media scenarios.
9. Browser, device, bitrate, resolution, and codec matrices reflect actual platform capabilities.
10. Security and privacy tests cover important authentication, authorization, data-isolation, and disclosure risks.
11. Accessibility checks cover important web and mobile journeys.
12. Performance tests are repeatable, have explicit conditions and thresholds, and do not claim unsupported scale.
13. Failure-path tests cover important dependency outages, interrupted work, and retry behavior.
14. CI integration runs the appropriate test suites and reports failures accurately.
15. Test data and fixtures are deterministic, isolated, and free of unauthorized production data.
16. Tests and assertions are meaningful rather than placeholders.
17. Documentation explains execution, limitations, exclusions, and actual coverage.
18. Every command and validation result reported as complete was genuinely executed.
19. No fabricated passing results, silently disabled mandatory tests, fake production service tests, or unexplained test exclusions remain within the assigned scope.

### 26. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Testing architecture and frameworks**
- **Backend and API coverage**
- **Database and migration coverage**
- **Event and queue coverage**
- **Search and recommendation coverage**
- **Web frontend test coverage**
- **Mobile test coverage**
- **Media and playback compatibility matrix**
- **Browser, device, bitrate, resolution, and codec coverage**
- **Security and privacy test coverage**
- **Accessibility test coverage**
- **Performance-test scenarios and thresholds**
- **Failure-path and resilience coverage**
- **CI integration**
- **Tests created**
- **Commands actually executed**
- **Passed, failed, skipped, and unexecuted test suites**
- **Coverage and performance results where measured**
- **Documentation created or updated**
- **External test-environment requirements**
- **Known limitations and coverage gaps**
- **Unresolved integration issues**
- **Definition of Done status**

Do not claim that tests were run merely because they were added. Do not equate a successful local test suite with a release certified for global-scale production.

### 27. Final Execution Directive

Treat this prompt as the active implementation assignment for the YouTube-style video platform's functional, integration, compatibility, security, privacy, accessibility, and bounded performance QA foundation.

Inspect the repository and test artifacts genuinely available in the execution environment. Implement the complete bounded scope, preserve existing product behavior and integration contracts, execute applicable tests and validations, and document the actual result.

Do not respond with a testing plan alone. Do not ask the user to select test categories. Do not invent product functionality, fabricate successful test results, weaken assertions to make CI pass, or create unplanned project phases.

Deliver a maintainable, meaningful, automated test foundation that provides actionable evidence about the correctness of the platform's implemented behavior.

**Begin implementation now.**
