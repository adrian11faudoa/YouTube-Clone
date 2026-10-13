# YouTube-Style Video Platform — QA Prompt — Volume 2

## Release Certification, High-Concurrency Testing, End-to-End Reliability, Security, Disaster Recovery, and Operational Readiness

### 1. Mission and Implementation Scope

Implement the comprehensive **release-certification and production-readiness testing capability** for the YouTube-style video platform.

The platform comprises web and mobile applications, NestJS backend services, PostgreSQL, Redis, Kafka-compatible event streaming, BullMQ workers, OpenSearch, S3 object storage, CloudFront, FFmpeg media processing, HLS/DASH delivery, realtime services, creator workflows, monetization, recommendations, and moderation capabilities.

The long-term platform target is approximately **250 million registered users and 50 million daily active users**. The purpose of this milestone is to produce measurable evidence that the implemented system is correct, secure, recoverable, observable, and capable of handling its explicitly tested workloads.

This milestone concentrates on broad system validation and release certification across:

1. End-to-end user journeys and cross-service integration.
2. High-concurrency and capacity testing.
3. Video processing, playback, and media-delivery reliability.
4. Upload, creator, and publishing workflows.
5. Realtime communication and asynchronous processing.
6. Rights, copyright, reporting, and moderation enforcement.
7. Security, privacy, data retention, and account lifecycle.
8. Monetization, transactions, and entitlement correctness.
9. Disaster recovery, backup restoration, and deployment rollback.
10. Observability, SLO validation, and incident response.
11. Production-like browser, device, network, and media compatibility.
12. Release gates, defect management, and certification evidence.

This is a testing and release-certification assignment. Its purpose is to validate the actual system, identify defects, implement the necessary testing infrastructure, and provide actionable release evidence—not to rewrite the product or make every failed test pass by weakening its assertions.

This prompt is independently executable in a fresh coding-agent conversation. Inspect the repository, existing test infrastructure, operational configuration, and actual execution environment. Do not assume other coding-agent conversations share files, test results, credentials, or deployment access.

### 2. Technology and Testing Constraints

Use the established project direction:

- **Web:** Next.js, React, TypeScript, Tailwind, shadcn/ui, TanStack Query, and Zustand.
- **Mobile:** React Native, Expo, and TypeScript.
- **Backend:** Node.js, NestJS, and TypeScript.
- **Database:** PostgreSQL and Prisma.
- **Distributed state:** Redis.
- **Event streaming:** Kafka-compatible infrastructure.
- **Background jobs:** BullMQ.
- **Search:** OpenSearch/Elasticsearch-compatible infrastructure.
- **Storage and delivery:** Amazon S3 and CloudFront.
- **Media processing:** FFmpeg with HLS/DASH delivery.
- **Realtime:** WebSockets or Socket.IO where established.
- **Infrastructure:** AWS, Docker, Kubernetes, Helm, and Terraform.
- **Observability:** OpenTelemetry, Prometheus, Grafana, and the configured AWS monitoring services.

Use the testing, browser automation, mobile testing, load testing, infrastructure validation, and security tools already established by the project wherever possible.

Inspect the actual repository to discover the installed tools, service boundaries, supported media formats, API contracts, environment configuration, CI workflows, and existing test results before expanding the test program.

Do not introduce competing test frameworks or duplicate a working testing system without a demonstrated gap.

If necessary external services, credentials, devices, infrastructure, or production-like datasets are unavailable, implement the appropriate repeatable test procedures and execute the validations that are possible. Explicitly distinguish unexecuted tests from successful certification results.

### 3. Required Deliverables

Implement the following release-certification capabilities:

1. End-to-end tests spanning the actual application and backend boundaries.
2. High-concurrency, throughput, capacity, and saturation testing.
3. Video upload, processing, publication, and playback certification.
4. Media quality and adaptive-streaming validation.
5. Creator, live-streaming, and asynchronous workflow certification.
6. Rights, moderation, reporting, and restricted-content tests.
7. Monetization, purchase, membership, and entitlement integrity testing.
8. Security and privacy testing across critical system boundaries.
9. Data integrity, deletion, migration, backup, and restoration verification.
10. Deployment rollback and operational recovery exercises.
11. Observability and SLO validation under normal and degraded conditions.
12. Browser, device, OS, codec, resolution, bitrate, and network compatibility testing.
13. Release-gate automation and evidence generation.
14. Certification reports, defect prioritization, and remediation verification.

