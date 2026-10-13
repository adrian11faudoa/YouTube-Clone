# YouTube-Style Video Platform — Infrastructure Prompt — Volume 2

## CI/CD, Media-Worker Autoscaling, Observability, Reliability, Disaster Recovery, and Operational Readiness

### 1. Mission and Implementation Scope

Implement the production-grade **deployment automation, workload scaling, observability, reliability controls, backup and recovery, disaster-recovery readiness, infrastructure security validation, capacity management, and operational release safeguards** for the YouTube-style video platform on AWS.

The platform targets approximately 250 million registered users and 50 million daily active users. Its infrastructure must be designed to evolve toward this scale through measurable capacity planning, controlled deployments, workload-specific scaling, secure operations, and verifiable recovery procedures.

This milestone covers the operational capabilities required to deploy and run the platform safely after its infrastructure foundation has been established. It includes continuous integration and delivery, FFmpeg worker scaling, application and infrastructure telemetry, service-level objectives, CDN monitoring, database and storage recovery, regional-failure planning, controlled chaos testing, cost governance, operational runbooks, and release gates.

Implement functional automation, configuration, monitoring, policies, tests, and documentation. Do not deliver merely conceptual dashboards, theoretical recovery plans, nonfunctional pipeline examples, or placeholder operational resources.

This prompt is independently executable in a fresh coding-agent conversation. Inspect the repository and environment artifacts genuinely available to you, preserve existing compatible implementations, and define portable contracts for anything that cannot be discovered. Do not assume access to resources or decisions from another coding-agent conversation.

### 2. Technology Stack and Operating Principles

Use the established project technology direction:

- **Cloud:** AWS.
- **Infrastructure as code:** Terraform.
- **Containers and orchestration:** Docker, Amazon EKS, and Kubernetes.
- **Application deployment:** Helm.
- **Web:** Next.js, React, TypeScript, Tailwind, and shadcn/ui.
- **Mobile:** React Native, Expo, and TypeScript, subject to the actual repository configuration.
- **Backend:** Node.js, NestJS, and TypeScript.
- **Data:** PostgreSQL, Prisma, and Redis.
- **Event streaming:** Kafka-compatible infrastructure using the established Kafka/Redpanda-compatible architecture.
- **Background work:** BullMQ and Kubernetes workers.
- **Search:** OpenSearch/Elasticsearch-compatible infrastructure.
- **Media:** Amazon S3, CloudFront, FFmpeg, HLS, and DASH.
- **Realtime:** WebSockets or Socket.IO where established.
- **Observability:** OpenTelemetry, Prometheus, and Grafana, integrated with appropriate AWS-native monitoring and logging services.
- **Security:** AWS IAM, workload identity, AWS Secrets Manager or an established equivalent, TLS, image security, infrastructure scanning, and auditability.

Follow the actual repository's existing provider versions, CI platform, Kubernetes configuration, resource naming, service contracts, environment variables, and deployment architecture.

Prefer supported managed AWS services where they provide a reasonable operational benefit. Avoid adding overlapping monitoring platforms, queue technologies, autoscalers, or orchestration systems without a clear architectural reason.

### 3. Required Deliverables

Implement the following operational capabilities:

1. CI/CD pipelines and deployment automation.
2. Secure image building, publishing, and release identification.
3. Kubernetes application and worker deployment automation.
4. FFmpeg media-worker autoscaling and capacity controls.
5. Application, infrastructure, media, database, queue, and CDN observability.
6. Service-level indicators, SLOs, dashboards, and actionable alerting.
7. CDN delivery monitoring and troubleshooting.
8. Backup, restoration, and recovery automation.
9. Disaster-recovery procedures and regional-readiness configuration.
10. Security validation, supply-chain controls, and operational guardrails.
11. Capacity forecasting, cost visibility, and resource-efficiency controls.
12. Controlled chaos and resilience testing.
13. Operational runbooks, incident procedures, and release gates.
14. Automated tests, documentation, and a factual completion report.

Keep all capabilities integrated with the established AWS, Terraform, EKS, Kubernetes, Helm, database, storage, messaging, and application configuration. Do not introduce incompatible infrastructure contracts.

### 4. Repository Inspection and Implementation Discipline

Before modifying anything, inspect the actual repository and identify:

- Terraform modules and environment composition.
- Kubernetes manifests, Helm charts, and workload definitions.
- Existing CI/CD workflows.
- Container build and image-publishing conventions.
- Application, worker, and media-processing deployment boundaries.
- PostgreSQL, Redis, Kafka-compatible, and OpenSearch configuration.
- S3 and CloudFront resources.
- Logging, metrics, tracing, and alerting configuration.
- Existing backup, restore, and disaster-recovery resources.
- Existing test frameworks, security scanning, and release controls.
- Available operational documentation and runbooks.

