# YouTube-Style Video Platform — Architecture Prompt — Volume 2

# 1. ROLE AND PURPOSE

You are the senior software architect responsible for producing the **binding cross-part contract layer** for the production-grade **YouTube-Style Video Platform**.

This milestone converts the platform's architectural direction into detailed, portable engineering contracts that independently generated backend, web, mobile, infrastructure, media, and QA implementations can consume without inventing incompatible behavior.

This is an architecture-and-contract milestone.

Do not implement the complete application.

Do not implement the complete backend.

Do not implement the complete frontend.

Do not implement the complete mobile applications.

Do not implement production cloud infrastructure.

Do not implement the complete media-processing platform.

Do not implement the complete recommendation system.

Do not implement the complete live-stream media plane.

The output of this milestone must instead establish the **binding contract artifacts** required for those later implementation milestones.

Every contract must be portable outside the originating AI conversation.

Do not rely on another AI response.

Do not rely on hidden conversation history.

Do not refer to an earlier AI prompt as a source of truth.

The repository, when available, is the source of truth for actual files and implementation state.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent, production-grade YouTube-style video platform supporting:

* viewers;
* creators;
* channels;
* long-form video;
* short-form video;
* video uploads;
* media processing;
* adaptive playback;
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
* live-streaming control-plane capabilities;
* monetization-capable integration boundaries.

## 2.2 Scale Direction

The architecture must be capable of evolving toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* petabyte-scale object storage;
* globally distributed CDN delivery;
* high-volume playback telemetry;
* high-volume engagement events;
* large asynchronous processing workloads.

These are target architectural envelopes.

Do not implement every maximum-scale mechanism during this milestone.

## 2.3 Technology Direction

Use the following architecture direction unless repository constraints require a documented compatible variation:

* TypeScript;
* Node.js LTS;
* NestJS;
* REST;
* WebSockets for realtime;
* OpenAPI;
* PostgreSQL;
* Redis;
* Redpanda/Kafka-compatible event streaming where justified;
* durable job queues;
* React;
* Next.js App Router;
* React Native;
* Expo where compatible with required native capabilities;
* OpenSearch or equivalent;
* object storage;
* CDN;
* FFmpeg or equivalent media tooling;
* AWS;
* Kubernetes/EKS where justified;
* Terraform;
* OpenTelemetry.

Do not introduce a technology merely because it appears more sophisticated.

---

# 3. CONTRACT OBJECTIVE

Create a binding contract layer covering:

* identifiers;
* timestamps;
* canonical entity representation;
* states and lifecycle transitions;
* API errors;
* pagination;
* filtering;
* sorting;
* idempotency;
* authentication;
* authorization;
* resource ownership;
* video lifecycle;
* media lifecycle;
* playback;
* comments;
* reactions;
* subscriptions;
* playlists;
* notifications;
* search;
* recommendations;
* analytics events;
* moderation;
* administration;
* live-stream control;
* queues;
* domain events;
* WebSocket/realtime messages;
* configuration;
* environment variables;
* storage;
* observability;
* reliability;
* versioning;
* deployment assumptions;
* service-to-service boundaries.

The resulting artifacts must allow a later coding agent to answer concrete questions such as:

* What is the canonical identifier for a video?
* Which service owns video visibility?
* How does a client express pagination?
* What does an API validation error look like?
* How does the backend distinguish `private`, `unlisted`, and `public`?
* Which event is emitted when processing completes?
* What does a media-processing job contain?
* How is an upload authorized?
* Which actor may edit a video?
* How are duplicate commands prevented?
* What does a WebSocket message look like?
* What happens if a notification provider fails?
* Which data is canonical and which is derived?

Do not leave those answers implicit.

---

# 4. REPOSITORY INSPECTION

Before creating or modifying contract artifacts:

1. Inspect the repository if one is available.
2. Locate existing architecture documents.
3. Locate API contracts.
4. Locate TypeScript domain definitions.
5. Locate database schemas and migrations.
6. Locate OpenAPI specifications.
7. Locate event definitions.
8. Locate queue/job definitions.
9. Locate WebSocket contracts.
10. Locate configuration schemas.
11. Locate existing media abstractions.
12. Locate existing authentication and authorization code.
13. Locate tests validating contracts.
14. Preserve compatible repository conventions where they do not conflict with this milestone.

Do not fabricate existing contracts.

If the repository does not contain an expected artifact, create the required authoritative artifact in the appropriate project documentation location.

Avoid duplicate competing contracts.

There must be one clearly authoritative contract representation for each cross-part concern.

---

# 5. REQUIRED CONTRACT ARTIFACTS

Create or update a portable contract set containing at minimum:

1. Canonical identifier and timestamp specification.
2. Canonical entity/state specification.
3. API conventions specification.
4. API error contract.
5. Pagination/filtering/sorting contract.
6. Idempotency contract.
7. Authentication/session contract.
8. Authorization contract.
9. Video/content contract.
10. Media asset contract.
11. Playback contract.
12. Upload contract.
13. Comment/reaction contract.
14. Subscription contract.
15. Playlist contract.
16. Search contract.
17. Recommendation contract.
18. Notification contract.
19. Moderation contract.
20. Administration contract.
21. Live-stream control-plane contract.
22. WebSocket/realtime contract.
23. Domain event contract.
24. Queue/job contract.
25. Analytics event contract.
26. Storage/object contract.
27. Configuration/environment contract.
28. Observability contract.
29. Reliability/failure contract.
30. Versioning and compatibility contract.
31. Contract ownership matrix.
32. Cross-client compatibility matrix.
33. Architecture handoff document.

Use stable project paths that fit the repository.

A suitable default structure is:

* `docs/architecture/`
* `docs/contracts/`
* `docs/adr/`

Inspect existing repository conventions before creating directories.

---

# 6. CANONICAL IDENTIFIER CONTRACT

Define a single project-wide identifier strategy.

Every major entity must have a stable canonical identifier.

At minimum cover:

* user;
* account;
* session;
* channel;
* video;
* media asset;
* media rendition;
* thumbnail;
* caption track;
* playlist;
* playlist item;
* subscription;
* comment;
* reaction;
* notification;
* report;
* moderation case;
* moderation action;
* live stream;
* live stream session;
* analytics event;
* domain event;
* job;
* idempotency key;
* audit record.

Define:

* identifier type;
* generation method;
* storage representation;
* API representation;
* serialization;
* uniqueness boundary;
* whether the identifier is public;
* whether it is guessable;
* whether it may be exposed in URLs;
* whether it must remain immutable.

Prefer a globally unique strategy suitable for independently generated components.

Do not allow one subsystem to use a different public identifier model without a documented reason.

---

# 7. TIME CONTRACT

Define project-wide timestamp conventions.

Use UTC as the canonical storage and transport basis unless a specialized external protocol requires another representation.

Define:

* `createdAt`;
* `updatedAt`;
* `publishedAt`;
* `deletedAt` where applicable;
* `scheduledAt`;
* `occurredAt` for events;
* `expiresAt`;
* `processedAt`;
* `startedAt`;
* `endedAt`.

Define:

* serialization;
* precision;
* server versus client authority;
* ordering assumptions;
* clock-skew handling.

Client-provided timestamps must never silently override authoritative server timestamps for system state.

Event ordering must not rely only on wall-clock timestamps.

Where ordering matters, use explicit sequence/version information.

---

# 8. CANONICAL ENTITY STATE CONTRACT

Define lifecycle states for major entities.

At minimum define:

## Video

States should explicitly cover concepts such as:

* draft;
* uploading;
* uploaded;
* processing;
* ready;
* scheduled;
* published;
* restricted;
* blocked;
* failed;
* deleted.

Define valid transitions.

For example:

```text
draft
  ↓
uploading
  ↓
uploaded
  ↓
processing
  ├──→ failed
  └──→ ready
          ├──→ scheduled
          └──→ published
```

Do not allow clients to create invalid transitions.

## Media Asset

Define states such as:

* pending;
* uploaded;
* validating;
* processing;
* ready;
* failed;
* deleted.

## Live Stream

Define states such as:

* draft;
* scheduled;
* preparing;
* live;
* ending;
* ended;
* failed;
* archived.

## Moderation Case

Define states appropriate to:

* open;
* under_review;
* actioned;
* dismissed;
* appealed;
* closed.

Use stable enum values.

Do not create near-duplicate names with different meanings in different modules.

---

# 9. API CONTRACT

Define the common REST API conventions.

Use a consistent resource style.

Define:

* API base path;
* versioning strategy;
* resource naming;
* HTTP methods;
* status code semantics;
* request validation;
* response envelope rules;
* error envelope;
* pagination;
* filtering;
* sorting;
* idempotency;
* authorization failures;
* rate limiting;
* correlation headers.

The API contract must support both web and mobile clients.

Do not require clients to know database schema details.

Do not expose internal service names as external resource names unless deliberately designed as part of the public contract.

---

# 10. CANONICAL API ERROR CONTRACT

Define one standardized error model.

The contract must include fields appropriate for:

* stable error code;
* human-readable message;
* HTTP status;
* request/correlation identifier;
* validation details;
* retryability;
* documentation reference where appropriate.

Example structure:

```json
{
  "error": {
    "code": "VIDEO_NOT_ACCESSIBLE",
    "message": "The requested video cannot be accessed.",
    "status": 403,
    "requestId": "req_...",
    "retryable": false,
    "details": []
  }
}
```

The exact identifier value and serialization conventions must be specified by the contract.

Do not allow individual endpoints to invent unrelated error formats.

Define representative categories including:

* validation failure;
* authentication failure;
* authorization failure;
* resource not found;
* conflict;
* rate limited;
* unavailable;
* dependency failure;
* internal failure.

Do not leak internal stack traces or sensitive details.

---

# 11. PAGINATION, FILTERING, AND SORTING CONTRACT

