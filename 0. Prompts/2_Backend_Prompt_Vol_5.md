# YouTube-Style Video Platform — Backend Prompt — Volume 5

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the fifth bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **notification, product-analytics, creator-analytics, and behavioral-event processing backend**.

This milestone establishes the backend capabilities required to transform domain events and product activity into:

* in-app notifications;
* push/email notification workflows;
* notification preferences;
* notification delivery state;
* durable product telemetry;
* playback analytics ingestion;
* engagement analytics;
* creator analytics;
* content-performance aggregates;
* audience analytics;
* analytics processing jobs;
* event deduplication;
* analytical retention boundaries;
* privacy-aware analytics;
* operational analytics metrics.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of the full moderation system, administration platform, live-streaming media infrastructure, monetization systems, advertising infrastructure, frontend applications, or mobile applications.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier AI prompt was executed merely because it exists in the conversation.

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
* media uploads;
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

This milestone implements the backend systems that communicate important product activity to users and transform product events into analytical information.

## 2.2 Scale Direction

The completed platform is intended to evolve toward:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* extremely high playback-event volume;
* high engagement-event volume;
* large notification fan-out;
* large creator-analytics workloads.

This milestone must therefore avoid:

* writing every playback heartbeat synchronously to PostgreSQL;
* generating one synchronous external notification call per domain mutation;
* coupling transactional requests to analytical processing;
* creating unbounded notification fan-out inside a request;
* using product analytics as a direct dependency of core playback.

---

# 3. TECHNOLOGY DIRECTION

Use the repository's existing compatible stack.

Target components include:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* durable job queues;
* Redpanda/Kafka-compatible event streaming where already established;
* object storage or analytical storage where required;
* OpenAPI;
* OpenTelemetry;
* external push/email providers behind abstractions.

Do not introduce a second event-processing platform without a concrete architectural reason.

Do not build a full analytical data warehouse if the current repository and milestone only require the bounded analytical persistence and processing layer.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Notification domain.
2. Notification preference management.
3. In-app notification persistence.
4. Notification deduplication.
5. Notification aggregation where justified.
6. Push-notification integration boundary.
7. Email-notification integration boundary.
8. Notification delivery jobs.
9. Notification retry/dead-letter handling.
10. Product analytics event ingestion.
11. Playback telemetry ingestion.
12. Engagement telemetry ingestion.
13. Discovery telemetry ingestion.
14. Creator analytics event processing.
15. Video-performance aggregates.
16. Channel-performance aggregates.
17. Audience summaries.
18. Watch-time analytics.
19. Engagement analytics.
20. Traffic/source summaries where supported by current event contracts.
21. Analytics event validation.
22. Analytics deduplication.
23. Analytics privacy controls.
24. Analytics retention controls.
25. Aggregation jobs.
26. Analytics query APIs for creator-owned data.
27. Notification and analytics observability.
28. Tests for notification and analytics behavior.
29. API documentation.
30. Operational documentation.

This milestone does not implement:

* moderation operations;
* full administrative dashboards;
* advanced recommendation models;
* model training;
* advertising;
* payment processing;
* live-stream media infrastructure;
* complete analytics warehouse infrastructure beyond the current scoped needs;
* web UI;
* mobile UI.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect the notification-related architecture.
2. Inspect existing domain events.
3. Inspect subscriptions.
4. Inspect user/account data.
5. Inspect channels and videos.
6. Inspect playback-progress infrastructure.
7. Inspect reactions/comments/subscriptions.
8. Inspect search/discovery events.
9. Inspect queue/job infrastructure.
10. Inspect Redis.
11. Inspect configuration.
12. Inspect existing external-provider abstractions.
13. Inspect analytics/event contracts.
14. Inspect database migrations.
15. Inspect API documentation.
16. Inspect tests.
17. Inspect observability.

Reuse compatible infrastructure.

Do not create duplicate event buses, queue systems, configuration systems, or authentication mechanisms.

---

# 6. DOMAIN BOUNDARIES

Create explicit backend ownership boundaries.

## Notifications

Own:

* notification definitions;
* recipient state;
* notification preferences;
* notification delivery state;
* deduplication;
* notification aggregation;
* delivery jobs.

