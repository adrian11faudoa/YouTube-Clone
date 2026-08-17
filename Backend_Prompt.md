Using the Master Prompt above and the approved:

Architecture Prompt Volume 1
Architecture Prompt Volume 2

Existing Project Index

Begin the backend implementation phase.

Do NOT restart or regenerate the architecture.

Use the approved architecture as the source of truth.

────────────────────────────────────────

IMPLEMENTATION OBJECTIVE

Build the complete production-grade backend for the enterprise-scale global video platform.

The backend must support the approved domains, including:

• Identity
• Authentication
• Authorization
• Users
• Profiles
• Channels
• Videos
• Uploads
• Media
• Video Processing
• Streaming
• Live Streaming
• Playlists
• Subscriptions
• Interactions
• Comments
• Search
• Discovery
• Recommendations
• Notifications
• Advertising
• Monetization
• Payments
• Creator Analytics
• Moderation
• Trust and Safety
• Copyright
• Administration
• Feature Flags
• Audit
• Developer Platform

Implement incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

Every milestone must compile successfully before continuing.

Do not skip implementation details.

Do not use placeholders.

Do not use TODO comments.

Do not generate pseudocode.

Do not regenerate completed files unless modifications are required.

────────────────────────────────────────

BACKEND TECHNOLOGY STACK

Use the approved architecture and the following technologies unless a previously approved architectural decision specifies otherwise:

Runtime:

• Node.js
• TypeScript
• Strict TypeScript configuration

Framework:

• NestJS

Database:

• PostgreSQL
• Prisma ORM

Caching and Coordination:

• Redis

Event Streaming:

• Kafka or Redpanda

Background Jobs:

• BullMQ

Search:

• Elasticsearch or OpenSearch

Object Storage:

• AWS S3-compatible storage

Video Processing:

• FFmpeg

Realtime:

• WebSockets
• Socket.IO where approved

Authentication:

• JWT
• Refresh Tokens
• OAuth where configured
• Passkeys where implemented
• MFA where implemented

Payments:

• Stripe or approved payment provider abstraction

Observability:

• OpenTelemetry
• Prometheus-compatible metrics
• Structured logging
• Distributed tracing

API Documentation:

• OpenAPI / Swagger

Testing:

• Unit tests
• Integration tests
• Contract tests where appropriate
• End-to-end tests for critical flows

────────────────────────────────────────

MONOREPO IMPLEMENTATION

Implement the backend according to the approved monorepo architecture.

Maintain clear separation between:

• Applications
• Services
• Workers
• Shared packages
• Infrastructure libraries
• API contracts
• Event contracts
• Database packages
• Observability packages
• Configuration packages
• Testing utilities

Do not create a generic shared package containing unrelated business logic.

Shared packages must have explicit ownership and purpose.

────────────────────────────────────────

IMPLEMENTATION ORDER

Implement the backend in dependency-aware milestones.

Use approximately the following order unless the approved architecture requires a different dependency sequence.

MILESTONE GROUP 1 — FOUNDATION

Implement:

1. Monorepo configuration
2. TypeScript configuration
3. ESLint
4. Prettier
5. Environment configuration
6. Configuration validation
7. Shared error architecture
8. Structured logging
9. Correlation IDs
10. Request tracing
11. OpenTelemetry foundation
12. Health checks
13. Readiness checks
14. Graceful shutdown
15. Shared API response conventions
16. Shared pagination utilities
17. Authentication primitives
18. Authorization primitives
19. Database infrastructure
20. Redis infrastructure
21. Kafka or Redpanda infrastructure
22. BullMQ infrastructure
23. Object storage infrastructure

The first milestone must establish a stable foundation for all subsequent services.

────────────────────────────────────────

MILESTONE GROUP 2 — IDENTITY AND AUTHENTICATION

Implement:

• User registration
• Login
• Logout
• Password hashing
• Email verification
• Password reset
• Password changes
• JWT issuance
• Refresh token rotation
• Session management
• Device management
• Token revocation
• Suspicious session detection boundaries
• OAuth architecture where approved
• MFA architecture where approved
• Passkey architecture where approved

Security requirements:

• Secure password hashing
• Refresh token rotation
• Token reuse detection
• Session revocation
• Secure cookie support where applicable
• Rate limiting
• Brute-force protection
• Audit logging
• Input validation

────────────────────────────────────────

MILESTONE GROUP 3 — AUTHORIZATION

Implement:

• RBAC
• Permission definitions
• Resource-level authorization
• Ownership checks
• Channel permissions
• Administrative permissions
• Service-to-service authorization boundaries

Support approved roles including:

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

Authorization must be enforced server-side.

────────────────────────────────────────

MILESTONE GROUP 4 — USERS AND PROFILES

Implement:

• User retrieval
• User updates
• Profile management
• Avatar management
• Privacy settings
• Notification preferences
• Account status
• Blocked users
• Muted users
• Data access boundaries

Implement validation, authorization, auditing, and tests.

────────────────────────────────────────

MILESTONE GROUP 5 — CHANNELS

Implement:

• Channel creation
• Channel updates
• Channel branding
• Channel metadata
• Channel visibility
• Channel managers
• Channel members
• Channel roles
• Channel permissions
• Featured content
• Channel sections where approved

Every channel operation must enforce resource-level authorization.

────────────────────────────────────────

MILESTONE GROUP 6 — VIDEO DOMAIN

Implement the complete video lifecycle.

Support:

• Video creation
• Draft videos
• Metadata updates
• Titles
• Descriptions
• Tags
• Categories
• Visibility
• Public videos
• Private videos
• Unlisted videos
• Scheduled publishing
• Age restrictions
• Publishing
• Archiving
• Deletion

Implement explicit video state transitions.

Do not allow invalid lifecycle transitions.

────────────────────────────────────────

MILESTONE GROUP 7 — VIDEO UPLOADS

Implement production-ready uploads.

Support:

• Upload session creation
• Signed upload URLs
• Multipart uploads
• Resumable uploads where supported
• Upload validation
• MIME validation
• File size validation
• Upload ownership
• Upload expiration
• Upload cancellation
• Idempotent completion

The backend must not proxy large video files unnecessarily.

Use direct-to-object-storage upload architecture.

────────────────────────────────────────

MILESTONE GROUP 8 — MEDIA AND OBJECT STORAGE

Implement:

• Object storage abstraction
• Signed URL generation
• Upload authorization
• Download authorization
• Object lifecycle integration
• Metadata persistence
• Asset ownership validation
• Private object access
• Public delivery boundaries

Support assets including:

• Source videos
• Processed videos
• Thumbnails
• Preview images
• Subtitles
• Captions
• Audio assets
• Channel images
• Advertising media

────────────────────────────────────────

MILESTONE GROUP 9 — VIDEO PROCESSING

Implement the asynchronous video processing pipeline.

Use Kafka or Redpanda events and BullMQ jobs according to the approved architecture.

Implement stages including:

1. Upload completion
2. Validation
3. Malware scanning integration boundary
4. Metadata extraction
5. Media inspection
6. Transcoding job creation
7. FFmpeg processing
8. Rendition generation
9. HLS generation
10. DASH generation where approved
11. Thumbnail generation
12. Preview generation
13. Subtitle processing
14. Processing completion
15. Processing failure
16. Retry handling
17. Dead-letter handling

Implement explicit processing states.

Workers must be idempotent.

Failures must be recoverable.

────────────────────────────────────────

VIDEO PROCESSING REQUIREMENTS

Generate configurable rendition profiles.

Support source-dependent generation for resolutions such as:

• 144p
• 240p
• 360p
• 480p
• 720p
• 1080p
• 1440p
• 2160p

Do not generate resolutions larger than the source unless explicitly required by approved processing policy.

Implement:

• Job retries
• Timeout handling
• Worker concurrency configuration
• Processing locks where required
• Idempotency
• Cleanup of failed artifacts
• Metrics
• Structured logging

────────────────────────────────────────

MILESTONE GROUP 10 — VIDEO PLAYBACK

Implement backend support for:

• Playback authorization
• Playback metadata
• Manifest access
• Public playback
• Private playback
• Unlisted playback
• Age-restricted playback
• Geographic restrictions where approved
• Signed playback access
• CDN integration boundaries

Do not expose permanently public URLs for protected content.

────────────────────────────────────────

MILESTONE GROUP 11 — STREAMING

Implement the backend contracts required for:

• HLS manifests
• DASH manifests where approved
• Adaptive bitrate metadata
• Rendition selection
• Playback authorization
• Stream expiration
• CDN integration

The CDN should handle high-volume media delivery.

Backend APIs should primarily handle authorization, metadata, and control-plane responsibilities.

────────────────────────────────────────

MILESTONE GROUP 12 — PLAYBACK EVENTS AND WATCH HISTORY

Implement high-throughput ingestion for:

• Playback started
• Playback progress
• Playback paused
• Playback resumed
• Playback completed
• Playback abandoned

Support:

• Batched ingestion
• Validation
• Idempotency
• Event publication
• Privacy controls
• History deletion
• Pause history
• Resume playback
• Recently watched

Do not synchronously update expensive aggregate counters for every playback event.

────────────────────────────────────────

MILESTONE GROUP 13 — VIEW COUNTING

Implement scalable view counting.

Support:

• View events
• Deduplication
• Idempotency
• Aggregation windows
• Redis hot counters where approved
• Kafka event ingestion
• Persistent aggregation
• Eventually consistent totals

Integrate approved anti-fraud boundaries.

────────────────────────────────────────

MILESTONE GROUP 14 — PLAYLISTS

Implement:

• Playlist creation
• Playlist updates
• Playlist deletion
• Playlist visibility
• Playlist items
• Ordering
• Reordering
• Add/remove videos
• Saved playlists
• Watch later

Ensure playlist operations enforce ownership and permissions.

────────────────────────────────────────

MILESTONE GROUP 15 — SUBSCRIPTIONS

Implement:

• Subscribe
• Unsubscribe
• Subscription status
• Subscription feeds
• Subscriber count aggregation
• Notification preferences

Use events where appropriate.

────────────────────────────────────────

MILESTONE GROUP 16 — INTERACTIONS

Implement:

• Likes
• Alternative feedback mechanisms where approved
• Reactions
• Saves
• Shares
• Reports

Ensure operations are:

• Idempotent
• Rate limited
• Auditable where required

────────────────────────────────────────

MILESTONE GROUP 17 — COMMENTS

Implement:

• Comments
• Replies
• Threading
• Pagination
• Editing
• Deletion
• Reactions
• Mentions
• Creator pinning
• Reporting
• Moderation state

Design for high-volume access.

────────────────────────────────────────

MILESTONE GROUP 18 — SEARCH

Implement the Search Service.

Support search for:

• Videos
• Channels
• Creators
• Playlists
• Live streams
• Topics
• Categories

Implement:

• Full-text search
• Autocomplete
• Suggestions
• Filters
• Sorting
• Pagination
• Ranking

Implement event-driven index synchronization.

The search index must not become the transactional source of truth.

────────────────────────────────────────

MILESTONE GROUP 19 — DISCOVERY

Implement APIs for:

• Trending content
• Popular content
• New releases
• Category discovery
• Topic discovery
• Creator discovery
• Live content discovery

Separate discovery aggregation from the core video service.

────────────────────────────────────────

MILESTONE GROUP 20 — RECOMMENDATIONS

Implement the initial recommendation service architecture.

Support:

• Candidate retrieval
• Candidate filtering
• Ranking interfaces
• Personalization signals
• Popularity signals
• Freshness
• Diversity
• Safety filtering
• Blocked content filtering
• Moderation filtering
• Privacy filtering

The initial implementation must use a clearly replaceable ranking strategy.

Do not tightly couple recommendation algorithms to the API Gateway or Video Service.

────────────────────────────────────────

MILESTONE GROUP 21 — NOTIFICATIONS

Implement:

• Notification creation
• Notification preferences
• In-app notifications
• Push notification integration
• Email notification integration
• Delivery retries
• Deduplication
• Priority
• Delivery tracking

Support:

• New video notifications
• Comment notifications
• Reply notifications
• Subscription notifications
• Live stream reminders
• Live stream started
• Moderation actions
• Copyright actions
• Security alerts

────────────────────────────────────────

MILESTONE GROUP 22 — LIVE STREAMING

Implement the backend control plane for:

• Live stream creation
• Stream scheduling
• Stream keys
• Stream key rotation
• Broadcaster authorization
• Stream lifecycle
• Stream status
• Stream health
• Recording configuration
• Stream completion
• VOD creation events

The implementation must respect the approved architecture separating:

• Ingestion
• Processing
• Packaging
• Delivery
• Interaction
• Analytics

────────────────────────────────────────

MILESTONE GROUP 23 — LIVE CHAT

Implement scalable real-time chat.

Support:

• WebSocket connections
• Authentication
• Authorization
• Chat messages
• Reactions
• Slow mode
• Subscriber-only mode
• Moderator roles
• Bans
• Message deletion
• Spam protection

Support horizontal scaling using the approved Redis and WebSocket coordination architecture.

────────────────────────────────────────