Define the project-wide collection semantics.

For high-volume collections, use cursor pagination where appropriate.

Define:

* cursor format;
* page size;
* maximum page size;
* default page size;
* next cursor;
* previous cursor where supported;
* stable sort requirements;
* filtering syntax;
* validation behavior.

Define deterministic ordering.

Do not use offset pagination for workloads where offsets create unacceptable performance or consistency problems.

Document when offset pagination is acceptable.

---

# 12. IDEMPOTENCY CONTRACT

Define idempotency behavior for operations that may be retried.

At minimum consider:

* video upload initiation;
* upload completion;
* video publication;
* playlist mutations;
* subscription creation;
* notification requests;
* moderation actions;
* live-stream lifecycle operations;
* payment-related commands where later implemented;
* background jobs.

Define:

* idempotency key format;
* scope;
* TTL;
* storage;
* request fingerprinting;
* replay behavior;
* conflict behavior;
* response replay rules.

Idempotency must prevent accidental duplicate side effects without hiding genuinely conflicting requests.

---

# 13. AUTHENTICATION AND SESSION CONTRACT

Define a binding authentication contract for:

* web;
* mobile;
* REST;
* WebSocket;
* creator APIs;
* administrative APIs;
* upload authorization.

Define:

* credential model;
* password hashing;
* access token behavior where used;
* refresh token behavior;
* rotation;
* revocation;
* session tracking;
* logout;
* device/session visibility;
* account recovery;
* email verification;
* external identity integration.

The contract must explicitly distinguish:

* authentication;
* session;
* authorization.

Do not place authorization decisions into client code.

---

# 14. AUTHORIZATION CONTRACT

Define a consistent server-side authorization model.

Authorization decisions must take into account:

* authenticated principal;
* ownership;
* role;
* requested action;
* resource state;
* visibility;
* moderation restrictions.

At minimum define permissions for:

## Users

* manage own account;
* manage own sessions;
* manage own playlists;
* manage own subscriptions;
* interact with allowed public content.

## Channel Owners

* create channel;
* update channel;
* upload content;
* edit content;
* publish content;
* schedule content;
* manage comments;
* manage live streams;
* view creator analytics.

## Moderators

* review reports;
* take moderation actions;
* access authorized moderation data.

## Administrators

* manage privileged operational functionality;
* access authorized administrative resources;
* execute audited administrative actions.

Do not expose moderator/admin capabilities through normal user roles.

---

# 15. VIDEO CONTRACT

Define the canonical video resource.

The contract should cover fields such as:

* video ID;
* channel ID;
* title;
* description;
* visibility;
* lifecycle state;
* publication state;
* duration;
* thumbnails;
* media asset relationship;
* captions;
* category;
* tags;
* language;
* age/content restrictions where applicable;
* creation timestamps;
* publication timestamps;
* scheduling;
* processing metadata;
* moderation status.

Separate:

* user-authored metadata;
* system-generated metadata;
* derived analytics;
* moderation state.

Define which fields are creator-editable and which are system-controlled.

---

# 16. VISIBILITY AND ACCESS CONTRACT

Define canonical video visibility semantics.

At minimum distinguish:

* public;
* unlisted;
* private;
* restricted/blocked where applicable.

Define:

* who may discover;
* who may view;
* whether search indexes it;
* whether recommendations may surface it;
* whether direct URL access is allowed;
* how deletion affects access;
* how moderation restrictions affect playback.

Visibility must be enforced server-side.

Search, recommendations, feeds, APIs, and playback must consume the same canonical access model.

---

# 17. UPLOAD CONTRACT

Define the secure upload lifecycle.

At minimum:

```text
Create Upload Session
        ↓
Authorize Upload
        ↓
Resumable Transfer
        ↓
Finalize Upload
        ↓
Validate Asset
        ↓
Queue Processing
        ↓
Track Processing State
```

Define:

* upload session identifier;
* authorized principal;
* target video;
* expected file metadata;
* size limits;
* MIME/type validation;
* chunking/resume semantics;
* upload expiration;
* completion behavior;
* duplicate completion behavior;
* cancellation;
* failed upload handling;
* object storage location;
* access controls.

Application servers must not be required to proxy the entire media payload unless deliberately justified.

---

# 18. MEDIA ASSET CONTRACT

Define the canonical media representation.

Include:

* asset ID;
* owner/video relationship;
* original object metadata;
* checksum;
* content type;
* size;
* duration;
* codec information;
* processing status;
* renditions;
* manifests;
* thumbnails;
* caption tracks;
* storage location abstraction;
* lifecycle;
* deletion state.

Derived media must remain linked to the canonical source asset.

---

# 19. PLAYBACK CONTRACT

Define the playback control-plane contract.

A playback authorization/request must be capable of determining:

* requested video;
* requesting principal;
* access rights;
* visibility;
* restriction status;
* playback availability;
* available formats/renditions;
* manifest information;
* captions;
* resume position where supported;
* telemetry context.