Notifications do not own subscription relationships.

## Analytics

Own:

* analytical event ingestion;
* event validation;
* event normalization;
* deduplication;
* aggregation;
* creator analytics read models;
* retention policies.

Analytics does not own transactional product entities.

## Creator Analytics

Own:

* creator-facing aggregate read models;
* video performance summaries;
* channel performance summaries;
* audience summaries;
* analytics query APIs.

Creator analytics must derive from canonical event data and product domains.

---

# 7. NOTIFICATION DOMAIN MODEL

Implement a canonical notification model.

At minimum include:

* notification ID;
* recipient user ID;
* notification type;
* actor ID where applicable;
* target resource type;
* target resource ID;
* payload metadata;
* createdAt;
* readAt;
* delivery status;
* delivery channels;
* deduplication key;
* aggregation key where applicable;
* expiration where applicable.

Do not store arbitrary unvalidated JSON as the only representation of notification semantics.

Use typed notification types and schemas.

---

# 8. NOTIFICATION TYPES

Implement notification types appropriate to the current product scope.

At minimum support the architecture for:

* new subscriber;
* new comment;
* comment reply;
* comment reaction;
* video publication from subscribed channel;
* live-stream notification boundary;
* creator processing completion;
* creator processing failure;
* important account/security notification.

Do not implement notification types for future functionality unless their contract is explicitly required by this milestone.

Each type must define:

* triggering event;
* recipient;
* payload;
* delivery channels;
* deduplication behavior;
* aggregation behavior;
* priority.

---

# 9. NOTIFICATION PREFERENCE MODEL

Implement preference storage for:

* in-app;
* push;
* email.

Preferences must support the product's canonical categories.

At minimum distinguish:

* enabled;
* disabled;
* personalized/filtered where the product contract requires it.

Define defaults.

Never interpret absence of a preference inconsistently across notification types.

Do not use UI-only preference state.

Server-side notification decisions must honor stored preferences.

---

# 10. NOTIFICATION GENERATION

Implement asynchronous notification generation.

The flow should resemble:

```text
Domain Event
  ↓
Notification Eligibility
  ↓
Recipient Resolution
  ↓
Preference Evaluation
  ↓
Deduplication / Aggregation
  ↓
Notification Record
  ↓
Delivery Job
```

Do not generate notifications synchronously inside unrelated domain transactions unless the operation is explicitly a security-critical notification that requires synchronous confirmation.

Core domain operations must not fail simply because push/email infrastructure is unavailable.

---

# 11. NOTIFICATION DEDUPLICATION

Define and implement deduplication keys.

Examples may include:

* event ID;
* recipient + notification type + source event;
* recipient + aggregation target;
* notification-specific idempotency key.

Repeated domain events must not create duplicate notifications.

Deduplication must remain safe under:

* retries;
* worker restarts;
* at-least-once event delivery;
* concurrent consumers.

---

# 12. NOTIFICATION AGGREGATION

Where appropriate, aggregate high-volume notifications.

Examples:

* multiple comments;
* multiple reactions;
* multiple new subscribers.

Do not create one notification row for every trivial repeated action when the product contract explicitly supports aggregation.

Define:

* aggregation key;
* aggregation window;
* display count;
* representative actors where applicable;
* flush behavior.

Do not aggregate security-critical notifications incorrectly.

---

# 13. IN-APP NOTIFICATIONS

Implement:

* unread count;
* notification list;
* read state;
* mark-read;
* mark-all-read where supported;
* expiration/retention.

Use cursor pagination.

Do not load an entire notification history into memory.

Notification reads must be scoped to the authenticated recipient.

A user must never be able to retrieve another user's notifications by changing an ID.

---

# 14. PUSH NOTIFICATION MODEL

Implement the backend device-token abstraction required for push delivery.

Represent:

* device/token ID;
* user ID;
* platform;
* application version where useful;
* provider;
* status;
* lastSeenAt;
* createdAt;
* revokedAt where applicable.

Do not assume a device token remains valid forever.

Invalid provider tokens must be deactivated.

Do not log full push tokens unnecessarily.

---

# 15. EMAIL NOTIFICATION MODEL