Produce executable tests, reusable test environments and fixtures, automation, measurable acceptance criteria, and reproducible reports.

Do not treat the existence of a test plan as evidence that the platform passed it.

### 4. Release-Certification Architecture

Organize the certification program into distinct test layers with explicit execution prerequisites.

The implementation should distinguish:

- Fast automated checks.
- Integration and contract tests.
- Cross-service end-to-end tests.
- Controlled high-concurrency tests.
- Media and playback certification.
- Security and privacy assessments.
- Data-integrity and recovery tests.
- Browser and physical-device compatibility tests.
- Deployment and operational-readiness exercises.

For each suite, define:

- What behavior it validates.
- The environment in which it runs.
- Required services and permissions.
- Test data and fixture requirements.
- Workload or device configuration.
- Assertions and measurable pass criteria.
- Failure evidence.
- Cleanup behavior.
- Known exclusions.
- Whether the suite blocks a release.

Integrate the certification suites into the project's existing CI/CD architecture. Reuse the established CI system, test reports, artifact storage, and environment-provisioning approach.

Do not create a new deployment architecture or substitute another testing framework for existing project infrastructure merely to organize this suite.

### 5. Cross-Service End-to-End Certification

Implement end-to-end tests for the critical user journeys supported by the actual platform.

#### 5.1 Identity and account lifecycle

Validate applicable flows such as:

- Account creation and sign-in.
- Session restoration and expiration.
- Sign-out.
- Account switching.
- Password recovery where supported.
- Authorization changes.
- Privacy settings.
- Account-data export and deletion where supported.

Verify that authentication state, persisted application state, backend authorization, and account-specific data remain consistent across the tested surfaces.

A sign-out test must verify more than navigation to a logged-out screen: it should also validate credential handling and appropriate clearing or isolation of protected account state.

#### 5.2 Video consumption

Test complete journeys that may include:

- Discovery-feed retrieval.
- Search.
- Channel navigation.
- Video metadata retrieval.
- Playback-source authorization.
- Media playback.
- Likes and comments.
- Subscription changes.
- Viewing-history behavior.
- Playlist and saved-content actions.
- Sharing and deep links.

Validate actual backend state transitions and media responses where appropriate rather than relying exclusively on visible button state.

#### 5.3 Creator publishing

Test the full supported publishing lifecycle:

1. Select or upload eligible media.
2. Initialize an authorized upload.
3. Transfer the media.
4. Finalize the upload.
5. Complete processing.
6. Validate generated outputs.
7. Save metadata and publishing settings.
8. Publish or schedule the content where supported.
9. Retrieve the published video.
10. Play the resulting media through the actual delivery path.

Include negative cases such as rejected media, expired authorization, interrupted upload, duplicate completion requests, processing failures, and unauthorized publishing attempts.

#### 5.4 Monetization and entitlements

Validate supported purchase, verification, subscription, membership, refund, expiration, and revocation workflows.

Where external billing environments are required, use approved sandbox transactions and verify the corresponding backend state.

Ensure that a client-side purchase callback alone cannot grant protected benefits when backend transaction verification is required.

#### 5.5 Mobile-specific journeys

Run representative mobile end-to-end tests for the implemented native capabilities, including applicable navigation, permissions, deep links, notifications, upload, live playback, short-form feeds, offline downloads, and account switching.

Only certify capabilities that exist and are actually accessible in the tested build.

### 6. High-Concurrency and Capacity Testing

Implement repeatable workload tests for important platform services and user journeys.

The global target of 250 million registered users and 50 million daily active users is a design objective—not proof that a particular environment can execute that volume.

Translate the target into explicit test scenarios supported by the actual architecture. Distinguish measured capacity, extrapolated estimates, and untested future requirements.

#### 6.1 Workload modeling

Define realistic workload profiles for relevant operations, including:

- Authentication and session restoration.
- Home and subscription-feed retrieval.
- Video metadata and playback authorization.
- Search requests.
- Channel and playlist retrieval.
- Likes, comments, and subscriptions.
- Creator uploads and publication.
- Media-processing queue consumption.
- Live-stream metadata and chat.
- Notifications.
- Purchase verification and entitlement reads.
- Administrative and moderation workflows where appropriate.

Base request mixes, arrival rates, concurrency, data sizes, and operation frequency on available measurements or explicitly documented assumptions.

Include both steady-state workloads and burst scenarios.

Do not equate registered accounts with concurrent active users, or request rate with unique users. Model these dimensions separately.

