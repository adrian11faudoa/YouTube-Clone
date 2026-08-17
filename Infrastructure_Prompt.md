Using the Master Prompt above and the approved:

Architecture Prompt Volume 1
Architecture Prompt Volume 2
Completed backend implementation
Completed frontend and mobile implementation
Existing Project Index

Begin the Infrastructure, DevOps, Observability, Testing, and Deployment phase.

Do NOT restart the project.

Do NOT regenerate completed application code unless an infrastructure integration change requires it.

Use the approved architecture and existing implementation as the source of truth.

────────────────────────────────────────

IMPLEMENTATION OBJECTIVE

Build the complete production-ready infrastructure required to deploy, operate, monitor, secure, scale, and recover the Enterprise YouTube-Style Video Platform.

The infrastructure must support:

• Global users
• Millions of videos
• High-volume uploads
• Large-scale video processing
• Adaptive video streaming
• Live streaming
• Real-time live chat
• Search
• Recommendations
• Notifications
• Creator analytics
• Advertising
• Monetization
• Moderation
• Administration

Design for:

• Horizontal scaling
• High availability
• Multi-region expansion
• Zero-downtime deployments
• Disaster recovery
• Infrastructure automation
• Secure operations
• Observability
• Cost-aware scaling

────────────────────────────────────────

PRIMARY INFRASTRUCTURE STACK

Use the approved architecture and implement production-ready infrastructure using:

Containerization:

• Docker
• Multi-stage Docker builds

Local Development:

• Docker Compose

Orchestration:

• Kubernetes

Packaging:

• Helm

Infrastructure as Code:

• Terraform

CI/CD:

• GitHub Actions

Cloud Architecture:

• AWS-compatible architecture unless the approved architecture specifies another provider

Compute:

• Kubernetes worker nodes
• Autoscaling node groups where applicable

Database:

• PostgreSQL

Caching:

• Redis

Event Streaming:

• Kafka or Redpanda

Background Processing:

• BullMQ workers

Search:

• Elasticsearch or OpenSearch

Object Storage:

• AWS S3-compatible storage

CDN:

• CloudFront or approved CDN

Secrets:

• HashiCorp Vault or approved secrets architecture

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Security:

• TLS
• Network policies
• IAM / least privilege
• Secret management
• Container security
• Supply-chain security

────────────────────────────────────────

INFRASTRUCTURE PRINCIPLES

Implement infrastructure according to the following principles:

• Infrastructure as Code
• Immutable deployments
• Declarative configuration
• Environment isolation
• Least privilege
• Defense in depth
• Zero-trust service boundaries where practical
• Horizontal scalability
• Stateless application services where possible
• Automated recovery
• Observability by default
• Secure defaults
• Cost visibility
• Reproducible environments

Do not rely on undocumented manual production steps.

Every production infrastructure component must be reproducible from version-controlled configuration.

────────────────────────────────────────

ENVIRONMENT STRATEGY

Implement separate environments for:

• Local
• Development
• Staging
• Production

Support environment-specific:

• Configuration
• Domains
• Secrets
• Resource sizing
• Scaling
• External integrations
• Feature flag environments

Never hard-code production credentials.

Never commit secrets.

────────────────────────────────────────

MILESTONE GROUP 1 — INFRASTRUCTURE FOUNDATION

Implement:

• Infrastructure repository structure
• Docker standards
• Shared Docker build strategy
• Environment configuration
• Terraform foundation
• Provider configuration
• Remote state architecture
• State locking
• Environment separation
• Naming conventions
• Resource tagging
• Base IAM architecture
• Base networking architecture

Generate documentation for required deployment configuration.

────────────────────────────────────────

MILESTONE GROUP 2 — DOCKER

Create production-ready Dockerfiles for:

• API Gateway
• Authentication Service
• User Service
• Channel Service
• Video Service
• Media Service
• Video Processing Workers
• Streaming-related control services
• Search Service
• Recommendation Service
• Notification Service
• Live Streaming control services
• Live Chat Service
• Moderation Service
• Copyright Service
• Advertising Service
• Monetization Service
• Analytics Service
• Administration Service
• Web application
• Other implemented services

Requirements:

• Multi-stage builds
• Minimal runtime images
• Non-root users
• Production dependency installation
• Build caching optimization
• Health check compatibility
• Signal handling
• Graceful shutdown support

Do not include development dependencies unnecessarily in production images.

────────────────────────────────────────

MILESTONE GROUP 3 — LOCAL DEVELOPMENT

Implement Docker Compose for local development.

Support:

• PostgreSQL
• Redis
• Kafka or Redpanda
• Elasticsearch or OpenSearch
• Object storage emulator where appropriate
• Application services required for development
• Video processing workers
• Observability components where practical

Provide:

• Development overrides
• Persistent volumes where appropriate
• Health checks
• Dependency startup ordering
• Local environment configuration

The local environment should allow developers to run the platform without manually installing every infrastructure dependency.

────────────────────────────────────────

MILESTONE GROUP 4 — NETWORK ARCHITECTURE

Implement Terraform networking.

Design:

• VPC
• Public subnets
• Private application subnets
• Private data subnets
• Availability zones
• Internet gateway
• NAT architecture
• Route tables
• Security groups
• Network ACL strategy where appropriate
• Private service communication

Production application and data services must not be unnecessarily exposed to the public internet.

────────────────────────────────────────

MILESTONE GROUP 5 — KUBERNETES FOUNDATION

Implement Kubernetes infrastructure for:

• Namespaces
• Resource quotas
• Limit ranges
• Service accounts
• RBAC
• Network policies
• ConfigMaps
• Secret integration
• Services
• Deployments
• StatefulSets where required
• Jobs
• CronJobs

Separate workloads according to environment and operational responsibility.

────────────────────────────────────────

MILESTONE GROUP 6 — APPLICATION DEPLOYMENTS

Create Kubernetes and Helm configurations for every implemented application.

Each service deployment must include where applicable:

• Deployment
• Service
• ServiceAccount
• ConfigMap references
• Secret references
• Resource requests
• Resource limits
• Liveness probes
• Readiness probes
• Startup probes
• Graceful termination configuration
• Pod disruption budgets
• Autoscaling configuration

Support independent service deployment.

Do not require redeploying the entire platform when only one service changes.

────────────────────────────────────────

MILESTONE GROUP 7 — AUTOSCALING

Implement:

• Horizontal Pod Autoscaler
• Metrics-based scaling
• CPU scaling
• Memory scaling
• Queue-depth scaling for workers where appropriate
• Custom metrics integration where appropriate

Design scaling policies for:

• API services
• Video processing workers
• Upload processing
• Search services
• Recommendation services
• Live chat
• Analytics ingestion

Avoid scaling policies that create excessive infrastructure thrashing.

────────────────────────────────────────

MILESTONE GROUP 8 — DATABASE INFRASTRUCTURE

Implement production PostgreSQL infrastructure.

Support:

• Primary database
• Read replicas where required
• Automated backups
• Point-in-time recovery where supported
• Encryption
• Monitoring
• Connection management
• Connection pooling
• Maintenance windows
• Upgrade strategy

Define recovery objectives for:

• RPO
• RTO

Do not expose database instances publicly.

────────────────────────────────────────

MILESTONE GROUP 9 — REDIS INFRASTRUCTURE

Implement Redis infrastructure.

Support approved use cases including:

• Caching
• Distributed coordination
• Rate limiting
• Sessions where approved
• Queue dependencies
• Temporary state

Implement:

• High availability where required
• Persistence strategy where required
• Monitoring
• Backup strategy where applicable
• Memory policies
• Eviction policy appropriate to workload

Do not treat Redis as the authoritative source of transactional data unless explicitly approved.

────────────────────────────────────────

MILESTONE GROUP 10 — EVENT STREAMING

Deploy and configure Kafka or Redpanda.

Implement:

• Cluster configuration
• Topic configuration
• Replication
• Partition strategy
• Retention
• Consumer groups
• Access control
• Encryption
• Monitoring
• Capacity planning

Create infrastructure support for approved event domains including:

• Identity
• Video lifecycle
• Media processing
• Playback
• Search indexing
• Recommendations
• Notifications
• Live streaming
• Analytics
• Moderation
• Copyright
• Advertising
• Monetization

────────────────────────────────────────

MILESTONE GROUP 11 — BACKGROUND JOB INFRASTRUCTURE

