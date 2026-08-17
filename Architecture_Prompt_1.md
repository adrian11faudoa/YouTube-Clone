Using the Master Prompt above:

Build a production-ready, enterprise-scale global video platform comparable in architecture and capabilities to modern video-sharing and streaming platforms such as YouTube.

The goal is not to clone any existing product or copy its proprietary implementation.

The goal is to design and build an independent, scalable, cloud-native video platform capable of supporting:

• Hundreds of millions of users
• Millions of creators
• Billions of video views
• Massive video storage
• Global video delivery
• High-volume uploads
• Video transcoding
• Live streaming
• Real-time interactions
• Search and discovery
• Personalized recommendations
• Creator analytics
• Advertising
• Monetization
• Content moderation
• Copyright management
• Global infrastructure

This project must be designed as a long-running enterprise platform.

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Web Frontend

• Next.js
• React
• TypeScript
• Tailwind CSS

Mobile

• React Native
• Expo
• TypeScript

Backend

• Node.js
• NestJS
• TypeScript

Database

• PostgreSQL
• Prisma ORM

Caching

• Redis

Event Streaming

• Kafka or Redpanda

Background Processing

• BullMQ

Search

• Elasticsearch or OpenSearch

Object Storage

• AWS S3-compatible storage

CDN

• CloudFront or equivalent global CDN

Video Processing

• FFmpeg
• Dedicated transcoding workers
• HLS
• DASH
• Adaptive bitrate streaming

Live Streaming

• RTMP or SRT ingestion
• FFmpeg-based processing
• HLS delivery
• Low-latency architecture where appropriate

Realtime

• WebSockets
• Socket.IO where appropriate

Notifications

• Firebase Cloud Messaging
• Apple Push Notification Service
• Email notification provider

Payments

• Stripe or architecture-approved payment provider

Infrastructure

• Docker
• Kubernetes
• Helm
• Terraform
• GitHub Actions

Observability

• Prometheus
• Grafana
• Loki
• Tempo
• OpenTelemetry

Secrets

• HashiCorp Vault or architecture-approved secrets management

────────────────────────────────────────

PLATFORM DOMAINS

Design clear domain boundaries for:

• Identity
• Authentication
• Authorization
• Users
• Profiles
• Channels
• Videos
• Media
• Uploads
• Transcoding
• Streaming
• Live Streaming
• Playlists
• Subscriptions
• Social Interactions
• Comments
• Reactions
• Search
• Discovery
• Recommendations
• Advertising
• Monetization
• Payments
• Creator Analytics
• Notifications
• Moderation
• Trust and Safety
• Copyright
• Administration
• Feature Flags
• Audit
• Developer Platform

Use Domain-Driven Design boundaries.

Do not create microservices without clear ownership and operational justification.

────────────────────────────────────────

CORE MICROSERVICES

Generate architecture for independent services where justified:

• API Gateway
• Authentication Service
• Authorization Service
• Identity Service
• User Service
• Profile Service
• Channel Service
• Video Service
• Upload Service
• Media Service
• Video Processing Service
• Transcoding Worker Service
• Thumbnail Service
• Streaming Service
• Live Streaming Service
• Playlist Service
• Subscription Service
• Interaction Service
• Comment Service
• Search Service
• Discovery Service
• Recommendation Service
• Notification Service
• Push Notification Service
• Advertising Service
• Ad Delivery Service
• Monetization Service
• Payment Service
• Creator Analytics Service
• Analytics Service
• Moderation Service
• Trust and Safety Service
• Copyright Service
• Feature Flag Service
• Administration Service
• Audit Service
• Developer Platform Service

Each service must have clearly defined:

• Responsibilities
• Owned data
• APIs
• Events produced
• Events consumed
• Dependencies
• Scaling characteristics
• Failure boundaries

────────────────────────────────────────

IDENTITY AND AUTHENTICATION

Support:

• Registration
• Login
• Logout
• Email verification
• Password reset
• Password change
• OAuth
• Session management
• Device management
• Refresh tokens
• JWT authentication
• Multi-factor authentication
• Passkeys
• Recovery codes
• Account recovery
• Suspicious login detection

Design secure multi-device session management.

────────────────────────────────────────

USERS AND PROFILES

Support:

• User profiles
• Display names
• Usernames
• Avatars
• Banners
• Bios
• Links
• Social links
• Channel ownership
• Privacy settings
• Notification preferences
• Blocked users
• Muted users
• Account status
• Account verification status

────────────────────────────────────────

CHANNELS

Implement:

• Channel creation
• Channel profiles
• Channel customization
• Channel branding
• Channel descriptions
• Channel links
• Featured videos
• Channel sections
• Channel playlists
• Channel analytics
• Channel permissions
• Multiple channel managers
• Team access
• Creator roles

