# YouTube-Style Video Platform — Backend Prompt — Volume 3

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the third bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **media, playback, media-processing orchestration, and high-volume delivery control plane**.

It is responsible for turning uploaded video assets into a production-capable processing pipeline and exposing the backend contracts required for playback.

This milestone includes:

* media asset management;
* object-storage integration;
* secure resumable-upload completion handling;
* media validation;
* transcoding job orchestration;
* processing-state management;
* rendition management;
* thumbnail generation orchestration;
* caption-track metadata;
* adaptive-streaming manifest generation/orchestration;
* playback authorization;
* playback metadata APIs;
* signed media-access boundaries;
* CDN integration boundaries;
* processing retries;
* processing failure recovery;
* media cleanup;
* playback progress integration where necessary;
* media-related observability;
* media security;
* media-processing tests.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of search, recommendations, notifications, analytics pipelines, moderation tooling, payments, advertising, full live-stream media infrastructure, web UI, or mobile UI.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier prompt was executed merely because it exists in the conversation.

Do not fabricate repository state.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent, production-grade video platform supporting:

* viewers;
* creators;
* channels;
* long-form videos;
* short-form videos;
* uploads;
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
* live streaming;
* monetization-capable integrations.

This milestone implements the media plane and playback control plane required by the video product.

## 2.2 Scale Direction

The completed platform is intended to evolve toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* petabyte-scale media storage;
* globally distributed CDN delivery;
* large media-processing workloads.

The current milestone does not need to operate at the maximum global target immediately.

However, the implementation must avoid:

* routing large media payloads through application servers unnecessarily;
* storing video binaries in PostgreSQL;
* synchronous transcoding in API requests;
* unbounded worker concurrency;
* single-instance processing assumptions;
* provider-specific storage logic scattered throughout the domain layer.

---

# 3. TECHNOLOGY DIRECTION

Use the repository's established compatible stack.

The target direction is:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* object storage;
* CDN;
* FFmpeg or equivalent media processing;
* HLS and DASH-compatible adaptive streaming;
* durable background jobs;
* event streaming where already established;
* OpenAPI;
* OpenTelemetry-compatible observability.

For cloud storage, the target infrastructure direction is AWS-compatible object storage and CDN delivery.

Do not hardcode cloud credentials.

Do not claim external infrastructure is provisioned unless it has actually been provisioned and validated.

Provider-specific SDK usage must remain behind clear infrastructure abstractions.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Media-asset domain.
2. Media-object abstraction.
3. Object-storage integration.
4. Secure resumable upload completion.
5. Uploaded-object verification.
6. Media metadata extraction.
7. Media validation.
8. Processing-job orchestration.
9. Processing state transitions.
10. Transcoding-worker integration.
11. Rendition registration.
12. Thumbnail generation orchestration.
13. Caption-track metadata.
14. Manifest generation/orchestration.
15. Media publication readiness.
16. Playback authorization.
17. Playback metadata API.
18. Signed playback-access boundary.
19. CDN-origin integration boundary.
20. Media lifecycle cleanup.
21. Retry and dead-letter behavior.
22. Processing idempotency.
23. Playback security.
24. Media-related metrics, logs, and tracing.
25. Media-processing API and contract tests.
26. Operational documentation.

Do not implement the complete recommendation system.

Do not implement the search system.

Do not implement notification delivery.

Do not implement the full analytics pipeline.

Do not implement the moderation operator system.

Do not implement the live-stream media ingest platform.

Do not implement payments or advertising.

Do not implement frontend playback UI.

Do not implement mobile playback UI.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect the backend architecture.
2. Inspect the existing video module.
3. Inspect upload-session implementation.
4. Inspect the existing storage abstraction.
5. Inspect database migrations.
6. Inspect existing job infrastructure.
7. Inspect event publication.
8. Inspect Redis usage.
9. Inspect configuration.
10. Inspect API error handling.
11. Inspect authentication and authorization.
12. Inspect observability infrastructure.
13. Inspect existing tests.
14. Inspect any existing media contracts and architecture documentation.

