# YouTube-Style Video Platform — Architecture Prompt — Volume 1

# 1. ROLE AND PURPOSE

You are the senior software architect responsible for defining the foundational architecture of the **YouTube-Style Video Platform**.

Your task is to create the project's **implementation-useful foundational architecture artifacts**.

This is an architecture milestone.

It is not the task to implement the entire platform.

It is not the task to implement the complete backend, frontend, mobile applications, infrastructure, QA system, recommendation engine, search platform, media-processing platform, or live-streaming platform.

The purpose of this milestone is to establish sufficiently concrete architectural contracts and boundaries so that independently generated implementation milestones can later be assembled into one coherent production system.

The architecture produced in this milestone must be written as **portable artifacts** that can be transferred between independent AI coding conversations and used by Codex or another integration environment as authoritative engineering context.

Do not rely on hidden conversation history.

Do not rely on another AI response.

Do not assume that another architecture prompt has already been executed.

Inspect the repository when one is available and preserve compatible existing decisions, but treat the architecture defined by this prompt as the target architecture for the current milestone.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The system is a production-grade, global-scale video platform supporting:

* viewer accounts;
* creator accounts;
* channels;
* long-form video;
* short-form vertical video;
* video upload and processing;
* adaptive playback;
* playlists;
* subscriptions;
* comments;
* engagement;
* notifications;
* search;
* personalized discovery;
* recommendations;
* creator analytics;
* moderation;
* administration;
* live streaming;
* monetization-capable integration boundaries.

The implementation must remain an independent product and must not use proprietary YouTube source code, internal services, private interfaces, or proprietary infrastructure.

## 2.2 Architectural Scale Target

The architecture should be capable of evolving toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* petabyte-scale object storage;
* globally distributed CDN delivery;
* high-volume playback telemetry;
* high-volume engagement events;
* high-volume asynchronous media processing.

These are architectural target envelopes.

They do not mean that every component must immediately be deployed at maximum global scale during this milestone.

## 2.3 Technology Direction

The target technology direction is:

### Backend

* TypeScript;
* Node.js LTS;
* NestJS;
* REST APIs;
* WebSockets where realtime functionality requires them;
* OpenAPI;
* PostgreSQL;
* Redis;
* background workers.

### Web

* TypeScript;
* React;
* Next.js App Router;
* typed API clients;
* accessible responsive interfaces.

### Mobile

* React Native;
* Expo where appropriate;
* shared TypeScript contracts where practical.

### Search and Data

* PostgreSQL;
* Redis;
* OpenSearch or equivalent production search infrastructure;
* object storage;
* CDN.

### Events and Async Processing

* Redpanda/Kafka-compatible event streaming where justified;
* durable job queues;
* explicit retry and idempotency policies.

### Media

* FFmpeg or equivalent media processing;
* HLS/DASH-compatible adaptive streaming;
* multi-bitrate output;
* object storage;
* CDN delivery;
* secure resumable uploads.

### Infrastructure Direction

* AWS;
* Kubernetes/EKS where orchestration is justified;
* Terraform;
* managed PostgreSQL where appropriate;
* managed Redis where appropriate;
* S3-compatible object storage;
* CDN such as CloudFront or an equivalent;
* production search infrastructure;
* production event streaming infrastructure.

### Observability

* OpenTelemetry;
* structured logs;
* metrics;
* distributed tracing;
* centralized logging;
* dashboards;
* alerting;
* correlation/request identifiers.

Do not introduce technology merely because it appears sophisticated.

Every architectural component must have an explicit operational purpose.

---

# 3. ARCHITECTURAL OBJECTIVE

Produce a coherent architecture that:

* separates business domains clearly;
* establishes ownership boundaries;
* defines data ownership;
* defines system-of-record boundaries;
* defines synchronous and asynchronous communication;
* defines media-plane versus control-plane responsibilities;
* defines client/backend boundaries;
* defines storage responsibilities;
* defines event and queue responsibilities;
* defines authentication and authorization boundaries;
* defines search and recommendation boundaries;
* defines observability boundaries;
* defines failure boundaries;
* defines scalability boundaries;
* enables independent implementation of later project parts;
* minimizes integration ambiguity.

The architecture must be concrete enough that a backend, frontend, mobile, infrastructure, and QA engineer can implement against it without inventing fundamental system contracts independently.

---

# 4. REPOSITORY INSPECTION

Before producing architecture artifacts:

1. Inspect the repository if one is available.
2. Identify the existing project structure.
3. Inspect package manifests.
4. Inspect existing application modules.
5. Inspect existing infrastructure code.
6. Inspect existing database definitions and migrations.
7. Inspect existing API contracts.
8. Inspect existing event definitions.
9. Inspect existing configuration.
10. Inspect existing tests.
11. Identify existing architecture documentation.
12. Preserve compatible existing implementation decisions when they do not conflict with the target requirements of this prompt.

Do not fabricate repository state.

