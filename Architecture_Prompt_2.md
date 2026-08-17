Using the approved Project 5 — Enterprise YouTube-Style Video Platform Architecture Prompt — Volume 1, the resulting architecture, Project Index, and the Master Prompt above:

Continue the architecture phase.

This is Architecture Prompt — Volume 2.

Do NOT restart Architecture Volume 1.

Do NOT repeat previously generated architecture.

Continue from the exact approved stopping point.

The purpose of this volume is to complete the enterprise architecture required before backend implementation begins.

Do NOT implement backend application code yet.

Do NOT implement frontend or mobile application code yet.

Do NOT generate infrastructure implementation files yet.

────────────────────────────────────────

ARCHITECTURE CONSISTENCY

Use Architecture Volume 1 as the source of truth.

Maintain consistency with the approved:

• Domain decomposition
• Service boundaries
• Service ownership
• Data ownership
• Event architecture
• API architecture
• Authentication architecture
• Authorization architecture
• Video lifecycle
• Upload architecture
• Processing architecture
• Streaming architecture
• Live streaming architecture
• Search architecture
• Recommendation architecture
• Deployment strategy

If a decision from Volume 1 requires refinement:

1. Identify the existing decision.
2. Explain the reason for refinement.
3. Preserve backward compatibility with the approved architecture whenever possible.
4. Update the Project Index.

Do not silently redesign previously approved architecture.

────────────────────────────────────────

COMPLETE DATABASE ARCHITECTURE

Expand the database design into a complete enterprise-grade data architecture.

Define ownership and storage strategy for:

• Users
• Profiles
• Authentication identities
• Sessions
• Devices
• Channels
• Channel members
• Channel permissions
• Videos
• Video versions
• Video metadata
• Video assets
• Video renditions
• Processing jobs
• Thumbnails
• Subtitles
• Captions
• Audio tracks
• Playlists
• Playlist items
• Subscriptions
• Likes
• Reactions
• Comments
• Comment threads
• Watch history
• Playback progress
• Saved videos
• Notifications
• Notification preferences
• Search synchronization
• Recommendations
• Creator analytics
• Video analytics
• Advertising
• Campaigns
• Ad inventory
• Ad impressions
• Ad delivery
• Monetization
• Revenue records
• Payments
• Payouts
• Moderation
• Reports
• Trust and safety actions
• Copyright claims
• Copyright ownership
• Feature flags
• Audit logs
• API clients
• Developer integrations

For every major entity define:

• Owning service
• Primary identifier strategy
• Relationships
• Foreign-key boundaries
• Indexing strategy
• Partitioning strategy where appropriate
• Retention policy
• Archival policy
• Deletion policy
• Privacy requirements

────────────────────────────────────────

POSTGRESQL SCHEMA DESIGN

Generate the detailed PostgreSQL schema design.

Include:

• Tables
• Columns
• Data types
• Primary keys
• Foreign keys where appropriate
• Unique constraints
• Check constraints
• Indexes
• Composite indexes
• Partial indexes where appropriate
• Timestamp strategy
• Soft deletion where justified
• Versioning strategy where needed
• Tenant or ownership boundaries where applicable

Do not create foreign-key coupling across independently owned microservice databases when it violates service boundaries.

Document:

• Which data is strongly consistent.
• Which data is eventually consistent.
• Which data is event-derived.
• Which data is denormalized for performance.

────────────────────────────────────────

PRISMA ARCHITECTURE

Define the Prisma strategy.

Specify:

• Prisma schema organization
• Database ownership per service
• Migration ownership
• Shared versus service-local types
• Transaction boundaries
• Connection pooling
• Read/write patterns
• Read replicas where appropriate

Do not create one giant Prisma schema that tightly couples unrelated services.

Each service must own its database schema or clearly defined bounded context.

────────────────────────────────────────

DATABASE SCALING

Design scaling strategies for high-volume entities.

Address:

• Video metadata
• Views
• Watch history
• Playback events
• Analytics events
• Comments
• Reactions
• Notifications
• Advertising impressions
• Recommendation signals
• Search synchronization events

Define when to use:

• PostgreSQL
• Redis
• Kafka or Redpanda
• Elasticsearch or OpenSearch
• Object storage
• Analytical storage where architecturally justified

Do not overload PostgreSQL with workloads better handled asynchronously or by specialized systems.

────────────────────────────────────────

VIDEO VIEW ARCHITECTURE