Reuse and extend compatible resources. Avoid regenerating unchanged files or replacing working configurations unnecessarily.

If a required service, pipeline, AWS account, CI identity, metric, or test environment is unavailable, implement what can be verified locally, document the exact dependency, and provide concrete execution procedures. Never fabricate successful deployments, recovery tests, alerts, or load-test results.

### 5. CI/CD Architecture and Pipeline Implementation

Implement a maintainable CI/CD workflow using the project's existing CI system. If none exists, establish one compatible with the repository and its deployment model.

Provide reusable workflow components where they offer a clear benefit, but preserve distinct responsibilities for application validation, image publishing, infrastructure changes, and production deployment.

#### 5.1 Continuous integration

Implement appropriate checks for affected project components:

- Type checking and linting for TypeScript applications.
- Unit and integration tests.
- Backend build validation.
- Web build validation.
- Mobile validation appropriate to the available Expo and native toolchain.
- Docker image builds.
- Terraform formatting and validation.
- Helm linting and template rendering.
- Kubernetes manifest validation.
- Dependency and vulnerability scanning.
- Secret scanning.
- Container image scanning.
- Infrastructure policy checks.
- Contract and configuration consistency checks where suitable.

Use caching appropriately without allowing stale dependencies or generated artifacts to bypass important validation.

A failed required check must fail the pipeline with useful diagnostics. Do not convert critical security or test failures into warning-only steps merely to obtain a green build.

#### 5.2 Image build and publication

Implement reproducible, identifiable container builds for applicable services and workers.

Requirements:

- Use controlled base images and supported runtime versions.
- Pin dependencies appropriately.
- Avoid running containers as root unless a documented exception is necessary.
- Publish versioned images using immutable identifiers, preferably including a source revision.
- Generate or preserve image digests for deployment traceability.
- Apply registry access controls.
- Avoid embedding secrets in image layers.
- Support vulnerability and provenance checks where available.
- Preserve compatibility between application configuration and runtime images.

Deployments must identify the exact image being released. A mutable tag such as `latest` must not be the sole production release identifier.

#### 5.3 Secure CI identity

Use the established secure CI-to-AWS identity mechanism, preferably short-lived role assumption through OIDC when supported by the CI provider.

Constrain role trust policies to the intended repository, branch, environment, workflow, or equivalent identity attributes.

Do not introduce long-lived AWS access keys into repository secrets when a supported short-lived identity mechanism is available.

Separate build permissions from infrastructure modification and production deployment permissions. A source build should not automatically acquire unrestricted access to production data or infrastructure.

### 6. Deployment Automation and Release Safety

Implement deployment workflows compatible with the project's established Kubernetes and Helm architecture.

Support appropriate environment promotion through development, testing, staging, and production.

Requirements:

- Use versioned application images and explicit chart values.
- Validate deployment configuration before rollout.
- Preserve environment-specific secret references.
- Apply changes through reviewable infrastructure and deployment workflows.
- Configure readiness and liveness behavior according to application semantics.
- Respect Kubernetes disruption and rollout constraints.
- Support rollout-status validation.
- Detect failed deployments.
- Provide a documented rollback or forward-recovery procedure.
- Verify that a rollback does not introduce an incompatible database or event-schema version.
- Preserve deployment and image provenance.
- Record the source revision, image digest, and environment for each release.

Use rolling, canary, blue/green, or other deployment strategies only where they fit the service and current architecture.

Do not assume every service is stateless or can be rolled back safely after a database migration.

#### 6.1 Deployment ordering

Document safe deployment ordering for components whose compatibility depends on one another, including:

- Database schema changes.
- API versions.
- Event schemas and consumers.
- Background workers.
- Media-processing jobs.
- Web applications.
- Realtime services.
- Kubernetes configuration changes.

Support backward-compatible migrations and expand/contract patterns where appropriate. Avoid release workflows that require all application instances to switch versions simultaneously.

#### 6.2 Mobile and web release boundaries

Implement the CI validation and release hooks appropriate to the repository's mobile and web projects.

Do not pretend that a successful mobile build is equivalent to publishing through the Apple App Store or Google Play. Store signing, credentials, account permissions, review, and staged publication must follow the actual release configuration.

Keep mobile release secrets outside source control. Document the approved release procedure and identify any store-account actions that require authorized human participation.

### 7. FFmpeg Worker Scaling and Media-Processing Reliability

Implement workload-specific scaling and operational controls for FFmpeg-based processing workers.