MILESTONE GROUP 24 — MODERATION

Implement:

• User reports
• Video reports
• Comment reports
• Channel reports
• Moderation queues
• Moderation decisions
• Enforcement actions
• Content restrictions
• Appeals
• Moderator notes
• Evidence references
• Audit logs

Implement explicit moderation state transitions.

────────────────────────────────────────

MILESTONE GROUP 25 — TRUST AND SAFETY

Implement service boundaries and initial capabilities for:

• Spam detection
• Account abuse detection
• API abuse
• Upload abuse
• View fraud integration
• Engagement fraud integration
• Risk scoring
• Temporary restrictions
• Permanent restrictions
• Appeals

Detection systems must integrate through defined interfaces and events.

────────────────────────────────────────

MILESTONE GROUP 26 — COPYRIGHT

Implement:

• Rights holders
• Copyright ownership records
• Claims
• Disputes
• Appeals
• Geographic restrictions
• Monetization restrictions
• Content blocking

Implement integration boundaries for media fingerprinting.

Do not hard-code a specific external fingerprinting vendor throughout domain logic.

────────────────────────────────────────

MILESTONE GROUP 27 — ADVERTISING

Implement the approved advertising domain.

Support:

• Advertisers
• Organizations
• Ad accounts
• Campaigns
• Ad groups
• Advertisements
• Creative assets
• Targeting
• Budgets
• Scheduling
• Delivery constraints
• Frequency capping

Maintain strict boundaries between campaign management and low-latency ad delivery.

────────────────────────────────────────

MILESTONE GROUP 28 — AD DELIVERY

Implement:

• Advertisement eligibility
• Targeting boundaries
• Ad selection interfaces
• Frequency controls
• Delivery responses
• Impression tracking
• Click tracking
• Fallback behavior

Video playback must continue when advertisement infrastructure is unavailable.

────────────────────────────────────────

MILESTONE GROUP 29 — MONETIZATION

Implement:

• Creator balances
• Revenue records
• Revenue calculation boundaries
• Revenue-sharing rules
• Financial ledger architecture
• Payout eligibility
• Payout scheduling
• Audit trails

Financial operations must be:

• Idempotent
• Auditable
• Transactionally safe

Do not use cached counters as the authoritative source for financial balances.

────────────────────────────────────────

MILESTONE GROUP 30 — PAYMENTS

Implement the payment provider integration.

Support:

• Payment intents or approved equivalent
• Webhook verification
• Idempotency
• Payment state transitions
• Refund boundaries
• Dispute boundaries
• Audit logging

Never store unnecessary payment card data.

────────────────────────────────────────

MILESTONE GROUP 31 — CREATOR ANALYTICS

Implement creator analytics pipelines for:

• Views
• Watch time
• Audience retention
• Unique viewers
• Subscriber growth
• Subscriber loss
• Revenue
• Traffic sources
• Geographic metrics
• Device metrics
• Video performance
• Live stream metrics

Separate high-volume analytics ingestion from transactional APIs.

────────────────────────────────────────

MILESTONE GROUP 32 — ADMINISTRATION

Implement administration APIs for:

• User administration
• Channel administration
• Video administration
• Moderation management
• Copyright management
• Advertising management
• Monetization administration
• Feature flags
• System configuration
• Audit logs

Every sensitive administrative action must:

• Require explicit authorization
• Produce an audit event
• Include correlation information
• Avoid exposing unnecessary sensitive information

────────────────────────────────────────

MILESTONE GROUP 33 — FEATURE FLAGS

Implement:

• Feature definitions
• Environment targeting
• User targeting
• Percentage rollouts
• Kill switches
• Audit logs

Feature flag failures must fail safely.

────────────────────────────────────────

MILESTONE GROUP 34 — DEVELOPER PLATFORM

Implement approved developer platform capabilities.

Support:

• API clients
• API credentials
• Credential rotation
• Scoped permissions
• Rate limits
• API versioning
• Webhook subscriptions
• Webhook signing
• Delivery logs
• Retry handling
• Dead-letter handling

Never expose internal service credentials to public API consumers.

────────────────────────────────────────

DATABASE IMPLEMENTATION

Generate:

• Service-specific Prisma schemas or approved schema organization
• Migrations
• Indexes
• Constraints
• Partitioning where required
• Repository implementations
• Transaction handling
• Connection management

Follow the approved database ownership boundaries.

Do not create cross-service database access that bypasses service APIs or approved event contracts.

────────────────────────────────────────