If the repository is empty or nearly empty, create the architecture artifacts required by this milestone without pretending that application implementation already exists.

If the repository contains implementation decisions that materially conflict with this architecture, document the conflict and define an explicit compatibility or migration strategy rather than silently ignoring it.

---

# 5. ARCHITECTURE DELIVERABLES

Create a portable architecture document set containing, at minimum:

1. System architecture overview.
2. Context diagram.
3. Container/component architecture.
4. Domain boundary model.
5. Service/module ownership matrix.
6. Data ownership matrix.
7. Core entity/domain model.
8. Identity and authorization architecture.
9. API architectural conventions.
10. Event and messaging architectural conventions.
11. Asynchronous processing architecture.
12. Media architecture.
13. Search architecture.
14. Recommendation architecture.
15. Notification architecture.
16. Analytics architecture.
17. Moderation architecture.
18. Administration architecture.
19. Live-stream architecture at control-plane level.
20. Infrastructure topology at logical level.
21. Cross-part contract matrix.
22. Technology decision record.
23. Architectural assumptions and constraints.
24. Major risks and mitigations.
25. Architecture decision records for material non-obvious decisions.

Use Mermaid, structured Markdown, tables, or other portable formats where diagrams or matrices are useful.

The architecture document set must be understandable outside the originating AI conversation.

---

# 6. SYSTEM CONTEXT ARCHITECTURE

Define the system boundary and all major external actors and systems.

The architecture must distinguish at minimum:

## Internal Areas

* Web application.
* Mobile applications.
* Public backend APIs.
* Realtime gateway.
* Identity and account domain.
* Channel domain.
* Video/content domain.
* Media processing workers.
* Playback metadata services.
* Engagement domain.
* Subscription domain.
* Playlist domain.
* Search subsystem.
* Recommendation subsystem.
* Notification subsystem.
* Analytics/event subsystem.
* Moderation subsystem.
* Administration subsystem.
* Live-stream control plane.
* Background job system.
* Event streaming infrastructure.
* Transactional database.
* Cache.
* Search index.
* Object storage.
* CDN integration.
* Observability platform.

## External Dependencies

Define explicit boundaries for possible:

* OAuth/OIDC providers;
* email providers;
* push notification providers;
* payment providers;
* advertising platforms;
* cloud services;
* CDN;
* object storage;
* external content safety/scanning providers;
* external analytics systems where applicable.

Do not fabricate provider behavior.

The architecture must make clear which capabilities are core platform responsibilities and which are external integrations.

---

# 7. SYSTEM ARCHITECTURE

Define the logical system topology.

At minimum, distinguish the following layers:

## Client Layer

* web;
* mobile;
* creator experiences;
* administrative interfaces.

## API and Edge Layer

* TLS termination;
* CDN interaction;
* WAF boundary;
* API ingress;
* authentication boundary;
* rate limiting;
* request correlation;
* API routing.

## Application Layer

Define domain services/modules for:

* identity;
* accounts;
* channels;
* videos;
* media orchestration;
* playback metadata;
* comments;
* reactions;
* subscriptions;
* playlists;
* search;
* recommendations;
* notifications;
* analytics;
* moderation;
* administration;
* live streaming;
* monetization boundaries.

## Data Layer

Define responsibilities for:

* PostgreSQL;
* Redis;
* object storage;
* search index;
* event stream;
* analytics storage where required;
* CDN cache.

## Async Layer

Define:

* queues;
* workers;
* scheduled jobs;
* event producers;
* event consumers;
* retry infrastructure;
* dead-letter handling.

Do not force every domain into a physically independent microservice.

Define which responsibilities should initially remain modules within a deployable backend and which have justified reasons to become independently deployable services or workers.

---

# 8. DOMAIN BOUNDARIES

Define explicit domain ownership.

At minimum create a domain boundary table containing:

| Domain              | Responsibilities                     | Owns                        | Reads                        | Writes                       | Publishes                      | Consumes                         |
| ------------------- | ------------------------------------ | --------------------------- | ---------------------------- | ---------------------------- | ------------------------------ | -------------------------------- |
| Identity & Accounts | Authentication and account lifecycle | User/account identity       | Authorized account data      | Account records              | Identity events                | Relevant identity events         |
| Channels            | Creator/channel identity             | Channel metadata            | User identity                | Channel records              | Channel events                 | Account events                   |
| Video Content       | Video metadata and publication state | Video metadata              | Channel/content data         | Video metadata               | Video lifecycle events         | Media processing events          |
| Media Processing    | Transcoding and derived media        | Processing jobs/assets      | Video metadata               | Processing state/assets      | Media events                   | Upload/video events              |
| Playback            | Playback metadata and entitlement    | Playback metadata           | Video/media metadata         | Playback-specific state      | Playback events where required | Media/video events               |
| Engagement          | Likes, comments, reactions           | Engagement records          | User/video/channel data      | Engagement records           | Engagement events              | Moderation events                |
| Subscriptions       | Viewer-creator relationships         | Subscription relationships  | User/channel data            | Subscription records         | Subscription events            | Account/channel events           |
| Playlists           | User collections                     | Playlist ownership/items    | Video metadata               | Playlist records             | Playlist events                | Video deletion/visibility events |
| Search              | Search retrieval                     | Search index                | Indexed representations      | Search index documents       | Indexing events if required    | Content lifecycle events         |
| Recommendations     | Candidate generation/ranking         | Derived recommendation data | Events/content signals       | Derived recommendation state | Recommendation telemetry       | Engagement/content events        |
| Notifications       | Notification delivery                | Notification state          | User/subscription/event data | Notification records         | Delivery events                | Domain events                    |
| Analytics           | Product telemetry                    | Analytical datasets         | Event streams                | Analytical storage           | Analytical processing events   | Product events                   |
| Moderation          | Trust & safety enforcement           | Moderation decisions        | Reports/content/account data | Moderation records           | Enforcement events             | Report/content events            |
| Administration      | Platform operations                  | Administrative state/audit  | Platform domains             | Administrative records       | Admin audit events             | Operational events               |
| Live Streaming      | Stream control plane                 | Stream session metadata     | Channel/user/content data    | Stream state                 | Live lifecycle events          | Media/live events                |

Refine the table when necessary, but do not leave ownership ambiguous.

Each important entity must have one authoritative write owner.

---

# 9. CORE DOMAIN ENTITY MODEL

Define the canonical entities and their relationships.

At minimum model:

* User;
* Account;
* Session;
* Channel;
* ChannelMembership/Role where applicable;
* Video;
* VideoVariant/Rendition;
* MediaAsset;
* Thumbnail;
* CaptionTrack;
* Playlist;
* PlaylistItem;
* Subscription;
* Comment;
* CommentReply;
* Reaction;
* WatchHistoryEntry;
* PlaybackProgress;
* Notification;
* Report;
* ModerationCase;
* ModerationAction;
* LiveStream;
* LiveStreamSession;
* SearchDocument;
* RecommendationCandidate or equivalent derived representation;
* AnalyticsEvent;
* AdministrativeAuditEntry.

For each entity define:

* purpose;
* owning domain;
* identifier;
* core fields;
* lifecycle;
* relationships;
* mutability;
* deletion behavior;
* privacy sensitivity;
* source of truth;
* derived representations.

Do not over-specify fields that belong to implementation details unless they are contractually important.

However, identifiers, status values, ownership, timestamps, and relationships must be concrete enough for later implementation.

---

# 10. IDENTIFIER AND TIME MODEL

Establish a project-wide identifier strategy.

Define:

* identifier format;
* uniqueness boundary;
* generation strategy;
* serialization format;
* API representation;
* database representation;
* public versus internal identifiers;
* privacy considerations for exposed identifiers.

Prefer identifiers that do not require database-local numeric sequences to remain globally unique across independently generated components.

Establish timestamp conventions including:

* UTC storage;
* ISO-compatible API serialization;
* created-at semantics;
* updated-at semantics;
* event timestamp semantics;
* ordering semantics;
* client-generated timestamps versus server-generated timestamps.

Server-generated timestamps must be authoritative for system state.

---

# 11. AUTHENTICATION ARCHITECTURE

Define the authentication architecture for:

* web;
* mobile;
* API;
* administrative interfaces;
* creator functionality;
* WebSocket connections;
* upload authorization.

Define:

* login flow;
* session model;
* access-token model where used;
* refresh-token model where used;
* token rotation;
* token revocation;
* logout semantics;
* device/session tracking;
* account recovery;
* email verification;
* OAuth/OIDC integration boundary;
* service-to-service authentication.

The architecture must distinguish authentication from authorization.

Do not define a client-only security model.

---

# 12. AUTHORIZATION ARCHITECTURE

Define authorization boundaries for:

* user-owned resources;
* channel ownership;
* creator roles;
* moderator roles;
* administrator roles;
* platform operators;
* private/unlisted/public content;
* moderation-restricted content;
* scheduled content;
* live-stream management.

Define the authorization model at a level that later backend prompts can implement consistently.

At minimum distinguish:

* identity;
* resource ownership;
* role;
* action;
* resource state.

Authorization decisions must be server-side.

---

# 13. API ARCHITECTURE

Define the API design standard.

Specify:

* REST conventions;
* base URL conventions;
* API versioning;
* resource naming;
* HTTP method semantics;
* request validation;
* response structures;
* error envelope;
* pagination;
* filtering;
* sorting;
* idempotency;
* conditional operations where useful;
* rate-limit responses;
* authentication requirements;
* authorization requirements;
* correlation headers;
* request identifiers.

Define the canonical error structure.

Define a standard pagination contract.

Use cursor pagination for large collections where appropriate.

Do not expose internal implementation structure through accidental API naming.

The API architecture must be suitable for both web and mobile clients.

---

# 14. EVENT ARCHITECTURE