Implement infrastructure for BullMQ workers.

Support:

• Dedicated worker deployments
• Queue-specific concurrency
• Autoscaling
• Retry configuration
• Dead-letter handling
• Monitoring
• Resource isolation

Prioritize independent scaling of:

• Video transcoding
• Thumbnail generation
• Preview generation
• Media processing
• Notification delivery
• Search indexing
• Analytics aggregation
• Moderation processing

────────────────────────────────────────

MILESTONE GROUP 12 — OBJECT STORAGE

Implement production object storage architecture.

Support separate storage boundaries for:

• Original uploads
• Processed video renditions
• HLS manifests
• DASH manifests where approved
• Thumbnails
• Preview assets
• Subtitle files
• Channel assets
• Advertising media
• Temporary uploads

Implement:

• Bucket policies
• IAM access
• Encryption
• Lifecycle rules
• Versioning where required
• Cleanup policies
• Access logging
• Signed URL architecture

Separate temporary and permanent media lifecycles.

────────────────────────────────────────

MILESTONE GROUP 13 — CDN AND MEDIA DELIVERY

Implement CDN architecture.

Support:

• Global media delivery
• Cache behaviors
• Origin configuration
• Signed access where required
• Manifest caching
• Video segment caching
• Thumbnail caching
• Image caching
• Cache invalidation strategy

Configure CDN behavior separately for:

• Public assets
• Protected assets
• Short-lived signed content
• Streaming manifests
• Media segments

Do not use the application servers as high-bandwidth video delivery proxies.

────────────────────────────────────────

MILESTONE GROUP 14 — VIDEO PROCESSING INFRASTRUCTURE

Implement infrastructure specifically for FFmpeg and media processing workloads.

Support:

• Dedicated worker node pools where appropriate
• CPU-intensive workloads
• Memory-intensive workloads
• Temporary processing storage
• Horizontal worker scaling
• Queue-driven execution
• Job isolation
• Retry behavior
• Failure cleanup
• Processing metrics

Design for future support of:

• GPU acceleration
• Hardware transcoding
• Specialized media processing nodes

Do not require GPU infrastructure unless the current implementation requires it.

────────────────────────────────────────

MILESTONE GROUP 15 — LIVE STREAMING INFRASTRUCTURE

Implement infrastructure boundaries for:

• Stream ingestion
• Stream processing
• Transcoding
• Packaging
• HLS generation
• Live delivery
• Recording
• VOD generation

Separate the live streaming data plane from normal application APIs.

Design for independent scaling.

────────────────────────────────────────

MILESTONE GROUP 16 — REAL-TIME INFRASTRUCTURE

Implement infrastructure for:

• Live chat
• WebSockets
• Socket.IO where approved
• Connection scaling
• Redis adapter where applicable
• Sticky session requirements if necessary
• Connection recovery
• Load balancing
• Graceful connection draining

Support independent scaling for high-connection workloads.

────────────────────────────────────────

MILESTONE GROUP 17 — SEARCH INFRASTRUCTURE

Deploy and configure Elasticsearch or OpenSearch.

Implement:

• Cluster configuration
• Index templates
• Lifecycle policies
• Sharding
• Replication
• Snapshot strategy
• Access controls
• Monitoring
• Capacity planning

Support indexes for:

• Videos
• Channels
• Playlists
• Live streams
• Topics
• Search suggestions

────────────────────────────────────────

MILESTONE GROUP 18 — RECOMMENDATION INFRASTRUCTURE

Implement infrastructure support for:

• Recommendation API workloads
• Candidate retrieval workloads
• Ranking workloads
• Feature storage boundaries where approved
• Batch processing
• Offline processing
• Event ingestion

Design recommendation infrastructure so algorithms can evolve without requiring a complete infrastructure redesign.

────────────────────────────────────────

MILESTONE GROUP 19 — ANALYTICS INFRASTRUCTURE

Implement scalable analytics infrastructure.

Support:

• Event ingestion
• Stream processing boundaries
• Aggregation workers
• Long-term analytics storage where approved
• Creator analytics
• Platform analytics
• Operational analytics

Define:

• Retention policies
• Aggregation schedules
• Backfill procedures
• Data recovery procedures