Reuse compatible existing abstractions.

Do not create duplicate storage or job systems.

If an expected infrastructure abstraction does not exist, implement the minimal reusable abstraction required by this milestone.

---

# 6. MEDIA DOMAIN BOUNDARY

Create or extend a dedicated media domain that owns:

* media assets;
* processing state;
* renditions;
* thumbnails;
* caption-track metadata;
* manifests;
* processing attempts;
* media lifecycle;
* media-derived metadata.

The video domain owns:

* video identity;
* video ownership;
* publication state;
* video visibility;
* creator-authored metadata.

The media domain must not become the source of truth for channel ownership.

A media asset must always be associated with the canonical video it serves.

---

# 7. MEDIA ASSET MODEL

Implement the canonical media asset model.

At minimum represent:

* media asset ID;
* video ID;
* source object reference;
* source checksum where available;
* source size;
* source MIME type;
* media duration;
* video width;
* video height;
* frame rate where available;
* audio presence;
* codec information;
* processing state;
* processing profile/version;
* createdAt;
* updatedAt;
* deletedAt where applicable.

Do not persist raw binary video data in PostgreSQL.

Store only metadata and controlled references to object storage.

---

# 8. MEDIA LIFECYCLE

Implement explicit media states such as:

* pending;
* uploaded;
* validating;
* processing;
* ready;
* failed;
* deleting;
* deleted.

Define valid transitions.

At minimum:

```text
pending
  ↓
uploaded
  ↓
validating
  ├──→ failed
  └──→ processing
          ├──→ failed
          └──→ ready
```

Deletion must have an explicit lifecycle.

Do not permit arbitrary client-controlled media state transitions.

System state changes must be triggered by backend operations or trusted worker results.

---

# 9. STORAGE ABSTRACTION

Implement or extend a provider-neutral media storage abstraction.

It must support at minimum:

* create resumable upload target;
* inspect object metadata;
* verify object existence;
* verify checksum where supported;
* generate controlled upload authorization;
* move/copy objects where required;
* create derived-object references;
* delete objects;
* generate controlled read access;
* apply lifecycle metadata where appropriate.

The abstraction must not expose provider-specific credential material to application code unnecessarily.

Provider-specific storage paths must not become domain-level contracts.

---

# 10. OBJECT KEY STRATEGY

Define a deterministic storage-key strategy.

Object keys must be derived from:

* environment;
* media ownership boundary;
* media asset ID;
* object purpose;
* rendition or artifact identity;
* version where applicable.

Do not use user-controlled file names directly as trusted object paths.

Prevent path traversal or arbitrary object-key manipulation.

Avoid embedding sensitive personal information in object keys.

The same object-key convention must be used consistently by:

* upload;
* processing;
* rendition generation;
* thumbnail generation;
* caption storage;
* cleanup.

---

# 11. UPLOAD COMPLETION VERIFICATION

Extend the foundational upload session so that finalization performs real verification.

The backend must verify:

* upload session ownership;
* upload session validity;
* upload expiration;
* expected object existence;
* object size;
* content type;
* checksum where available;
* storage metadata;
* association with the correct media asset.

Do not trust the client to declare an upload complete.

Do not mark the video processing-ready merely because the client called a completion endpoint.

---

# 12. MEDIA VALIDATION

Implement server-side validation before transcoding.

Validate:

* file existence;
* file size;
* supported container;
* supported codecs;
* duration limits;
* resolution limits;
* malformed media;
* dangerous or unsupported media structures;
* expected metadata;
* audio/video stream presence as required;
* corrupted source data.

Reject invalid media deterministically.

Produce a stable media-validation error.

Do not expose low-level FFmpeg or parser internals directly to API clients.

---

# 13. SECURITY SCANNING BOUNDARY