Define the event architecture at a contract level.

Every durable event must define:

* event name;
* event version;
* event ID;
* occurred-at timestamp;
* producer;
* schema;
* actor/subject where applicable;
* correlation ID;
* causation ID where useful;
* compatibility strategy.

Define event naming conventions.

Define event ownership.

Identify foundational domain events such as:

* user.created;
* channel.created;
* channel.updated;
* video.upload.initiated;
* video.upload.completed;
* video.processing.started;
* video.processing.completed;
* video.processing.failed;
* video.published;
* video.unpublished;
* video.deleted;
* comment.created;
* comment.deleted;
* reaction.created;
* subscription.created;
* subscription.deleted;
* playlist.updated;
* notification.requested;
* live_stream.created;
* live_stream.started;
* live_stream.ended;
* moderation.report.created;
* moderation.action.applied.

The final implementation may refine names, but the event taxonomy must remain internally consistent.

Define:

* producer;
* consumers;
* delivery assumptions;
* retry policy;
* idempotency;
* dead-letter strategy;
* evolution strategy.

---

# 15. QUEUE AND BACKGROUND JOB ARCHITECTURE

Define the background processing model.

At minimum cover job categories for:

* media processing;
* thumbnail generation;
* caption processing;
* notification dispatch;
* search indexing;
* analytics processing;
* recommendation computation;
* moderation automation;
* cleanup/lifecycle jobs;
* periodic aggregation.

For each major job type define:

* queue;
* payload;
* producer;
* consumer;
* maximum execution expectations;
* concurrency;
* retry behavior;
* backoff;
* idempotency key;
* timeout;
* dead-letter handling;
* observability.

Separate durable domain events from operational jobs when their semantics differ.

---

# 16. DATA OWNERSHIP ARCHITECTURE

Create a data ownership matrix.

Every important data class must have exactly one authoritative owner.

At minimum cover:

* account identity;
* channel metadata;
* video metadata;
* media-processing state;
* media asset metadata;
* subscription relationships;
* comments;
* reactions;
* playlists;
* notification state;
* moderation records;
* live-stream state;
* search index;
* recommendation state;
* analytics data;
* audit records.

Clearly distinguish:

* source-of-truth data;
* cached data;
* derived data;
* indexed data;
* analytical data;
* ephemeral data.

Derived systems must have a defined rebuild/recovery path.

---

# 17. DATABASE ARCHITECTURE

Define the PostgreSQL architecture at a logical level.

Specify:

* primary transactional ownership;
* schema strategy;
* migration model;
* transaction boundaries;
* foreign-key usage;
* indexes;
* unique constraints;
* isolation expectations;
* concurrency control;
* high-volume data considerations;
* partitioning candidates;
* archival strategy;
* backup strategy;
* restore strategy;
* read-scaling strategy.

Do not prematurely split the platform into multiple databases without domain or operational justification.

However, identify future database separation boundaries where scale or isolation makes it reasonable.

Define which entities may generate hot write patterns and how the architecture avoids putting all high-frequency counters directly on the same transactional row.

---

# 18. REDIS ARCHITECTURE

Define explicit Redis responsibilities.

Potential uses include:

* cache;
* rate limiting;
* session-related ephemeral state where appropriate;
* upload session state where justified;
* short-lived coordination;
* locks where unavoidable;
* feed caching;
* playback-related ephemeral metadata.

For each use, define:

* owner;
* key namespace;
* key structure;
* TTL;
* invalidation behavior;
* source of truth;
* failure behavior;
* consistency expectations.

Redis must never silently become the authoritative source of durable business data unless explicitly architected for that responsibility.

---

# 19. MEDIA ARCHITECTURE

Define the full logical media flow.

At minimum:

```text
Client
  ↓
Upload Authorization
  ↓
Resumable Upload
  ↓
Object Storage
  ↓
Media Validation
  ↓
Processing Queue
  ↓
Transcoding Workers
  ↓
Derived Renditions
  ↓
Thumbnail / Caption Processing
  ↓
Manifest Generation
  ↓
Publishability Check
  ↓
CDN
  ↓
Playback Client
```

Define:

* original asset storage;
* processing workspace;
* output renditions;
* manifests;
* thumbnails;
* captions;
* object naming;
* metadata;
* access control;
* signed delivery where needed;
* lifecycle;
* deletion;
* cleanup;
* retries;
* failed-processing recovery.

Application APIs must not become the high-bandwidth media transport unless there is a deliberate reason.

---

# 20. PLAYBACK ARCHITECTURE

Define playback control-plane architecture.

Separate:

* playback API;
* authorization;
* content visibility;
* playback manifest metadata;
* media URLs;
* CDN delivery;
* telemetry.

The architecture must support:

* adaptive bitrate;
* multiple qualities;
* captions;
* playback position;
* resume;
* content restrictions;
* visibility enforcement;
* deleted/restricted video behavior.

High-volume media bytes should be delivered through the media delivery infrastructure rather than through transactional APIs.

