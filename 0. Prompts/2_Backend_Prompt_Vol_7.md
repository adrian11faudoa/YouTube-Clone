# YouTube-Style Video Platform — Backend Prompt — Volume 7

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the seventh bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **live-streaming backend control plane and live-interaction foundation**.

It is responsible for:

* live-stream creation and configuration;
* stream scheduling;
* stream lifecycle management;
* secure ingest configuration;
* stream authorization;
* live playback metadata;
* live-stream state propagation;
* live-stream thumbnails and metadata;
* stream health/state reporting;
* live chat;
* live-chat moderation;
* live participant/viewer-state boundaries;
* live-stream notifications through existing notification contracts;
* live-stream analytics event production;
* stream-to-VOD archival orchestration;
* live-stream processing jobs;
* live-stream failure and recovery behavior;
* concurrency and idempotency;
* operational observability;
* security and abuse prevention;
* testing and operational documentation.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of production-grade global media ingest infrastructure beyond the repository-level control-plane integration required here.

It does not authorize implementation of advertising, payments, web UI, mobile UI, or advanced machine-learning systems.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier AI prompt was executed merely because it exists in the user's conversation.

Do not fabricate repository state.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent, production-grade video platform supporting:

* viewers;
* creators;
* channels;
* long-form video;
* short-form video;
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

This milestone adds the backend control plane required to create, operate, moderate, and consume live streams.

## 2.2 Scale Direction

The completed platform is intended to evolve toward:

* millions of concurrent viewers;
* large numbers of simultaneous streams;
* globally distributed media delivery;
* high-volume live-chat traffic;
* large live-stream event volumes.

This milestone must therefore separate:

* stream control;
* media ingest;
* live playback delivery;
* chat;
* analytics.

Do not route live video bytes through the transactional application backend.

---

# 3. TECHNOLOGY DIRECTION

Use the repository's compatible technology direction:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* durable queues;
* event streaming;
* WebSockets or equivalent realtime transport;
* object storage;
* CDN;
* HLS/DASH-compatible streaming;
* OpenAPI;
* OpenTelemetry-compatible observability.

For live media ingest, use a provider-neutral integration boundary around an actual ingest implementation.

Do not hardcode one cloud provider's private live-stream behavior into the domain layer.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Live-stream domain.
2. Stream creation.
3. Stream metadata management.
4. Stream scheduling.
5. Stream lifecycle state machine.
6. Secure ingest credential/control-plane management.
7. Stream-start authorization.
8. Stream-stop authorization.
9. Live playback metadata.
10. Live manifest/access integration boundary.
11. Stream health/status representation.
12. Live-stream thumbnails.
13. Live-stream chat.
14. Chat message persistence where required.
15. Live-chat realtime transport.
16. Chat moderation integration.
17. Live-chat rate limiting.
18. Live participant/session state where needed.
19. Stream event publication.
20. Live analytics event production.
21. Stream archival/VOD handoff.
22. Stream cleanup.
23. Failure/recovery workflows.
24. Redis usage for ephemeral live state where justified.
25. Notifications through existing notification contracts.
26. Security and abuse prevention.
27. Observability.
28. Unit, integration, realtime, concurrency, security, and API tests.
29. API documentation.
30. Operational documentation.

This milestone does not implement:

* global live-video ingest infrastructure from scratch;
* custom hardware encoding infrastructure;
* full advertising insertion;
* payments;
* advanced live recommendation algorithms;
* full analytics warehouse;
* complete frontend live UI;
* complete mobile live UI.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect the backend architecture.
2. Inspect the channel and video modules.
3. Inspect the media domain.
4. Inspect object storage and CDN abstractions.
5. Inspect authentication and authorization.
6. Inspect notification infrastructure.
7. Inspect moderation.
8. Inspect WebSocket/realtime infrastructure.
9. Inspect queues and event streaming.
10. Inspect Redis.
11. Inspect analytics events.
12. Inspect database migrations.
13. Inspect OpenAPI.
14. Inspect existing tests and observability.

Reuse existing foundations.

Do not create duplicate:

* media systems;
* authentication systems;
* notification systems;
* moderation systems;
* WebSocket gateways;
* event infrastructure.