Where security or malware scanning is configured, establish an explicit scanning boundary before processing untrusted uploaded content.

The architecture must support:

* scanning state;
* scanning result;
* failure;
* rejection;
* retry;
* auditability.

Do not claim malware scanning exists merely because an interface was created.

If no scanner is configured in the execution environment, implement the correct integration boundary and report the external dependency accurately.

Do not invent scanner results.

---

# 14. MEDIA METADATA EXTRACTION

Implement metadata extraction using a controlled media-processing component.

Extract appropriate information such as:

* duration;
* video dimensions;
* frame rate;
* codec;
* bitrate;
* audio presence;
* audio codec;
* source container;
* stream metadata.

Persist authoritative metadata in the media domain.

Do not trust user-provided metadata when actual media inspection can determine the value.

The extracted metadata must be available to:

* processing;
* playback;
* thumbnails;
* API responses;
* later analytics.

---

# 15. TRANSCODING PROFILE MODEL

Define explicit transcoding profiles.

The profile must identify:

* profile ID;
* profile version;
* target resolution;
* video codec;
* audio codec;
* bitrate;
* frame-rate policy;
* audio sample rate where relevant;
* container;
* segment duration;
* quality policy.

The system must not hardcode encoding parameters inside controllers or arbitrary worker functions.

Store profile/version references with processing jobs.

This allows the platform to evolve its encoding ladder later without changing the core media model.

---

# 16. ADAPTIVE BITRATE RENDITIONS

Implement the backend representation of multiple renditions.

A rendition must include:

* rendition ID;
* media asset ID;
* profile/version;
* width;
* height;
* frame rate;
* video bitrate;
* audio bitrate;
* codec;
* object reference;
* manifest inclusion status;
* processing state;
* createdAt.

The platform should support multiple quality levels.

Do not assume one rendition is sufficient for production playback.

Exact encoding profiles must follow repository configuration and architecture rather than being duplicated throughout business logic.

---

# 17. TRANSCODING JOBS

Create durable media-processing jobs.

A job must include:

* job ID;
* media asset ID;
* video ID;
* processing profile/version;
* input object reference;
* output policy/profile references;
* attempt;
* idempotency key;
* correlation ID;
* createdAt;
* scheduledAt where applicable.

Do not include raw media bytes.

Jobs must be safe to retry.

Do not create duplicate outputs when the same idempotent processing request is retried.

---

# 18. WORKER IMPLEMENTATION

Implement the actual media-processing worker required by this milestone.

The worker must:

1. claim a job safely;
2. verify the asset still exists;
3. verify the source object;
4. transition processing state;
5. execute media inspection/transcoding;
6. generate required renditions;
7. generate thumbnails;
8. generate or prepare manifests;
9. persist derived metadata;
10. publish completion or failure events;
11. record processing duration;
12. release job resources correctly.

Do not implement the worker as a fake stub.

Use real media-processing tooling available in the execution environment.

Do not substitute placeholder files for actual transcoded output.

---

# 19. WORKER CONCURRENCY

Control worker concurrency.

Do not launch an unbounded number of FFmpeg processes.

Define:

* concurrency limit;
* CPU/memory expectations;
* job timeout;
* cancellation behavior;
* graceful shutdown;
* retry behavior.

Worker concurrency must be configurable.

The worker must not process the same media asset concurrently through multiple attempts unless explicitly safe.

Use job locking or equivalent infrastructure.

---

# 20. TRANSCODING FAILURE HANDLING

A processing failure must:

* record a stable failure category;
* preserve enough diagnostic metadata for operators;
* transition the media state correctly;
* increment the attempt;
* retry when retryable;
* stop retrying when permanent;
* move permanently failed jobs to dead-letter handling where applicable;
* emit a failure event.

Do not expose internal stack traces or process command lines to public clients.

Differentiate:

* invalid source media;
* transient infrastructure failure;
* storage failure;
* worker timeout;
* unsupported codec;
* resource exhaustion;
* permanent processing failure.

---

# 21. RETRY POLICY

Implement bounded retries.

Use:

* maximum attempts;
* exponential backoff;
* jitter;
* timeout;
* dead-letter behavior.

Do not retry permanent media-validation failures indefinitely.

Do not retry non-idempotent operations without protection.

Record retry attempts for operational visibility.

---

# 22. THUMBNAIL GENERATION

Implement real thumbnail generation.

Generate configured thumbnail representations using the media-processing pipeline.

Support:

* deterministic thumbnail selection or configured capture positions;
* suitable dimensions;
* image encoding;
* object storage;
* media-asset association;
* cleanup.

Do not trust arbitrary client-supplied thumbnail files as the canonical thumbnail unless the product contract explicitly permits them.

If custom creator-uploaded thumbnails are supported, validate and integrate them through a separate controlled path.

---

# 23. THUMBNAIL CONTRACT

Each thumbnail record should contain:

* thumbnail ID;
* media asset ID or video ID;
* purpose;
* width;
* height;
* format;
* object reference;
* selected/default state;
* createdAt.

Ensure only authorized principals can change the selected thumbnail.

Do not expose raw provider storage credentials.

---

# 24. CAPTION TRACK METADATA

Implement caption/subtitle metadata management needed for playback.

At minimum support:

* caption-track ID;
* media asset/video ID;
* language;
* label;
* format;
* object reference;
* status;
* createdAt;
* updatedAt.

This milestone does not require a complete automatic speech recognition system.

However, the media model and processing pipeline must be capable of representing future generated captions.

Do not fabricate generated captions.

If caption ingestion is supported by the current repository contract, validate uploaded caption files and persist them through the storage abstraction.

---

# 25. MANIFEST GENERATION

Implement adaptive-streaming manifest generation or orchestration.

Support an architecture compatible with:

* HLS;
* DASH where required.

The resulting manifest must reference valid processed renditions.

The manifest-generation step must not run before required renditions are ready.

A manifest must not expose nonexistent media objects.

Manifest generation must be idempotent.

---

# 26. MEDIA READINESS

The backend must distinguish:

* source upload completed;
* source validated;
* processing started;
* processing completed;
* media ready;
* video publishable.

A video must not be treated as playback-ready merely because the source object exists.

The video domain must receive a trusted media-readiness signal.

Publishability must be driven by verified media state.

---

# 27. MEDIA-VIDEO INTEGRATION

Integrate the media domain with the video domain.

At minimum:

* video references its canonical media asset;
* media asset references its owning video;
* processing completion updates video publishability;
* media failure prevents publication;
* deletion removes/invalidates playback access;
* restricted video state affects playback access.

Do not create duplicate video ownership models inside the media module.

---

# 28. PLAYBACK AUTHORIZATION

Implement the backend playback authorization boundary.

A playback request must verify:

1. authenticated principal when authentication is required;
2. video existence;
3. video visibility;
4. moderation/restriction state;
5. publication state;
6. media readiness;
7. requester's access rights;
8. playback eligibility.

Support:

* public videos;
* private videos;
* unlisted videos;
* restricted videos.

Do not authorize playback based solely on possession of a video ID.

---

# 29. PLAYBACK METADATA API

Implement a playback metadata API.

It must return only information necessary for a client to begin playback.

Depending on the established contract, include:

* video ID;
* duration;
* available renditions;
* manifest reference;
* thumbnails;
* captions;
* playback restrictions;
* playback authorization metadata;
* server timing/context needed by the client.

Do not expose internal database records.

Do not expose private object-storage credentials.

Do not return arbitrary storage paths when signed/CDN access is required.

---

# 30. SIGNED PLAYBACK ACCESS

Implement controlled media-access authorization.

Where private or protected assets require authorization, generate short-lived access through the storage/CDN abstraction.