Design a scalable view-counting system.

Support:

• High-volume view ingestion
• Duplicate prevention
• Fraud detection boundaries
• Delayed aggregation
• Near-real-time counters
• Eventually consistent totals
• Redis-based hot counters where appropriate
• Kafka event ingestion
• Persistent aggregation

Define:

• What constitutes a valid view.
• Idempotency strategy.
• Deduplication strategy.
• Aggregation windows.
• Anti-fraud integration boundaries.

Do not perform synchronous relational writes for every playback event at massive scale.

────────────────────────────────────────

WATCH HISTORY AND PLAYBACK EVENTS

Design high-throughput architecture for:

• Playback started
• Playback progress
• Playback paused
• Playback resumed
• Playback completed
• Video abandoned

Support:

• Batched ingestion
• Event streaming
• Privacy controls
• History deletion
• Pause history
• Resume playback
• Recommendation signal generation

Define data retention and deletion propagation.

────────────────────────────────────────

RECOMMENDATION ARCHITECTURE

Complete the recommendation system architecture.

Define:

### Data Sources

• Watch history
• Playback duration
• Completion rate
• Likes
• Reactions
• Comments
• Shares
• Saves
• Subscriptions
• Search activity
• Channel interactions
• Topic interactions
• Content metadata
• Popularity
• Freshness

### Recommendation Pipeline

Design:

1. Event ingestion
2. Feature generation
3. Candidate generation
4. Candidate filtering
5. Ranking
6. Re-ranking
7. Diversity
8. Exploration
9. Policy filtering
10. Response generation

Define boundaries between:

• Online serving
• Offline processing
• Feature generation
• Experimentation
• Model evaluation

The architecture must support replacing or improving ranking models without rewriting the core platform.

────────────────────────────────────────

RECOMMENDATION SAFETY

Design safeguards for:

• Repetitive content
• Filter bubbles
• Unsafe content
• Age-restricted content
• Blocked channels
• Muted topics
• Moderation decisions
• Copyright restrictions
• User privacy settings

Recommendation outputs must respect authorization, moderation, safety, and privacy policies.

────────────────────────────────────────

SEARCH ARCHITECTURE

Expand Elasticsearch or OpenSearch architecture.

Define indexes for:

• Videos
• Channels
• Creators
• Playlists
• Live streams
• Topics
• Categories
• Hashtags where supported

For each index define:

• Mapping
• Analyzers
• Tokenization strategy
• Autocomplete fields
• Ranking fields
• Filtering fields
• Sorting fields
• Denormalized fields
• Index lifecycle
• Reindexing strategy
• Event synchronization strategy

Define the search ingestion pipeline.

Support eventual consistency between transactional data and search indexes.

────────────────────────────────────────

SEARCH RANKING

Define ranking signals including:

• Text relevance
• Watch count
• Engagement
• Freshness
• Channel authority
• Personalization
• Language
• Geographic relevance where appropriate
• Safety and moderation state

Separate search ranking policy from the core transactional video service.

────────────────────────────────────────

VIDEO DELIVERY SECURITY

Define authorization for:

• Public videos
• Private videos
• Unlisted videos
• Age-restricted videos
• Subscriber-only content where supported
• Paid content where supported
• Geographic restrictions
• Copyright restrictions

Define:

• Playback authorization
• Signed URLs
• Signed cookies where appropriate
• Token expiration
• CDN authorization
• Manifest protection
• Segment access strategy

Do not expose private media through permanently public URLs.

────────────────────────────────────────

CONTENT DELIVERY ARCHITECTURE

Define the full delivery path:

User
→ Edge/CDN
→ Playback authorization
→ Manifest
→ Video segments

Address:

• Origin shielding
• Cache hierarchy
• Cache keys
• Signed access
• Geographic routing
• Origin failover
• Segment caching
• Live stream delivery
• Cache invalidation

Design for massive global read traffic.

────────────────────────────────────────

LIVE STREAMING ARCHITECTURE

Complete the live streaming architecture.

Define the lifecycle:

1. Stream creation
2. Stream scheduling
3. Stream key generation
4. Broadcaster authentication
5. Stream ingestion
6. Validation
7. Transcoding
8. Packaging
9. CDN delivery
10. Viewer interaction
11. Moderation
12. Recording
13. Stream completion
14. VOD conversion
15. Analytics

Define service boundaries for:

• Ingestion
• Processing
• Packaging
• Delivery
• Chat
• Viewer metrics
• Moderation