Create an abstraction for email notification delivery where configured.

The abstraction must support:

* recipient;
* template/type;
* locale where applicable;
* template parameters;
* idempotency key;
* retry behavior.

Do not hardcode provider-specific APIs throughout the notification domain.

Do not embed production provider credentials.

---

# 16. NOTIFICATION DELIVERY JOBS

Implement notification delivery jobs for configured channels.

Each job must include:

* job ID;
* notification ID;
* recipient;
* delivery channel;
* template/type;
* payload reference;
* attempt;
* idempotency key;
* createdAt.

The worker must:

1. validate notification state;
2. validate recipient preferences;
3. invoke the provider abstraction;
4. record success/failure;
5. retry transient failures;
6. dead-letter permanent failures;
7. emit delivery events.

---

# 17. NOTIFICATION RETRY POLICY

Retry only failures that are plausibly transient.

Examples:

Retryable:

* provider timeout;
* network failure;
* temporary provider unavailable;
* rate limit from provider.

Non-retryable:

* invalid recipient;
* invalid token;
* malformed request;
* permanently rejected message.

Use:

* exponential backoff;
* jitter;
* maximum attempts;
* dead-letter behavior.

Do not retry forever.

---

# 18. NOTIFICATION EVENTS

Publish:

* notification.created;
* notification.read;
* notification.delivery.requested;
* notification.delivery.succeeded;
* notification.delivery.failed;
* notification.preference.updated.

Events must use the canonical event envelope.

Consumers must be idempotent.

Do not publish an event claiming successful delivery before the provider result is known.

---

# 19. EXTERNAL PROVIDER ABSTRACTIONS

Create explicit interfaces for:

* push provider;
* email provider.

Provider implementations must remain behind infrastructure adapters.

The domain layer must not depend directly on provider SDK types.

If no real external provider is configured, tests may use a test implementation, but production code must preserve a real provider integration boundary.

Do not claim real provider delivery when credentials are unavailable.

---

# 20. ANALYTICS EVENT INGESTION

Implement a durable analytics ingestion boundary.

Support incoming events such as:

* video impression;
* video play start;
* video play progress;
* video play completion;
* video pause/stop where defined;
* video like;
* video share;
* subscription;
* search performed;
* search result selected;
* recommendation impression;
* recommendation selected;
* playlist interaction;
* comment creation;
* channel view;
* creator publishing.

Validate all analytics events against typed schemas.

Do not accept arbitrary unbounded JSON and treat it as trusted analytical data.

---

# 21. ANALYTICS EVENT ENVELOPE

Use a canonical envelope containing, at minimum:

* event ID;
* event name;
* schema version;
* occurredAt;
* actor identifier where appropriate;
* anonymous/session identifier where supported;
* target/resource identifier;
* client platform;
* client application version;
* correlation ID where appropriate;
* privacy classification;
* payload.

Validate timestamps and IDs.

Reject malformed events.

Do not trust client-generated actor identity without server validation.

---

# 22. ANALYTICS DEDUPLICATION

Analytics ingestion may be at-least-once.

Implement deduplication using:

* event ID;
* producer identity;
* schema version;
* appropriate idempotency storage.

Do not double-count critical creator metrics because a client retried an event.

Define the retention window for deduplication state.

Do not retain unlimited deduplication keys.

---

# 23. ANALYTICS PRIVACY CONTROLS

Classify analytics events according to privacy sensitivity.

At minimum distinguish:

* low-sensitivity product telemetry;
* user-associated behavioral telemetry;
* sensitive viewing behavior;
* creator/business analytics.

Do not expose raw event streams directly to creator-facing APIs.

Creator APIs must read from controlled aggregate models.

Do not log raw playback telemetry in application logs.

---

# 24. PLAYBACK TELEMETRY INGESTION

Implement ingestion appropriate for high-volume playback events.

The system must not synchronously write every heartbeat directly to the primary PostgreSQL database.

Use:

* batching;
* queues;
* event streaming;
* asynchronous aggregation;

as appropriate.

Support events such as:

* play started;
* playback progress;
* buffering where defined;
* playback completed;
* playback abandoned where defined.

Define aggregation semantics for watch time.