---

# 6. LIVE-STREAM DOMAIN BOUNDARY

Create or extend a dedicated live-stream domain responsible for:

* stream metadata;
* stream scheduling;
* lifecycle;
* ingest configuration reference;
* playback configuration reference;
* chat configuration;
* live-stream authorization;
* stream-session state;
* archival coordination.

The media subsystem remains responsible for high-bandwidth media processing and storage.

The live-stream domain owns the control-plane state.

Do not store raw live media in PostgreSQL.

---

# 7. LIVE STREAM MODEL

Implement a canonical live-stream entity.

At minimum include:

* live stream ID;
* channel ID;
* owner user ID;
* title;
* description;
* visibility;
* scheduledAt;
* lifecycle state;
* ingest reference;
* playback reference;
* thumbnail reference;
* chat configuration;
* moderation configuration;
* recording/archive configuration;
* createdAt;
* updatedAt;
* startedAt;
* endedAt;
* failure metadata where appropriate.

Do not expose provider-specific credentials in ordinary API responses.

---

# 8. LIVE-STREAM STATES

Implement an explicit state machine.

At minimum support:

* draft;
* scheduled;
* preparing;
* live;
* ending;
* ended;
* failed;
* cancelled.

Valid examples include:

```text
draft
  ├──→ scheduled
  └──→ preparing

scheduled
  └──→ preparing

preparing
  ├──→ live
  ├──→ failed
  └──→ cancelled

live
  └──→ ending

ending
  └──→ ended
```

Do not allow arbitrary client-selected state values.

Provider callbacks or trusted internal events must drive external-state transitions.

---

# 9. STREAM CREATION

Implement creator-authorized stream creation.

Support:

* title;
* description;
* visibility;
* schedule;
* thumbnail metadata;
* chat configuration;
* archive/VOD preference.

Validate:

* channel ownership;
* content metadata;
* scheduling constraints;
* visibility;
* rate limits.

The backend must derive channel ownership from persisted relationships.

Do not trust client-provided owner IDs.

---

# 10. STREAM UPDATE

Allow authorized creators to update editable stream metadata.

Define which fields are editable:

* before going live;
* while live;
* after ending.

Do not allow state-sensitive fields to change arbitrarily.

For example, changing a stream from private to public while already live must pass explicit policy validation.

Do not silently alter canonical lifecycle state through metadata updates.

---

# 11. STREAM SCHEDULING

Implement scheduled streams.

Support:

* future scheduledAt;
* schedule update;
* cancellation;
* transition toward preparing.

Scheduling must be idempotent.

Repeated scheduling requests must not create duplicate preparation jobs.

Scheduled stream state must survive application restarts.

Do not depend on process-local timers for authoritative scheduling.

Use durable jobs or an equivalent scheduler.

---

# 12. INGEST CONFIGURATION

Implement a provider-neutral ingest abstraction.

The abstraction must support:

* ingest endpoint/reference;
* stream identifier;
* secure stream credential/reference;
* lifecycle;
* expiration/rotation where applicable;
* revocation;
* provider metadata.

Do not return long-lived provider secrets through APIs unless the contract explicitly requires a securely controlled stream-key retrieval operation.

Never log stream keys.

Never store stream secrets in plaintext if the architecture allows secure storage/rotation.

---

# 13. STREAM CREDENTIAL SECURITY

Protect ingest credentials.

Requirements:

* creator authorization;
* no public exposure;
* controlled retrieval;
* rotation support;
* revocation;
* auditability.

Do not allow one creator to retrieve another creator's ingest credentials.

Do not accept arbitrary externally supplied stream keys as trusted authorization without explicit validation.

---

# 14. START-STREAM OPERATION

Implement creator-authorized start/control behavior.

A stream can transition toward `live` only when:

* the stream is valid;
* the creator is authorized;
* the stream is in a valid preparatory state;
* the ingest system confirms readiness where the external provider supports it.

The backend must be able to distinguish:

* control-plane start requested;
* ingest detected;
* playback available;
* stream officially live.

Do not declare a stream live merely because a creator pressed a button.

---