Define:

* expiration;
* resource scope;
* audience;
* signing boundary;
* revocation limitations;
* cache behavior.

Do not generate long-lived public media URLs for private content.

Do not embed cloud signing credentials in application code.

Keep signing implementation behind infrastructure abstractions.

---

# 31. CDN INTEGRATION

Implement the backend/CDN boundary required for media delivery.

The backend must be capable of resolving media access through:

* CDN URL conventions;
* signed access where required;
* cache behavior;
* origin/path abstraction.

Do not route media bytes through NestJS controllers.

Do not proxy high-bandwidth video data through the transactional backend.

The backend owns authorization and access metadata.

The CDN/object storage system owns high-volume media delivery.

---

# 32. PRIVATE AND UNLISTED VIDEO ACCESS

Implement correct semantics.

## Private

Only authorized principals may obtain playback metadata and access.

## Unlisted

The content may be accessible using an authorized direct reference according to the product contract, but must not be treated as public discovery content.

Future search/recommendation systems must be able to consume the canonical visibility state.

Do not allow unlisted/private content to become unintentionally enumerable.

---

# 33. PLAYBACK ACCESS EXPIRATION

Playback authorization must expire appropriately.

Do not issue effectively permanent signed URLs for protected content.

The expiration period must be configurable and appropriate for streaming startup/access behavior.

Ensure clock skew and expiration validation are handled safely.

---

# 34. PLAYBACK CACHE STRATEGY

Cache playback metadata only when safe.

Public media metadata may be cacheable.

Private authorization decisions must not be cached in a way that can leak access across users.

When caching playback metadata:

* include relevant content state/version;
* invalidate after visibility changes;
* invalidate after deletion/restriction;
* define TTL;
* avoid cross-user contamination.

---

# 35. PLAYBACK PROGRESS INTEGRATION

Integrate this milestone with the existing playback-progress domain.

The playback API may return the user's existing resume position where authorized.

It must not expose another user's progress.

Do not move ownership of playback progress into the media domain.

The existing playback-progress owner remains authoritative.

---

# 36. VIDEO PUBLICATION INTEGRATION

Integrate media readiness with video publication.

A video may transition into `published` only when:

* required source validation has succeeded;
* required processing has completed;
* required manifest/rendition artifacts exist;
* content is not blocked/restricted;
* publication requirements are satisfied.

Do not implement publication as a blind status update.

If scheduled publication is retried, the media readiness check must remain deterministic.

---

# 37. MEDIA DELETION

Implement media cleanup.

When a video/media asset is deleted according to lifecycle rules:

1. remove or invalidate playback access;
2. mark media state appropriately;
3. schedule/delete source object;
4. schedule/delete renditions;
5. schedule/delete thumbnails;
6. schedule/delete manifests;
7. remove captions where applicable;
8. clear caches;
9. publish the appropriate lifecycle event.

Do not make a destructive storage operation the only record of deletion.

Maintain metadata required for auditability and recovery policy.

---

# 38. CLEANUP JOBS

Implement background cleanup jobs for media artifacts.

They must support:

* retry;
* idempotency;
* dead-letter behavior;
* observability.

Do not immediately perform potentially expensive multi-object deletion inside a user-facing request unless the operation is demonstrably small and safe.

The API should return after the canonical domain state is safely committed.

---

# 39. STORAGE FAILURE HANDLING

Handle:

* object-not-found;
* permission failure;
* timeout;
* transient provider error;
* checksum mismatch;
* incomplete multipart state;
* CDN-origin failure.

Do not convert every storage error into an internal 500 without useful classification.

Expose stable public errors while retaining diagnostic internal metadata.

---

# 40. DATABASE MODEL FOR MEDIA

Implement or update database models for:

* media asset;
* media rendition;
* thumbnail;
* caption track;
* processing job metadata;
* manifest metadata where persisted;
* processing attempt records where needed.

