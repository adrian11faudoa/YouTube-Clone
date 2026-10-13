# YouTube-Style Video Platform — Infrastructure Prompt — Volume 1

## AWS Cloud Foundation, Networking, Kubernetes, Data Services, Storage, and Security

### 1. Mission and Implementation Scope

Implement the foundational production infrastructure for the YouTube-style video platform on **Amazon Web Services (AWS)** using Terraform, Docker, Kubernetes, Helm, and the project's established deployment conventions.

The platform targets approximately 250 million registered users and 50 million daily active users. The infrastructure must establish a secure, repeatable, observable, and scalable foundation capable of evolving toward this target without requiring a fundamental infrastructure redesign.

This milestone covers cloud foundations, environment isolation, networking, identity and access management, Kubernetes, core data services, object storage, CDN foundations, secrets, network protection, and infrastructure deployment configuration.

The target platform includes web and mobile clients, NestJS backend services, PostgreSQL, Redis, Kafka-compatible event streaming, BullMQ workers, OpenSearch-compatible search, video-processing workloads using FFmpeg, HLS/DASH delivery, real-time communication, and supporting analytics and moderation services.

Build actual infrastructure-as-code modules, configuration, deployment resources, policies, validation, and documentation. Do not deliver merely theoretical architecture diagrams or Terraform examples that cannot be applied.

This prompt is independently executable in a fresh coding-agent conversation. Inspect the repository and available specifications genuinely accessible in the environment. Do not assume files, infrastructure, credentials, or decisions were shared between separate coding-agent conversations.

### 2. Technology Stack and Infrastructure Principles

Use the following project direction:

- **Cloud:** AWS.
- **Infrastructure as code:** Terraform.
- **Containers:** Docker.
- **Orchestration:** Amazon EKS and Kubernetes.
- **Application deployment:** Helm where appropriate.
- **Backend:** Node.js, NestJS, and TypeScript.
- **Primary database:** PostgreSQL with Prisma.
- **Cache and distributed state:** Redis.
- **Event streaming:** Kafka-compatible infrastructure, using the project's selected Amazon-managed or compatible implementation.
- **Background jobs:** BullMQ with Redis.
- **Search:** OpenSearch-compatible infrastructure.
- **Object storage:** Amazon S3.
- **CDN:** Amazon CloudFront.
- **Media processing:** FFmpeg-based workers.
- **Streaming:** HLS/DASH packaging and authorized delivery.
- **Secrets:** AWS Secrets Manager or an explicitly justified compatible mechanism.
- **Identity and access:** AWS IAM, Kubernetes service accounts, and least-privilege workload identity.
- **Security:** TLS, security groups, private networking, appropriate web application protection, encryption, and auditability.
- **Observability foundation:** OpenTelemetry-compatible instrumentation and integration points for Prometheus and Grafana.

Preserve the authoritative architecture and service contracts available in the project artifacts. Do not introduce incompatible service names, environment variables, ports, queue names, storage layouts, or IAM assumptions.

### 3. Required Deliverables

Implement the following foundational infrastructure:

1. Terraform project structure and environment isolation.
2. Secure AWS networking, subnet layout, and routing.
3. IAM roles, policies, and workload identity.
4. Amazon EKS cluster and foundational Kubernetes configuration.
5. Container registry integration and image-pull permissions.
6. PostgreSQL infrastructure and secure connectivity.
7. Redis infrastructure for cache and queue workloads.
8. Kafka-compatible event-streaming infrastructure.
9. OpenSearch infrastructure and network isolation.
10. S3 storage foundations for media, uploads, processing artifacts, and relevant platform data.
11. CloudFront distribution foundations for approved media-delivery paths.
12. Secrets management, encryption, TLS, and applicable network-protection resources.
13. Foundational ingress, service connectivity, environment configuration, and resource boundaries.
14. Infrastructure tests, security validation, deployment instructions, and operational documentation.

Infrastructure must be usable by separately developed backend, frontend, mobile, worker, and real-time components through explicit configuration and service contracts.

### 4. Infrastructure Repository Organization