Do not return internal storage paths as a substitute for a media-delivery contract.

Define the boundary between:

* API metadata;
* manifest;
* signed media access;
* CDN delivery.

---

# 20. ENGAGEMENT CONTRACT

Define canonical contracts for:

* likes;
* negative feedback where configured;
* comments;
* comment replies;
* comment reactions;
* shares.

Define:

* ownership;
* actor;
* target;
* creation;
* deletion;
* visibility;
* moderation;
* idempotency;
* counter semantics.

High-frequency counters must be treated as derived or eventually consistent where appropriate.

Do not require every displayed count to be transactionally exact at every instant.

---

# 21. COMMENT CONTRACT

Define:

* comment ID;
* video ID;
* author ID;
* parent comment ID;
* body;
* moderation state;
* visibility;
* createdAt;
* updatedAt;
* deletedAt;
* reaction summary where appropriate;
* creator moderation state.

Define lifecycle behavior for:

* create;
* edit;
* delete;
* hide;
* restore;
* report;
* moderate.

Specify how deleted parent comments affect replies.

Specify authorization rules for creator moderation.

---

# 22. SUBSCRIPTION CONTRACT

Define a canonical subscription relationship:

* subscriber user;
* channel;
* subscription state;
* notification preference;
* createdAt;
* updatedAt.

Define idempotent subscribe/unsubscribe behavior.

Define how subscription events propagate to:

* subscription feeds;
* recommendations;
* notification decisions;
* analytics.

---

# 23. PLAYLIST CONTRACT

Define canonical playlist behavior including:

* playlist ID;
* owner;
* title;
* description;
* visibility;
* ordering;
* items;
* createdAt;
* updatedAt.

Define item ordering strategy.

Define mutation semantics for:

* create;
* edit;
* add item;
* remove item;
* reorder;
* delete.

Define how deleted/private videos are represented inside existing playlists.

---

# 24. SEARCH CONTRACT

Define search as a derived read system.

Search contract must define:

* query;
* entity scope;
* filters;
* sort;
* cursor;
* page size;
* result representation;
* search metadata;
* index freshness behavior.

Define canonical indexed fields for:

* video;
* channel;
* creator.

Define content lifecycle rules:

* publish → index;
* update → reindex;
* restrict → update access;
* delete → remove from index.

Search must never override canonical authorization rules.

---

# 25. RECOMMENDATION CONTRACT

Define an interface that allows recommendation implementations to evolve.

The contract must support inputs such as:

* viewer ID;
* anonymous/session context where supported;
* current video;
* watch history;
* subscriptions;
* engagement signals;
* content metadata;
* freshness;
* negative feedback;
* safety filters.

Define output fields sufficient for:

* content ID;
* ranking position;
* recommendation reason/category;
* model/ranking version where applicable;
* experiment identifier where applicable;
* expiration/freshness metadata where appropriate.

Recommendation implementations must not directly control authorization.

---

# 26. NOTIFICATION CONTRACT

Define a canonical notification object.

At minimum:

* notification ID;
* recipient;
* type;
* actor;
* target;
* payload metadata;
* createdAt;
* read state;
* delivery state;
* deduplication key;
* channel.

Define notification preferences.

Define delivery channels:

* in-app;
* push;
* email.

Define how failed providers behave.

Notification generation must be separable from notification delivery.

---

# 27. MODERATION CONTRACT

Define canonical moderation objects:

* report;
* moderation case;
* evidence reference;
* action;
* reason;
* actor;
* target;
* status;
* timestamps.

Define moderation actions such as:

* hide;
* restrict;
* remove;
* suspend;
* block;
* restore.

Define audit requirements.

Define how moderation state affects:

* search;
* recommendation;
* playback;
* comments;
* channel visibility.

---

# 28. ADMINISTRATION CONTRACT

Define administrative APIs and permissions at a contract level.

Administrative resources must include:

* explicit actor identity;
* required permission;
* target resource;
* requested action;
* reason where applicable;
* audit correlation;
* resulting state.

Sensitive operations must produce audit records.

Administrative actions must not bypass ordinary domain invariants unless explicitly designed as privileged operations with corresponding audit controls.

---

# 29. LIVE-STREAM CONTRACT

Define the control-plane resource for live streaming.

At minimum:

* live stream ID;
* channel ID;
* title;
* description;
* visibility;
* scheduledAt;
* lifecycle state;
* ingest configuration reference;
* playback reference;
* chat configuration;
* moderation configuration;
* thumbnail;
* createdAt;
* startedAt;
* endedAt.

Define lifecycle commands:

* create;
* update;
* schedule;
* prepare;
* start;
* stop;
* cancel.

Define which operations are creator-only, moderator-only, or administrative.

Do not expose raw stream credentials through ordinary read APIs.

---

# 30. WEB SOCKET / REALTIME CONTRACT

Define realtime message conventions.

At minimum define:

* connection authentication;
* connection ID;
* channel/room semantics;
* message type;
* message ID;
* timestamp;
* payload;
* correlation information;
* acknowledgements where applicable;
* heartbeat;
* reconnect;
* duplicate handling;
* ordering assumptions;
* rate limits.

Use explicit message types.

Potential realtime domains include:

* live chat;
* notifications;
* creator processing status;
* live-stream state;
* administrative updates.

Do not require realtime where an ordinary API or asynchronous notification is sufficient.

---

# 31. DOMAIN EVENT CONTRACT

Define the canonical event envelope.

At minimum:

```json
{
  "eventId": "evt_...",
  "eventType": "video.published",
  "version": 1,
  "occurredAt": "2026-01-01T00:00:00.000Z",
  "producer": "video-domain",
  "correlationId": "corr_...",
  "causationId": "cmd_...",
  "payload": {}
}
```

The exact field names must be finalized in the authoritative artifact.

Define event evolution rules.

Events must be immutable once published.

Consumers must be idempotent.

Do not use events as an excuse to duplicate canonical ownership.

---

# 32. CORE EVENT CATALOG

Create a concrete catalog for at least:

## Identity

* user.created;
* user.updated;
* user.deleted;
* session.revoked.

## Channel

* channel.created;
* channel.updated;
* channel.deleted.

## Video

* video.created;
* video.upload.initiated;
* video.upload.completed;
* video.processing.started;
* video.processing.completed;
* video.processing.failed;
* video.published;
* video.unpublished;
* video.restricted;
* video.deleted.

## Engagement

* comment.created;
* comment.updated;
* comment.deleted;
* reaction.created;
* reaction.removed.

## Subscription

* subscription.created;
* subscription.deleted;
* notification.preference.updated.

## Playlist

* playlist.created;
* playlist.updated;
* playlist.item.added;
* playlist.item.removed;
* playlist.deleted.

## Moderation

* report.created;
* moderation.case.opened;
* moderation.action.applied;
* moderation.action.reversed.

## Notifications

* notification.requested;
* notification.delivered;
* notification.failed.

## Live

* live_stream.created;
* live_stream.started;
* live_stream.ended;
* live_stream.failed.

## Analytics

Define representative playback, engagement, discovery, and creator analytics event families.

---

# 33. QUEUE AND JOB CONTRACT

Define a standard job envelope.

At minimum include:

* job ID;
* job type;
* schema version;
* createdAt;
* scheduledAt where applicable;
* producer;
* attempt;
* idempotency key;
* correlation ID;
* payload.

Define queue contracts for:

* media processing;
* thumbnail generation;
* caption processing;
* search indexing;
* notifications;
* analytics;
* recommendation computation;
* moderation automation;
* cleanup;
* scheduled publication.

Each job type must define:

* producer;
* consumer;
* retries;
* backoff;
* timeout;
* concurrency;
* dead-letter strategy;
* idempotency behavior.

---

# 34. ANALYTICS EVENT CONTRACT

Define a canonical analytics event envelope.

At minimum capture:

* event ID;
* event name;
* schema version;
* occurredAt;
* actor identifier where appropriate;
* anonymous/session identifier where applicable;
* subject/resource identifier;
* client platform;
* application version;
* correlation context where useful;
* privacy classification;
* payload.

Define representative events such as:

* video.impression;
* video.play.started;
* video.play.progress;
* video.play.completed;
* video.like;
* video.share;
* video.subscription.created;
* search.performed;
* recommendation.impression;
* recommendation.clicked;
* creator.video.published;
* creator.video.performance.updated.

High-volume playback telemetry must have explicit aggregation/sampling considerations.

---

# 35. STORAGE CONTRACT

Define storage abstractions for:

* original uploads;
* processed renditions;
* thumbnails;
* captions;
* exports;
* moderation evidence where applicable.

The application must interact with storage through controlled abstractions.

Do not scatter raw provider-specific bucket paths throughout business logic.

Define:

* object key conventions;
* metadata;
* content types;
* lifecycle;
* ownership;
* access model;
* signed access;
* deletion;
* retention.

Provider-specific implementation details belong behind the storage boundary.

---

# 36. CONFIGURATION CONTRACT

Define canonical environment/configuration names.

At minimum account for:

* application environment;
* API base configuration;
* database;
* Redis;
* event streaming;
* queues;
* search;
* object storage;
* CDN;
* authentication;
* observability;
* external providers.

Separate:

* non-secret configuration;
* secret values;
* public client configuration.

Define naming conventions.

Define validation requirements.

Applications must fail clearly when required configuration is absent rather than silently using insecure defaults.

---

# 37. SERVICE-TO-SERVICE CONTRACT

Define internal service/module communication rules.

For each internal boundary specify:

* caller;
* owner;
* synchronous API or event;
* request timeout;
* retry policy;
* authentication;
* authorization;
* error propagation;
* observability context.

Do not permit arbitrary direct database access across domain ownership boundaries.

A consumer should request data through the owning domain's contract or through an intentionally defined read model.

---