Use foreign keys and constraints.

Index:

* video → media asset;
* media asset → renditions;
* media asset → thumbnails;
* processing state;
* scheduled processing;
* failed jobs requiring retry.

Do not persist large manifests unnecessarily when they can be derived reliably, unless operational requirements justify persistence.

---

# 41. PROCESSING JOB STATE

Use an explicit job lifecycle such as:

* queued;
* running;
* completed;
* retrying;
* failed;
* dead_lettered;
* cancelled.

A job attempt must have enough metadata to diagnose failures.

Do not allow an old retry to overwrite a newer successful state.

Use job versioning, attempt IDs, or state checks where required.

---

# 42. IDEMPOTENCY

Make media operations idempotent where retries are expected.

At minimum:

* upload finalization;
* media-processing job creation;
* transcoding output registration;
* thumbnail generation;
* manifest generation;
* cleanup;
* playback-access generation where meaningful.

Duplicate processing attempts must not produce conflicting database records or duplicate canonical artifacts.

---

# 43. EVENT MODEL

Publish media-domain events using the established event contract.

At minimum:

* media.uploaded;
* media.validation.started;
* media.validation.completed;
* media.validation.failed;
* media.processing.started;
* media.processing.completed;
* media.processing.failed;
* media.rendition.created;
* media.thumbnail.created;
* media.manifest.created;
* media.ready;
* media.deleted.

Events must contain:

* event ID;
* event type;
* version;
* occurredAt;
* producer;
* correlation ID where applicable;
* payload.

Do not publish duplicate or contradictory events.

---

# 44. EVENT DELIVERY RELIABILITY

Use transactional event delivery where required.

An event describing committed media state must not be published as though it succeeded if the database transaction later rolls back.

Use an outbox or equivalent reliable mechanism.

Worker-generated completion events must only represent successfully persisted processing results.

If event publication fails, the system must have a retry/recovery mechanism.

---

# 45. OBSERVABILITY

Implement media-specific observability.

Track:

* upload-finalization latency;
* validation duration;
* transcoding duration;
* processing queue depth;
* processing attempts;
* processing failures;
* worker CPU/memory usage where measurable;
* rendition generation success;
* thumbnail generation failures;
* manifest generation failures;
* playback authorization latency;
* signed-access generation failures;
* storage latency;
* storage error rate;
* CDN-origin errors where visible to the backend;
* cleanup backlog.

Use standard:

* request ID;
* correlation ID;
* trace ID;
* job ID;
* media asset ID;
* video ID.

Do not log private signed URLs or cloud credentials.

---

# 46. SECURITY REQUIREMENTS

Protect the media subsystem against:

* unauthorized upload;
* arbitrary object access;
* object-key manipulation;
* private-content disclosure;
* signed-URL abuse;
* replay of upload completion requests;
* path traversal;
* malicious media input;
* resource exhaustion;
* processing-worker overload;
* unauthorized deletion.

Use:

* strict ownership checks;
* input validation;
* short-lived signed access;
* storage isolation;
* resource limits;
* worker concurrency limits;
* timeouts;
* audit logging for privileged media actions.

Do not trust client-provided:

* object path;
* media readiness;
* duration;
* codec;
* content type;
* processing result.

---

# 47. RESOURCE LIMITS

Define and enforce limits for:

* maximum upload size;
* maximum duration;
* maximum source resolution;
* maximum number of renditions;
* maximum processing time;
* maximum worker memory/CPU request where supported;
* maximum concurrent jobs;
* maximum caption size;
* maximum thumbnail dimensions.

Exact values should come from the repository's configuration conventions or project configuration.

Do not hardcode production limits into business logic.

---

# 48. API SURFACE

Implement the media/playback API surface required by this milestone.

At minimum include endpoint families for:

## Upload

* create upload target/session;
* inspect upload state;
* finalize upload;
* cancel upload where applicable.

## Media