────────────────────────────────────────

LIVE CHAT

Design scalable real-time live chat.

Support:

• Messages
• Reactions
• Replies where appropriate
• Moderation
• Slow mode
• Subscriber-only mode
• Creator moderation
• Moderator roles
• Bans
• Message deletion
• Spam detection

Define:

• WebSocket architecture
• Horizontal scaling
• Redis coordination
• Rate limiting
• Message ordering
• Persistence strategy
• Retention policy

────────────────────────────────────────

ADVERTISING ARCHITECTURE

Design an enterprise advertising domain.

Support:

• Advertisers
• Advertising organizations
• Ad accounts
• Campaigns
• Ad groups
• Advertisements
• Creative assets
• Video advertisements
• Targeting
• Budgets
• Scheduling
• Frequency controls
• Delivery constraints
• Reporting

Define clear boundaries between:

• Campaign management
• Targeting
• Ad selection
• Ad delivery
• Impression tracking
• Click tracking
• Billing
• Reporting

────────────────────────────────────────

AD DELIVERY

Design low-latency ad delivery.

Support:

• Video pre-roll
• Mid-roll
• Post-roll
• Display placements where approved
• Live-stream advertising
• Frequency capping
• Targeting
• Eligibility filtering
• Auction architecture where justified
• Experimentation

Define fallback behavior when advertising infrastructure is unavailable.

Video playback must not fail because an advertisement cannot be served.

────────────────────────────────────────

MONETIZATION ARCHITECTURE

Design monetization features supporting:

• Advertising revenue
• Creator revenue sharing
• Paid subscriptions where approved
• Channel memberships where approved
• One-time purchases where approved
• Donations or tips where approved

Define:

• Revenue calculation
• Ledger architecture
• Payment integration boundaries
• Payout scheduling
• Creator balances
• Tax integration boundaries
• Fraud detection boundaries
• Dispute handling
• Auditability

Financial calculations must not rely exclusively on mutable cached values.

────────────────────────────────────────

PAYMENT SECURITY

Design secure payment integration.

Support:

• Payment provider integration
• Webhook verification
• Idempotency
• Payment state transitions
• Refunds where applicable
• Chargeback handling boundaries
• Audit logging

Do not store unnecessary payment card data.

Use provider-hosted or tokenized payment flows.

────────────────────────────────────────

CREATOR ANALYTICS

Design analytics for:

• Views
• Watch time
• Audience retention
• Unique viewers
• Subscribers gained
• Subscribers lost
• Revenue
• Traffic sources
• Geographic distribution
• Device distribution
• Content performance
• Live stream metrics

Define:

• Event collection
• Aggregation
• Storage
• Query models
• Refresh frequency
• Data retention

Separate high-volume analytics ingestion from transactional APIs.

────────────────────────────────────────

ANALYTICS ARCHITECTURE

Design a general analytics pipeline.

Support:

• Product analytics
• Video analytics
• Creator analytics
• Advertising analytics
• Operational analytics
• Business metrics

Define:

Event producers
→ Kafka or Redpanda
→ Stream processing or workers
→ Aggregation
→ Analytical storage
→ Query APIs
→ Dashboards

Select analytical storage only where justified.

Do not introduce technology without clear operational value.

────────────────────────────────────────

CONTENT MODERATION ARCHITECTURE

Design the complete moderation workflow.

Support:

• User reports
• Video reports
• Comment reports
• Channel reports
• Automated detection
• Manual review
• Policy decisions
• Enforcement actions
• Appeals
• Moderator notes
• Evidence retention
• Audit trails

Define content states such as:

• Draft
• Processing
• Pending review
• Published
• Restricted
• Age restricted
• Demonetized
• Blocked
• Removed
• Under appeal

All moderation state transitions must be auditable.

────────────────────────────────────────

TRUST AND SAFETY

Design architecture for:

• Spam detection
• Bot detection
• Account abuse
• View fraud
• Engagement fraud
• Upload abuse
• API abuse
• Harassment reporting
• Coordinated abuse detection

Define:

• Detection signals
• Risk scoring boundaries
• Enforcement integration
• Rate limiting
• Temporary restrictions
• Permanent actions
• Appeals

────────────────────────────────────────

COPYRIGHT MANAGEMENT

Design a copyright management domain.

Support:

• Rights holders
• Copyright ownership records
• Reference media
• Claims
• Disputes
• Appeals
• Geographic restrictions
• Monetization claims
• Blocking policies