#### 6.2 Load profiles

Implement appropriately bounded scenarios for:

- Baseline load.
- Expected peak load.
- Sudden traffic bursts.
- Sustained elevated load.
- Increasing concurrency.
- Queue backlog recovery.
- Dependency degradation.
- Capacity saturation.
- Recovery after load subsides.

For each scenario, record the environment configuration, test duration, workload distribution, concurrency, request rate, response-size assumptions, error rate, latency percentiles, resource utilization, and queue behavior.

Use the actual service boundaries and deployment configuration. Avoid creating a synthetic workload that bypasses the bottleneck the test is intended to evaluate.

#### 6.3 Acceptance criteria

Define measurable acceptance criteria for each target service.

Where approved SLOs exist, use those as the source of truth.

Where no approved thresholds exist, propose explicit provisional thresholds, explain their rationale, and mark them as unapproved until the responsible engineering team accepts them.

Evaluate relevant signals, including:

- Request success rates.
- p50, p95, and p99 latency where meaningful.
- Throughput.
- CPU and memory utilization.
- Database connection saturation.
- Cache behavior.
- Queue backlog and oldest-job age.
- Media-processing latency.
- Playback startup and rebuffering.
- Dependency errors.
- Recovery after overload.

Do not report that a capacity target has been achieved based solely on the number of virtual users configured in a test.

### 7. Stress, Spike, and Soak Testing

Implement carefully controlled stress, spike, and soak scenarios for services where the environment supports them.

#### 7.1 Stress testing

Gradually increase load beyond the expected operating level in a controlled environment to identify:

- Capacity ceilings.
- Resource exhaustion.
- Queue saturation.
- Connection-pool bottlenecks.
- Nonlinear latency growth.
- Unstable autoscaling behavior.
- Failure isolation boundaries.
- Error propagation.

Record the observed failure modes and the last stable operating point under the tested configuration.

Do not claim a universal maximum capacity from one deployment or one workload profile.

#### 7.2 Spike testing

Apply controlled sudden increases in traffic to evaluate:

- Scaling reaction time.
- Request queuing.
- Load-balancer behavior.
- Cache effectiveness.
- Connection establishment.
- Queue accumulation.
- Recovery once traffic returns to normal.

Validate that scaling limits prevent runaway resource creation.

#### 7.3 Soak testing

Run sustained workloads long enough to expose relevant:

- Memory leaks.
- Resource leaks.
- Queue growth.
- Connection accumulation.
- Storage growth.
- Telemetry cost and volume.
- Degradation in latency or error rates.
- Repeated media-processing failures.

Define test duration according to the problem being investigated and the available environment. Record any conclusions that require longer production observation than the test provides.

Never fabricate a soak-test duration or claim that a memory leak was eliminated without actual evidence.

### 8. Media Pipeline and Playback Certification

Validate the full media path from source input through processing, storage, CDN delivery, and playback.

#### 8.1 Upload and processing

Test:

- Supported source-media formats.
- Metadata extraction.
- Duration and size limits.
- Invalid and corrupted input.
- Transcoding success and failure.
- Thumbnail generation.
- Captions and subtitle processing where supported.
- HLS/DASH packaging.
- Manifest and segment integrity.
- Retry and idempotency behavior.
- Worker interruption.
- Queue recovery.
- Publication readiness.

Ensure partially processed content is not exposed as successfully published when the product contract requires processing completion first.

#### 8.2 Adaptive-streaming integrity

Validate the actual encoding ladder and streaming outputs.

For supported HLS/DASH assets, test:

- Manifest syntax.
- Variant references.
- Segment availability.
- Codec and profile compatibility.
- Resolution and frame-rate metadata.
- Audio tracks.
- Caption or subtitle references.
- Segment timing and continuity.
- Seek and range behavior where supported.
- Expired or unauthorized playback resources.
- Output integrity after worker failure or retry.

Use real generated test media and inspect the actual resulting manifests or segments.

A valid response status alone does not prove that a media stream is correctly packaged or playable.

#### 8.3 Playback quality

Measure playback startup time, buffering, failed starts, and recovery using the actual player and media delivery path where feasible.

Separate:

- Client initialization latency.
- Playback-source resolution.
- Time to first playable media.
- CDN delivery latency.
- Rebuffering.
- Media-decoding failures.

Use consistent definitions and instrumentation for comparisons between test runs.

Do not infer end-user experience solely from backend endpoint latency or CloudFront request metrics.