Do not overload transactional PostgreSQL workloads with large-scale analytics queries.

────────────────────────────────────────

MILESTONE GROUP 20 — SECRETS MANAGEMENT

Implement secrets architecture using:

• HashiCorp Vault

or the approved production secrets system.

Support:

• Database credentials
• API credentials
• JWT signing secrets
• Encryption keys
• Object storage credentials
• Payment provider secrets
• OAuth credentials
• Third-party service credentials

Implement:

• Secret rotation
• Least privilege
• Kubernetes integration
• Audit logging
• Environment separation

Never place long-lived production secrets directly in GitHub Actions configuration or source control.

────────────────────────────────────────

MILESTONE GROUP 21 — TLS AND EDGE SECURITY

Implement:

• TLS certificates
• Certificate renewal
• HTTPS enforcement
• Secure headers
• CDN security
• WAF where approved
• DDoS protection boundaries
• Rate limiting architecture
• Bot protection integration boundaries

Protect:

• Public APIs
• Authentication endpoints
• Upload authorization endpoints
• Administrative interfaces
• WebSocket endpoints

────────────────────────────────────────

MILESTONE GROUP 22 — KUBERNETES SECURITY

Implement:

• Namespace isolation
• RBAC
• Service accounts
• Least privilege
• Network policies
• Pod security standards
• Read-only root filesystems where practical
• Non-root containers
• Capability restrictions
• Resource quotas
• Secret injection

Prevent unnecessary east-west traffic between unrelated services.

────────────────────────────────────────

MILESTONE GROUP 23 — OBSERVABILITY FOUNDATION

Implement:

• OpenTelemetry Collector
• Metrics collection
• Distributed tracing
• Centralized logging
• Log correlation
• Correlation IDs
• Trace IDs
• Grafana dashboards

Integrate:

• Prometheus
• Grafana
• Loki
• Tempo

All major services must expose observable health and performance signals.

────────────────────────────────────────

MILESTONE GROUP 24 — METRICS

Create production metrics for:

Application:

• Request rate
• Error rate
• Latency
• Saturation
• Authentication failures
• Rate limiting

Video:

• Upload throughput
• Upload failures
• Processing duration
• Processing failures
• Queue depth
• Playback authorization
• Playback event ingestion

Live:

• Concurrent streams
• Concurrent viewers
• Active WebSocket connections
• Chat throughput
• Connection failures

Infrastructure:

• CPU
• Memory
• Disk
• Network
• Pod restarts
• Database connections
• Cache utilization
• Kafka lag
• Search cluster health

────────────────────────────────────────

MILESTONE GROUP 25 — LOGGING

Implement centralized logging.

Requirements:

• Structured JSON logs
• Correlation IDs
• Trace IDs
• Service identification
• Environment identification
• Log levels
• Retention policies
• Searchable logs

Never log:

• Passwords
• Authentication tokens
• Payment secrets
• Private keys
• Sensitive personal data unnecessarily

────────────────────────────────────────

MILESTONE GROUP 26 — TRACING

Implement distributed tracing for critical flows:

• Registration
• Login
• Video upload
• Upload completion
• Video processing
• Video publishing
• Playback authorization
• Playback event ingestion
• Search
• Recommendations
• Notifications
• Live streaming
• Live chat
• Payments
• Moderation actions

Trace propagation must work across approved service boundaries and asynchronous event flows where supported.

────────────────────────────────────────

MILESTONE GROUP 27 — ALERTING

Create alerting rules for:

Critical:

• Application unavailable
• Database unavailable
• Kafka unavailable
• Redis unavailable
• Search unavailable
• Object storage failures
• High authentication failures

Warning:

• Increased error rates
• High latency
• Queue backlog
• Processing failures
• Kafka consumer lag
• Database saturation
• Memory pressure
• Disk pressure

Avoid alert fatigue.

Every critical alert should have a clear operational meaning.

────────────────────────────────────────

MILESTONE GROUP 28 — GRAFANA DASHBOARDS

Generate dashboards for:

• Platform Overview
• API Gateway
• Authentication
• Video Uploads
• Video Processing
• Playback
• Search
• Recommendations
• Live Streaming
• Live Chat
• Notifications
• Payments
• Moderation
• Database
• Redis
• Kafka
• Kubernetes
• CDN and media delivery