Define a scalable media fingerprinting integration boundary.

Do not assume all fingerprinting technology must be built directly into the first-party application.

Design provider or internal service integration points.

────────────────────────────────────────

NOTIFICATION ARCHITECTURE

Complete notification design.

Support:

• New videos
• Channel subscriptions
• Comments
• Replies
• Live stream reminders
• Live stream start notifications
• Moderation actions
• Copyright actions
• Monetization events
• Security alerts

Channels:

• Push
• Email
• In-app
• Web

Define:

• Notification preferences
• Deduplication
• Rate limiting
• Priority
• Retry
• Delivery tracking
• Failure handling

────────────────────────────────────────

AUTHORIZATION MODEL

Define enterprise authorization.

Support roles such as:

• Viewer
• Creator
• Channel Owner
• Channel Manager
• Channel Editor
• Moderator
• Administrator
• Support Operator
• Advertiser
• Advertising Manager
• Rights Holder
• Developer

Define:

• RBAC
• Resource-level authorization
• Ownership checks
• Service-to-service authorization
• Administrative boundaries
• Principle of least privilege

Do not depend solely on frontend role checks.

────────────────────────────────────────

API ARCHITECTURE

Define complete API boundaries.

Organize APIs for:

• Authentication
• Users
• Profiles
• Channels
• Videos
• Uploads
• Playback
• Playlists
• Subscriptions
• Comments
• Interactions
• Search
• Discovery
• Recommendations
• Live streaming
• Live chat
• Notifications
• Creator Studio
• Advertising
• Monetization
• Payments
• Moderation
• Copyright
• Administration
• Developer APIs

For every API category define:

• Authentication requirements
• Authorization requirements
• Pagination
• Filtering
• Sorting
• Error model
• Idempotency where required
• Rate limits

Generate an OpenAPI strategy.

────────────────────────────────────────

API GATEWAY

Define API Gateway responsibilities.

Support:

• Routing
• Authentication integration
• Authorization boundaries
• Rate limiting
• Request validation
• Request size limits
• Correlation IDs
• Observability
• API versioning
• Public versus internal APIs

Do not move domain business logic into the API Gateway.

────────────────────────────────────────

WEBHOOK ARCHITECTURE

Support secure webhooks for approved developer and partner integrations.

Define:

• Event subscriptions
• Signing
• Verification
• Retry policies
• Idempotency
• Delivery logs
• Dead-letter handling
• Replay support
• Rate limits

────────────────────────────────────────

FEATURE FLAGS

Design feature flag architecture.

Support:

• Feature definitions
• Environment targeting
• User targeting
• Percentage rollouts
• Kill switches
• Experiments
• Audit logs

Feature flag failure must have safe fallback behavior.

────────────────────────────────────────

ADMINISTRATION ARCHITECTURE

Define administration boundaries.

Support:

• User administration
• Channel administration
• Video administration
• Moderation management
• Copyright administration
• Advertising administration
• Monetization administration
• Feature flags
• System configuration
• Audit logs

Administrative operations must require explicit authorization and produce audit records.

────────────────────────────────────────

SECURITY ARCHITECTURE

Complete the platform security model.

Address:

• Authentication security
• Token security
• Session security
• Passkeys
• MFA
• OAuth
• API security
• Rate limiting
• DDoS boundaries
• File upload security
• Malware scanning
• MIME validation
• Content validation
• Object storage security
• CDN security
• Encryption in transit
• Encryption at rest
• Secret management
• Service identity
• Network isolation
• Audit logging
• Dependency security
• Container security

Apply OWASP best practices.

────────────────────────────────────────

PRIVACY ARCHITECTURE

Define privacy controls for:

• Profile visibility
• Channel visibility
• Watch history
• Search history
• Recommendations
• Personalization
• Analytics
• Advertising preferences
• Data export
• Account deletion

Define:

• Data access boundaries
• Data retention
• Data deletion
• Eventual deletion propagation
• Backup deletion limitations
• Audit requirements

────────────────────────────────────────

MULTI-REGION ARCHITECTURE

Design global deployment strategy.

Address:

• Regional traffic routing
• Stateless service scaling
• Database primary and replica strategy
• Read locality
• Object storage replication
• CDN delivery
• Event streaming replication where required
• Regional failure
• Failover
• Failback

Do not introduce globally distributed strong consistency unless the domain requires it.