Establish a maintainable Terraform structure appropriate to the repository.

Where no established structure exists, use a clear separation between reusable modules, environment-specific configuration, shared conventions, and operational documentation.

A possible structure is:

- `infrastructure/terraform/modules/` for reusable resource modules.
- `infrastructure/terraform/environments/` for environment-specific composition.
- `infrastructure/helm/` for application-platform deployment configuration within this scope.
- `infrastructure/policies/` for applicable infrastructure security policies.
- `infrastructure/tests/` for infrastructure validation and policy tests.
- `infrastructure/docs/` for configuration and operations documentation.

Adapt the structure when compatible infrastructure already exists. Do not reorganize unrelated application modules without a concrete integration need.

Requirements:

- Use strongly typed Terraform variables and outputs.
- Define input validation where useful.
- Add clear resource names, tags, and ownership metadata.
- Avoid unnecessary module indirection.
- Document module dependencies.
- Keep environment-specific values separate from reusable infrastructure logic.
- Ensure outputs expose only the non-sensitive identifiers and connection information necessary to integrate consuming services.

The infrastructure repository must not contain hardcoded production credentials, private keys, passwords, API secrets, or sensitive state data.

### 5. Environment and Account Isolation

Establish a clear separation between development, testing, staging, and production.

The infrastructure must make environment boundaries explicit and minimize accidental cross-environment access.

Requirements:

- Use isolated resource naming, tagging, and configuration.
- Separate production data and credentials from non-production environments.
- Define environment-specific network, compute, data, and storage settings.
- Ensure development and test environments cannot casually access production databases, media, or secrets.
- Document the AWS account and region assumptions.
- Support environment-specific Terraform state without relying on one mutable local state file for every environment.
- Define a safe resource-creation and destruction policy for production.
- Require appropriate controls around destructive infrastructure operations.

Where separate AWS accounts are required by the operational model, represent account boundaries explicitly rather than simulating isolation solely through resource names.

Do not automatically create new production accounts or modify organization-level settings unless the repository and execution permissions authorize that work.

### 6. Terraform State and Execution Safety

Implement secure Terraform state handling appropriate to the target deployment model.

Use a remote state backend with encryption, tightly restricted access, locking appropriate to the selected Terraform backend, and environment separation.

Where an existing remote backend is available, preserve its established configuration.

If the remote backend has not been provisioned, provide a documented and executable bootstrap procedure that does not create a circular dependency between the backend resources and their own state storage.

Requirements:

- Do not commit Terraform state files.
- Do not commit sensitive plan files.
- Do not store state-access credentials in source code.
- Document initialization and workspace or environment-selection procedures.
- Define how state backups and recovery are handled.
- Make destructive changes visible during planning.
- Avoid broad state manipulation or resource replacement without justification.
- Prefer additive and reversible changes for production resources.
- Document provider versions and required tooling.

Run `terraform fmt`, `terraform validate`, and appropriate static checks where tooling is available. Do not claim that a plan or apply succeeded unless the command was actually executed successfully.

### 7. AWS Networking Foundation

Design and implement a secure network topology appropriate for the platform's services.

Where the existing architecture calls for a VPC, implement:

- VPC address-space configuration.
- Availability Zone distribution.
- Public subnets only for components that require public network entry or egress.
- Private application subnets.
- Isolated or restricted data subnets where appropriate.
- Route tables and associations.
- Internet gateway configuration where required.
- NAT or other controlled egress architecture.
- VPC endpoints for suitable AWS services where justified.
- Security groups with explicit ingress and egress rules.
- DNS and service-discovery integration as appropriate.
- Load-balancer subnet configuration.
- Network-flow visibility where configured.

Avoid unnecessarily exposing worker nodes, databases, Redis, Kafka brokers, OpenSearch, internal APIs, or administrative endpoints to the public internet.

Do not automatically assign public IP addresses to workloads that have no legitimate requirement for them.

#### 7.1 Connectivity boundaries

Define how the following components communicate:

- Public ingress and the application cluster.
- Backend services and PostgreSQL.
- Backend services and Redis.
- Event producers and Kafka-compatible brokers.
- Workers and object storage.
- Search clients and OpenSearch.
- Applications and internal telemetry endpoints.
- CloudFront and authorized object-storage origins.

Use the authoritative port and protocol requirements when provided. Do not invent incompatible application ports.

Document network flows and ensure security-group rules permit only required communication.

### 8. IAM and Workload Identity

Implement least-privilege AWS identity configuration.

Use IAM roles and the selected EKS workload-identity mechanism to grant permissions to the workloads that need them.

Where appropriate, configure:

- EKS cluster and node roles.
- Workload-specific roles.
- Container-registry access.
- S3 access for upload, processing, and approved delivery workflows.
- Secrets retrieval.
- Relevant database or supporting AWS service access.
- Infrastructure deployment roles.
- Read-only operational access.
- CI identities when a supported CI environment exists.

Do not use a single unrestricted role for every service.

Separate permissions for media upload, video processing, thumbnail generation, content delivery, search indexing, and operational administration when these responsibilities have different access requirements.

Requirements:

- Avoid wildcard permissions when practical.
- Scope resource permissions to appropriate ARNs.
- Use short-lived credentials and workload identity rather than embedded access keys.
- Avoid sharing production credentials with development workloads.
- Document trust relationships and permission boundaries.
- Validate that an application does not need to embed cloud credentials in its mobile or web bundle.

Do not commit AWS access keys or require static production credentials to build client applications.

### 9. Amazon EKS and Kubernetes Foundation

Implement an Amazon EKS cluster and its foundational Kubernetes configuration.

Use private networking for workloads where appropriate and define the cluster's API-access policy according to the actual administrative requirements.

Configure:

- Supported cluster and node configuration.
- Availability Zone distribution.
- Managed node groups or an explicitly justified compute alternative.
- Cluster networking.
- Workload identity.
- Required cluster add-ons.
- Resource tagging and ownership.
- Namespace boundaries.
- Service accounts.
- RBAC foundations.
- Network-policy integration where supported by the selected CNI and configuration.
- Container resource requests and limits.
- Application health-check conventions.
- Pod disruption and availability settings for applicable critical workloads.
- Deployment configuration compatible with rolling updates.

Select supported, compatible AWS and Kubernetes configurations based on the project requirements and available tooling. Do not blindly pin obsolete Kubernetes versions or unavailable add-on versions.

#### 9.1 Workload placement

Provide a deployment foundation suitable for distinct workload categories, including:

- API and web-facing backend services.
- Event consumers.
- Queue workers.
- FFmpeg media-processing workers.
- Search indexing jobs.
- Scheduled maintenance jobs.
- Realtime services.
- Supporting internal workloads.

Use node selectors, taints, tolerations, autoscaling boundaries, or separate node groups when there is a clear operational or resource-isolation benefit.

Media-processing workloads can be CPU-, memory-, disk-, and network-intensive. Prevent them from exhausting resources required by latency-sensitive APIs.

Do not implement all backend application code in this infrastructure milestone.

### 10. Container Registry and Image Supply Chain

Implement integration with the project's container registry, using Amazon ECR when consistent with the established architecture.

Provide:

- Repository configuration for applicable container images.
- Appropriate image-pull permissions.
- Immutable or otherwise controlled image-tag practices.
- Lifecycle policies.
- Encryption configuration.
- Image retention settings.
- Least-privilege access.
- A clear separation between production and non-production image permissions where required.

Where the CI system is already present, preserve its existing integration points. Otherwise, document the required identity and image-publication interface without inventing a working CI pipeline in this scope.

Do not use mutable convenience tags such as `latest` as the only production deployment identifier.

Do not place credentials inside Docker images or committed image-pull secrets.

### 11. PostgreSQL Infrastructure

Implement the PostgreSQL infrastructure foundation using the project's approved database deployment model.

If managed PostgreSQL is the selected architecture, configure Amazon RDS or Aurora PostgreSQL as appropriate to documented requirements. Do not migrate an established self-managed database to a different service without authorization.

Cover:

- Private networking.
- Encryption at rest.
- Encrypted connections where supported.
- Authentication and credential management.
- High availability according to environment.
- Backup retention and recovery foundations.
- Parameter-group configuration where justified.
- Storage sizing and growth considerations.
- Monitoring integration.
- Maintenance settings.
- Database subnet groups.
- Access restrictions.
- Connection and service-discovery configuration.

Distinguish development settings from production settings.

Production must not rely on an unprotected publicly accessible database or credentials baked into application images.

Document the database endpoints and secret references required by application workloads, but do not expose actual passwords in Terraform outputs, logs, or deployment manifests.

Do not generate or modify application Prisma models and database migrations merely to provision PostgreSQL infrastructure. Those responsibilities belong to the relevant application scope unless a small infrastructure compatibility artifact is explicitly necessary.

### 12. Redis Infrastructure

Provide the Redis foundation needed for caching, distributed state, rate-limiting support where applicable, and BullMQ workloads.

Use the established Redis deployment architecture. Where a managed service is selected, configure an appropriate AWS-managed Redis-compatible service rather than silently introducing a different compatibility model.

Define:

- Private network access.
- Authentication and encryption.
- Subnet and security-group configuration.
- Appropriate availability settings by environment.
- Resource sizing.
- Eviction and capacity considerations.
- Monitoring.
- Maintenance and recovery behavior.
- Secret integration.
- Client connection configuration.

Caching and BullMQ can have different persistence, eviction, latency, and isolation requirements. Do not blindly force them into one shared Redis deployment when doing so creates an unacceptable reliability or data-loss boundary.

If separate deployments are warranted, make the separation explicit and document the operational trade-off.

Do not invent Redis key schemas or application cache semantics in this infrastructure scope. Provide the infrastructure connectivity and configuration required by the established applications.

### 13. Kafka-Compatible Event Streaming

Implement the foundational event-streaming infrastructure using the project's selected Kafka-compatible service.

Choose the managed or self-managed approach based on the established architecture, supported AWS services, operational requirements, and cost considerations.

Provide:

- Secure client connectivity.
- Appropriate private networking.
- Authentication and authorization.
- Encryption in transit.
- Encryption at rest where applicable.
- Environment separation.
- Monitoring and capacity visibility.
- Retention and storage configuration.
- Access control for producers, consumers, and operators.
- Bootstrap-server configuration.
- Secret references where needed.

Document compatibility assumptions and the responsibilities of application teams for event schemas, delivery semantics, idempotency, ordering, retries, and dead-letter handling.

Do not create an unbounded number of Kafka topics or invent incompatible event definitions merely to populate the infrastructure.

Do not expose streaming brokers publicly without a justified requirement and suitable controls.

### 14. BullMQ and Background-Worker Infrastructure

Provide the Kubernetes and Redis foundations required for BullMQ workers and other queue-based background processing.

Support workloads such as:

- Media-processing tasks.
- Thumbnail-generation tasks.
- Search-indexing jobs.
- Notification delivery tasks.
- Analytics processing.
- Maintenance and reconciliation jobs.

The actual job schemas and consumer implementations remain application responsibilities.

Configure the infrastructure needed for:

- Worker deployment.
- Resource requests and limits.
- Graceful termination.
- Health checks.
- Retry-compatible shutdown behavior.
- Controlled concurrency.
- Log collection.
- Metrics integration.
- Environment-specific worker scaling boundaries.

Do not scale workers blindly based only on CPU if the established queue metrics provide a more appropriate signal.

Avoid a deployment configuration where terminating a pod routinely causes acknowledged jobs to be lost or external operations to be repeated unsafely.

Do not implement the BullMQ job processors in this infrastructure prompt.

### 15. OpenSearch Infrastructure

Provision the OpenSearch foundation through the selected supported AWS deployment model.

Configure:

- Private connectivity.
- Authentication and authorization.
- Encryption.
- Appropriate instance or capacity configuration.
- Storage sizing.
- Availability settings.
- Snapshot and recovery foundations where available.
- Monitoring and alerting integration points.
- Client endpoint configuration.
- Restricted administrative access.