### 9. Browser, Device, and Network Compatibility

Implement a representative compatibility matrix covering supported production targets.

Include relevant combinations of:

- Supported browsers and browser versions.
- Desktop and mobile web.
- iOS and Android versions.
- Supported device capability classes.
- Native media-player versions.
- Codec and media profiles.
- Resolution and frame rate.
- Bitrate tiers.
- HLS/DASH delivery.
- Captions and subtitle formats.
- Network conditions.

Where appropriate, include low-bandwidth, high-latency, packet-loss, unstable, and offline scenarios using controlled network shaping.

Validate critical behavior such as:

- Initial playback.
- Quality adaptation where supported.
- Recovery after network interruption.
- Video transitions.
- Authentication expiration.
- Deep-link handling.
- Native resource cleanup.
- Audio interruption handling.
- Application background and foreground transitions.

Do not attempt every theoretical device and codec combination. Establish a justified representative matrix, prioritize high-risk combinations, and document untested coverage.

Distinguish simulator and emulator results from actual device validation.

### 10. Realtime and Asynchronous Workflow Reliability

Test the supported realtime and asynchronous workflows under realistic operating conditions.

Cover applicable services such as live chat, notifications, event processing, media workers, analytics aggregation, and search indexing.

Validate:

- Connection establishment.
- Authentication and authorization.
- Reconnection.
- Duplicate events.
- Out-of-order delivery where applicable.
- Queue backlog.
- Delayed consumers.
- Worker restart.
- Graceful shutdown.
- Retry and backoff.
- Dead-letter or terminal-failure handling.
- Idempotent processing.
- Event-schema compatibility.
- Trace and correlation propagation.
- Recovery after dependency failure.

Do not assume exactly-once processing or guaranteed ordering unless the underlying architecture provides those properties.

For live chat and other realtime workloads, measure meaningful connection and message behavior without generating uncontrolled load against shared environments.

Verify that failures do not cause unbounded retries, duplicate privileged actions, or permanent accumulation of queue work.

### 11. Rights, Copyright, and Content-Access Enforcement

Implement end-to-end tests for the platform's established rights, copyright, and content-access controls.

Test supported behaviors involving:

- Private and unlisted content.
- Restricted or age-gated content.
- Geographic restrictions where applicable.
- Content that has been removed or blocked.
- Copyright or rights-related restrictions.
- Video visibility changes.
- Owner and collaborator permissions.
- Restricted playback URLs.
- CDN cache behavior after access changes.
- Content that becomes unavailable after being cached by a client.
- Applicable offline-download authorization.

Requirements:

- Unauthorized users must not gain access by guessing an identifier.
- A cached public-looking resource must not bypass authoritative access control.
- Private storage origins must remain protected.
- Revoked or restricted content must follow the platform's defined enforcement behavior.
- Changes to content visibility must propagate through the appropriate authorization and caching mechanisms.

Test the actual system's policies rather than inventing new copyright rules or legal interpretations.

Do not use real copyrighted content in unauthorized ways for testing. Use controlled, properly licensed fixtures and synthetic rights states.

### 12. Moderation, Abuse Prevention, and Trust/Safety

Certify the implemented moderation and abuse-prevention workflows.

Where the platform supports them, test:

- Content and account reporting.
- Comment moderation.
- Blocking and muting.
- Restricted or removed content.
- Moderator permissions.
- Creator moderation privileges.
- Report submission and deduplication.
- Rate limiting.
- Abuse-related access restrictions.
- Audit records for sensitive administrative operations.
- Enforcement propagation to search, recommendations, and playback.

Verify that unauthorized users cannot perform moderator or administrator actions through direct API requests.

Test that content removed or restricted by the authoritative backend does not remain accessible through stale application lists, search results, or unauthorized cached media paths beyond the documented propagation behavior.

Validate that moderation errors and internal enforcement details do not leak sensitive information to ordinary users.

Do not create new moderation policy or automated detection systems in this milestone. Test actual implemented behavior and document missing enforcement coverage.

### 13. Monetization and Transaction Integrity

Certify the implemented monetization and entitlement flows using approved test environments.

Depending on the product scope, this may include:

- Premium subscriptions.
- Channel memberships.
- App-store purchase verification.
- Purchase restoration.
- Entitlement refresh.
- Renewal and expiration states.
- Cancellation.
- Refund or revocation.
- Billing-provider webhook processing.
- Creator benefit enforcement.
- Advertisement authorization or delivery boundaries.
- Membership-restricted content.