---

# 21. SEARCH ARCHITECTURE

Define search as a derived system.

Specify:

* indexed entities;
* indexing triggers;
* document schema;
* tokenizer/analyzer direction;
* searchable fields;
* filters;
* sorting;
* ranking inputs;
* autocomplete architecture;
* reindexing;
* consistency expectations;
* deletion propagation;
* fallback behavior.

PostgreSQL remains the authoritative transactional source for content metadata unless a later architecture decision explicitly changes ownership.

Search outages must not corrupt canonical content state.

---

# 22. RECOMMENDATION ARCHITECTURE

Define a layered recommendation architecture.

At minimum distinguish:

1. candidate generation;
2. filtering;
3. ranking;
4. personalization;
5. diversity/freshness;
6. experimentation;
7. safety/moderation filtering.

Define initial recommendation inputs:

* watch history;
* subscriptions;
* engagement;
* content metadata;
* recency;
* creator relationships;
* negative feedback;
* session context.

Define how the architecture evolves from deterministic ranking toward more advanced recommendation systems.

Define fallback behavior.

Recommendation failures must not make the entire home experience unavailable.

---

# 23. NOTIFICATION ARCHITECTURE

Define the notification pipeline:

```text
Domain Event
  ↓
Notification Decision
  ↓
Notification Job
  ↓
Preference Check
  ↓
Channel Delivery
  ├── In-App
  ├── Push
  └── Email
```

Define:

* notification types;
* preference model;
* deduplication;
* delivery state;
* retries;
* provider boundaries;
* quiet periods where applicable;
* failure behavior;
* auditability.

Notification delivery must be asynchronous where appropriate.

---

# 24. ANALYTICS ARCHITECTURE

Define the analytical event flow.

At minimum distinguish:

* operational database;
* event ingestion;
* durable event stream;
* processing;
* analytical storage;
* creator analytics;
* operational analytics.

Playback telemetry must be designed for very high event volume.

Do not write every playback heartbeat synchronously to PostgreSQL.

Define:

* event taxonomy;
* sampling strategy where appropriate;
* aggregation boundaries;
* retention;
* privacy;
* late-arriving event handling;
* deduplication;
* replay/reprocessing.

---

# 25. MODERATION ARCHITECTURE

Define the trust-and-safety flow.

At minimum:

```text
User / System Report
  ↓
Report Intake
  ↓
Moderation Queue
  ↓
Automated Signals where applicable
  ↓
Human Review where applicable
  ↓
Moderation Decision
  ↓
Enforcement
  ↓
Audit Event
```

Define moderation objects such as:

* report;
* case;
* evidence;
* action;
* actor;
* reason;
* status;
* appeal boundary where applicable.

Separate moderation state from ordinary content metadata where appropriate.

Ensure moderation decisions are auditable.

---

# 26. ADMINISTRATION ARCHITECTURE

Define administrative boundaries for:

* user management;
* channel management;
* content management;
* moderation operations;
* system configuration;
* operational diagnostics;
* audit review;
* support workflows.

Administrative capabilities must use explicit privileged authorization.

Administrative actions must generate audit records where appropriate.

Do not expose operational controls through ordinary user APIs.

---

# 27. LIVE STREAMING CONTROL-PLANE ARCHITECTURE

Define the control-plane architecture for:

* stream creation;
* scheduling;
* stream metadata;
* ingest configuration;
* stream status;
* viewer-facing playback metadata;
* chat configuration;
* moderation;
* stream termination;
* archival/VOD coordination.

Clearly separate the control plane from the high-bandwidth media ingest and delivery plane.

Define the interfaces between:

* channel domain;
* live-stream control plane;
* ingest;
* media processing;
* playback;
* live chat;
* moderation;
* notifications.

Do not attempt to fully implement media ingest infrastructure in this architecture milestone.

The objective here is to define boundaries and contracts.

---

# 28. SECURITY ARCHITECTURE

Create a high-level threat boundary model.

Identify trust boundaries around:

* browsers;
* mobile devices;
* public APIs;
* upload endpoints;
* media object storage;
* internal services;
* workers;
* event streams;
* administrative interfaces;
* third-party providers.

At minimum account for:

* credential theft;
* token replay;
* account takeover;
* unauthorized media access;
* malicious uploads;
* abusive automation;
* API abuse;
* comment spam;
* privilege escalation;
* insecure direct object access;
* event forgery;
* administrative misuse;
* secret leakage.

Define security controls at the architecture level.

Do not perform exploit development.

---

# 29. PRIVACY ARCHITECTURE

Define privacy-sensitive boundaries.

Identify:

* account data;
* private content;
* unlisted content;
* viewing history;
* analytics data;
* creator analytics;
* moderation records;
* administrative audit data.

Define:

* access restrictions;
* retention;
* deletion;
* propagation of deletion to derived systems;
* logging restrictions;
* analytics minimization;
* data lifecycle.

---