Separate search workloads from the PostgreSQL primary application database. Do not use OpenSearch as a replacement for authoritative relational persistence.

Document the integration settings required by indexing workers and search services.

Do not invent production index mappings, analyzer definitions, ranking functions, or recommendation algorithms in this infrastructure milestone unless an existing artifact requires a concrete compatibility setting.

### 16. Object Storage and Media Infrastructure

Implement S3 storage foundations for the platform's media lifecycle.

Support appropriate storage responsibilities, including:

- Original or uploaded video media.
- Processed media variants.
- HLS/DASH packaging artifacts.
- Video thumbnails.
- Channel avatars and other approved images.
- Captions and subtitles where applicable.
- Temporary processing artifacts.
- Other documented application-owned media.

Use separate buckets or explicitly defined isolation boundaries when required by privacy, retention, access-control, or lifecycle differences.

Requirements:

- Block public access by default.
- Apply encryption at rest.
- Restrict write and read access through least-privilege policies.
- Define versioning where appropriate.
- Define lifecycle policies where appropriate.
- Configure multipart-upload and incomplete-upload cleanup.
- Set retention and deletion behavior according to the authoritative media lifecycle.
- Configure CORS only where browser clients require it.
- Avoid exposing internal bucket names and object keys unnecessarily.
- Preserve ownership boundaries and application authorization semantics.

Do not grant blanket access to all buckets to every backend service.

Do not configure media buckets as publicly readable merely to simplify playback. Delivery must follow the platform's authorized media-access architecture.

### 17. CloudFront and Authorized Media Delivery

Implement CloudFront foundations for approved media delivery.

Integrate the CDN with the established storage and authorization architecture. Use the appropriate origin access configuration and prevent unauthorized direct origin access.

Where required, support:

- HTTPS.
- Secure origin access.
- Cache behaviors for documented media paths.
- Correct MIME-type and range-request behavior.
- HLS/DASH manifest and segment delivery.
- Thumbnail caching.
- Cache-control configuration.
- Invalidation or versioned-asset deployment strategies.
- Logging and diagnostic integration.
- Geographic behavior and restrictions where required by product policy.

If private media requires signed access, configure the infrastructure and policy integration for the chosen authorization mechanism.

Do not invent signed URL formats or authorization claims incompatible with the backend.

Do not make private videos publicly retrievable by changing cache settings without the corresponding access-control model.

Distinguish between a CDN's ability to cache content and the application's authority to grant a user access to that content.

### 18. Secrets, Encryption, and TLS

Implement the infrastructure foundation for secure secret and certificate management.

Use the approved AWS secrets and key-management services.

Cover:

- Database credentials.
- Redis credentials.
- Event-streaming credentials where applicable.
- External integration secrets.
- Application secret references.
- Encryption keys.
- TLS certificates.
- Rotation-compatible configuration.
- Access restrictions.
- Auditability.

Prefer secret references and runtime retrieval over placing raw values in committed configuration.

Ensure sensitive Terraform attributes and state access are handled appropriately. Mark sensitive outputs, but do not assume that a Terraform `sensitive` flag encrypts or removes values from state.

Define how Kubernetes workloads obtain secrets without placing secret values in ordinary Helm values files or public container metadata.

Configure TLS for applicable ingress and service endpoints. Prefer secure TLS defaults and document certificate ownership and renewal responsibilities.

Do not create fake production secrets or claim certificate issuance succeeded without an accessible certificate authority and successful execution.

### 19. Ingress, WAF, and Public Exposure

Implement a controlled ingress foundation for web-facing and API-facing services.

Use the established AWS load-balancer and ingress architecture. Configure public entry points only for components that legitimately require internet access.

Where required, provide:

- Load balancers.
- HTTPS listener foundations.
- Certificate references.
- Routing integration.
- Health-check conventions.
- Web application firewall configuration.
- Applicable request-size and timeout settings.
- Access logging.
- Security-group integration.
- Restrictions on administrative endpoints.

WebSockets and realtime connections must be supported through an ingress configuration compatible with the application's transport and timeout requirements.