Use sandbox transactions and controlled test identities wherever possible.

Validate:

- A duplicate transaction does not grant duplicate entitlements.
- Client-supplied success flags cannot bypass server verification.
- Entitlements are associated with the correct account.
- Expired or revoked benefits follow the authoritative policy.
- Retry and callback ordering do not corrupt the subscription state.
- A cancelled subscription does not incorrectly lose benefits before its authorized expiration when the provider permits continued access.
- Protected creator or video features reflect authoritative entitlement state.

Do not execute real production charges as part of certification. Do not invent billing-provider guarantees or claim successful financial settlement based only on client-side results.

### 14. Security and Privacy Release Assessment

Implement targeted security and privacy testing across the critical system boundaries.

The assessment must include applicable web, mobile, API, backend, storage, media-delivery, infrastructure, and administrative surfaces.

#### 14.1 Security scenarios

Test for:

- Broken object-level authorization.
- Privilege escalation.
- Authentication bypass.
- Session misuse.
- Insecure direct-object references.
- Injection and input-validation failures.
- Unsafe rendering of user-generated content.
- File-upload and media-processing risks.
- Unauthorized playback and download access.
- Secret or credential exposure.
- Insecure configuration.
- Rate-limit bypass.
- Unsafe redirects or deep links.
- API mass assignment where relevant.
- Cross-account data leakage.
- Excessive permissions.
- Vulnerable dependencies and container images.

Use established scanners and controlled adversarial tests. Findings must identify the affected component, reproducible behavior, severity, impact, and remediation guidance.

#### 14.2 Privacy scenarios

Validate that applicable privacy controls behave as specified, including:

- Account data isolation.
- Data retention.
- Watch and search history controls.
- Data-export workflows.
- Account deletion.
- Relevant downstream data removal.
- Log and telemetry redaction.
- Data minimization.
- Access to private content.
- Entitlement and billing-data exposure.

A successful account-deletion response does not prove that all required downstream data has been removed. Verify the actual deletion contract and supported completion evidence.

Do not claim legal compliance certification based on automated tests alone.

### 15. Database Consistency and Migration Certification

Validate data integrity across critical workflows and service boundaries.

Test applicable properties such as:

- Referential integrity.
- Unique constraints.
- Concurrent writes.
- Idempotency.
- Transaction boundaries.
- Migration compatibility.
- Backward-compatible deployment ordering.
- Referential cleanup.
- Deletion and retention behavior.
- Cache invalidation.
- Eventual consistency.
- Recovery following interrupted operations.

Include tests for races involving important operations, such as concurrent likes, upload completion, duplicate webhook delivery, purchase verification, membership changes, and publication transitions where applicable.

For migrations:

- Validate clean installation.
- Validate supported upgrade paths.
- Identify destructive schema changes.
- Check compatibility with mixed-version deployments.
- Exercise migration failure handling where safely testable.
- Verify application behavior after migration.

Do not perform destructive schema tests against shared or production databases.

Ensure that cached, indexed, and asynchronously derived state has documented consistency expectations and that the corresponding tests evaluate those expectations.

### 16. Backup, Restoration, and Disaster-Recovery Certification

Implement controlled recovery exercises for the established infrastructure.

Cover applicable resources such as:

- PostgreSQL.
- Redis where durability requirements apply.
- Kafka-compatible event data and configuration.
- OpenSearch indexes and snapshots.
- S3 media and application data.
- Terraform state and critical configuration.
- Kubernetes deployment resources.
- Secrets and identity configuration needed for recovery.

#### 16.1 Recovery tests

A meaningful recovery test must evaluate the restored resource rather than only confirming that a backup artifact exists.

Where infrastructure and permissions permit, validate:

- Backup discoverability.
- Restore initiation.
- Recovery-point identification.
- Data integrity.
- Database connectivity.
- Schema compatibility.
- Object availability.
- Event or index recoverability.
- Application compatibility.
- Controlled cutover or validation.
- Cleanup after the exercise.

Record actual recovery time and recovered data boundaries for each completed exercise.

#### 16.2 Recovery objectives

Compare measured recovery behavior against the explicitly defined recovery-point objectives and recovery-time objectives.

If approved objectives do not exist, document proposed objectives and identify the decisions required before the platform can be certified against them.

Do not manufacture recovery metrics.

#### 16.3 Regional failure