* inspect media processing status;
* retrieve canonical media metadata where authorized.

## Playback

* request playback metadata;
* resolve playback access;
* retrieve available renditions/captions metadata where required.

## Creator Media Management

* list processing state for owned videos;
* retry eligible failed processing;
* select supported thumbnail where applicable;
* manage caption metadata where explicitly supported.

Do not expose internal worker-control endpoints publicly.

Privileged worker operations must use authenticated service-to-service boundaries.

---

# 49. SERVICE-TO-SERVICE SECURITY

Protect worker and internal media APIs.

Worker actions must authenticate using service identity or another explicitly defined internal authentication mechanism.

Do not allow an anonymous caller to:

* mark media ready;
* create arbitrary renditions;
* declare transcoding complete;
* delete arbitrary media;
* alter processing state.

Internal APIs must validate:

* caller identity;
* job identity;
* media identity;
* allowed action;
* request version.

---

# 50. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Cover:

* media-state transitions;
* processing-profile selection;
* upload verification;
* visibility/playback authorization;
* signed-access policy;
* cleanup decisions;
* retry classification;
* idempotency.

## Integration Tests

Cover:

* object-storage integration through the abstraction;
* upload finalization;
* media metadata persistence;
* processing jobs;
* worker state transitions;
* database transactions;
* event publication;
* Redis/cache behavior;
* cleanup.

Where external cloud resources are unavailable, use a realistic local/emulator/test implementation without pretending it is the production cloud.

## Media Processing Tests

Use real sample media fixtures that are safe to include in the repository or generated during tests.

Test:

* metadata extraction;
* validation;
* transcoding;
* rendition creation;
* thumbnail generation;
* manifest generation;
* failure behavior.

Do not replace all media tests with mocks.

## API Tests

Test:

* public playback;
* private playback;
* unlisted playback;
* restricted playback;
* unauthorized access;
* expired signed access;
* invalid media;
* processing failure;
* upload finalization.

## Concurrency Tests

Test:

* duplicate processing;
* duplicate finalization;
* concurrent worker attempts;
* cleanup versus playback;
* retry after partial processing;
* old job completion after newer state.

---

# 51. PERFORMANCE TESTING

Measure media-processing and API behavior appropriate to this scope.

At minimum inspect:

* processing throughput;
* job latency;
* worker concurrency;
* playback metadata latency;
* signed-access generation latency;
* storage interaction latency.

Do not benchmark only happy-path application code while ignoring media-processing bottlenecks.

Document performance observations honestly.

---

# 52. API DOCUMENTATION

Update OpenAPI documentation for all public APIs introduced by this milestone.

Document:

* authentication;
* authorization;
* request schemas;
* response schemas;
* playback states;
* processing states;
* errors;
* pagination where applicable;
* signed-access semantics;
* retry behavior where externally relevant.

Do not document internal worker commands as public endpoints.

---

# 53. OPERATIONAL DOCUMENTATION

Document:

* media-processing worker setup;
* required FFmpeg/runtime dependencies;
* storage configuration;
* processing profiles;
* job queues;
* retry policies;
* dead-letter behavior;
* worker concurrency;
* local development;
* sample media fixtures;
* troubleshooting;
* media cleanup;
* storage failure recovery;
* operational dashboards and key metrics.

Do not include real cloud credentials.

Do not claim production CDN, object storage, or Kubernetes resources exist when the repository only contains configuration for them.

---

# 54. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* full search;
* search indexing;
* recommendation ranking;
* recommendation candidate generation;
* notification delivery;
* analytics warehouse;
* creator analytics;
* moderation operator dashboard;
* automated trust-and-safety classification;
* advertising;
* payment processing;
* full live-stream media ingest;
* live CDN infrastructure;
* web playback UI;
* mobile playback UI.

The media contracts and events may be consumed by these future domains.

Do not implement those domains in this milestone.

---

# 55. VALIDATION REQUIREMENTS