Do not count duplicate or replayed events as additional watch time.

---

# 25. WATCH-TIME AGGREGATION

Implement reliable watch-time processing.

At minimum calculate:

* total watch time;
* approximate watch duration;
* completed plays;
* average view duration where derivable;
* completion rate where derivable.

Define how:

* duplicated events;
* out-of-order events;
* late events;
* interrupted playback;
* seeking;
* buffering;
* multiple concurrent sessions

affect calculations.

Do not assume every playback-progress event represents a unique additional second watched.

---

# 26. ENGAGEMENT ANALYTICS

Process signals from:

* likes/reactions;
* comments;
* subscriptions;
* playlist interaction;
* sharing;
* video views.

Produce controlled aggregates for:

* engagement count;
* engagement rate;
* subscriber growth;
* comment volume;
* reaction volume.

Keep raw event collection separate from derived aggregate calculation.

---

# 27. DISCOVERY ANALYTICS

Consume events from search/discovery systems.

Support analysis of:

* impressions;
* selections;
* searches;
* zero-result searches;
* recommendation impressions;
* recommendation selections;
* subscriptions-feed impressions;
* related-video selections.

These events must not become a hard dependency of the search/discovery request path.

If analytics ingestion fails, search and discovery must continue operating.

---

# 28. CREATOR VIDEO ANALYTICS

Implement creator-facing aggregate data for videos.

At minimum provide:

* views/plays;
* watch time;
* average view duration where derivable;
* completion rate where derivable;
* likes/reactions;
* comments;
* shares where represented;
* subscribers attributed where supported;
* traffic/discovery source summaries where available;
* time-based trend data.

Creator analytics must enforce ownership.

A creator may only retrieve analytics for channels/videos they are authorized to manage.

---

# 29. CREATOR CHANNEL ANALYTICS

Implement channel-level summaries.

Support:

* total views;
* total watch time;
* subscriber growth;
* engagement;
* top-performing videos;
* recent-performance trends;
* audience activity summaries where available.

Use precomputed or asynchronously updated aggregates rather than expensive raw-event queries on every dashboard request.

---

# 30. AUDIENCE ANALYTICS

Where supported by available privacy-safe data, provide aggregate audience information such as:

* broad geography;
* language;
* device/platform distribution;
* returning versus new viewers;
* viewing-time trends.

Do not expose individual viewer identities.

Do not expose small cohorts when the data would create an obvious privacy risk according to the project's configured aggregation thresholds.

Define minimum cohort or aggregation thresholds where appropriate.

---

# 31. TRAFFIC-SOURCE ANALYTICS

Support controlled attribution categories such as:

* search;
* home feed;
* subscriptions;
* related videos;
* external/referral;
* direct.

Use explicit event fields.

Do not attempt to infer traffic source from arbitrary strings supplied by clients.

---

# 32. ANALYTICS AGGREGATION WINDOWS

Implement aggregate dimensions appropriate to the creator analytics contract.

Support time windows such as:

* hourly where useful;
* daily;
* weekly;
* monthly.

Avoid recalculating unlimited historical aggregates for every request.

Use incremental or scheduled aggregation jobs.

Define timezone conventions for date buckets.

Prefer a canonical UTC bucket while allowing presentation-layer localization.

---

# 33. ANALYTICS DATA MODEL

Implement storage appropriate for analytics aggregates.

Separate:

* raw events;
* normalized events;
* aggregate facts;
* creator-facing read models.

Do not force high-volume raw telemetry into the same tables used for transactional account/video operations.

Where PostgreSQL is used for current-scope aggregates, design tables for efficient time-range queries.

Identify future migration paths to dedicated analytical storage if volume requires it.

---

# 34. RAW EVENT RETENTION

Define a retention policy appropriate to the current milestone.

Differentiate:

* raw high-volume playback events;
* normalized events;
* creator-facing aggregates;
* audit/security events.

Do not retain everything indefinitely.

Retention must be configurable.

Deletion/expiration jobs must be idempotent.

---

# 35. CREATOR ANALYTICS API

Implement APIs for creator-owned analytics.

At minimum support:

* video analytics;
* channel analytics;
* audience summary;
* time-series performance;
* top-performing content;
* traffic-source summary.