Where the architecture provides a recovery region, execute a controlled failover or recovery exercise when the environment supports it.

Validate the relevant DNS, infrastructure, data restoration or replication, secret access, service configuration, and post-recovery checks.

If a functioning recovery region is unavailable, test the available components and document the unverified regional failover requirements.

Do not declare disaster recovery certified merely because infrastructure code contains a second region.

### 17. Deployment, Rollback, and Release Recovery

Validate the actual deployment and recovery mechanisms.

Test applicable scenarios involving:

- Successful application deployment.
- Failed rollout.
- Readiness failure.
- Container startup failure.
- Image retrieval failure.
- Incompatible configuration.
- Database migration failure.
- Worker deployment interruption.
- Event-schema incompatibility.
- Incorrect environment values.
- Release regression.
- Rollback or forward recovery.

Confirm that health checks and deployment gates detect the relevant failure conditions.

Where rollback is unsafe because a schema or event contract has changed, validate the documented forward-recovery procedure instead.

Measure the actual time required to detect and recover from controlled release failures where the environment permits.

Verify that recovery does not silently duplicate jobs, lose acknowledged work, or expose unavailable features as operational.

Do not use production traffic or user data for destructive rollback testing without explicit authorization and a reviewed plan.

### 18. Observability, SLOs, and Incident-Response Validation

Certify that operational telemetry is useful for detecting and investigating real failures.

Validate the actual implementation of:

- Structured logs.
- Metrics.
- Distributed traces.
- Correlation identifiers.
- Health and readiness checks.
- Dashboards.
- Alert rules.
- Alert routing.
- SLO calculations.
- Error reporting.
- Operational runbooks.

#### 18.1 SLO validation

Use the platform's approved service-level objectives when available.

Validate relevant indicators for:

- API success and latency.
- Playback startup and rebuffering.
- Media-processing completion.
- Queue processing.
- Search.
- Realtime connectivity.
- Database availability.
- CDN delivery.
- Other established critical workflows.

Check the aggregation rules, filters, service boundaries, and failure classifications underlying each SLI.

Ensure the tests detect known controlled failures. An alert rule that renders successfully but never observes the intended metric is not sufficient evidence of operational coverage.

#### 18.2 Incident exercises

Where appropriate, perform controlled incident simulations in non-production environments.

Validate that the expected alert fires, reaches its configured destination, links to the correct dashboard and runbook, and supports a documented recovery action.

Do not claim a notification was delivered or an incident was detected unless that behavior was actually observed.

Ensure sensitive personal information, credentials, signed media URLs, and transaction data do not appear in telemetry artifacts.

### 19. Network, Dependency, and Degradation Testing

Exercise critical workflows under controlled dependency failures.

Simulate or reproduce scenarios such as:

- Increased API latency.
- Database unavailability.
- Redis degradation.
- Event-broker outage.
- Search timeout.
- S3 request failure.
- CDN origin errors.
- Queue backlog.
- Realtime disconnect.
- Expired credentials.
- Rate limiting.
- Partial service responses.
- DNS or network interruption where safely testable.

Verify timeouts, retries, circuit breakers where implemented, fallback behavior, and graceful degradation.

The system should fail safely rather than continue with incorrect authorization, duplicate destructive operations, or fabricated success states.

Test recovery after the dependency returns. Some failures are only visible in recovery behavior, such as a growing queue or stale cache after the original outage ends.

Do not introduce new application resilience mechanisms simply to make the test pass unless the change is part of the explicitly bounded remediation needed to achieve the established contract. Otherwise, record the defect and define the necessary follow-up.

### 20. Production Readiness and Release Gates

Implement a release-certification workflow that consumes the actual results from relevant test suites.

Define gates for:

- Critical functional journeys.
- API and cross-service contracts.
- Media-processing and playback.
- Required browser and device coverage.
- Performance thresholds.
- Security and privacy findings.
- Database and migration compatibility.
- Rights and moderation enforcement.
- Billing and entitlement correctness where applicable.
- Backup and restoration evidence.
- Rollback readiness.
- Observability and alerting.
- Known defect severity.
- Documentation and operational ownership.

Release decisions must be based on explicit policies.

#### 20.1 Defect severity

Define or reuse a severity model that considers:

- Customer impact.
- Security and privacy impact.
- Data loss or corruption.
- Financial or entitlement correctness.
- Media availability.
- Scope of affected users.
- Workaround availability.
- Probability and duration of failure.