The media pipeline may perform:

- Video probing and validation.
- Transcoding.
- HLS/DASH packaging.
- Thumbnail generation.
- Caption or subtitle processing where applicable.
- Media-quality checks.
- Other established media-processing jobs.

Use the platform's actual queues, job types, worker deployments, and processing contracts.

#### 7.1 Queue-aware scaling

Implement an autoscaling strategy that responds to appropriate signals, such as:

- Queue depth.
- Oldest-job age.
- Processing latency.
- Worker utilization.
- Pending-job throughput.
- Resource saturation.
- Backlog growth and drain rate.

Prefer workload-aware scaling signals when available rather than relying exclusively on CPU utilization.

If Kubernetes queue-based autoscaling requires an additional supported component, such as KEDA, use it only when compatible with the current cluster and operational model. Provision and secure its required permissions, or use an established alternative with equivalent documented behavior.

Define:

- Minimum and maximum replica counts.
- Scale-up and scale-down policies.
- Cooldown or stabilization behavior.
- Resource requests and limits.
- Queue ownership and metric sources.
- Failure behavior when the scaling metric is unavailable.
- Environment-specific safety limits.

Do not scale without bounds simply because a queue grows. A downstream storage, network, database, or transcoding bottleneck could make unrestricted scaling counterproductive.

#### 7.2 Resource and job isolation

Treat FFmpeg workloads as resource-intensive and potentially long-running.

Implement appropriate CPU, memory, ephemeral-storage, and concurrency limits.

Separate media-processing workloads from latency-sensitive API services when the architecture justifies it. Use appropriate scheduling constraints or node pools to prevent FFmpeg resource pressure from starving essential application workloads.

Support graceful termination, job interruption handling, idempotent retries, and cleanup of temporary artifacts.

Do not assume a terminated worker's unfinished job will be recovered automatically. Verify that the established queue configuration and worker shutdown behavior actually support safe recovery.

#### 7.3 Backpressure and failure handling

Implement operational controls for:

- Queue backlog thresholds.
- Long-running jobs.
- Repeated processing failures.
- Poison jobs.
- Worker crashes.
- Dependency outages.
- Temporary storage exhaustion.
- Invalid or unsupported source media.
- Dead-letter or terminal-failure handling where supported.
- Controlled retry and backoff behavior.

Alert on sustained backlog age and failing jobs, not only on a large instantaneous queue count.

Do not redesign the media-processing service itself in this milestone. Implement the infrastructure, scaling policy, instrumentation, and operational safeguards around the established processing architecture.

### 8. Autoscaling Beyond Media Workers

Establish autoscaling configuration for other applicable platform workloads.

Consider separate policies for:

- Backend API deployments.
- Realtime services.
- Queue consumers.
- Media workers.
- Search-indexing workers.
- Notification workers.
- Scheduled or maintenance workloads.
- Other established services with different capacity profiles.

Use the scaling mechanism already established by the project. Where justified, apply Kubernetes HPA, KEDA, cluster autoscaling, node autoscaling, or AWS-managed service scaling.

For each applicable workload, document:

- Scaling signals.
- Minimum and maximum capacity.
- Resource requests and limits.
- Scale-up behavior.
- Scale-down stabilization.
- Dependency capacity constraints.
- Failure behavior when scaling signals are unavailable.
- Environment-specific bounds.

Do not configure every deployment with identical CPU thresholds. A CPU-bound FFmpeg worker, a latency-sensitive API, and an I/O-heavy queue consumer have different scaling characteristics.

Validate that pod-level scaling can obtain cluster capacity where required. Application replica autoscaling is ineffective if suitable nodes cannot be scheduled.

### 9. Observability Architecture

Implement end-to-end operational visibility using the platform's established observability stack.

Integrate:

- OpenTelemetry-compatible traces.
- Structured application logs.
- Infrastructure and Kubernetes metrics.
- Application-level metrics.
- Database and cache metrics.
- Queue and consumer metrics.
- Media-processing metrics.
- CDN and delivery metrics.
- Error reporting.
- Dashboards.
- Actionable alerts.

Use existing AWS-native monitoring services for appropriate infrastructure signals, while preserving the established Prometheus, Grafana, and OpenTelemetry integration.

Do not introduce redundant monitoring agents or duplicate exporters without a clear reason.

#### 9.1 Trace propagation

Define and configure trace context propagation across the actual supported boundaries, including where applicable:

- API requests.
- Internal service calls.
- Database operations.
- Queue producers and consumers.
- Kafka-compatible events.
- Media-processing jobs.
- Storage operations.
- Realtime requests.
- CDN authorization or origin-related diagnostic paths where trace integration is actually possible.