Support role-based access to channel management.

────────────────────────────────────────

VIDEO DOMAIN

Support:

• Video upload
• Draft videos
• Scheduled publishing
• Public videos
• Private videos
• Unlisted videos
• Age-restricted videos
• Video metadata
• Titles
• Descriptions
• Tags
• Categories
• Thumbnails
• Chapters
• Subtitles
• Captions
• Multiple audio tracks where supported
• Video editing metadata
• Video replacement strategy
• Processing states
• Publishing states
• Archiving
• Deletion

Design a complete video lifecycle.

────────────────────────────────────────

VIDEO UPLOAD ARCHITECTURE

Generate a scalable upload system supporting:

• Direct-to-object-storage uploads
• Signed upload URLs
• Multipart uploads
• Resumable uploads
• Upload validation
• File size limits
• MIME validation
• Malware scanning
• Metadata extraction
• Upload progress
• Upload cancellation
• Upload recovery
• Idempotent upload completion

The application backend must not unnecessarily proxy large video files.

────────────────────────────────────────

VIDEO PROCESSING PIPELINE

Design a complete asynchronous processing pipeline.

Support:

• Upload completion events
• Validation
• Virus scanning
• Metadata extraction
• Video inspection
• Transcoding
• Resolution generation
• Adaptive bitrate generation
• HLS generation
• DASH generation where approved
• Thumbnail generation
• Preview generation
• Subtitle processing
• Audio processing
• Content moderation integration
• Copyright analysis integration
• Processing status updates
• Failure recovery
• Retry policies
• Dead-letter handling

Generate clear state transitions.

────────────────────────────────────────

VIDEO QUALITY PROFILES

Support multiple quality levels such as:

• 144p
• 240p
• 360p
• 480p
• 720p
• 1080p
• 1440p
• 2160p where infrastructure supports it

Do not assume every uploaded video supports every quality.

Generate renditions based on source characteristics and platform policy.

────────────────────────────────────────

STREAMING ARCHITECTURE

Support:

• Adaptive bitrate streaming
• HLS
• DASH where appropriate
• CDN delivery
• Signed access where required
• Private video authorization
• Stream manifest generation
• Segment lifecycle management
• Cache strategy
• Geographic delivery

Design for very high read volume.

────────────────────────────────────────

LIVE STREAMING

Support:

• Stream scheduling
• Live stream creation
• Stream keys
• RTMP ingestion
• SRT support where appropriate
• Stream validation
• Transcoding
• Multi-bitrate delivery
• Live HLS
• Low-latency delivery where appropriate
• Live chat
• Stream reactions
• Live viewer counts
• Stream health
• Stream recording
• Automatic VOD generation
• Stream moderation
• Stream termination

Design clear boundaries between:

• Stream ingestion
• Processing
• Delivery
• Interaction
• Analytics

────────────────────────────────────────

VIDEO PLAYER

Design backend contracts supporting:

• Playback authorization
• Adaptive quality selection
• Playback progress
• Watch history
• Resume playback
• Captions
• Subtitles
• Audio tracks
• Playback speed
• Quality selection
• Fullscreen
• Picture-in-picture where supported
• Live playback
• DVR where supported

────────────────────────────────────────

PLAYLISTS

Support:

• Playlist creation
• Editing
• Ordering
• Collaborative permissions where approved
• Privacy
• Add/remove videos
• Saved playlists
• Watch later
• Queue support

────────────────────────────────────────

SUBSCRIPTIONS

Support:

• Subscribe
• Unsubscribe
• Subscription feeds
• Creator notifications
• Subscriber counts
• Private subscriber information
• Notification preferences

────────────────────────────────────────

SOCIAL INTERACTIONS

Support:

• Likes
• Dislikes or alternative feedback architecture where approved
• Reactions
• Shares
• Saves
• Watch later
• Reports

Use event-driven processing where appropriate.

────────────────────────────────────────

COMMENTS

Support:

• Video comments
• Replies
• Threading
• Pagination
• Editing
• Deletion
• Reactions
• Mentions
• Creator pinning
• Moderation
• Reporting
• Spam detection

Design for extremely high comment volume.

────────────────────────────────────────

SEARCH

Support search for:

• Videos
• Channels
• Creators
• Playlists
• Live streams
• Categories
• Hashtags
• Topics

Implement:

• Full-text search
• Autocomplete
• Search suggestions
• Typo tolerance where supported
• Filters
• Sorting
• Recency ranking
• Popularity ranking
• Personalized ranking where approved

────────────────────────────────────────

DISCOVERY

Implement discovery systems for:

• Trending videos
• Popular videos
• New releases
• Categories
• Topics
• Creator discovery
• Live streams
• Personalized discovery