# 30. OBSERVABILITY ARCHITECTURE

Define observability boundaries for:

* API layer;
* domain services;
* media workers;
* queues;
* event streams;
* database;
* cache;
* search;
* notifications;
* live-stream control plane;
* infrastructure;
* clients where telemetry is applicable.

Define standard:

* correlation ID;
* trace ID;
* request ID;
* job ID;
* event ID.

Define major service-level metrics and failure indicators.

The resulting architecture must allow future implementation prompts to add observability without inventing different conventions per subsystem.

---

# 31. RELIABILITY ARCHITECTURE

Define architectural failure domains.

At minimum specify behavior for failure of:

* PostgreSQL;
* Redis;
* search;
* event streaming;
* queue workers;
* media workers;
* object storage;
* CDN;
* notification providers;
* external identity providers;
* payment providers;
* recommendation services.

For each major dependency, identify:

* timeout expectations;
* retry behavior;
* fallback;
* circuit isolation where applicable;
* data consistency consequences;
* recovery strategy.

Prioritize resilience of:

* authentication;
* video metadata;
* publication;
* playback control;
* media delivery.

Define graceful degradation for non-critical dependencies.

---

# 32. INFRASTRUCTURE TOPOLOGY

Create a logical infrastructure topology showing:

```text
Internet
  ↓
DNS / CDN / WAF
  ↓
Load Balancer / Ingress
  ↓
Web Application + API
  ↓
Application Modules / Services
  ├── PostgreSQL
  ├── Redis
  ├── Search
  ├── Event Streaming
  ├── Job Queues
  └── Object Storage
          ↓
         CDN
```

Also show:

* worker pools;
* media-processing workers;
* analytics processing;
* external integrations;
* observability systems.

Distinguish:

* synchronous request path;
* asynchronous processing path;
* media delivery path;
* analytics path.

Do not claim that this infrastructure is already deployed.

---

# 33. DEPLOYMENT BOUNDARIES

Define which components are expected to be:

* deployable together initially;
* independently scalable;
* independently deployable later;
* worker processes;
* external managed services.

Provide initial deployment boundaries that remain practical for a funded startup without forcing premature microservice fragmentation.

Identify which components have independent scaling requirements:

* API;
* media workers;
* search;
* analytics processing;
* recommendation workers;
* notification workers;
* WebSocket/realtime infrastructure.

---

# 34. CROSS-PART CONTRACT MATRIX

Create a portable matrix containing at minimum:

| Producer | Consumer | Contract | Transport | Data Format | Failure Behavior | Owner |
| -------- | -------- | -------- | --------- | ----------- | ---------------- | ----- |

Cover major integrations including:

* web → API;
* mobile → API;
* API → PostgreSQL;
* API → Redis;
* API → object storage;
* API → event streaming;
* video domain → media workers;
* media workers → object storage;
* media pipeline → playback;
* video domain → search;
* video domain → recommendations;
* domain events → notifications;
* domain events → analytics;
* reports → moderation;
* live control plane → ingest;
* live control plane → playback;
* administrative UI → administration APIs.

The matrix must identify ownership rather than only describing technical connectivity.

---

# 35. API CONTRACT ARTIFACT

Create an initial API contract specification covering foundational conventions and representative resource contracts.

At minimum define the architectural shape for:

* authentication;
* users;
* channels;
* videos;
* subscriptions;
* comments;
* playlists;
* search;
* notifications;
* reports/moderation;
* creator operations;
* live-stream control.

The artifact does not need to contain every final endpoint of the completed product.

It must define enough representative contracts to establish consistent conventions.

Do not create fake implementations.

These are architecture contracts, not mock APIs.

---

# 36. EVENT CONTRACT ARTIFACT

Create a portable event contract specification covering the core domain events introduced in this milestone.

Each event definition must include:

* event name;
* version;
* producer;
* consumers;
* payload shape;
* identifier fields;
* timestamp fields;
* delivery semantics;
* retry behavior;
* idempotency expectations;
* compatibility policy.

Do not define events merely as informal prose.

The artifact must be implementation-usable.

---

# 37. CONFIGURATION ARCHITECTURE

Define project-wide configuration conventions.

At minimum distinguish:

* public client configuration;
* server configuration;
* secrets;
* credentials;
* environment selection;
* service endpoints;
* database configuration;
* Redis configuration;
* search configuration;
* object storage configuration;
* event-stream configuration;
* queue configuration;
* observability configuration;
* feature flags.

Define naming conventions.

Define which values may safely reach clients.

Define secret-handling boundaries.

Never place production credentials in the repository.

---

# 38. VERSIONING STRATEGY

Define how the platform evolves.

Cover:

* REST API versioning;
* event schema versioning;
* database migration versioning;
* media metadata evolution;
* search document evolution;
* mobile/web client compatibility;
* rolling deployments;
* backward-compatible deployment order.

Do not make every contract versioned merely for appearance.

Version when compatibility or independent deployment requires it.

---