Use stable correlation identifiers for operations that span asynchronous services.

Do not claim full distributed tracing if a component does not propagate or expose trace context. Document limitations and make the visible boundaries explicit.

#### 9.2 Logging

Use structured logging with consistent service, environment, severity, timestamp, correlation, and version fields.

Provide appropriate log retention and access restrictions.

Avoid logging:

- Authentication credentials.
- Session tokens.
- Raw signed URLs containing secrets.
- Passwords.
- Private media contents.
- Unnecessary personal information.
- Sensitive payment or verification data.

Establish redaction behavior and prevent high-volume media or realtime workloads from generating uncontrolled log volumes.

#### 9.3 Metrics cardinality and cost

Avoid unbounded labels such as arbitrary user IDs, request bodies, video IDs, signed URLs, or raw exception text.

Use bounded labels and aggregation for high-volume services.

Define retention and sampling policies that balance diagnostic value with infrastructure cost and privacy.

### 10. Service-Level Indicators and SLOs

Establish measurable service-level indicators and service-level objectives for critical user-facing and platform workflows.

Use actual service capabilities and available metrics to define SLIs.

Relevant service domains include:

- API availability and latency.
- Video playback startup and rebuffering.
- Media-processing completion latency.
- Upload-to-publication processing.
- Search availability and latency.
- Realtime connection success and message-delivery behavior where measurable.
- Background-job completion.
- Notification-processing outcomes.
- Data-store availability.
- CDN delivery performance.
- Deployment success and rollback frequency where useful.

Do not invent precise production SLO values without sufficient basis. Propose concrete initial objectives, document the rationale and limitations, and make configurable or explicitly labeled objectives distinguishable from approved targets.

For each defined objective, specify:

- User or business outcome.
- SLI definition.
- Measurement source.
- Aggregation window.
- Target and evaluation window.
- Exclusion criteria.
- Known measurement limitations.
- Dashboard.
- Relevant alert or response behavior.

Where sufficient evidence exists, define multi-window, multi-burn-rate alerting for important SLOs. Avoid treating every isolated error as a production incident.

Create service dashboards that connect symptoms to relevant dependency signals. A playback incident should help operators investigate API latency, authorization, CDN delivery, player startup, and media availability rather than providing an isolated generic error count.

### 11. CDN and Media-Delivery Monitoring

Implement operational monitoring of CloudFront and the established media-delivery architecture.

Monitor available signals appropriate to the delivery model, including:

- Request volume.
- Cache-hit ratio.
- Origin request volume.
- HTTP 4xx and 5xx errors.
- Origin errors and timeouts.
- Request latency.
- Data transfer volume.
- Geographic delivery patterns where available.
- Cache invalidation outcomes.
- Manifest and media-segment availability.
- Relevant cost and bandwidth trends.

Use CloudFront and origin metrics that are actually supported and enabled. Do not fabricate player quality metrics from CDN counters alone.

Where application-level playback telemetry exists, connect relevant signals to CDN and origin metrics without exposing user identity or sensitive playback URLs.

Implement useful dashboards and alerts for sustained degradation, unusual error increases, origin failure, and material cost anomalies.

Document cache invalidation behavior and the consequences of invalidating high-volume media paths.

Do not weaken authorization or make private origins public merely to improve the observed cache-hit ratio.

### 12. Database, Redis, Kafka, and Search Reliability

Implement monitoring, alerting, and operational guidance for the established stateful and messaging services.

#### 12.1 PostgreSQL

Where the deployment architecture supports the relevant metrics, monitor:

- Availability.
- Connection usage.
- CPU and memory pressure.
- Storage capacity.
- Query latency.
- Locking and contention signals.
- Replication or failover health where configured.
- Backup completion.
- Connection-pool saturation.

Alert on credible data-service risks with actionable thresholds.

Document capacity limits and safe responses. Do not automatically scale or fail over PostgreSQL based only on a single transient metric.

#### 12.2 Redis

Monitor:

- Memory utilization.
- Evictions where relevant.
- Connection saturation.
- Latency.
- Availability.
- Replication or failover health where configured.
- Queue-related backlog symptoms.
- Persistence behavior for deployments that depend on it.

Document the reliability implications of using Redis for both cache and queue workloads.

Do not assume a cache eviction policy is appropriate for every Redis deployment, especially where queue state has different durability expectations.

#### 12.3 Kafka-compatible streaming

Monitor relevant signals such as:

- Broker and cluster health.
- Consumer lag.
- Processing throughput.
- Under-replicated partitions where exposed.
- Storage capacity.
- Request errors.
- Client connectivity.
- Event-processing delay.