Separate discovery logic from core video storage.

────────────────────────────────────────

RECOMMENDATION ENGINE

Design a recommendation architecture supporting:

• Candidate generation
• Candidate filtering
• Ranking
• Personalization
• Watch history
• User interactions
• Subscription signals
• Content similarity
• Popularity signals
• Freshness
• Diversity
• Exploration
• Feedback loops

The recommendation system must be designed as an independent domain.

Do not embed recommendation logic directly into the primary API service.

────────────────────────────────────────

WATCH HISTORY

Support:

• Playback progress
• Watch completion
• Resume playback
• Recently watched
• History deletion
• Pause history
• Privacy controls

Design write-heavy ingestion separately from read models where appropriate.

────────────────────────────────────────

EVENT-DRIVEN ARCHITECTURE

Use Kafka or Redpanda as the event backbone.

Define event contracts for events including:

• UserRegistered
• UserLoggedIn
• ChannelCreated
• VideoUploadStarted
• VideoUploadCompleted
• VideoProcessingStarted
• VideoTranscoded
• VideoProcessingFailed
• VideoPublished
• VideoDeleted
• VideoViewed
• VideoLiked
• VideoCommented
• ChannelSubscribed
• ChannelUnsubscribed
• PlaylistCreated
• LiveStreamStarted
• LiveStreamEnded
• AdvertisementRequested
• AdvertisementServed
• PaymentCompleted
• ModerationReportCreated
• ContentModerated
• CopyrightClaimCreated
• CopyrightClaimResolved
• NotificationRequested

Every event must define:

• Producer
• Consumers
• Payload ownership
• Versioning strategy
• Idempotency strategy
• Retry behavior
• Failure handling

────────────────────────────────────────

REDIS ARCHITECTURE

Use Redis for appropriate workloads such as:

• Caching
• Rate limiting
• Distributed locks
• Sessions where approved
• Temporary upload state
• Live viewer counters
• Real-time presence
• WebSocket coordination
• Hot video metadata
• Queue infrastructure

Do not use Redis as the permanent source of truth for core transactional data.

────────────────────────────────────────

PHASE 1 REQUIREMENTS

Generate only:

1. Complete enterprise system architecture
2. Domain decomposition
3. Service boundaries
4. Service ownership matrix
5. Monorepo architecture
6. Folder hierarchy
7. High-level ERD
8. PostgreSQL database strategy
9. Prisma ownership strategy
10. Redis architecture
11. Kafka or Redpanda event architecture
12. Event catalog
13. Queue architecture
14. Video upload architecture
15. Video processing pipeline
16. Streaming architecture
17. Live streaming architecture
18. CDN architecture
19. Search architecture
20. Recommendation architecture
21. Authentication architecture
22. Authorization model
23. API architecture
24. WebSocket architecture
25. Observability architecture
26. Security architecture
27. Multi-region deployment architecture
28. Disaster recovery strategy
29. Project Index

Do not implement backend application code yet.

Do not generate frontend implementation code yet.

Do not generate infrastructure implementation files yet.

Stop after completing Architecture Volume 1.

Wait for confirmation before continuing.

────────────────────────────────────────

ARCHITECTURAL DECISIONS

Unless there is a compelling technical reason otherwise, assume:

• NestJS for backend services.
• PostgreSQL for transactional data.
• Prisma for database access where appropriate.
• Redis for caching, coordination, counters, and transient state.
• Kafka or Redpanda as the event backbone.
• BullMQ for asynchronous jobs where Redis-backed queues are appropriate.
• Elasticsearch or OpenSearch for search.
• S3-compatible storage for source and processed media.
• CloudFront or equivalent CDN for global delivery.
• FFmpeg workers for media processing.
• HLS as the primary adaptive streaming format.
• DASH where justified.
• RTMP or SRT for live ingestion.
• WebSockets or Socket.IO for real-time interactions.
• Kubernetes for orchestration.
• Terraform for infrastructure provisioning.
• GitHub Actions for CI/CD.
• OpenTelemetry for observability.
• Prometheus, Grafana, Loki, and Tempo for the observability stack.
• Vault or approved equivalent for secrets management.
• Clean Architecture.
• Domain-Driven Design.
• Repository Pattern.
• Dependency Injection.
• Event-driven communication where appropriate.
• CQRS where appropriate.

Design every decision for a future platform supporting:

• Hundreds of millions of users
• Millions of creators
• Billions of video views
• Massive video libraries
• Global video delivery
• High-volume live streaming
• Enterprise-grade reliability
• Long-term maintainability
• Future expansion into podcasts, music, short-form video, live commerce, education, creator tools, and other media products.

Maintain the Project Index throughout the architecture phase.

STOP after Architecture Prompt — Volume 1.

Wait for confirmation.