Support:

* time range;
* granularity;
* pagination where needed;
* filtering by channel/video;
* authorization.

Do not expose raw analytics event streams.

---

# 36. ANALYTICS AUTHORIZATION

Creator analytics access must require:

* authenticated principal;
* channel ownership or authorized creator role;
* appropriate scope.

Administrative access may be privileged but must remain auditable.

A creator must not obtain another creator's analytics by altering a video/channel ID.

---

# 37. ANALYTICS CACHE

Use Redis caching where justified for:

* creator dashboard summaries;
* channel summary;
* common time-series queries;
* top-content lists.

Every cache must define:

* key;
* owner;
* TTL;
* invalidation;
* source of truth;
* failure behavior.

Do not cache sensitive analytics across users.

---

# 38. ANALYTICS JOBS

Implement background jobs for:

* event normalization;
* watch-time aggregation;
* video metrics aggregation;
* channel metrics aggregation;
* audience aggregation;
* traffic-source aggregation;
* retention cleanup;
* analytics reconciliation.

Each job must define:

* input;
* output;
* idempotency;
* retry;
* timeout;
* concurrency;
* dead-letter behavior.

---

# 39. ANALYTICS RECONCILIATION

Implement mechanisms to detect discrepancies between:

* raw events;
* aggregate records;
* creator-facing read models.

Where possible provide reconciliation/rebuild operations.

A rebuild must be safe to rerun.

Do not silently overwrite suspicious aggregates without an audit trail where auditability is required.

---

# 40. ANALYTICS EVENT VERSIONING

Implement analytics schema versions.

A new field may generally be additive.

Breaking event changes require:

* a new schema version;
* compatibility handling;
* producer/consumer migration.

Do not silently reinterpret historical events using a new schema definition.

---

# 41. NOTIFICATION AND ANALYTICS DECOUPLING

Ensure that:

* notification failures do not block analytics;
* analytics failures do not block notifications;
* analytics failures do not break playback;
* notification-provider failures do not break core domain writes.

Use asynchronous infrastructure.

Do not place analytical processing in the synchronous transaction path of core product operations.

---

# 42. SECURITY AND PRIVACY

Protect:

* notification recipient data;
* push tokens;
* email addresses;
* watch behavior;
* playback telemetry;
* creator business analytics.

Do not log:

* full device tokens;
* authentication tokens;
* raw sensitive analytics payloads;
* private viewing information.

Use data minimization.

Apply access checks before returning creator analytics.

---

# 43. RATE LIMITING

Rate-limit:

* notification list;
* notification mutation;
* analytics ingestion;
* creator analytics reads;
* device-token registration;
* preference updates.

High-volume analytics ingestion should also have abuse controls protecting the platform from event floods.

Do not allow a client to generate unlimited fabricated analytics events.

---

# 44. EVENT ABUSE PREVENTION

Implement validation against obvious analytics abuse.

At minimum:

* authenticated event sources where required;
* server-assigned identity;
* request-origin validation;
* rate limits;
* event size limits;
* event-type allowlist;
* schema validation;
* timestamp bounds;
* deduplication.

Do not treat every client telemetry event as unquestionable truth.

Document which metrics are client-derived versus server-authoritative.

---

# 45. OBSERVABILITY

Implement metrics for:

## Notifications

* notification creation;
* unread counts;
* delivery latency;
* provider failure;
* invalid token rate;
* retry count;
* dead-letter count;
* aggregation rate.

## Analytics

* event ingestion rate;
* rejected events;
* deduplication rate;
* queue lag;
* processing latency;
* aggregation lag;
* reconciliation failures;
* creator-query latency;
* retention-job failures.

Use:

* event ID;
* job ID;
* notification ID;
* user ID only when appropriate and privacy-safe;
* video ID;
* channel ID;
* correlation ID.

Do not emit excessive high-cardinality metrics.

---

# 46. PERFORMANCE REQUIREMENTS

Optimize for:

* high-volume event ingestion;
* asynchronous processing;
* notification fan-out;
* creator analytics queries;
* aggregate recalculation;
* time-series reads.

Avoid:

* raw-event scans for every creator dashboard request;
* synchronous fan-out to thousands of recipients;
* unbounded notification queries;
* synchronous external provider calls from domain transactions;
* transaction locks spanning asynchronous provider operations.

---

# 47. API SURFACE

Implement API families for:

## Notifications

* list notifications;
* unread count;
* mark read;
* mark all read where supported;
* notification preferences;
* device-token registration/revocation.

## Creator Analytics

* video analytics;
* channel analytics;
* audience summary;
* performance timeseries;
* traffic-source summary.

## Analytics Ingestion

Expose only the ingestion endpoints required by the client architecture.

Do not expose administrative raw-event APIs publicly.

---

# 48. AUTHORIZATION MATRIX

Create an implementation-level matrix.

At minimum:

| Operation                           | Anonymous | Authenticated User  | Channel Owner | Moderator/Admin |
| ----------------------------------- | --------- | ------------------- | ------------- | --------------- |
| Read own notifications              | No        | Allowed             | Allowed       | Privileged      |
| Mark own notification read          | No        | Allowed             | Allowed       | Privileged      |
| Manage own notification preferences | No        | Allowed             | Allowed       | Privileged      |
| Register own device token           | No        | Allowed             | Allowed       | Privileged      |
| Read video analytics                | No        | No                  | Owner only    | Privileged      |
| Read channel analytics              | No        | No                  | Owner only    | Privileged      |
| Read audience analytics             | No        | No                  | Owner only    | Privileged      |
| Submit product telemetry            | Limited   | Allowed by contract | Allowed       | Privileged      |

Refine permissions to exactly match the implemented routes.

---

# 49. TESTING REQUIREMENTS

Create real tests.

## Notification Unit Tests

Test:

* event-to-notification mapping;
* preference evaluation;
* deduplication;
* aggregation;
* recipient resolution;
* delivery classification;
* retry classification.

## Notification Integration Tests

Test:

* notification persistence;
* device-token state;
* queue jobs;
* provider adapters;
* retries;
* dead-letter behavior;
* notification reads;
* authorization.

## Analytics Unit Tests

Test:

* schema validation;
* event normalization;
* deduplication;
* watch-time calculation;
* engagement aggregation;
* attribution;
* privacy thresholds.

## Analytics Integration Tests

Test:

* event ingestion;
* queue/event processing;
* aggregate persistence;
* creator analytics queries;
* retention;
* reconciliation.

## API Tests

Test:

* notification APIs;
* preference APIs;
* device-token APIs;
* creator analytics APIs;
* analytics ingestion;
* authorization;
* pagination;
* rate limits.

## Failure Tests

Test:

* provider unavailable;
* queue unavailable;
* duplicate event;
* delayed event;
* out-of-order event;
* worker retry;
* partial aggregation;
* cache failure.

## Security Tests

Test:

* cross-user notification access;
* cross-creator analytics access;
* device-token ownership;
* telemetry abuse;
* private analytics leakage.

---

# 50. PERFORMANCE VALIDATION

Measure, within the available environment:

* analytics event ingestion throughput;
* notification creation throughput;
* notification query latency;
* creator analytics query latency;
* aggregation job latency;
* queue lag;
* deduplication performance.

Do not claim global-scale capacity from local tests.

Report the environment and limitations.

---

# 51. API DOCUMENTATION

Update OpenAPI documentation for:

* notifications;
* notification preferences;
* device tokens;
* creator analytics;
* analytics ingestion.

Document:

* authentication;
* authorization;
* pagination;
* date ranges;
* response schemas;
* error contracts;
* rate limits.

Do not expose internal analytical storage structures.

---

# 52. OPERATIONAL DOCUMENTATION

Document:

* notification queues;
* notification providers;
* retry policies;
* dead-letter handling;
* analytics event schemas;
* aggregation jobs;
* retention;
* reconciliation;
* creator-analytics troubleshooting;
* provider configuration;
* observability dashboards;
* privacy controls.

Do not include real credentials.

Do not claim provider accounts or external infrastructure have been configured unless verified.

---

# 53. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement in this milestone:

* moderation tooling;
* administration dashboards;
* automated moderation;
* advanced recommendation models;
* model training;
* feature stores;
* advertising;
* payments;
* live-stream media infrastructure;
* web UI;
* mobile UI.