────────────────────────────────────────

MILESTONE GROUP 29 — CI

Implement GitHub Actions workflows.

Support:

• Dependency installation
• Type checking
• Linting
• Unit tests
• Integration tests
• Contract tests
• Build verification
• Docker image builds
• Security scanning
• Dependency scanning
• Secret scanning
• Container scanning

Pull requests must validate application quality before merge.

────────────────────────────────────────

MILESTONE GROUP 30 — CD

Implement deployment workflows.

Support:

• Development deployment
• Staging deployment
• Production deployment
• Environment promotion
• Image versioning
• Helm deployment
• Deployment verification
• Rollback

Production deployment must support:

• Rolling updates
• Zero-downtime deployment where architecture allows
• Health validation
• Automatic rollback boundaries

────────────────────────────────────────

MILESTONE GROUP 31 — DATABASE MIGRATIONS

Implement safe migration workflows.

Support:

• Migration validation
• Staging migration
• Production migration
• Backward-compatible changes
• Expand/contract migration strategy
• Rollback strategy where possible

Do not automatically apply destructive database changes without explicit safeguards.

────────────────────────────────────────

MILESTONE GROUP 32 — BACKUPS AND DISASTER RECOVERY

Implement:

• PostgreSQL backups
• Point-in-time recovery
• Object storage protection
• Search snapshots
• Infrastructure state protection
• Configuration recovery
• Disaster recovery procedures

Define:

• Recovery Point Objective
• Recovery Time Objective

Generate recovery runbooks.

────────────────────────────────────────

MILESTONE GROUP 33 — MULTI-REGION STRATEGY

Implement infrastructure foundations for future or approved multi-region deployment.

Define:

• Regional clusters
• Traffic routing
• Global DNS
• CDN distribution
• Data residency boundaries
• Database replication strategy
• Event replication considerations
• Regional failover
• Service recovery

Do not prematurely introduce active-active complexity unless required by the approved architecture.

────────────────────────────────────────

MILESTONE GROUP 34 — COST MANAGEMENT

Implement cost-awareness measures.

Include:

• Resource requests and limits
• Autoscaling
• Storage lifecycle policies
• CDN caching
• Worker scaling
• Environment sizing
• Monitoring of expensive workloads

Identify major cost drivers including:

• Video storage
• Video transcoding
• CDN bandwidth
• Live streaming
• Search
• Analytics
• Kafka
• Database replication

────────────────────────────────────────

MILESTONE GROUP 35 — SECURITY AND SUPPLY CHAIN

Implement CI/CD and infrastructure security controls.

Include:

• Dependency scanning
• Container image scanning
• Secret scanning
• SBOM generation where supported
• Image provenance where supported
• Signed artifacts where supported
• Base image update strategy
• Vulnerability remediation process

────────────────────────────────────────

MILESTONE GROUP 36 — PERFORMANCE AND LOAD TESTING

Implement infrastructure and test tooling for:

• API load testing
• Video upload testing
• Playback authorization testing
• Search load testing
• Recommendation load testing
• WebSocket load testing
• Live chat load testing
• Queue stress testing

Define:

• Test environments
• Test data strategy
• Success thresholds
• Bottleneck identification
• Capacity planning process

Do not execute destructive load tests against production.

────────────────────────────────────────

MILESTONE GROUP 37 — OPERATIONAL RUNBOOKS

Generate operational documentation for:

• Service deployment
• Rollback
• Database recovery
• Kafka incidents
• Redis incidents
• Search incidents
• Video processing backlog
• CDN failures
• Object storage failures
• WebSocket incidents
• Live streaming incidents
• Security incidents
• Secret rotation
• Disaster recovery

Runbooks must contain actionable procedures.

────────────────────────────────────────

TESTING REQUIREMENTS

Generate infrastructure validation for:

• Terraform validation
• Terraform formatting
• Helm linting
• Kubernetes manifest validation
• Docker image builds
• Container security scanning
• Deployment smoke tests
• Health checks
• Rollback validation where possible

Include automated verification in CI/CD.

────────────────────────────────────────

IMPLEMENTATION ORDER

Implement infrastructure incrementally.