Before completion, verify:

## Upload

* only authorized users can initialize uploads;
* upload session ownership is enforced;
* object verification is real;
* invalid files are rejected;
* duplicate finalization is safe.

## Processing

* valid uploads enter processing;
* workers claim jobs safely;
* real media processing occurs;
* renditions are registered correctly;
* failures produce correct state;
* retries are bounded;
* dead-letter behavior works.

## Playback

* public videos can be authorized;
* private videos remain protected;
* unlisted semantics are correct;
* restricted videos cannot be played;
* media must be ready before normal playback access;
* signed access expires appropriately.

## Storage

* object keys are controlled;
* storage credentials are protected;
* deletion is idempotent;
* cleanup is recoverable.

## Events

Verify:

* event names;
* event versions;
* payloads;
* transactional consistency;
* retry behavior.

## Security

Verify:

* authorization;
* upload ownership;
* signed-access restrictions;
* object-key security;
* worker authentication;
* rate limits;
* sensitive log exclusion.

## Observability

Verify:

* processing metrics;
* worker traces;
* request correlation;
* failure logs;
* job IDs;
* media IDs.

---

# 56. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. The media domain is implemented.
3. Media assets are persisted correctly.
4. Object storage integration is real.
5. Upload completion performs server-side verification.
6. Media validation is implemented.
7. Metadata extraction is implemented.
8. Processing profiles are implemented.
9. Media-processing jobs are implemented.
10. Real media-processing workers are implemented.
11. Processing concurrency is bounded.
12. Retry behavior is implemented.
13. Dead-letter handling is implemented where required.
14. Rendition metadata is persisted.
15. Thumbnail generation is implemented.
16. Manifest generation is implemented.
17. Caption-track metadata is implemented.
18. Media readiness is integrated with video publication.
19. Playback authorization is implemented.
20. Playback metadata APIs are implemented.
21. Signed/private media-access boundaries are implemented.
22. CDN integration boundaries are implemented.
23. Media deletion/cleanup is implemented.
24. Cleanup jobs are implemented.
25. Media domain events are implemented.
26. Reliable event publication is implemented.
27. Observability is implemented.
28. Security protections are implemented.
29. Resource limits are enforced.
30. API documentation is updated.
31. Operational documentation is updated.
32. Media-processing tests exist.
33. Integration tests exist.
34. API tests exist.
35. Security tests exist.
36. Concurrency tests exist.
37. Relevant performance validation has been performed.
38. No fake media-processing implementation remains within scope.
39. No placeholder output substitutes for required transcoding or processing.
40. No hardcoded secrets exist.
41. Known limitations are reported honestly.

---

# 57. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Media Architecture

Summarize:

* media asset model;
* storage;
* processing;
* renditions;
* thumbnails;
* captions;
* manifests.

## Processing

Summarize:

* workers;
* queues;
* concurrency;
* retries;
* dead-letter behavior.

## Playback

Summarize:

* authorization;
* metadata;
* signed access;
* CDN boundary.

## Database Changes

List:

* tables/models;
* migrations;
* indexes;
* constraints.

## Events

List:

* media events;
* producers;
* delivery mechanism.

## Tests

List:

* media fixtures;
* unit tests;
* integration tests;
* API tests;
* security tests;
* concurrency tests;
* performance validation.

## Documentation

List documentation created or updated.

## Known Limitations

List intentionally deferred functionality.

## Unresolved Issues

List only genuine unresolved issues.

Do not claim production cloud deployment or external-provider provisioning unless it actually occurred.

# 58. FINAL EXECUTION RULE

Implement only the media, processing, playback-control, storage, and supporting backend functionality defined by this milestone.

Do not implement unrelated future backend domains.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake media output, fake transcoding, fake storage, placeholders, pseudo-code, or intentionally incomplete implementations within this scope.

Produce real, tested, secure, observable, scalable media and playback backend functionality.