Distinguish blocking defects from accepted limitations. Exceptions must be explicitly recorded with their rationale, owner, mitigation, and review or expiration conditions where appropriate.

Do not silently convert a failed mandatory test into a passing result.

#### 20.2 Gate behavior

A release gate must:

- Consume the required test results.
- Validate that required suites actually executed.
- Detect missing evidence.
- Apply the defined severity and threshold policy.
- Produce actionable failure details.
- Prevent release when mandatory criteria fail.
- Preserve an auditable result.

A green build is not equivalent to a certified release if required security, media, recovery, or operational checks were skipped.

### 21. Test Environments, Safety, and Evidence

Run certification tests only in environments authorized for the workload and test data involved.

#### 21.1 Environment controls

Require explicit environment identification for high-concurrency, destructive, recovery, and resilience suites.

Implement appropriate safeguards, such as:

- Explicit non-production allowlists.
- Maximum concurrency and duration limits.
- Resource quotas.
- Test-data isolation.
- Cleanup verification.
- Approved credentials.
- Restricted access to test reports.
- Confirmation or authorization for destructive operations.

Do not run unrestricted load, destructive deletion, or chaos experiments against production merely because the required tooling is available.

#### 21.2 Certification evidence

Produce machine-readable test results and human-readable summaries where appropriate.

Preserve relevant evidence such as:

- Test-suite identifiers and versions.
- Source revision.
- Environment and configuration.
- Workload definitions.
- Browser or device information.
- Media fixture identifiers.
- Test start and completion times.
- Actual measured metrics.
- Failures and logs with secrets redacted.
- Recovery and rollback results.
- Skipped tests and the reason for each exclusion.
- Known defects and accepted exceptions.

Reports must distinguish measured evidence from estimates, expected outcomes, and unverified assertions.

### 22. Defect Reporting and Remediation Verification

When certification exposes defects, create reproducible reports with actionable details.

For every significant defect, record:

- Affected feature or service.
- Environment and tested revision.
- Reproduction steps.
- Expected behavior.
- Actual behavior.
- Evidence.
- Impact and severity.
- Failure conditions.
- Likely ownership boundary where identifiable.
- Recommended remediation.
- Regression-test requirements.

When a bounded correction is appropriate and safe within this QA assignment, implement it only when it is directly necessary to establish the testing infrastructure or certification gate and does not amount to an unplanned product-development phase.

Otherwise, leave application remediation to the appropriate owner and verify it when the corrected implementation becomes available.

Do not broaden this assignment into rewriting unrelated production services. Do not hide a defect by changing the expected result without an authoritative requirement.

### 23. Required Automated and Controlled Test Suites

Organize the certification program into executable suites.

#### 23.1 End-to-end and cross-service tests

Validate major user journeys across the actual browser/mobile client, API, persistence, asynchronous processing, and media delivery.

Verify both user-visible behavior and resulting server state where practical.

#### 23.2 High-concurrency and performance tests

Run controlled workload scenarios with documented concurrency, request mix, duration, and acceptance criteria.

Record actual latency, error rate, throughput, resource utilization, and recovery behavior.

#### 23.3 Media compatibility tests

Validate source-media handling, processing outputs, manifests, CDN delivery, player compatibility, adaptive quality, and playback recovery using real controlled media fixtures.

#### 23.4 Security and rights tests

Exercise authorization boundaries, restricted content, reporting, moderation, protected media, account isolation, and relevant privacy controls.

#### 23.5 Resilience and recovery tests

Validate failure detection, job recovery, database restoration, deployment rollback, and supported regional-recovery procedures.

#### 23.6 Release-gate tests

Exercise the gate against known pass, fail, missing-evidence, threshold-exceeded, and accepted-exception fixtures. Verify that failed mandatory conditions cannot silently produce a successful certification outcome.

Use the established test frameworks and integrate these suites into the CI/CD system where applicable.

### 24. Out-of-Scope Boundaries

Do not use this milestone to introduce unrelated product functionality or a new platform architecture.

Specifically, do not:

- Rebuild the web or mobile applications.
- Replace existing backend services.
- Redesign the video-processing architecture.
- Create a new recommendation engine.
- Replace the payment or entitlement system.
- Rewrite the rights or moderation domain.
- Build a separate infrastructure platform.
- Claim regulatory certification based solely on automated tests.
- Run destructive experiments against production without authorization.
- Invent global-scale capacity or recovery results.
- Append additional implementation phases beyond this defined certification scope.