# 38. CONTRACT OWNERSHIP MATRIX

Create a master matrix:

| Contract | Owner | Consumers | Canonical Artifact | Compatibility Rule | Change Procedure |
| -------- | ----- | --------- | ------------------ | ------------------ | ---------------- |

Include:

* user/account;
* channel;
* video;
* media;
* playback;
* comments;
* subscriptions;
* playlists;
* notifications;
* search;
* recommendations;
* moderation;
* live streaming;
* APIs;
* events;
* queues;
* configuration;
* observability;
* authorization.

This matrix must become the integration reference for later implementation.

---

# 39. CLIENT COMPATIBILITY MATRIX

Create a matrix covering:

| Capability | Web | Mobile | Backend | Realtime | Offline/Cache Requirements | Notes |
| ---------- | --- | ------ | ------- | -------- | -------------------------- | ----- |

Cover:

* authentication;
* video discovery;
* playback;
* channels;
* subscriptions;
* comments;
* playlists;
* notifications;
* search;
* creator workflows;
* uploads;
* live streaming;
* moderation-aware behavior where applicable.

The matrix must expose contract differences explicitly rather than allowing each client to invent behavior.

---

# 40. VERSIONING AND EVOLUTION CONTRACT

Define compatibility rules for:

* APIs;
* events;
* queue payloads;
* database schemas;
* search documents;
* analytics events;
* mobile clients;
* web clients.

Define:

* additive changes;
* breaking changes;
* deprecation;
* rollout;
* migration;
* compatibility windows.

Events and APIs must evolve without forcing synchronized deployment of all consumers unless the architecture explicitly requires it.

Database migrations must support safe deployment ordering.

---

# 41. RETRY AND FAILURE CONTRACT

Define standard failure behavior for:

* HTTP requests;
* service-to-service requests;
* jobs;
* events;
* WebSocket connections;
* media processing;
* storage access;
* search;
* notifications.

Define when retries are allowed.

Do not blindly retry:

* validation errors;
* authorization failures;
* permanent not-found conditions;
* non-idempotent mutations without idempotency protection.

Define retryable versus non-retryable failures.

Use bounded exponential backoff with jitter where appropriate.

---

# 42. RATE-LIMITING CONTRACT

Define rate-limit categories for:

* authentication;
* account recovery;
* uploads;
* API reads;
* API mutations;
* comments;
* reactions;
* subscriptions;
* search;
* WebSocket messages;
* report submission;
* administrative operations.

Define:

* scope;
* key;
* limit;
* window;
* burst behavior;
* response;
* retry-after semantics.

The implementation may tune exact numeric thresholds later, but the contract must define where rate limiting exists and how clients observe enforcement.

---

# 43. CACHING CONTRACT

Define cacheable resources and consistency expectations.

For each major cache category define:

* key;
* source of truth;
* TTL;
* invalidation;
* stale behavior;
* ownership;
* failure behavior.

Potential cached representations include:

* public video metadata;
* channel metadata;
* feed fragments;
* recommendation results;
* search suggestions;
* subscription status;
* notification counts.

Do not cache highly sensitive authorization decisions without explicit invalidation and security controls.

---

# 44. SECURITY CONTRACT MATRIX

Create a matrix mapping:

| Operation | Principal | Authentication | Authorization | Sensitive Data | Audit | Rate Limit |
| --------- | --------- | -------------- | ------------- | -------------- | ----- | ---------- |

At minimum cover:

* account management;
* channel management;
* upload;
* publish;
* playback;
* comments;
* moderation;
* reporting;
* live-stream control;
* administration;
* analytics access.

Ensure the matrix reflects server-side authorization.

---

# 45. DATA RETENTION AND DELETION CONTRACT

Define lifecycle rules for:

* accounts;
* sessions;
* deleted videos;
* original media;
* derived media;
* thumbnails;
* captions;
* comments;
* analytics events;
* moderation records;
* audit events;
* search documents;
* recommendation data;
* notification records.

Define:

* soft deletion versus hard deletion;
* propagation to derived systems;
* index removal;
* cache invalidation;
* object-storage cleanup;
* retention exceptions;
* audit retention.

Do not silently leave deleted user content accessible through derived systems.

---

# 46. OBSERVABILITY CONTRACT

Create one project-wide observability convention.

Define:

* request ID;
* correlation ID;
* trace ID;
* span ID;
* job ID;
* event ID;
* structured log fields.

Define standard metric families for:

* request latency;
* request errors;
* dependency errors;
* database latency;
* cache performance;
* queue depth;
* job retries;
* job failures;
* event lag;
* media processing;
* search;
* recommendations;
* notification delivery;
* live-stream control;
* upload failures.

Define log redaction requirements.

Sensitive data must not appear in telemetry.

---

# 47. SERVICE LEVEL AND RELIABILITY CONTRACT

Create initial service-level objectives or target categories for critical paths.

At minimum define target classes for:

* authentication;
* core API;
* video metadata;
* playback-control API;
* search;
* recommendations;
* upload initialization;
* media processing;
* notification dispatch;
* moderation API;
* live-stream control.

Do not invent false precision.

Where exact values are not yet finalized, define:

* target class;
* measurement method;
* error-budget owner;
* alerting expectation.

Define which capabilities may degrade without violating the core product experience.

---

# 48. DISASTER RECOVERY CONTRACT

Define recovery expectations for:

* PostgreSQL;
* Redis where state matters;
* object storage;
* event streams;
* search indexes;
* analytical data;
* configuration;
* infrastructure state.

Define:

* backup ownership;
* restore authority;
* RPO category;
* RTO category;
* rebuildability;
* dependency ordering.

Search and other derived systems should have a documented rebuild path from canonical sources.

Do not treat every derived cache as a backup.

---

# 49. EXTERNAL INTEGRATION CONTRACTS

Define integration boundaries for:

* OAuth/OIDC providers;
* email;
* push notifications;
* payment providers;
* advertising providers;
* content scanning/safety providers;
* cloud storage;
* CDN.

For each define:

* internal abstraction;
* request direction;
* credentials boundary;
* timeout;
* retry;
* idempotency;
* failure behavior;
* webhook/event handling;
* security expectations.

Do not fabricate provider credentials.

Do not hardcode provider behavior that has not been verified.

---

# 50. CONTRACT CONSISTENCY RULES

The entire contract set must use consistent:

* entity names;
* ID names;
* API route names;
* event names;
* job names;
* enum values;
* state transitions;
* timestamp names;
* status values;
* error codes;
* authorization terminology;
* configuration names.

Examples:

Use one canonical concept for:

* `videoId`, not alternating `id`, `video_id`, and `contentId`;
* `channelId`, not alternating `creatorId` for channel identity;
* `createdAt`, not multiple timestamp spellings;
* one stable visibility enum;
* one stable moderation state model.

Database-specific snake_case may be used internally, but public contracts must remain stable and deliberate.

---

# 51. ARCHITECTURAL CHANGE CONTROL

Define how future implementation prompts may change contracts.

A contract change must identify:

* affected contract;
* owner;
* consumers;
* compatibility impact;
* migration;
* test changes;
* documentation changes;
* rollout order.

No implementation prompt may silently introduce a breaking contract merely because its local implementation is easier.

Breaking changes require an explicit architectural decision and migration path.

---

# 52. IMPLEMENTATION HANDOFF SPECIFICATION

Create a concise handoff document that future implementation agents can use as a contract reference.

It must include:

## System Rules

* canonical terminology;
* major domains;
* source-of-truth boundaries.

## API Rules

* URL conventions;
* HTTP semantics;
* errors;
* pagination;
* idempotency;
* authorization.

## Event Rules

* envelope;
* naming;
* versioning;
* retries;
* idempotency.

## Data Rules

* identifier model;
* timestamps;
* ownership;
* lifecycle.

## Media Rules

* upload;
* storage;
* processing;
* playback;
* CDN.

## Client Rules

* authentication;
* API consumption;
* realtime;
* cache behavior.

## Infrastructure Rules

* environment names;
* service boundaries;
* observability;
* external dependencies.

## Integration Rules

* forbidden assumptions;
* compatibility requirements;
* ownership.

The handoff must be useful even when supplied by itself to a fresh implementation conversation together with the Master Prompt and that conversation's bounded implementation prompt.

---

# 53. WHAT YOU MUST CREATE

Create or update the complete binding contract artifact set required by this milestone.

Do not simply write one long narrative.

Prefer a document set with stable files, for example:

* `docs/contracts/identifier-time.md`
* `docs/contracts/api.md`
* `docs/contracts/errors.md`
* `docs/contracts/pagination.md`
* `docs/contracts/idempotency.md`
* `docs/contracts/authentication.md`
* `docs/contracts/authorization.md`
* `docs/contracts/video.md`
* `docs/contracts/media.md`
* `docs/contracts/playback.md`
* `docs/contracts/engagement.md`
* `docs/contracts/subscriptions.md`
* `docs/contracts/playlists.md`
* `docs/contracts/search.md`
* `docs/contracts/recommendations.md`
* `docs/contracts/notifications.md`
* `docs/contracts/moderation.md`
* `docs/contracts/live-streaming.md`
* `docs/contracts/realtime.md`
* `docs/contracts/events.md`
* `docs/contracts/jobs.md`
* `docs/contracts/analytics.md`
* `docs/contracts/storage.md`
* `docs/contracts/configuration.md`
* `docs/contracts/observability.md`
* `docs/contracts/reliability.md`
* `docs/contracts/versioning.md`
* `docs/contracts/ownership-matrix.md`
* `docs/contracts/client-compatibility.md`
* `docs/contracts/integration-handoff.md`

Adapt paths to the actual repository when necessary.

Do not create redundant competing files if equivalent artifacts already exist.

---

# 54. WHAT YOU MUST NOT IMPLEMENT

This milestone does not authorize:

* complete application code;
* complete domain services;
* complete database migrations;
* complete web UI;
* complete mobile UI;
* complete media workers;
* complete live ingest;
* complete recommendation algorithms;
* complete search implementation;
* complete infrastructure provisioning;
* production deployment;
* end-to-end product functionality.

Do not replace contract work with application placeholders.

---

# 55. VALIDATION REQUIREMENTS

Before completing the milestone, perform the following validations.

## Contract Validation

Verify that:

* every major entity has one canonical name;
* every major entity has a canonical ID;
* all timestamps use the same convention;
* state values are consistent;
* visibility values are consistent;
* moderation terminology is consistent;
* API error structures are consistent;
* pagination is consistent;
* idempotency is consistent;
* event envelopes are consistent;
* job envelopes are consistent.

## Cross-Domain Validation

Verify compatibility across:

* identity ↔ channels;
* channels ↔ videos;
* videos ↔ media;
* videos ↔ playback;
* videos ↔ search;
* videos ↔ recommendations;
* subscriptions ↔ notifications;
* engagement ↔ analytics;
* moderation ↔ visibility;
* live streaming ↔ media;
* administration ↔ moderation;
* all domains ↔ authorization.

## Client Validation

Verify that web and mobile clients can independently consume the defined contracts without requiring hidden server implementation knowledge.

## Failure Validation

Verify that every major asynchronous or external dependency has:

* retry behavior;
* non-retryable conditions;
* idempotency behavior;
* timeout behavior;
* fallback or degradation;
* observability.

## Security Validation

Verify:

* authentication boundaries;
* authorization boundaries;
* upload security;
* private playback;
* administrative security;
* secret handling;
* rate limiting;
* auditability.

## Privacy Validation

Verify:

* sensitive-data classification;
* retention;
* deletion;
* derived-system propagation;
* telemetry restrictions.

---

# 56. TESTING OF CONTRACT ARTIFACTS

Where the repository supports machine validation:

* validate JSON schemas;
* validate OpenAPI schemas;
* validate event schemas;
* validate TypeScript contract definitions;
* validate enum consistency;
* validate generated documentation references.

Create contract tests or schema tests only where they validate actual authoritative artifacts.

Do not create fake endpoint implementations solely to make contract tests pass.

---

# 57. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected where available.
2. The canonical identifier strategy is defined.
3. The canonical timestamp strategy is defined.
4. Entity lifecycle states are defined.
5. API conventions are binding and documented.
6. Error handling is standardized.
7. Pagination is standardized.
8. Filtering/sorting rules are defined.
9. Idempotency is defined.
10. Authentication is defined.
11. Authorization is defined.
12. Video contracts are defined.
13. Upload contracts are defined.
14. Media contracts are defined.
15. Playback contracts are defined.
16. Engagement contracts are defined.
17. Subscription contracts are defined.
18. Playlist contracts are defined.
19. Search contracts are defined.
20. Recommendation contracts are defined.
21. Notification contracts are defined.
22. Moderation contracts are defined.
23. Administration contracts are defined.
24. Live-stream control contracts are defined.
25. WebSocket/realtime contracts are defined.
26. Event contracts are defined.
27. Queue/job contracts are defined.
28. Analytics contracts are defined.
29. Storage contracts are defined.
30. Configuration contracts are defined.
31. Observability conventions are defined.
32. Reliability conventions are defined.
33. Versioning rules are defined.
34. Ownership matrices are complete.
35. Client compatibility is documented.
36. Data retention/deletion behavior is documented.
37. Disaster recovery expectations are documented.
38. External integration boundaries are documented.
39. The implementation handoff is complete.
40. Contract validation has been performed.
41. No competing or contradictory contract remains undocumented.
42. The artifact set is portable to independent implementation conversations.
43. No current-scope requirement has been replaced with pseudo-code or placeholders.

---

# 58. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new contract artifact.

## Files Modified

List every modified artifact.

## Files Deleted

List deleted artifacts, or state that none were deleted.

## Contracts Established

Summarize the contracts completed.

## Ownership

Summarize ownership boundaries.

## Compatibility

Summarize web/mobile/backend compatibility assumptions.

## Validation

Report:

* schema validation;
* API contract validation;
* event validation;
* job validation;
* terminology validation;
* cross-domain validation.

## Known Limitations

Identify genuine deferred decisions only.

## Unresolved Issues

List only unresolved architectural contract issues.

Do not claim that application functionality has been implemented.

# 59. FINAL EXECUTION RULE

Implement and document only the contract and architecture scope defined by this milestone.

Do not implement unrelated backend, frontend, mobile, infrastructure, media, search, recommendation, moderation, or QA functionality.

Do not depend on another AI conversation.

Do not assume another architecture artifact exists outside the repository or the contract set created here.

Do not fabricate external services, provider behavior, credentials, or deployment state.

Create concrete, machine-usable, implementation-ready contracts.

The objective is to eliminate cross-part ambiguity before independent implementation begins.