Create alerts for sustained consumer lag and abnormal delivery failures. Connect those alerts to documented investigation procedures.

#### 12.4 OpenSearch

Monitor the signals exposed by the selected deployment, including:

- Cluster or domain health.
- CPU and memory pressure.
- Storage capacity.
- Search latency.
- Indexing throughput and errors.
- Rejected requests.
- Relevant shard-allocation or recovery conditions.

Define operational guidance for capacity problems and degraded search. Do not treat a search outage as permission to bypass application authorization or return arbitrary results.

### 13. Backup and Recovery Architecture

Implement a verifiable backup and recovery strategy for critical data.

Cover the established stateful services and application-owned assets, including:

- PostgreSQL data.
- Redis data where persistence is required.
- Kafka-compatible event data and configuration where applicable.
- OpenSearch snapshots or supported recovery mechanisms.
- S3 object data and relevant metadata.
- Terraform state.
- Critical configuration and deployment artifacts.

Apply appropriate backup controls, encryption, retention, access restrictions, and recovery-point documentation.

#### 13.1 PostgreSQL backup

Use the selected database service's supported backup and point-in-time recovery mechanisms where available.

Document:

- Backup frequency or recovery-point behavior.
- Retention configuration.
- Encryption.
- Access restrictions.
- Point-in-time recovery conditions.
- Recovery procedure.
- Post-restore integrity and application-validation checks.

Do not claim point-in-time recovery is enabled simply because a database has ordinary automated backups.

#### 13.2 Object-storage recovery

Where the media lifecycle requires recovery from accidental or malicious deletion, configure appropriate supported controls, such as versioning, protected retention, or replication where justified.

Distinguish between restoration of metadata and restoration of large media objects. Include lifecycle and retention implications in the operational documentation.

Do not retain every temporary transcoding artifact indefinitely.

#### 13.3 Recovery validation

Implement recovery-test procedures and automate validation to the extent supported by the environment.

Where credentials and isolated infrastructure are available, execute controlled restore tests that verify more than the existence of a backup file.

A valid recovery test should confirm relevant integrity, connectivity, schema or format compatibility, and application-level usability.

When live restore testing cannot be executed safely or the required environment is unavailable, run the available automated checks and document the exact unverified steps. Do not report an unperformed restore as successful.

### 14. Disaster Recovery and Regional Readiness

Implement a practical disaster-recovery strategy that reflects the platform's data ownership, availability requirements, and current infrastructure architecture.

Distinguish:

- Local process or pod failure.
- Availability Zone failure.
- Regional service disruption.
- Accidental or malicious data deletion.
- Credentials or infrastructure misconfiguration.
- Loss of a critical external dependency.

#### 14.1 Recovery objectives

Define initial, explicit recovery-point objectives and recovery-time objectives for critical service classes.

Include relevant areas such as:

- Account and authorization data.
- Core video metadata.
- Upload and processing state.
- Playback metadata.
- Engagement and subscription data.
- Event streams.
- Search indexes.
- Analytics workloads.
- Media assets.
- Operational configuration.

Use more stringent objectives only where they are justified and supported by the architecture. Clearly label proposed objectives that have not yet been approved or validated.

Document dependencies between recovery objectives and the chosen database, backup, replication, queue, and storage architecture.

#### 14.2 Regional readiness

Provide a concrete path for establishing a recovery region, including the configuration or documentation needed for:

- Infrastructure provisioning.
- IAM and secret access.
- Database restoration or supported replication.
- Required storage access or replication.
- Required event-streaming and queue capabilities.
- Container image availability.
- DNS and traffic switching.
- TLS and certificates.
- Application configuration.
- Observability continuity.
- Operational verification.

Do not equate the existence of two AWS regions with a functioning disaster-recovery system.

The implementation may establish a warm-standby or another justified recovery approach rather than fully active-active operation. Select the approach according to the available infrastructure and operational cost.

Do not silently introduce cross-region active-active database writes, conflicting ownership, or distributed-consistency assumptions.

### 15. Security Hardening and Supply-Chain Protection

Implement operational security controls across the infrastructure delivery lifecycle.

Cover:

- CI identity and deployment-role restrictions.
- Container image vulnerability scanning.
- Dependency scanning.
- Secret scanning.
- Infrastructure-as-code scanning.
- Kubernetes configuration policy checks.
- Container non-root execution where appropriate.
- Image provenance and immutable release identification.
- Access control for CI, registries, infrastructure state, and observability.
- Secret rotation compatibility.
- Audit logging.
- Least-privilege service roles.
- Network exposure validation.
- Critical-vulnerability handling and exception tracking.