# 15. PROVIDER CALLBACK/STATUS INTEGRATION

Implement a secure boundary for receiving stream status from the live-ingest provider or internal media subsystem.

Validate:

* caller/service identity;
* stream identity;
* event version;
* current state;
* signature/authentication where supported.

Provider status must never be accepted from an unauthenticated arbitrary public request.

Handle:

* started;
* healthy;
* degraded;
* disconnected;
* ended;
* failed.

Stale callbacks must not regress current stream state.

---

# 16. STREAM HEALTH MODEL

Represent live-stream health separately from lifecycle state.

Possible health categories include:

* unknown;
* healthy;
* degraded;
* interrupted;
* failed.

Track metadata such as:

* last heartbeat;
* ingest latency where available;
* last provider update;
* bitrate/quality summaries where available;
* reconnect count.

Do not claim measurements that the external provider does not actually provide.

---

# 17. STREAM STOP

Implement authorized stream termination.

Support:

* creator stop;
* automated provider termination;
* administrative termination;
* moderation termination.

The stop operation must be idempotent.

A repeated stop request must not create multiple archival jobs or contradictory events.

---

# 18. LIVE PLAYBACK CONTRACT

Implement playback metadata for live streams.

The playback API must verify:

* stream exists;
* stream is currently playable;
* visibility;
* moderation state;
* playback authorization;
* provider/media readiness.

Return controlled playback metadata including:

* live stream ID;
* playback manifest reference;
* thumbnail;
* current state;
* latency information where available;
* captions where available;
* access metadata.

Do not return private provider credentials.

---

# 19. LIVE CDN/DELIVERY BOUNDARY

Separate:

* live control API;
* ingest;
* media processing;
* manifest;
* CDN delivery.

Transactional APIs must not carry live video bytes.

The live playback API should provide controlled metadata/access information while the CDN delivers the high-bandwidth stream.

---

# 20. LIVE THUMBNAILS

Support:

* scheduled thumbnail;
* creator-supplied thumbnail where supported;
* generated live thumbnail where the media provider exposes it;
* selection state.

Validate thumbnail access.

Do not expose arbitrary provider storage paths.

Do not fabricate generated thumbnails.

---

# 21. LIVE CHAT DOMAIN

Implement live-chat state and realtime messaging.

Support:

* room creation/configuration;
* room membership/session;
* send message;
* receive message;
* message deletion;
* moderation state;
* rate limits;
* slow mode where supported;
* subscriber-only mode where supported;
* member restrictions.

Chat must remain logically separate from the video media stream.

---

# 22. LIVE CHAT MESSAGE MODEL

Implement a canonical message containing:

* message ID;
* live stream ID;
* author user ID;
* body;
* timestamp;
* moderation state;
* reply/reference metadata where supported;
* createdAt;
* deletedAt where applicable.

Do not permit arbitrary users to impersonate authors.

The backend must derive author identity from the authenticated realtime connection.

---

# 23. REALTIME CHAT TRANSPORT

Use the established WebSocket/realtime infrastructure.

Define:

* authentication;
* connection ID;
* stream room;
* join/leave;
* message type;
* message ID;
* acknowledgement where appropriate;
* heartbeat;
* reconnect;
* backpressure;
* ordering;
* deduplication.

Do not create a second realtime transport.

---

# 24. CHAT MESSAGE ORDERING

Within a live-chat room, define practical ordering semantics.

Do not assume distributed wall-clock timestamps are sufficient.

Use:

* server sequence numbers;
* message IDs with ordering metadata;
* room-scoped ordering where appropriate.

Clients must be able to recover after reconnect.

Do not require exactly-once delivery from WebSockets.

Design for at-least-once or explicitly documented delivery semantics.

---

# 25. CHAT RATE LIMITING

Implement strong live-chat rate limits.

Consider:

* per-user;
* per-IP;
* per-stream;
* account age/risk;
* message burst;
* repeated identical message detection.

Support:

* slow mode;
* subscriber-only mode;
* restricted mode where configured.

Do not allow a small number of clients to overwhelm a live-chat room.

---

# 26. CHAT ABUSE PROTECTION

Prevent obvious abuse such as:

* message flooding;
* repeated identical messages;
* link spam;
* oversized messages;
* rapid join/leave churn;
* unauthorized moderation commands.

Do not implement a complete ML spam classifier in this milestone.

Expose structured events/signals for future moderation systems.

---

# 27. CHAT MODERATION

Integrate live chat with the existing moderation system.

Support authorized:

* message deletion;
* user timeout;
* user restriction;
* user removal from room;
* moderator mode;
* stream-level chat disablement.

Use the existing authorization model.

Do not create a separate moderator role hierarchy.

---

# 28. CHAT MODERATION EVENTS

Publish events such as:

* live_chat.message.created;
* live_chat.message.deleted;
* live_chat.user.restricted;
* live_chat.user.removed;
* live_chat.settings.updated.

Events must use the canonical envelope.

Consumers must be idempotent.

Do not publish sensitive moderator notes in public event payloads.

---

# 29. LIVE CHAT STORAGE STRATEGY

Do not store unlimited live-chat traffic in the primary transactional database without an explicit retention strategy.

The implementation may use:

* short-term durable storage;
* Redis for ephemeral delivery state;
* PostgreSQL for necessary durable records;
* event streaming for downstream analytics.

Define:

* retention;
* archival;
* deletion;
* hot/cold storage strategy.

Do not retain full chat history indefinitely by default.

---

# 30. LIVE PARTICIPANT STATE

Where needed, represent ephemeral stream participation state such as:

* active viewer session count;
* active chat connection;
* moderator connection;
* stream room membership.

Do not treat ephemeral concurrent viewer counts as exact transactional business truth unless the product explicitly requires exactness.

Use Redis or an equivalent ephemeral store where justified.

Define TTL/heartbeat behavior.

---

# 31. CONCURRENT VIEWER COUNT

If concurrent-viewer metrics are implemented:

* define the measurement semantics;
* use heartbeats/leases;
* expire inactive sessions;
* avoid unbounded sets;
* distinguish estimated live viewer count from durable historical analytics.

Do not claim exact real-time global concurrency from partially observed distributed data.

---

# 32. LIVE ANALYTICS EVENTS

Emit events required by the analytics system for:

* stream scheduled;
* stream started;
* stream ended;
* viewer joined;
* viewer left;
* playback started;
* chat message;
* stream engagement;
* stream failure.

Do not create a second analytics pipeline.

Use the existing event contracts.

High-volume events must remain asynchronous.

---

# 33. NOTIFICATION INTEGRATION

Emit events needed by the existing notification domain for:

* scheduled-stream reminders;
* stream started;
* stream ended;
* creator live-state changes.

Do not directly call push/email providers from the live-stream domain.

The notification system remains responsible for delivery.

---

# 34. STREAM ARCHIVAL

When recording/archive is enabled:

1. detect stream termination;
2. create an archival job;
3. reference the live recording source;
4. hand off to the media-processing system;
5. create or associate a VOD video;
6. preserve ownership and channel relationship;
7. retain relevant metadata;
8. publish archival lifecycle events.

Do not duplicate transcoding logic from the media subsystem.

The live-stream domain orchestrates the handoff.

---

# 35. LIVE-TO-VOD CONTRACT

Define the relationship between:

* live stream;
* recording;
* media asset;
* resulting VOD video.

The resulting VOD must preserve:

* channel;
* ownership;
* title/description where applicable;
* visibility policy;
* publication policy;
* timestamps;
* media relationship.

Do not automatically publish archived content if the stream's configuration does not authorize it.

---

# 36. STREAM FAILURE RECOVERY

Support recovery from:

* ingest disconnect;
* provider timeout;
* temporary playback failure;
* chat infrastructure failure;
* worker restart;
* application restart.

Distinguish:

* recoverable interruption;
* stream termination;
* permanent failure.

A brief ingest disconnect must not necessarily create a new stream entity.

Do not reset stream IDs unnecessarily.

---

# 37. STREAM RECONNECT

Where supported by the provider architecture, allow reconnect behavior.

Define:

* reconnect window;
* state persistence;
* session continuity;
* event semantics.

A reconnect must not create duplicate:

* archive jobs;
* start events;
* notifications;
* analytics session identifiers.

---

# 38. LIVE-STREAM SECURITY

Protect against:

* stream-key leakage;
* unauthorized start;
* unauthorized stop;
* stream hijacking;
* chat impersonation;
* chat abuse;
* private stream disclosure;
* moderation bypass;
* provider callback forgery.

Use:

* strong authentication;
* explicit authorization;
* secure credential storage;
* signed callbacks where available;
* nonce/request validation where appropriate;
* rate limiting;
* audit logging.

---

# 39. ADMINISTRATIVE LIVE CONTROLS

Provide authorized administrative controls for:

* inspect stream;
* terminate stream;
* restrict stream;
* disable chat;
* remove stream from discovery;
* inspect health.

Every administrative action must use the existing audit system.

Do not provide arbitrary provider commands through public APIs.

---

# 40. DATABASE MODEL

Implement or update models for:

* live streams;
* live-stream sessions;
* ingest configurations;
* live-stream events/state history where justified;
* chat rooms;
* chat messages where persistence is required;
* chat restrictions;
* archive jobs.

Use constraints for:

* stream/channel ownership;
* unique active sessions where required;
* valid states;
* message ownership.

Indexes should support:

* channel streams;
* scheduled streams;
* active streams;
* stream state;
* chat messages by stream and time;
* moderator restrictions.

---

# 41. REDIS USAGE

Use Redis for ephemeral live state where justified.

Potential uses:

* active stream state cache;
* viewer leases;
* chat fan-out;
* room membership;
* slow-mode throttling;
* rate limiting;
* short-lived provider status.

For each key define:

* namespace;
* TTL;
* owner;
* source of truth;
* invalidation;
* failure behavior.

Redis failure must have defined degradation behavior.

---

# 42. QUEUES AND JOBS

Implement jobs for:

* stream preparation;
* scheduled transitions;
* stream cleanup;
* archive/VOD handoff;
* expired stream state;
* chat retention;
* notification-trigger support where needed.

Each job must define:

* idempotency;
* retry;
* backoff;
* timeout;
* concurrency;
* dead-letter behavior;
* observability.

---

# 43. EVENT MODEL

Publish live-stream events such as:

* live_stream.created;
* live_stream.scheduled;
* live_stream.preparing;
* live_stream.started;
* live_stream.health.updated;
* live_stream.interrupted;
* live_stream.resumed;
* live_stream.ended;
* live_stream.failed;
* live_stream.archival.requested;
* live_stream.archival.completed;
* live_stream.archival.failed.

Use the canonical project event envelope.

Do not publish contradictory lifecycle events.

---

# 44. IDEMPOTENCY

Make these operations idempotent:

* create stream where client retries are possible;
* schedule;
* start;
* stop;
* stream-status callbacks;
* archive request;
* chat moderation action;
* moderation removal;
* notification-trigger event generation.

Repeated provider callbacks must not corrupt lifecycle state.

---

# 45. CONCURRENCY CONTROL

Protect against:

* simultaneous start/stop;
* provider callback racing with manual stop;
* reconnect racing with termination;
* two archive jobs;
* concurrent moderator actions;
* chat setting mutations;
* stream deletion while live.

Use:

* optimistic versioning;
* transactions;
* row locks;
* state-transition validation.

Do not use process-local state as the authoritative concurrency mechanism.

---

# 46. API SURFACE

Implement API families for:

## Live Streams

* create;
* get;
* update;
* schedule;
* cancel;
* prepare/start control where authorized;
* stop;
* health/status;
* playback metadata;
* archive status.

## Chat

* room configuration;
* historical/recent messages where supported;
* settings;
* moderator control endpoints where appropriate.

## Creator Controls

* ingest credential/reference management;
* thumbnail;
* visibility;
* scheduling;
* chat configuration.

## Administration

* inspect live stream;
* terminate;
* restrict;
* disable chat.

Use the canonical API error, authentication, authorization, and pagination contracts.

---

# 47. AUTHORIZATION MATRIX

Create/update an implementation-level matrix.

At minimum:

| Operation                    | Anonymous | Authenticated User    | Channel Owner            | Moderator    | Administrator |
| ---------------------------- | --------- | --------------------- | ------------------------ | ------------ | ------------- |
| Read public live metadata    | Allowed   | Allowed               | Allowed                  | Allowed      | Allowed       |
| Create stream                | No        | Allowed if authorized | Allowed                  | Privileged   | Privileged    |
| Update own stream            | No        | Owner only            | Allowed                  | Privileged   | Privileged    |
| Start own stream             | No        | Owner only            | Allowed                  | Privileged   | Privileged    |
| Stop own stream              | No        | Owner only            | Allowed                  | Privileged   | Privileged    |
| Manage own chat settings     | No        | Owner only            | Allowed                  | Privileged   | Privileged    |
| Moderate live chat           | No        | No                    | Where explicitly allowed | Permissioned | Allowed       |
| Terminate arbitrary stream   | No        | No                    | No                       | Permissioned | Allowed       |
| Read private stream playback | No        | Authorized principal  | Owner                    | Privileged   | Privileged    |

Refine the matrix to match the exact implemented roles and routes.

---

# 48. OBSERVABILITY

Implement:

## Stream Metrics

* stream creation;
* schedule-to-start latency;
* active streams;
* stream failures;
* disconnects;
* reconnects;
* start success;
* stop success;
* archive success/failure.

## Chat Metrics

* connections;
* messages per second;
* rejected messages;
* moderation actions;
* room latency;
* rate-limit events;
* connection failures.

## Infrastructure Metrics

* Redis health;
* queue depth;
* worker latency;
* provider callback failures;
* playback metadata latency.

Use:

* request ID;
* correlation ID;
* trace ID;
* stream ID;
* session ID;
* job ID.

Do not log stream keys or signed playback secrets.

---

# 49. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* lifecycle state machine;
* scheduling;
* authorization;
* ingest credential policies;
* playback authorization;
* chat policy;
* reconnect behavior;
* archive orchestration.

## Integration Tests

Test:

* stream persistence;
* provider-status callbacks;
* queue jobs;
* event publication;
* Redis ephemeral state;
* chat persistence/fan-out;
* archive handoff.

## Realtime Tests

Test:

* WebSocket authentication;
* room join;
* message delivery;
* reconnect;
* duplicate message handling;
* ordering;
* disconnect cleanup;
* chat rate limiting.

## Security Tests

Test:

* stream-key protection;
* unauthorized start/stop;
* callback forgery;
* private stream access;
* chat impersonation;
* moderator authorization.

## Concurrency Tests

Test:

* start/stop races;
* callback/manual-stop races;
* reconnect/termination races;
* duplicate archive jobs;
* concurrent chat moderation.

## Failure Tests

Test:

* ingest disconnect;
* Redis outage;
* queue outage;
* provider timeout;
* worker crash;
* playback metadata dependency failure.

---

# 50. PERFORMANCE VALIDATION

Measure:

* stream-control API latency;
* chat throughput;
* chat message latency;
* active-session tracking overhead;
* archive-job latency;
* Redis usage;
* queue throughput.

Use bounded local/test infrastructure.

Do not claim that a local chat benchmark proves global live-chat capacity.

Report measured conditions honestly.

---

# 51. API DOCUMENTATION

Update OpenAPI for:

* live-stream management;
* scheduling;
* playback metadata;
* stream status;
* chat configuration;
* moderator controls;
* archive status.

Do not expose internal provider credentials or worker APIs.

---

# 52. OPERATIONAL DOCUMENTATION

Document:

* live-stream lifecycle;
* ingest-provider configuration;
* credential handling;
* callback authentication;
* chat operations;
* moderation;
* queue jobs;
* archive workflows;
* failure recovery;
* reconnect behavior;
* retention;
* observability;
* incident troubleshooting.

Do not include real stream keys or provider credentials.

Do not claim external ingest/CDN resources are provisioned unless actually validated.

---

# 53. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* global live-ingest infrastructure from scratch;
* provider-specific proprietary media systems without an explicit integration boundary;
* advertising insertion;
* paid livestreams;
* payment processing;
* advanced live recommendation;
* complete analytics warehouse;
* web live-stream UI;
* mobile live-stream UI.