# 39. SECURITY AND PRIVACY CONTRACT MATRIX

Create a matrix mapping important data or operations to:

* actor;
* required authentication;
* authorization rule;
* sensitivity;
* transport;
* persistence;
* audit requirement;
* retention;
* deletion behavior.

At minimum cover:

* account access;
* channel management;
* video upload;
* video visibility;
* private playback;
* comment moderation;
* administrative actions;
* moderation actions;
* analytics;
* live-stream controls.

---

# 40. FAILURE AND DEGRADATION MATRIX

Create a matrix:

| Failure | Affected Capability | Expected Behavior | Data Risk | Recovery | Alerting |
| ------- | ------------------- | ----------------- | --------- | -------- | -------- |

Include at least:

* database unavailable;
* Redis unavailable;
* search unavailable;
* recommendation unavailable;
* event-stream unavailable;
* queue unavailable;
* media worker failure;
* object storage failure;
* notification provider failure;
* external auth-provider failure;
* CDN degradation.

The purpose is to establish predictable architectural behavior before implementation.

---

# 41. ARCHITECTURAL DECISION RECORDS

Create ADRs or equivalent decision records for major architectural decisions made in this milestone.

At minimum document decisions regarding:

* modular backend versus premature microservices;
* PostgreSQL as transactional source of truth;
* Redis role;
* event-stream usage;
* background job architecture;
* object storage and CDN media strategy;
* search as a derived subsystem;
* recommendation architecture;
* control-plane versus media-plane separation;
* API style and versioning;
* authentication architecture;
* domain ownership strategy.

Each ADR should include:

* decision;
* context;
* alternatives considered;
* consequences;
* operational implications.

Do not produce speculative ADRs for decisions that were not actually made.

---

# 42. ARCHITECTURAL RISKS

Document major risks, including where applicable:

* media-processing cost;
* storage growth;
* CDN bandwidth cost;
* playback concurrency;
* search index growth;
* event volume;
* telemetry volume;
* recommendation complexity;
* moderation scale;
* notification fan-out;
* hot counters;
* database contention;
* cloud operational complexity;
* distributed-system debugging;
* privacy-sensitive analytics;
* vendor lock-in;
* mobile/backend compatibility.

For each major risk provide:

* risk description;
* impact;
* likelihood category;
* mitigation;
* architectural escape path.

Do not fabricate numerical probabilities.

---

# 43. DOCUMENTATION STRUCTURE

Organize the architecture artifacts so that a future implementation agent can locate:

1. system context;
2. domain boundaries;
3. entity model;
4. data ownership;
5. API contracts;
6. event contracts;
7. asynchronous jobs;
8. media architecture;
9. search;
10. recommendations;
11. notifications;
12. analytics;
13. moderation;
14. live streaming;
15. security;
16. infrastructure;
17. observability;
18. reliability;
19. ADRs;
20. integration matrix.

Use stable filenames and headings.

Prefer deterministic architecture-document locations such as:

* `docs/architecture/`
* `docs/contracts/`
* `docs/adr/`

Do not impose a repository path that conflicts with an existing project convention. Inspect the repository first.

---

# 44. WHAT YOU MUST CREATE

Create the complete architecture artifact set required by this prompt.

That includes:

* architecture documentation;
* diagrams;
* domain ownership models;
* entity/domain model;
* API architectural contract;
* event contract;
* queue/job contract;
* media architecture;
* search architecture;
* recommendation architecture;
* notification architecture;
* analytics architecture;
* moderation architecture;
* live-stream control-plane architecture;
* security model;
* privacy model;
* reliability model;
* deployment topology;
* integration contract matrix;
* ADRs;
* risk register.

Where a repository already contains an equivalent artifact, update it rather than creating unnecessary duplicates.

---

# 45. WHAT YOU MUST NOT IMPLEMENT

This architecture milestone does not authorize implementation of:

* the complete backend business logic;
* complete database migrations for every domain;
* complete web UI;
* complete mobile UI;
* complete media-processing workers;
* complete transcoding infrastructure;
* production recommendation algorithms;
* complete search indexing implementation;
* complete notification delivery;
* complete moderation implementation;
* complete payment integration;
* complete live-stream media ingest;
* complete cloud deployment;
* complete QA automation.

Architecture artifacts may contain schemas and contracts necessary to make later implementation deterministic.

Do not replace architecture artifacts with placeholder application code.

---

# 46. ARCHITECTURAL QUALITY REQUIREMENTS

The resulting architecture must be:

* internally consistent;
* explicit;
* portable;
* implementation-useful;
* scalable;
* secure;
* privacy-aware;
* observable;
* operationally realistic;
* cost-aware;
* testable;
* maintainable.

No critical dependency may exist only as an undocumented assumption.

No major domain may have ambiguous ownership.

No major cross-part contract may be left undefined where later implementation depends on it.

No architectural choice may be justified solely by saying that it is "industry standard."

State why each material architectural decision is appropriate for this project's requirements.