Where supported by the existing build architecture, generate or retain software bills of materials and artifact provenance information.

Define a risk-based release policy for severe vulnerabilities and explicit, time-limited exceptions. Avoid treating every low-risk informational finding as an automatic release blocker unless an established policy requires it.

Do not disable vulnerability scanners, TLS checks, or policy enforcement solely to make pipelines pass.

Do not claim compliance certification based on the existence of selected controls.

### 16. Capacity Planning and Cost Governance

Implement a practical capacity and cost-management foundation.

Identify cost drivers across:

- EKS compute.
- FFmpeg worker CPU, memory, and ephemeral storage.
- Database capacity and replicas.
- Redis memory and availability.
- Event-streaming capacity and retention.
- OpenSearch compute and storage.
- S3 media storage and requests.
- CloudFront delivery bandwidth.
- NAT and inter-zone traffic.
- Observability ingestion and retention.
- Backups and cross-region transfer.
- CI and build artifacts.

Use AWS cost-visibility features and resource tagging where configured and available.

Implement appropriate budgets, threshold notifications, and cost dashboards or reports based on the available environment.

Document allocation tags and environment ownership. Avoid exposing financial data to unauthorized teams.

#### 16.1 Scaling economics

Use workload signals, measured utilization, and cost implications when choosing scaling behavior.

Avoid:

- Unlimited worker scale-out.
- Unbounded retries.
- Indefinite temporary media retention.
- Excessive log ingestion.
- Duplicate media storage.
- High-cardinality telemetry.
- Unnecessary always-on non-production infrastructure.
- Unjustified cross-region replication.

Document the trade-offs between availability, processing latency, redundancy, and operating cost.

Do not invent precise savings or claim cost optimizations have been proven without measurement.

### 17. Chaos and Resilience Testing

Implement a controlled resilience-testing capability for non-production environments.

Use existing tools where available. Introduce a chaos-testing tool only where its capabilities are justified, its permissions are constrained, and the team can operate it safely.

Design repeatable scenarios for relevant failures, such as:

- Termination of a worker during a job.
- Pod restarts during controlled traffic.
- Temporary dependency unavailability.
- Queue-worker backlog.
- Network interruption in an isolated test.
- Database connection exhaustion in a controlled environment.
- Media-processing resource pressure.
- Temporary storage-service errors.
- Repeated deployment failure and rollback.
- Failure of a non-production telemetry dependency.

#### 17.1 Experiment safety

Every experiment must define:

- Objective and hypothesis.
- Target environment and resources.
- Preconditions.
- Expected steady state.
- Failure injection method.
- Observed signals.
- Abort conditions.
- Cleanup procedure.
- Expected recovery.
- Evidence to record.

Use strict allowlists and environment guards. Deny production fault injection by default.

Do not run destructive experiments against real user data or live production infrastructure without explicit authorization and an approved operational procedure.

If the required isolated environment is unavailable, create executable scenarios and validation instructions and clearly mark them unexecuted. Do not invent successful chaos-test results.

### 18. Operational Runbooks

Create actionable runbooks that correspond to actual services, dashboards, alerts, and recovery mechanisms.

At minimum, cover applicable operational scenarios:

- Elevated API error rate or latency.
- Video playback startup degradation.
- CDN or media-origin failure.
- Transcoding backlog or stuck jobs.
- FFmpeg worker resource exhaustion.
- Database saturation or failover.
- Redis degradation.
- Kafka consumer lag.
- Search unavailability.
- Failed deployment or rollback.
- Suspected secret exposure.
- Backup failure.
- Database restoration.
- Regional service disruption.
- Unexpected cost escalation.
- Observability pipeline failure.

Each runbook should include:

1. Symptoms and alert references.
2. Severity and potential customer impact.
3. Initial diagnostic checks.
4. Relevant dashboards and logs.
5. Safe mitigations.
6. Escalation criteria.
7. Recovery or rollback steps.
8. Verification of recovery.
9. Data-integrity checks where relevant.
10. Post-incident evidence and follow-up.

Commands must reflect the actual infrastructure and resource naming. Clearly identify placeholders for environment-specific identifiers instead of presenting invented commands as executable production procedures.

Do not include destructive recovery commands without appropriate warnings, preconditions, authorization, and verification steps.

### 19. Release Gates and Rollback Readiness

Establish explicit release gates that can be automated wherever practical.

Applicable production gates should cover:

- Required automated test results.
- Build and image provenance.
- Critical security findings.
- Infrastructure policy validation.
- Migration compatibility.
- Application health checks.
- Deployment rollout status.
- Error-rate and latency regression.
- SLO or burn-rate conditions where available.
- Required approval for sensitive production changes.
- Rollback or recovery readiness.