────────────────────────────────────────

DISASTER RECOVERY

Define recovery objectives for major components.

Establish:

• RPO targets
• RTO targets

Cover:

• PostgreSQL
• Redis
• Kafka or Redpanda
• Search
• Object storage
• Kubernetes
• CDN
• DNS
• Video processing
• Live streaming

Generate recovery strategies and operational requirements.

────────────────────────────────────────

OBSERVABILITY ARCHITECTURE

Define complete observability.

Support:

Metrics:

• API latency
• Error rates
• Upload throughput
• Processing duration
• Transcoding failures
• CDN performance
• Playback failures
• Live stream health
• WebSocket connections
• Search latency
• Recommendation latency
• Queue depth
• Kafka consumer lag

Logs:

• Structured logging
• Correlation IDs
• Trace IDs
• Privacy-aware logging

Tracing:

• API requests
• Service calls
• Upload lifecycle
• Video processing pipeline
• Playback authorization
• Live streaming lifecycle
• Kafka event flows
• Background jobs

────────────────────────────────────────

SLO ARCHITECTURE

Define initial SLIs and SLOs for:

• API availability
• Authentication
• Video upload success
• Video processing success
• Video playback startup
• Streaming availability
• Live streaming availability
• Search latency
• Recommendation availability
• Notification delivery

Define error-budget concepts for deployment decisions.

────────────────────────────────────────

FINAL ARCHITECTURE REQUIREMENTS

Generate and finalize:

1. Complete detailed ERD
2. Database ownership matrix
3. PostgreSQL schema design
4. Prisma strategy
5. Partitioning strategy
6. Data retention strategy
7. Redis key-space and caching strategy
8. Kafka or Redpanda topic catalog
9. Event versioning strategy
10. Dead-letter strategy
11. BullMQ queue catalog
12. Elasticsearch or OpenSearch mappings
13. Search synchronization architecture
14. Recommendation system architecture
15. Video upload state machine
16. Video processing state machine
17. Video delivery architecture
18. Live streaming lifecycle
19. Live chat architecture
20. Advertising architecture
21. Monetization architecture
22. Payment architecture
23. Creator analytics architecture
24. Moderation architecture
25. Trust and Safety architecture
26. Copyright architecture
27. Notification architecture
28. Complete authorization model
29. API contract strategy
30. API Gateway architecture
31. WebSocket architecture
32. Webhook architecture
33. Feature flag architecture
34. Administration architecture
35. Security architecture
36. Privacy architecture
37. Multi-region deployment architecture
38. Disaster recovery strategy
39. Observability architecture
40. SLI/SLO strategy
41. Capacity and scaling strategy
42. Updated Project Index

────────────────────────────────────────

ARCHITECTURE VALIDATION

Before completing this architecture phase, validate:

• Every service has a clear responsibility.
• Every service has defined data ownership.
• Cross-service communication is explicitly defined.
• Event producers and consumers are documented.
• No circular service dependencies exist.
• High-volume workloads have scalable ingestion paths.
• Video uploads do not unnecessarily pass through API servers.
• Video processing is asynchronous.
• Playback delivery uses CDN architecture.
• Private content is protected.
• Live streaming has defined failure boundaries.
• Search is eventually synchronized correctly.
• Recommendations respect privacy and moderation.
• Financial data has auditability.
• Administrative actions are audited.
• Secrets are never part of application configuration files.
• Multi-region failure scenarios are documented.
• Disaster recovery objectives are defined.
• Observability covers critical workflows.
• The architecture supports future expansion.

────────────────────────────────────────

PROJECT INDEX

Update the living Project Index with:

• Current phase
• Completed architecture components
• Approved services
• Service ownership
• Database ownership
• Event catalog
• API domains
• Queue catalog
• Search indexes
• Video processing stages
• Streaming architecture
• Live streaming architecture
• Recommendation components
• Advertising components
• Monetization components
• Moderation components
• Copyright components
• Security decisions
• Privacy decisions
• Deployment decisions
• Disaster recovery decisions
• Remaining implementation work

Also identify the exact next phase:

Project 5 — Enterprise YouTube-Style Video Platform
Backend Prompt

────────────────────────────────────────

STOP CONDITION

After completing Architecture Volume 2:

STOP.

Do not begin backend implementation.

Wait for explicit approval.

The next implementation phase must be:

Project 5 — Enterprise YouTube-Style Video Platform
Backend Prompt