---

# 47. VALIDATION REQUIREMENTS

Before considering the architecture milestone complete, validate:

## Structural Validation

* All required architecture artifacts exist.
* All major diagrams are internally consistent.
* All domain ownership tables are complete.
* All contract matrices are populated.
* ADRs correspond to actual decisions.

## Contract Validation

Verify consistency of:

* entity names;
* identifier conventions;
* timestamps;
* enum/state naming;
* API terminology;
* event terminology;
* service/module names;
* ownership boundaries;
* error conventions;
* versioning conventions.

## Integration Validation

Verify that:

* web can consume backend contracts;
* mobile can consume backend contracts;
* backend can communicate with data stores;
* backend can publish events;
* workers can consume jobs/events;
* media processing can connect to storage;
* playback can consume media metadata;
* search can consume indexing events;
* recommendations can consume signals;
* notifications can consume domain events;
* moderation can observe relevant content and reports;
* infrastructure can host the defined components.

## Scalability Validation

Check for architectural bottlenecks around:

* playback;
* uploads;
* media processing;
* engagement;
* notifications;
* analytics;
* search;
* recommendations.

## Reliability Validation

Check that major dependencies have:

* failure behavior;
* retries where appropriate;
* fallback where appropriate;
* recovery path;
* observability.

## Security Validation

Check:

* trust boundaries;
* authentication;
* authorization;
* secret handling;
* media access;
* administrative privilege;
* abuse boundaries.

## Privacy Validation

Check:

* sensitive data;
* retention;
* deletion;
* derived-data propagation;
* logging restrictions.

---

# 48. TESTING OF ARCHITECTURE ARTIFACTS

Although this milestone does not implement the complete application, validate the architecture itself.

Perform:

* schema consistency checks;
* contract consistency checks;
* diagram consistency checks;
* terminology consistency checks;
* API/event naming checks;
* ownership checks;
* dependency-direction checks;
* repository documentation linting where available.

Where practical, create machine-checkable schemas for contracts that later implementation prompts can validate.

Do not create tests that claim application behavior exists when only architecture artifacts exist.

---

# 49. DEFINITION OF DONE

This architecture milestone is complete only when:

1. The repository has been inspected where available.
2. The target architecture is documented.
3. Major domains have explicit ownership.
4. Major entities have canonical ownership.
5. Major data stores have defined responsibilities.
6. API conventions are explicit.
7. Initial representative API contracts are defined.
8. Event conventions are explicit.
9. Initial core event contracts are defined.
10. Queue/job conventions are explicit.
11. Media architecture is explicit.
12. Playback architecture is explicit.
13. Search architecture is explicit.
14. Recommendation architecture is explicit.
15. Notification architecture is explicit.
16. Analytics architecture is explicit.
17. Moderation architecture is explicit.
18. Live-stream control-plane architecture is explicit.
19. Authentication and authorization architecture is explicit.
20. Privacy architecture is explicit.
21. Security trust boundaries are documented.
22. Observability architecture is documented.
23. Reliability and failure behavior are documented.
24. Infrastructure topology is documented.
25. Cross-part contracts are documented.
26. Configuration boundaries are documented.
27. Versioning strategy is documented.
28. Material architectural decisions have ADRs.
29. Major risks have mitigations.
30. Architecture artifacts are portable to independent implementation conversations.
31. No critical architectural requirement depends on hidden conversation history.
32. No critical scope has been replaced with pseudo-code or placeholders.
33. Documentation describes the actual architecture produced.
34. Validation has been performed and results are reported honestly.

---

# 50. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every newly created architecture artifact.

## Files Modified

List every existing file modified.

## Files Deleted

List any deleted files, or state that none were deleted.

## Architecture Delivered

Summarize the architectural artifacts created.

## Domains

List the domains and ownership boundaries established.

## Contracts

List the API, event, queue, data, media, authentication, authorization, and integration contracts established.

## Technology Decisions

List major technology and architecture decisions.

## ADRs

List ADRs created or updated.

## Validation

Report:

* checks performed;
* diagrams checked;
* contract consistency checks;
* schema validation;
* documentation validation.

## Known Limitations

Identify architecture areas intentionally deferred to later planned milestones.

## Unresolved Issues

List only genuine unresolved issues.

Do not claim that implementation or deployment has occurred when this milestone only produced architecture artifacts.

# 51. FINAL EXECUTION RULE

Implement and document only the scope defined by this architecture milestone.

Do not implement future backend, frontend, mobile, infrastructure, or QA work merely because this architecture references it.

Do not ask the user to restate the project.

Do not ask the user what architecture you should create.

Do not depend on another AI conversation.

Do not state that an earlier prompt was completed unless the repository proves it.

Use the repository as implementation-state truth.

Create real, portable, implementation-useful architecture artifacts.

Do not stop at a high-level essay.

The output of this milestone must be concrete enough to guide later implementation agents and final integration without requiring undocumented architectural decisions.