For stateful services, document how to respond when the code cannot be safely rolled back because of a schema, event, or data-format change.

Where canary or gradual delivery is supported, implement guardrails that can stop or roll back a release after a material degradation.

Avoid a single universal threshold that cannot account for service-specific behavior.

A release gate must fail or require the intended review when a mandatory condition fails. Do not report successful deployment simply because a deployment job submitted a request.

### 20. Alerts and Incident Response Integration

Implement actionable alerts for significant infrastructure and application risks.

Where data sources support them, cover:

- Sustained SLO burn.
- Elevated API errors.
- Video-delivery degradation.
- Queue backlog age.
- FFmpeg job failures.
- Unavailable or saturated data services.
- Database storage or connection pressure.
- Search degradation.
- CDN error increases.
- Backup failure.
- Failed release or rollback.
- Abnormal cost trends.
- Security-policy violations.

Ensure alert definitions point to relevant dashboards and runbooks.

Reduce noisy, duplicate, and non-actionable alerts. Apply appropriate grouping, pending periods, severity levels, and notification-routing boundaries according to the existing incident-management architecture.

If the project has no configured incident-management provider, define a portable alert-routing contract and document its configuration requirements without fabricating successful notifications.

Alert thresholds must be based on measured signals or explicitly labeled initial operational assumptions. Review thresholds for false positives and missed failures when test data or operational access is available.

### 21. Infrastructure Integration and Configuration Contracts

All deployment automation, dashboards, alerting rules, worker scaling policies, backup jobs, and release gates must use the established resource and environment contracts.

Preserve consistent identifiers and configuration across:

- Terraform outputs.
- Helm values.
- Kubernetes namespaces and labels.
- Application image references.
- AWS resource tags.
- Service names.
- Database and queue endpoints.
- Metrics and trace labels.
- Dashboard variables.
- Alert routing.
- Runbook resource references.
- Recovery procedures.

Where existing configuration contracts are unavailable, document explicit proposals including:

- Name and type.
- Owning component.
- Consumers.
- Secret classification.
- Required environment.
- Default or fallback behavior.
- Validation rules.
- Operational failure behavior.

Do not silently rename an established service, environment, queue, metric, or secret reference.

Keep the infrastructure implementation independently understandable and operable without requiring another coding-agent conversation.

### 22. Required Automated Tests and Validation

Implement and execute the available tests for this scope.

#### 22.1 CI/CD tests

Validate:

- Pipeline syntax.
- Required check enforcement.
- Image tagging and digest usage.
- Registry authorization.
- Deployment artifact consistency.
- Failure behavior of mandatory release gates.
- Secure CI identity configuration.
- Environment separation.

#### 22.2 Autoscaling and worker tests

Validate:

- Scaling configuration and bounds.
- Queue-metric availability.
- Worker resource constraints.
- Scale-up and scale-down policy behavior.
- Metric-source failure behavior.
- Graceful worker termination.
- Deployment rollout behavior.
- Queue recovery and retry compatibility where test infrastructure permits.

Do not claim production throughput capacity based solely on configuration tests.

#### 22.3 Observability and alert tests

Validate:

- Dashboard configuration.
- Metric queries against available test or real metric sources.
- Alert-rule syntax.
- Label and cardinality constraints where testable.
- Trace-propagation configuration.
- Redaction behavior.
- Notification-routing configuration.
- Runbook links and service references.

Where actual metric data is not available, validate configuration syntax and documented metric contracts without claiming that an operational alert fired successfully.

#### 22.4 Backup, recovery, and resilience tests

Test or validate:

- Backup configuration.
- Backup-completion detection.
- Restore-procedure automation.
- Recovery-point identification.
- Database and storage integrity checks.
- Recovery-environment configuration.
- Controlled failure scenarios.
- Abort and cleanup behavior.
- Release-gate behavior under injected failures.

Only report an actual successful restore or chaos experiment when it was executed and verified.

Run applicable Terraform formatting, validation, static analysis, Helm linting, Kubernetes validation, application tests, security scans, and build checks where tooling is available.

Document every skipped or environment-dependent validation and its reason.

### 23. Documentation and Operational Artifacts

Create or update documentation for:

- CI/CD architecture and required permissions.
- Image build, publishing, and release identification.
- Environment promotion and rollback.
- FFmpeg worker scaling and queue observability.
- Autoscaling policies.
- Service-level indicators and objectives.
- Metrics, traces, and log conventions.
- Dashboards and actionable alerts.
- CDN and media-delivery diagnostics.
- Database and stateful-service monitoring.
- Backup and restore.
- Disaster-recovery objectives and procedures.
- Regional readiness and switching.
- Security scanning and release policy.
- Capacity and cost governance.
- Chaos-test procedures.
- Incident-response runbooks.
- Release-gate requirements.
- Validation commands and test results.
- Known limitations and unresolved dependencies.

Documentation must correspond to the actual implemented configuration. Do not leave dead dashboard links, invented metric names, nonfunctional runbook references, or undocumented operational dependencies.

### 24. Explicitly Out of Scope

Do not implement the following as new systems in this milestone:

- The core application business logic.
- A replacement for the existing cloud infrastructure architecture.
- A new video-processing implementation.
- A replacement for PostgreSQL, Redis, Kafka-compatible streaming, OpenSearch, or S3.
- New recommendation algorithms.
- New web or mobile product features.
- A new payment system.
- Full active-active multi-region operation unless already explicitly supported by the established architecture and necessary for the defined recovery scope.
- Unrestricted production chaos testing.
- A new enterprise incident-management platform without an established requirement.
- An additional standalone QA or final-integration phase.

This milestone owns CI/CD and operational reliability automation, workload scaling, monitoring, recovery readiness, cost visibility, resilience validation, runbooks, and release gates. It does not replace the application or foundational infrastructure with an unrelated architecture.

### 25. Definition of Done

This milestone is complete only when all applicable criteria below are satisfied:

1. CI/CD performs the required build, test, security, and configuration checks for the relevant components.
2. Container artifacts are identifiable, controlled, and deployable by explicit image references.
3. AWS identity and production deployment permissions follow least-privilege principles.
4. Deployment automation validates rollout health and provides a documented recovery or rollback path.
5. FFmpeg worker scaling is bounded and based on appropriate workload signals.
6. Other applicable workloads have deliberate, documented autoscaling policies.
7. Application, infrastructure, queue, database, media, and CDN observability is implemented to the extent supported by the actual environment.
8. Relevant SLIs, initial SLOs, dashboards, and actionable alerting rules are defined and validated.
9. Backup and recovery procedures exist for critical data and configuration.
10. Disaster-recovery objectives, constraints, and regional-readiness procedures are explicitly documented.
11. Security scanning and mandatory release gates are integrated into applicable delivery paths.
12. Capacity and cost-visibility foundations are implemented.
13. Chaos-testing scenarios are safety-bounded and executable in suitable non-production environments.
14. Operational runbooks reflect real services, commands, dashboards, alerts, and recovery procedures.
15. Automated validation has been executed where the available environment permits.
16. Unperformed cloud-dependent, load, recovery, and chaos tests are explicitly identified rather than represented as successful.
17. Documentation accurately describes the implemented systems and remaining dependencies.
18. No placeholder production pipelines, disabled mandatory checks, hardcoded credentials, fabricated validation results, or undocumented operational assumptions remain within this scope.

### 26. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **CI/CD pipelines and release controls**
- **Container build and artifact-security implementation**
- **FFmpeg worker scaling**
- **Application autoscaling**
- **Observability and trace propagation**
- **SLIs, SLOs, dashboards, and alerts**
- **CDN and media-delivery monitoring**
- **Database, queue, and search monitoring**
- **Backup and restore implementation**
- **Disaster-recovery and regional-readiness artifacts**
- **Security validation and release gates**
- **Capacity and cost-management controls**
- **Chaos-testing scenarios**
- **Operational runbooks**
- **Tests and validations actually executed**
- **Commands and their actual results**
- **Real deployment, restore, or experiment results**, if executed
- **Documentation updated**
- **External credentials, accounts, or service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Clearly distinguish configuration created, checks successfully executed, resources deployed, recovery verified, and operational behavior confirmed. Do not claim an SLO has been achieved without measurement data or a disaster-recovery process has been verified without a successful test.

### 27. Final Execution Directive

Treat this prompt as the active implementation assignment for CI/CD, workload scaling, observability, reliability, backup and recovery, disaster-recovery readiness, capacity and cost governance, resilience testing, runbooks, and release gates for the YouTube-style video platform.

Inspect the project and infrastructure artifacts genuinely available to you. Implement the bounded scope, preserve established architecture and service contracts, execute available validations, and document the actual outcome.

Do not respond with a plan alone. Do not ask the user to choose a task. Do not implement unrelated product functionality, create unsupported infrastructure assumptions, disable mandatory security checks, perform unauthorized production experiments, or append unplanned project phases.

Deliver complete, verifiable operational engineering work that can be maintained and operated by a production engineering team.

**Begin implementation now.**