The assignment is to implement and execute the release-certification capability against the actual platform, repair narrowly scoped QA infrastructure defects when appropriate, and produce verifiable evidence about readiness and remaining risk.

### 25. Definition of Done

This milestone is complete only when all applicable criteria below are satisfied:

1. The certification suite covers the major implemented end-to-end user journeys.
2. Cross-service contracts and persistence outcomes are validated where practical.
3. High-concurrency tests run against controlled environments with explicit workload definitions and measurable criteria.
4. Capacity results distinguish directly measured performance from estimates and untested global-scale targets.
5. Video upload, processing, HLS/DASH packaging, CDN delivery, and playback have meaningful integration coverage.
6. Browser, mobile-device, codec, bitrate, resolution, and network coverage is documented and executed to the extent supported by the available environment.
7. Creator workflows and asynchronous processing are tested under success, failure, retry, and recovery scenarios.
8. Rights, copyright-related restrictions, moderation, reporting, and access-control enforcement have meaningful certification coverage.
9. Monetization and entitlement workflows use approved test environments and verify authoritative state transitions where implemented.
10. Security and privacy assessments cover important authentication, authorization, data-isolation, and sensitive-data risks.
11. Database integrity, migration compatibility, backup restoration, and supported disaster-recovery procedures are tested to the extent permitted by the environment.
12. Deployment failure and rollback or forward-recovery behavior are validated for the relevant release paths.
13. Observability, SLO measurements, alerts, and operational runbooks are validated against controlled scenarios.
14. Release gates accurately reject failed mandatory tests, missing evidence, and unapproved policy violations.
15. High-risk test suites enforce environment restrictions and safe resource limits.
16. Test reports preserve actual measurements, failures, exclusions, and environment details.
17. Defects and known limitations are recorded without falsifying test outcomes.
18. Relevant available tests and validations have been executed and their results reported truthfully.
19. Documentation explains the certification process, release gates, residual risks, and environment-dependent work.
20. No fabricated performance results, recovery claims, security assessments, test successes, or release approvals remain in the certification evidence.

### 26. Completion Report

After implementation and execution of the available certification suites, provide a factual report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Certification architecture**
- **End-to-end and cross-service coverage**
- **High-concurrency and capacity scenarios**
- **Measured throughput, latency percentiles, and error rates where available**
- **Media processing and playback certification**
- **Browser and device compatibility results**
- **Creator and asynchronous workflow results**
- **Rights, copyright, moderation, and access-control results**
- **Monetization and entitlement results**
- **Security and privacy findings**
- **Database and migration results**
- **Backup and restoration results**
- **Disaster-recovery and rollback results**
- **Observability, SLO, and alert-validation results**
- **Release-gate implementation**
- **Tests and validations actually executed**
- **Passed, failed, skipped, and unexecuted suites**
- **Defects discovered and their severity**
- **Remediation and regression-verification status**
- **Known risks and accepted exceptions**
- **External infrastructure, device, account, or credential requirements**
- **Documentation updated**
- **Release readiness assessment**
- **Definition of Done status**

Use an evidence-based assessment such as:

- **Pass:** Required criteria were verified using actual results.
- **Fail:** One or more mandatory criteria failed.
- **Blocked:** A required test could not be executed because of a specific missing dependency or environment.
- **Not tested:** No valid execution evidence exists.
- **Conditional:** Release depends on explicitly documented risk acceptance or additional verification.

Do not declare the platform fully production-ready merely because some suites pass. A release-readiness conclusion must reflect the scope of tested behavior, outstanding failures, unexecuted scenarios, and residual risks.

### 27. Final Execution Directive

Treat this prompt as the active engineering assignment for release certification, high-concurrency testing, end-to-end reliability, media playback, creator workflows, rights and moderation, security and privacy, disaster recovery, observability, rollback, and operational readiness of the YouTube-style video platform.

Inspect the repository and operational artifacts genuinely available in the execution environment. Implement the defined testing infrastructure, run the appropriate authorized certification suites, preserve the integrity of test assertions and evidence, and document the actual results.

Do not respond with a plan alone. Do not ask the user to choose testing categories. Do not fabricate test execution, invent production capacity, weaken mandatory acceptance criteria, perform unauthorized destructive testing, or add unplanned project phases.

Deliver a repeatable, evidence-based release-certification capability that clearly identifies what has been verified, what has failed, what remains untested, and which risks must be resolved or explicitly accepted before release.

**Begin implementation now.**