Do not apply overly restrictive generic limits that break legitimate uploads, streaming authorization, or realtime connections. Document service-specific limits and protect high-cost operations with appropriate controls.

Do not expose PostgreSQL, Redis, Kafka brokers, OpenSearch administrative endpoints, or internal Kubernetes APIs through general public ingress.

### 20. Storage, Database, and Service Connectivity Contracts

Provide clear, portable configuration interfaces for the application and infrastructure components.

Define how the environment supplies:

- Database connection configuration.
- Redis endpoints and credentials.
- Kafka-compatible bootstrap endpoints and authorization.
- OpenSearch endpoints.
- S3 bucket and region identifiers.
- CloudFront distribution and approved delivery configuration.
- Container image references.
- Kubernetes service endpoints.
- Secrets-manager references.
- Application environment identifiers.
- Required network and TLS settings.

Follow the project's established environment-variable and configuration names where they exist.

When names or contracts are missing, document proposed names, expected types, secret classifications, consumers, and default behavior.

Do not emit raw secret values as Terraform outputs.

Do not silently rename existing application settings or introduce incompatible endpoint assumptions across services.

### 21. Cost, Capacity, and Scale Foundations

Design the infrastructure for the stated long-term platform scale while keeping the current deployment economically realistic.

Consider:

- Kubernetes compute and node utilization.
- Media-transcoding CPU and memory consumption.
- Storage growth.
- CDN bandwidth and request volume.
- Database capacity and connection demand.
- Redis memory and workload isolation.
- Event-stream retention and throughput.
- Search-index growth.
- Logging and telemetry ingestion.
- NAT and inter-zone data transfer costs.
- Backup storage.
- High-availability requirements.
- Regional expansion requirements.

Use configurable sizing and environment-specific capacity choices.

Avoid prematurely provisioning the full theoretical global capacity when the current environment cannot justify its cost.

The infrastructure must preserve a credible scaling path through documented boundaries and configuration, not through unsupported claims that a small initial deployment can already handle the full target.

Document major cost drivers and any deliberate single-region or reduced-capacity assumptions.

Do not introduce advanced infrastructure solely for its sophistication when a simpler, secure, supportable AWS service meets the requirement.

### 22. Infrastructure Security and Compliance Foundations

Implement appropriate infrastructure safeguards throughout the deployment.

Requirements include:

- Least-privilege IAM.
- Private application and data networks.
- Encryption at rest and in transit.
- Secure secret storage.
- Restricted administrative access.
- Audit logging where appropriate.
- Container image access restrictions.
- Secure default storage policies.
- Environment separation.
- Infrastructure-policy validation.
- Resource ownership and tagging.
- Network boundaries.
- Controlled public ingress.
- Prevention of accidental public exposure.
- Appropriate workload resource limits.

Use applicable infrastructure scanning and policy tools that are already present or are justified by the repository.

Do not claim certification or compliance with a regulatory standard simply because some associated controls are configured.

Document controls implemented, external dependencies, and items that require organizational or account-level setup.

### 23. Infrastructure Validation and Testing

Implement automated infrastructure validation appropriate to the codebase.

Include relevant checks such as:

- Terraform formatting and validation.
- Provider and module compatibility.
- Static analysis.
- Terraform plan review.
- Infrastructure policy testing.
- IAM and network-policy checks.
- Helm linting and template rendering where applicable.
- Kubernetes manifest validation.
- Configuration consistency checks.
- Secret-scanning validation.
- Resource dependency checks.
- Validation of required environment outputs.

Where an existing infrastructure test framework is available, reuse it. Otherwise, add proportionate validation tools that can run in a local or CI environment without requiring unrestricted production access.

Do not fabricate a successful plan or apply result.

If AWS credentials or account permissions are unavailable, complete offline validation, document the exact outstanding account-dependent checks, and provide clear execution instructions.

Do not create, modify, or destroy live production resources merely to demonstrate that Terraform commands exist.

### 24. Deployment and Operational Documentation

Create or update the infrastructure documentation describing:

- Repository and module structure.
- Required Terraform, AWS, Docker, Kubernetes, and Helm tooling.
- AWS account and region assumptions.
- Remote-state setup and recovery.
- Environment initialization.
- Required identity and permissions.
- Network architecture.
- EKS configuration.
- Data-service connectivity.
- Media storage and CDN integration.
- Secret and certificate management.
- Ingress and public-exposure policy.
- Resource sizing and environment variations.
- Validation commands.
- Deployment and rollback considerations within this scope.
- Known limitations and external dependencies.

Provide useful example configuration files with non-sensitive values and explanations. Never include usable production credentials.

Document the distinction between infrastructure being defined in code, a Terraform plan being generated, resources being applied, and a deployed workload being operational.

### 25. Explicitly Out of Scope

Do not implement the following in this milestone:

- Application business logic.
- Backend APIs or database-domain migrations.
- Video transcoding worker implementations.
- Search indexing application code.
- Analytics aggregation logic.
- Recommendation algorithms.
- Web or React Native feature screens.
- Payment-provider integration.
- Complete CI/CD and release orchestration.
- Full SLO dashboards, alert policies, chaos testing, and disaster-recovery exercises beyond foundational hooks and configurations.
- A complete multi-region active-active platform.
- An unrelated replacement of the established infrastructure architecture.
- Additional architecture, implementation, or QA prompt phases.

Those capabilities must integrate with the infrastructure through documented interfaces. This prompt owns the AWS and Kubernetes foundations required for the platform, not every application or operational system that will eventually run on them.

### 26. Definition of Done

This milestone is complete only when all applicable criteria below are satisfied:

1. The Terraform structure and environment boundaries are implemented.
2. Remote state, execution safety, and environment configuration are documented and validated as far as the available environment permits.
3. AWS networking and access boundaries are implemented.
4. IAM and workload identity follow least-privilege principles.
5. EKS and foundational Kubernetes configuration are implemented.
6. PostgreSQL, Redis, Kafka-compatible infrastructure, and OpenSearch infrastructure are provisioned or fully defined through the established deployment model.
7. S3 and CloudFront configurations support the documented media architecture.
8. Secrets, encryption, TLS, and public-ingress safeguards are implemented.
9. Application-service connectivity requirements are represented through clear configuration contracts.
10. Infrastructure resources have appropriate ownership, tagging, and environment-specific settings.
11. Capacity and cost assumptions are documented and configurable.
12. Automated infrastructure validation is available and executed where possible.
13. Documentation explains the actual infrastructure, deployment requirements, and unresolved dependencies.
14. Environment-dependent operations that could not be performed are explicitly identified.
15. No hardcoded production secrets, broadly exposed sensitive services, placeholder infrastructure modules, or unexplained deployment assumptions remain within the assigned scope.

### 27. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Terraform modules and environment composition**
- **Networking and IAM implementation**
- **EKS and Kubernetes foundation**
- **PostgreSQL, Redis, event-streaming, and search infrastructure**
- **S3 and CloudFront configuration**
- **Secrets, TLS, ingress, and security controls**
- **Service configuration contracts**
- **Capacity and cost considerations**
- **Tests and validation checks created**
- **Commands actually executed**
- **Terraform validation and plan results**
- **Helm and Kubernetes validation results**
- **Deployment status**, clearly distinguishing code from applied resources
- **Documentation created or updated**
- **External account, credential, or service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Report only results supported by actual execution. Distinguish resources defined in Terraform from resources deployed to AWS, and distinguish a successful plan from an applied and operational environment.

### 28. Final Execution Directive

Treat this prompt as the active implementation assignment for the YouTube-style video platform's foundational AWS and Kubernetes infrastructure.

Inspect the repository and infrastructure artifacts genuinely available in the execution environment. Implement the complete bounded scope, preserve established architecture and service contracts, run the available validations, and document the actual outcome.

Do not respond with a plan alone. Do not ask the user to choose a task. Do not implement unrelated application features, invent unavailable cloud resources, hardcode credentials, or create unplanned project phases.

Deliver a secure, maintainable, operationally realistic infrastructure foundation that can be validated and deployed through the authorized environment.

**Begin implementation now.**