Do not implement a full analytical warehouse unless the repository already requires it for the current bounded architecture.

Do not replace current transactional systems with an analytical database prematurely.

---

# 54. VALIDATION REQUIREMENTS

Before completion, verify:

## Notifications

* recipients are correct;
* preferences are honored;
* duplicate events do not duplicate notifications;
* unread state works;
* unauthorized access fails;
* provider failures are isolated;
* retries are bounded.

## Analytics

* event schemas validate;
* malformed events are rejected;
* duplicate events are deduplicated;
* playback events aggregate correctly;
* creator aggregates are correct;
* private data does not leak;
* retention works;
* reconciliation detects discrepancies.

## Privacy

Verify:

* watch behavior is protected;
* creator analytics are isolated;
* device tokens are protected;
* raw telemetry is not publicly exposed.

## Reliability

Verify:

* queue failures;
* provider failures;
* event delays;
* event duplication;
* out-of-order events;
* worker restarts.

## Observability

Verify:

* notification metrics;
* delivery metrics;
* analytics ingestion metrics;
* aggregation lag;
* creator-query latency;
* error tracking.

---

# 55. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Notification domain is implemented.
3. Notification preferences are implemented.
4. In-app notification persistence is implemented.
5. Notification deduplication is implemented.
6. Notification aggregation is implemented where required.
7. Device-token management is implemented.
8. Push provider abstraction is implemented.
9. Email provider abstraction is implemented.
10. Notification jobs are implemented.
11. Notification retries are implemented.
12. Dead-letter handling is implemented where required.
13. Analytics ingestion is implemented.
14. Analytics schemas are validated.
15. Analytics deduplication is implemented.
16. Playback telemetry ingestion is implemented.
17. Watch-time aggregation is implemented.
18. Engagement aggregation is implemented.
19. Discovery analytics ingestion is implemented.
20. Video analytics aggregates are implemented.
21. Channel analytics aggregates are implemented.
22. Audience analytics are implemented within privacy constraints.
23. Traffic-source analytics are implemented where supported.
24. Creator analytics APIs are implemented.
25. Analytics retention is implemented.
26. Analytics reconciliation is implemented.
27. Notification and analytics systems are decoupled from core transactional operations.
28. Rate limiting is implemented.
29. Security and privacy controls are implemented.
30. Observability is implemented.
31. Notification tests are implemented.
32. Analytics tests are implemented.
33. API tests are implemented.
34. Failure/recovery tests are implemented.
35. Security tests are implemented.
36. Performance validation has been performed.
37. API documentation is updated.
38. Operational documentation is updated.
39. No fake provider integration is presented as a successful production integration.
40. No intentional TODO/FIXME gap substitutes for current-scope functionality.
41. No hardcoded secrets exist.
42. Known limitations are reported honestly.

---

# 56. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Notifications

Summarize:

* notification types;
* preference system;
* delivery workers;
* provider abstractions;
* retries;
* deduplication;
* aggregation.

## Analytics

Summarize:

* event ingestion;
* schemas;
* deduplication;
* playback telemetry;
* aggregation;
* creator analytics;
* retention;
* reconciliation.

## Database Changes

List:

* models;
* migrations;
* indexes;
* constraints.

## Events and Jobs

List:

* notification events;
* analytics events;
* workers;
* queues.

## Tests

List:

* unit tests;
* integration tests;
* API tests;
* security tests;
* failure tests;
* performance validation.

## Documentation

List documentation created or updated.

## Known Limitations

List intentionally deferred functionality.

## Unresolved Issues

List only genuine unresolved issues.

Do not claim that external notification providers, analytical infrastructure, cloud resources, or production integrations were provisioned unless that actually occurred.

# 57. FINAL EXECUTION RULE

Implement only the notification, analytics, creator-analytics, event-processing, and supporting backend functionality defined by this milestone.

Do not implement unrelated moderation, administration, live-streaming, monetization, frontend, mobile, or advanced machine-learning functionality.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake notifications, fake analytics, placeholder aggregates, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, secure, privacy-aware, observable, scalable backend functionality.