The control-plane implementation must remain compatible with future infrastructure and client work.

---

# 54. VALIDATION REQUIREMENTS

Before completion, verify:

## Lifecycle

* valid transitions succeed;
* invalid transitions fail;
* repeated transitions are idempotent;
* stale callbacks cannot regress state.

## Ingest

* credentials are protected;
* authorized owners can control their streams;
* provider callbacks are authenticated;
* unauthorized control fails.

## Playback

* only eligible streams can be played;
* private streams remain private;
* ended streams stop normal live playback;
* playback metadata does not expose provider secrets.

## Chat

* authentication works;
* message ordering is deterministic;
* rate limits work;
* moderation works;
* reconnect works;
* duplicate messages do not corrupt state.

## Archive

* ending a stream can create exactly one archive request;
* retry does not duplicate archive jobs;
* resulting VOD association remains correct.

## Security

* stream-key leakage tests pass;
* authorization tests pass;
* callback forgery tests pass;
* private-stream tests pass.

## Reliability

* Redis failure degrades appropriately;
* queue failure is recoverable;
* ingest disconnect handling works;
* worker restart recovery works.

---

# 55. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Live-stream domain is implemented.
3. Stream creation is implemented.
4. Stream configuration is implemented.
5. Scheduling is implemented.
6. Lifecycle state management is implemented.
7. Ingest integration boundary is implemented.
8. Stream credential security is implemented.
9. Start/stop controls are implemented.
10. Provider status integration is implemented.
11. Stream health is implemented.
12. Live playback metadata is implemented.
13. CDN/delivery boundary is implemented.
14. Live thumbnails are implemented.
15. Live chat is implemented.
16. Realtime chat transport is implemented.
17. Chat ordering/reconnect behavior is implemented.
18. Chat rate limiting is implemented.
19. Chat moderation integration is implemented.
20. Live participant/session state is implemented where required.
21. Live analytics events are emitted.
22. Notification integration events are emitted.
23. VOD archival orchestration is implemented.
24. Stream failure recovery is implemented.
25. Reconnect behavior is implemented where supported.
26. Administrative live controls are implemented.
27. Redis ephemeral-state behavior is implemented.
28. Required queues/jobs are implemented.
29. Idempotency is implemented.
30. Concurrency control is implemented.
31. Observability is implemented.
32. API documentation is updated.
33. Operational documentation is updated.
34. Unit tests are implemented.
35. Integration tests are implemented.
36. Realtime tests are implemented.
37. Security tests are implemented.
38. Concurrency tests are implemented.
39. Failure/recovery tests are implemented.
40. Performance validation has been performed.
41. No fake live-ingest behavior is presented as a functioning production service.
42. No hardcoded stream credentials or secrets exist.
43. No intentional TODO/FIXME gap substitutes for current-scope functionality.
44. Known limitations are reported honestly.

---

# 56. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Live Streaming

Summarize:

* stream domain;
* lifecycle;
* ingest;
* playback;
* health;
* credentials;
* scheduling.

## Live Chat

Summarize:

* transport;
* ordering;
* persistence;
* moderation;
* rate limits;
* reconnect behavior.

## Archival

Summarize:

* archive orchestration;
* media handoff;
* VOD association.

## Database Changes

List:

* models;
* migrations;
* indexes;
* constraints.

## Events and Jobs

List live-stream events and background jobs.

## Tests

List:

* unit tests;
* integration tests;
* realtime tests;
* security tests;
* concurrency tests;
* failure tests;
* performance validation.

## Documentation

List documentation created or updated.

## Known Limitations

List intentionally deferred functionality.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim that an external live-stream provider, CDN, or cloud environment was provisioned unless that actually occurred.

# 57. FINAL EXECUTION RULE

Implement only the live-streaming control plane, live chat, archival orchestration, security, observability, and supporting backend functionality defined by this milestone.

Do not implement unrelated monetization, advertising, recommendation, moderation-platform expansion, frontend, or mobile functionality.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake live streams, fake ingest callbacks, fake chat transport, placeholder archive behavior, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, secure, observable, scalable live-streaming backend functionality.