Suggested milestone sequence:

MILESTONE 1 — Infrastructure Foundation
MILESTONE 2 — Docker and Local Development
MILESTONE 3 — Terraform Networking and IAM
MILESTONE 4 — Kubernetes Foundation
MILESTONE 5 — Application Deployments and Helm
MILESTONE 6 — PostgreSQL and Redis Infrastructure
MILESTONE 7 — Kafka/Redpanda and BullMQ Infrastructure
MILESTONE 8 — Object Storage and CDN
MILESTONE 9 — Video Processing Infrastructure
MILESTONE 10 — Live Streaming and Real-Time Infrastructure
MILESTONE 11 — Elasticsearch/OpenSearch
MILESTONE 12 — Recommendation and Analytics Infrastructure
MILESTONE 13 — Secrets and Security
MILESTONE 14 — Observability Foundation
MILESTONE 15 — Metrics, Logging, Tracing, and Dashboards
MILESTONE 16 — Alerting
MILESTONE 17 — CI
MILESTONE 18 — CD
MILESTONE 19 — Database Migration Automation
MILESTONE 20 — Backup and Disaster Recovery
MILESTONE 21 — Multi-Region Strategy
MILESTONE 22 — Performance and Load Testing
MILESTONE 23 — Operational Runbooks and Production Readiness

Adjust the exact sequence only when dependency requirements make a different order necessary.

────────────────────────────────────────

MILESTONE EXECUTION RULES

For every milestone:

1. Define the exact scope.
2. Identify infrastructure files to create.
3. Identify existing files requiring modification.
4. Generate complete implementations.
5. Validate integration with the application architecture.
6. Generate infrastructure validation and tests.
7. Update the Project Index.
8. Stop.

Do not automatically begin the next milestone.

Wait for approval.

────────────────────────────────────────

CURRENT STARTING POINT

Start with:

INFRASTRUCTURE MILESTONE 1 — FOUNDATION

Implement the minimum coherent production-ready infrastructure foundation, including:

• Infrastructure repository structure
• Terraform root structure
• Environment separation
• Provider configuration
• Remote state architecture
• State locking configuration
• Naming conventions
• Resource tagging
• Base environment configuration
• Base IAM architecture
• Base networking architecture
• Infrastructure validation foundation
• Initial documentation

Respect the approximate 20–40 file milestone limit from the Master Prompt.

If the complete foundation requires more files, prioritize a coherent foundation that compiles and validates successfully, then continue the remaining infrastructure foundation work in the next milestone.

────────────────────────────────────────

PROJECT INDEX

After every milestone update:

• Current phase
• Current milestone
• Completed infrastructure components
• Generated files
• Modified files
• Cloud resources
• Kubernetes resources
• CI/CD workflows
• Monitoring and observability components
• Security controls
• Backup and recovery components
• Remaining work
• Exact next milestone

Never lose track of previously completed infrastructure.

────────────────────────────────────────

FINAL PRODUCTION READINESS CHECKLIST

Before declaring the infrastructure phase complete, verify:

• All services can be deployed reproducibly.
• Environments are isolated.
• Secrets are not committed.
• Application containers run as non-root where practical.
• Kubernetes workloads have health probes.
• Resource limits and requests are configured.
• Autoscaling is configured where required.
• Database backup and recovery procedures exist.
• Kafka/Redpanda recovery procedures exist.
• Redis failure behavior is documented.
• Search snapshots are configured.
• Object storage lifecycle policies are configured.
• CDN behavior is configured correctly.
• Metrics are collected.
• Logs are centralized.
• Distributed traces are available.
• Alerts are actionable.
• CI validates code and infrastructure.
• CD supports controlled deployments and rollback.
• Security scanning is integrated.
• Disaster recovery procedures are documented.
• Production load testing has defined thresholds.
• Operational runbooks exist.

────────────────────────────────────────

STOP CONDITION

Start only with:

INFRASTRUCTURE MILESTONE 1 — FOUNDATION

After completing the milestone:

• Verify all generated infrastructure files are internally consistent.
• Verify Terraform configuration is valid.
• Verify the infrastructure structure supports the approved architecture.
• Update the Project Index.
• Identify the exact next milestone.

STOP.

Wait for explicit approval before continuing.