EVENT IMPLEMENTATION

Implement the approved event catalog.

For every implemented event define:

• Event name
• Version
• Producer
• Consumer
• Schema
• Validation
• Idempotency strategy
• Retry behavior
• Dead-letter behavior

Use versioned contracts.

Do not publish untyped event payloads.

────────────────────────────────────────

QUEUE IMPLEMENTATION

Implement the approved BullMQ queues.

For every queue define:

• Producer
• Consumer
• Job schema
• Validation
• Concurrency
• Retry policy
• Backoff
• Timeout
• Dead-letter handling
• Idempotency

────────────────────────────────────────

API REQUIREMENTS

All APIs must include:

• DTOs
• Input validation
• Authentication
• Authorization
• Pagination where applicable
• Filtering where applicable
• Sorting where applicable
• Rate limiting
• Consistent error responses
• Correlation IDs
• Structured logging
• OpenAPI documentation

Use API versioning according to the approved architecture.

────────────────────────────────────────

SECURITY REQUIREMENTS

Implement:

• Secure authentication
• Refresh token rotation
• RBAC
• Resource-level authorization
• Input validation
• SQL injection protection
• XSS-aware output handling
• Secure HTTP headers
• CORS
• CSRF protection where applicable
• Rate limiting
• Abuse protection
• File validation
• Malware scanning integration
• Signed object storage access
• Secret management integration
• Encryption in transit
• Secure audit logging
• Least privilege

Apply OWASP best practices.

────────────────────────────────────────

OBSERVABILITY REQUIREMENTS

Every service must support:

• Structured logs
• Correlation IDs
• Trace IDs
• OpenTelemetry instrumentation
• Metrics
• Health checks
• Readiness checks
• Graceful shutdown

Instrument critical workflows including:

• Authentication
• Video upload
• Video processing
• Playback authorization
• Playback event ingestion
• Search
• Recommendations
• Live streaming
• Live chat
• Payments
• Moderation

────────────────────────────────────────

TESTING REQUIREMENTS

For every milestone generate appropriate tests.

Include:

• Unit tests
• Integration tests where appropriate
• Repository tests
• Service tests
• Controller/API tests
• Event contract tests where appropriate
• Queue worker tests where appropriate

Generate end-to-end tests for critical workflows including:

• Registration and login
• Refresh token rotation
• Channel creation
• Video upload
• Upload completion
• Video processing lifecycle
• Video publishing
• Playback authorization
• Search indexing
• Subscription
• Comment creation
• Live stream lifecycle
• Payment webhook processing
• Moderation actions

────────────────────────────────────────

MILESTONE EXECUTION RULES

Begin with the first backend milestone only.

For each milestone:

1. Identify the exact scope.
2. Identify files that will be created.
3. Identify existing files that must be modified.
4. Generate complete implementations.
5. Generate tests.
6. Verify integration with previously generated code.
7. Update the Project Index.
8. Stop.

Do not start the next milestone automatically.

Wait for approval.

────────────────────────────────────────

CURRENT STARTING POINT

Start with:

BACKEND MILESTONE 1

Implement the production backend foundation, including:

• Monorepo configuration required for backend implementation
• Shared TypeScript configuration
• Linting and formatting
• Environment configuration
• Configuration validation
• Structured logging
• Centralized error handling
• Correlation IDs
• Request context
• OpenTelemetry foundation
• Health checks
• Readiness checks
• Graceful shutdown
• API response and error conventions
• Pagination utilities
• Database infrastructure
• Redis infrastructure
• Kafka or Redpanda infrastructure
• BullMQ infrastructure
• Object storage infrastructure
• Base testing infrastructure

Respect the approximate 20–40 file milestone limit.

If the complete foundation requires more files, prioritize the minimum coherent, production-ready foundation that compiles successfully and continue the remaining foundation work in the next milestone.

────────────────────────────────────────

PROJECT INDEX

After every milestone update:

• Current phase
• Current milestone
• Completed services
• Completed domains
• Generated files
• Modified files
• Database objects
• APIs
• Events
• Queues
• Infrastructure dependencies
• Tests
• Remaining work
• Exact next milestone

Never lose track of previously implemented components.

────────────────────────────────────────

STOP CONDITION

Start only with Backend Milestone 1.

After completing the milestone:

• Ensure all generated files integrate correctly.
• Ensure the milestone is internally consistent.
• Update the Project Index.
• Identify the exact next milestone.

STOP.

Wait for explicit approval before continuing.
