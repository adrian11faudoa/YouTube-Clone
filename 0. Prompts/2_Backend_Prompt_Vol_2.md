# YouTube-Style Video Platform — Backend Prompt — Volume 2

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the second bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the core **viewer engagement and relationship layer** of the platform:

* comments;
* threaded replies;
* comment reactions;
* video reactions;
* subscriptions;
* subscription preferences;
* playlists;
* watch history;
* playback progress persistence;
* sharing-related backend state where applicable;
* engagement counters and derived summaries;
* the domain events required by these capabilities;
* abuse protections for these high-volume interaction paths.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of search, recommendations, notifications, full analytics, moderation tooling, live-streaming media, transcoding, advertising, payments, or the web/mobile clients.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier AI prompt was executed merely because a prompt exists in the user's conversation.

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
* upload and media processing;
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

This milestone implements the interaction and relationship domains that depend on the foundational identity, channel, and video model.

## 2.2 Scale Direction

The completed platform is intended to evolve toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* very large comment volumes;
* very large reaction volumes;
* very large subscription graphs;
* high-volume watch-history and playback-progress writes.

The current milestone does not have to operate at maximum global scale immediately.

However, it must not introduce a database or API design that makes the stated scale fundamentally impractical.

## 2.3 Technology Direction

Use the repository's established compatible backend stack:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* REST;
* OpenAPI;
* background jobs where justified;
* event publication;
* structured logging;
* OpenTelemetry-compatible observability.

Do not replace the established stack without a concrete repository-driven reason.

---

# 3. CURRENT MILESTONE SCOPE

This milestone implements:

1. Comment domain.
2. Comment creation.
3. Comment editing.
4. Comment deletion.
5. Threaded comment replies.
6. Comment visibility and moderation-state boundaries.
7. Comment reactions.
8. Video reactions.
9. Idempotent reaction operations.
10. Subscription relationships.
11. Subscription creation/removal.
12. Subscription preferences.
13. Subscription feed query foundation.
14. Playlist domain.
15. Playlist creation and management.
16. Playlist item management.
17. Playlist ordering.
18. Watch history.
19. Playback progress persistence.
20. Watch-later or equivalent personal collection only if supported by the existing product contract.
21. Engagement counters and derived summaries needed by this milestone.
22. Domain events for engagement and relationship changes.
23. Cache strategies for high-read interaction state where justified.
24. Abuse/rate-limit protections for interaction endpoints.
25. Security and authorization for every mutation.
26. Unit, integration, API, concurrency, and security testing for implemented functionality.
27. API documentation and operational documentation.

This milestone does not implement:

* notification delivery;
* recommendation ranking;
* search indexing;
* analytics warehouses or large-scale analytical processing;
* moderation operator dashboards;
* automated content safety;
* live-stream chat;
* live-stream media processing;
* transcoding;
* CDN infrastructure;
* payment processing;
* advertising;
* mobile UI;
* web UI.

The implementation may publish the domain events needed by those future systems.

---

# 4. REPOSITORY INSPECTION

Before implementing:

1. Inspect the repository structure.
2. Inspect the existing backend module boundaries.
3. Inspect user, account, session, and authorization code.
4. Inspect channel models and services.
5. Inspect video models and lifecycle handling.
6. Inspect existing database migrations.
7. Inspect API error and pagination utilities.
8. Inspect existing event infrastructure.
9. Inspect Redis usage.
10. Inspect rate-limiting infrastructure.
11. Inspect OpenAPI documentation.
12. Inspect existing tests.
13. Inspect logging and observability utilities.
14. Inspect existing domain event definitions.

Reuse compatible infrastructure.

Do not duplicate existing shared services.

If a required foundational component is missing, implement only the minimal supporting functionality necessary for this milestone.

---

# 5. DOMAIN BOUNDARIES

Implement clear backend modules for:

* engagement;
* comments;
* reactions;
* subscriptions;
* playlists;
* watch history;
* playback progress.

Keep these domains distinct even when they reside in the same NestJS deployable.

At minimum, maintain conceptual ownership:

## Comments

Own:

* comment records;
* replies;
* comment lifecycle;
* comment visibility state;
* comment reaction relationships where owned by the comment domain.

## Reactions

Own:

* video reactions;
* reaction state;
* reaction idempotency;
* reaction aggregates where appropriate.

## Subscriptions

Own:

* viewer/channel relationship;
* subscription lifecycle;
* notification preference associated with subscription where part of the subscription contract.

## Playlists

Own:

* playlists;
* playlist items;
* playlist ordering;
* playlist visibility.

## Watch History

Own:

* watch-history records;
* history visibility;
* deletion behavior.

## Playback Progress

Own:

* resumable playback state;
* last position;
* completion state where appropriate.

Do not give these domains arbitrary write access to users, channels, or videos.

Read canonical ownership information through existing application boundaries.

---

# 6. PROJECT-WIDE CONTRACTS

Use the project's canonical contracts for:

* entity IDs;
* timestamps;
* API errors;
* pagination;
* authorization;
* visibility;
* idempotency;
* domain events;
* configuration;
* observability.

Important canonical identifiers include:

* user ID;
* channel ID;
* video ID;
* comment ID;
* playlist ID;
* subscription ID;
* reaction ID;
* notification-related identifiers where events are emitted.

Use UTC timestamps.

Use stable enum values.

Do not introduce alternate representations.

---

# 7. DATABASE MODEL

Implement transactional persistence for the domains in this milestone.

At minimum create or update models for:

## Comment

Fields should include:

* comment ID;
* video ID;
* author user ID;
* parent comment ID;
* body;
* visibility/moderation state;
* createdAt;
* updatedAt;
* deletedAt where applicable.

## Comment Reaction

Include:

* reaction ID or deterministic relationship key;
* comment ID;
* user ID;
* reaction type;
* createdAt;
* updatedAt where applicable.

Enforce a uniqueness rule preventing unintended duplicate reactions by the same user on the same comment and reaction type.

## Video Reaction

Include:

* reaction relationship;
* video ID;
* user ID;
* reaction type;
* createdAt;
* updatedAt where applicable.

Define whether one user may hold one mutually exclusive reaction state or multiple reaction types.

Follow the authoritative product contract and implement the relationship consistently.

## Subscription

Include:

* subscription ID;
* subscriber user ID;
* channel ID;
* status;
* notification preference;
* createdAt;
* updatedAt;
* deletedAt where applicable.

Enforce unique active subscription relationships.

## Playlist

Include:

* playlist ID;
* owner user ID;
* title;
* description;
* visibility;
* createdAt;
* updatedAt;
* deletedAt where applicable.

## Playlist Item

Include:

* playlist item ID;
* playlist ID;
* video ID;
* ordering representation;
* addedAt;
* updatedAt where required.

## Watch History

Include:

* history ID;
* user ID;
* video ID;
* watchedAt;
* lastPositionSeconds where applicable;
* completedAt or completion state where applicable.

## Playback Progress

Include:

* user ID;
* video ID;
* position;
* duration snapshot where useful;
* completion state;
* lastUpdatedAt.

The exact table separation between watch history and playback progress must be explicit.

Do not make watch history and playback state accidentally overwrite one another.

---

# 8. DATABASE CONSTRAINTS

Implement appropriate constraints.

At minimum enforce:

* comment belongs to one video;
* comment author exists;
* parent comment belongs to the same video;
* subscription references a valid channel;
* subscription subscriber cannot subscribe to an invalid target;
* playlist belongs to one owner;
* playlist item belongs to an existing playlist;
* reaction references a valid target;
* duplicate active subscriptions are prevented;
* duplicate reaction state is prevented;
* invalid self-referential relationships are rejected where prohibited.

Do not rely only on application-level checks for uniqueness that must also be protected during concurrent requests.

Use database constraints as the final integrity boundary.

---

# 9. INDEXING STRATEGY

Create indexes based on real query patterns.

At minimum consider:

## Comments

* video + createdAt;
* video + visibility + createdAt;
* parent comment + createdAt;
* author + createdAt.

## Reactions

* video + reaction type;
* comment + reaction type;
* user + video;
* user + comment.

## Subscriptions

* subscriber + createdAt;
* channel + createdAt;
* subscriber + channel unique constraint.

## Playlists

* owner + createdAt;
* playlist + ordering;
* playlist + video.

## Watch History

* user + watchedAt;
* user + video;
* user + lastUpdatedAt.

## Playback Progress

* user + video unique access path.

Do not create redundant indexes that duplicate unique constraints without justification.

---

# 10. COMMENT CREATION

Implement authenticated comment creation.

A create-comment request must:

1. authenticate the actor;
2. resolve the target video;
3. verify that the video is accessible for commenting;
4. verify account/channel restrictions applicable to commenting;
5. validate the content;
6. validate parent-comment relationship if a reply;
7. persist the comment;
8. publish `comment.created`;
9. return the canonical comment representation.

Validate:

* body length;
* empty/whitespace-only input;
* Unicode handling;
* maximum request size;
* invalid control characters where appropriate.

Do not trust client-provided author identity.

The backend must derive the author from the authenticated principal.

---

# 11. COMMENT THREADING

Support threaded replies.

A reply must reference a parent comment.

Enforce:

* parent exists;
* parent belongs to the same video;
* parent is eligible to receive replies;
* nesting depth follows the product contract.

If the product supports only one reply level, enforce that rule.

If deeper nesting is supported, explicitly define and enforce the maximum depth.

Do not allow arbitrary cross-video parent references.

Do not allow a reply to silently attach to an unrelated video.

---

# 12. COMMENT EDITING

Implement author-authorized comment editing.

A comment edit must:

1. authenticate the user;
2. load the comment;
3. verify ownership or privileged authorization;
4. verify the comment is editable;
5. validate the new body;
6. update the record;
7. publish the appropriate event;
8. return the canonical representation.

Define whether editing after a time period is restricted.

Do not invent a silent editing window if the current product contract does not define one.

Where edit history or audit metadata is required by the product contract, preserve it without exposing private internal information.

---

# 13. COMMENT DELETION

Implement author-authorized deletion and privileged deletion boundaries.

Support deletion semantics appropriate to the product.

Do not physically destroy relational integrity merely because a comment becomes unavailable.

Use soft deletion or tombstone behavior where necessary to preserve thread structure.

Deleted comments must not reveal their original body through ordinary public APIs.

A deleted parent comment must have deterministic behavior for child replies.

Possible behavior may include:

* retaining the thread position with a deleted placeholder;
* hiding child replies;
* preserving child replies while replacing the parent body.

Choose and implement the behavior defined by the authoritative product contract.

---

# 14. COMMENT RETRIEVAL

Implement comment retrieval with cursor pagination.

Support:

* top-level comments;
* replies;
* sorting according to the defined contract;
* visibility filtering;
* reaction summary where appropriate.

Do not load an entire comment tree into memory.

Avoid recursive database traversal for unbounded thread structures.

Use bounded queries.

Define stable ordering.

The API must behave predictably when comments are created or deleted between page requests.

---

# 15. COMMENT AUTHORIZATION

Enforce authorization for:

* creating comments;
* editing own comments;
* deleting own comments;
* privileged deletion/hiding;
* replying;
* viewing restricted comment state where applicable.

Do not treat the ability to view a video as automatically granting unlimited moderation privileges.

Creator moderation rights must be explicit.

Administrative or moderator privileges must be explicit.

---

# 16. COMMENT REACTIONS

Implement comment reactions.

Support the reaction model established by the product contract.

At minimum support:

* add reaction;
* remove reaction;
* change reaction if the contract allows multiple mutually exclusive states.

Operations must be idempotent.

Repeated "add" operations must not create duplicates.

Repeated "remove" operations must not produce inconsistent state.

Reaction writes must be concurrency-safe.

---

# 17. VIDEO REACTIONS

Implement authenticated video engagement reactions.

Support:

* adding the allowed reaction;
* removing it;
* changing the reaction where applicable;
* reading the current viewer's reaction;
* retrieving aggregate reaction counts where required.

Ensure the relationship is unique per user/video/reaction semantics.

Do not trust client-provided aggregate counts.

Aggregate counts must be derived from authoritative state or a controlled derived counter.

---

# 18. REACTION COUNTERS

Implement scalable reaction summaries.

The system must distinguish:

* individual reaction state;
* aggregate counts.

Do not make a hot relational row the only path for every reaction increment when the expected scale would create contention.

For the current milestone, a transactional counter strategy is acceptable where justified, but it must remain safe under concurrent updates.

If Redis is used for caching:

* PostgreSQL or another authoritative store remains the source of truth;
* cache invalidation is explicit;
* stale counters are handled safely.

Do not claim counters are strongly consistent if the implementation is eventually consistent.

---

# 19. SUBSCRIPTION CREATION

Implement subscribing to a channel.

The operation must:

1. authenticate the user;
2. resolve the channel;
3. validate that the channel is subscribable;
4. reject invalid self-subscription cases if the product contract prohibits them;
5. create the relationship idempotently;
6. publish `subscription.created`;
7. return the canonical subscription state.

Repeated subscribe requests must not create duplicate active relationships.

---

# 20. UNSUBSCRIPTION

Implement unsubscribe behavior.

The operation must:

* authenticate;
* verify the existing relationship;
* update/remove according to the data model;
* publish `subscription.deleted`;
* invalidate appropriate caches;
* remain idempotent.

Repeated unsubscribe requests must not produce inconsistent state.

Historical analytics must remain possible through events even if the transactional relationship is removed.

---

# 21. SUBSCRIPTION PREFERENCES

Implement per-channel notification preference state associated with subscriptions where this milestone's contract includes it.

Support the defined preference states, for example:

* all notifications;
* personalized/selected notifications;
* none.

Do not implement the notification delivery system.

The subscription domain only owns the preference state required by future notification processing.

Validate that preference changes occur only for an active or otherwise valid subscription according to the product contract.

---

# 22. SUBSCRIPTION QUERIES

Implement APIs for:

* current user's subscriptions;
* channel subscriber summaries where authorized;
* subscription state for a specific channel;
* subscription lists with cursor pagination.

Do not expose private subscriber data beyond the product's privacy contract.

Use stable ordering.

Avoid N+1 queries when returning subscription collections.

---

# 23. SUBSCRIPTION FEED FOUNDATION

Implement the backend data-access foundation required for a future subscription feed.

The current milestone does not need to implement a sophisticated ranking system.

Provide a query or service capable of obtaining recently published eligible videos from channels subscribed to by a user.

The query must honor:

* current subscription state;
* video visibility;
* publication state;
* deleted/restricted content;
* cursor pagination.

The implementation must be deterministic and suitable for later optimization or replacement by a dedicated feed service.

Do not build the recommendation system here.

---

# 24. PLAYLIST CREATION

Implement playlist creation.

Support:

* title;
* description;
* visibility;
* owner.

Validate:

* ownership;
* text lengths;
* visibility;
* required fields.

Generate a canonical playlist ID.

Return a complete canonical playlist representation.

---

# 25. PLAYLIST MANAGEMENT

Implement owner-authorized:

* get playlist;
* update playlist;
* change visibility;
* delete playlist.

Do not allow arbitrary users to mutate another user's playlist.

Public playlist reads must return only fields intended for public consumption.

Private playlists must require appropriate authorization.

Deleted playlists must have predictable API behavior.

---

# 26. PLAYLIST ITEMS

Implement:

* add video;
* remove video;
* list playlist items;
* reorder items.

Validate:

* video exists;
* video is eligible for playlist inclusion;
* owner/permission;
* no invalid duplicate semantics;
* ordering correctness.

Determine whether duplicate copies of the same video are permitted by the product contract.

Do not silently choose a different rule across endpoints.

If duplicates are prohibited, enforce the rule transactionally.

---

# 27. PLAYLIST ORDERING

Implement a scalable ordering strategy.

Do not rely on naive repeated full-list renumbering for every move if the expected playlist size makes that approach inefficient.

Use a suitable ordering representation such as:

* stable integer positions with carefully scoped updates;
* fractional/rank values;
* another explicit ordering strategy.

The chosen implementation must remain deterministic and sortable.

Concurrent reorder operations must not leave duplicate or corrupt ordering state.

---

# 28. PLAYLIST VISIBILITY

Implement visibility semantics consistent with the platform's content visibility model.

At minimum distinguish:

* public;
* unlisted/private as supported by the product contract.

Visibility must affect:

* direct retrieval;
* playlist discovery;
* item access;
* API responses.

A private playlist must not become publicly accessible merely because one item is public.

---

# 29. WATCH HISTORY

Implement authenticated watch-history persistence.

Support:

* record viewing activity;
* update most recent watch time;
* retrieve history;
* remove individual history entries where supported;
* clear history where supported.

The system must distinguish viewing history from playback progress.

Do not write an unbounded immutable row for every playback heartbeat.

Use a history model appropriate to product semantics.

---

# 30. PLAYBACK PROGRESS

Implement persisted playback progress.

Support:

* save position;
* retrieve position;
* mark completion where appropriate;
* update position idempotently;
* remove/reset position.

Validate:

* user authorization;
* video accessibility;
* position range;
* video duration where known.

The backend must reject impossible negative positions.

If duration is known, reject or normalize positions beyond valid boundaries according to the product contract.

---

# 31. PLAYBACK WRITE CONTROL

Playback-progress writes can become extremely high volume.

Do not create an API that requires a database write for every tiny playback interval.

The backend should support client-controlled reporting intervals or appropriate throttling.

Define and enforce:

* minimum update interval where necessary;
* idempotency or monotonic update behavior;
* stale update protection;
* last-write semantics.

Older client updates must not overwrite a newer playback position accidentally.

Use an update timestamp/version or monotonic position rule where necessary.

---

# 32. WATCH HISTORY PRIVACY

Watch history is privacy-sensitive.

Do not expose a user's watch history to other users.

Do not include watch history in public profile responses.

Implement deletion/clear behavior according to the product contract.

Ensure analytics events and recommendation signals can remain separately governed without leaking watch-history data through ordinary APIs.

---

# 33. ENGAGEMENT EVENT MODEL

Publish domain events for this milestone.

At minimum include:

* comment.created;
* comment.updated;
* comment.deleted;
* reaction.created;
* reaction.removed;
* subscription.created;
* subscription.deleted;
* subscription.preference.updated;
* playlist.created;
* playlist.updated;
* playlist.item.added;
* playlist.item.removed;
* playlist.deleted;
* watch_history.updated where an event is required;
* playback_progress.updated where an event is required.

Events must use the project's canonical event envelope.

Every event must contain:

* event ID;
* type;
* version;
* occurredAt;
* producer;
* correlation context where applicable;
* payload.

Do not create duplicate event types representing the same business fact.

---

# 34. TRANSACTIONAL EVENT DELIVERY

Domain events must not be published before the relevant transactional state is durably committed.

Use an outbox or equivalent mechanism where required.

At minimum ensure:

* comment write and `comment.created` event;
* subscription write and `subscription.created`;
* reaction write and reaction event;
* playlist mutation and playlist event

cannot diverge because the database commit succeeds while event publication silently fails.

Consumers are out of scope.

Event publication must remain idempotent.

---

# 35. CACHE ARCHITECTURE

Use Redis only where caching materially improves this milestone.

Potential cache candidates include:

* public channel subscription summaries;
* video reaction counts;
* comment reaction summaries;
* subscription-state checks;
* playlist metadata where justified.

For every cache:

* define key format;
* define TTL;
* define owner;
* define source of truth;
* define invalidation;
* define stale behavior.

Do not cache private data under keys that can be guessed across users.

Do not let Redis become the only source of truth.

---

# 36. RATE LIMITING AND ABUSE PROTECTION

Protect high-abuse interactions.

At minimum rate-limit:

* comment creation;
* comment replies;
* reaction mutations;
* subscriptions;
* playlist mutations;
* watch-history mutations;
* playback-progress updates where necessary.

Use a combination of:

* authenticated principal;
* IP/device signal where appropriate;
* resource key;
* endpoint.

Do not make rate limits so aggressive that normal playback or legitimate engagement becomes unusable.

Return standard retry information.

---

# 37. ANTI-SPAM BOUNDARIES

Implement backend safeguards appropriate to the current scope.

At minimum detect/prevent obvious:

* duplicate comment flooding;
* duplicate reaction storms;
* repeated subscribe/unsubscribe abuse;
* excessive playlist mutation bursts;
* malformed or oversized comment payloads.

Do not implement a machine-learning spam classifier in this milestone.

Instead create extension points and events that future moderation/anti-abuse systems can consume.

---

# 38. CONCURRENCY REQUIREMENTS

Explicitly test concurrent operations.

At minimum cover:

* simultaneous comment creation;
* simultaneous reaction changes;
* simultaneous subscribe requests;
* simultaneous unsubscribe requests;
* subscribe/unsubscribe races;
* concurrent playlist reorder;
* concurrent playlist item mutations;
* stale playback-progress writes;
* concurrent history updates.

Use:

* unique constraints;
* transactions;
* row-level locking;
* optimistic concurrency;
* atomic updates;

where appropriate.

Do not rely on JavaScript in-process memory to solve multi-instance concurrency.

---

# 39. API SURFACE

Implement API families for this milestone.

## Comments

* create comment;
* list comments;
* get comment where needed;
* update own comment;
* delete own comment;
* reply;
* react to comment.

## Video Reactions

* get current reaction;
* add/change reaction;
* remove reaction;
* get aggregate summary where supported.

## Subscriptions

* subscribe;
* unsubscribe;
* get subscription state;
* list subscriptions;
* update notification preference.

## Playlists

* create;
* get;
* update;
* delete;
* list items;
* add item;
* remove item;
* reorder.

## Watch History

* list;
* clear;
* delete entry where supported.

## Playback Progress

* get progress;
* update progress;
* clear progress where supported.

Use the canonical API naming and error contract.

Do not add notification, search, or recommendation endpoints in this milestone.

---

# 40. AUTHORIZATION MATRIX

Create/update an implementation-level authorization matrix.

At minimum:

| Operation                | Anonymous | Authenticated User  | Resource Owner | Channel Owner | Moderator/Admin |
| ------------------------ | --------- | ------------------- | -------------- | ------------- | --------------- |
| Read public comments     | Allowed   | Allowed             | Allowed        | Allowed       | Allowed         |
| Create comment           | No        | Allowed if eligible | Allowed        | Allowed       | Privileged      |
| Edit own comment         | No        | Owner only          | Allowed        | N/A           | Privileged      |
| Delete own comment       | No        | Owner only          | Allowed        | N/A           | Privileged      |
| React to video           | No        | Allowed             | Allowed        | Allowed       | Privileged      |
| Subscribe                | No        | Allowed             | Allowed        | N/A           | Privileged      |
| Create playlist          | No        | Allowed             | Allowed        | N/A           | Privileged      |
| Modify playlist          | No        | Owner only          | Allowed        | N/A           | Privileged      |
| Read private playlist    | No        | Owner only          | Allowed        | N/A           | Privileged      |
| Read watch history       | No        | Own data only       | Allowed        | N/A           | Restricted      |
| Update playback progress | No        | Own data only       | Allowed        | N/A           | Restricted      |

Refine the matrix to exactly match the implemented API.

---

# 41. API VALIDATION

Validate:

* comment body;
* parent comment ID;
* reaction types;
* subscription target;
* playlist metadata;
* playlist visibility;
* playlist item IDs;
* ordering parameters;
* cursor;
* page size;
* watch-history filters;
* playback position;
* request sizes.

Return canonical validation errors.

Do not rely solely on database exceptions.

---

# 42. API PAGINATION

Use cursor pagination for:

* comments;
* subscriptions;
* playlists where collections require it;
* playlist items;
* watch history.

Define stable ordering.

Avoid offset-based pagination for high-volume comments and subscriptions unless explicitly justified.

The cursor must not reveal sensitive internal database structure unnecessarily.

---

# 43. PERFORMANCE REQUIREMENTS

Optimize for large-scale read/write behavior.

Avoid:

* N+1 comment queries;
* loading all playlist items into memory;
* loading all subscriptions at once;
* updating reaction counters by scanning every relationship;
* writing playback progress on every playback tick;
* recursive unbounded comment traversal;
* unbounded watch-history reads.

Use:

* appropriate indexes;
* cursor pagination;
* batched reads;
* aggregate queries;
* cache where justified;
* bounded transactions.

---

# 44. PRIVACY REQUIREMENTS

Protect:

* watch history;
* playback progress;
* private playlists;
* unlisted/private content relationships;
* account-specific subscriptions where privacy rules apply.

Do not expose another user's:

* viewing history;
* playback position;
* private playlists;
* private subscription information

through ordinary public APIs.

Logging must not include private comment content unnecessarily or leak sensitive user activity.

---

# 45. OBSERVABILITY

Implement observability for:

* comment creation latency;
* comment errors;
* reaction mutation rate;
* reaction conflicts;
* subscription mutations;
* playlist mutations;
* watch-history writes;
* playback-progress writes;
* rate-limit hits;
* cache hits/misses where applicable;
* event publication;
* database contention;
* concurrency failures.

Use standard:

* request ID;
* correlation ID;
* event ID;
* trace ID.

Do not log full sensitive user activity payloads unnecessarily.

---

# 46. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* comment authorization;
* thread validation;
* comment lifecycle;
* reaction state transitions;
* subscription state;
* playlist validation;
* visibility rules;
* watch-history behavior;
* playback-progress rules;
* anti-spam guards.

## Integration Tests

Test:

* comments persistence;
* threaded relationships;
* reactions;
* subscriptions;
* playlists;
* watch history;
* playback progress;
* transactions;
* event publication;
* cache behavior where applicable.

## API Tests

Test:

* authenticated requests;
* anonymous access;
* owner access;
* forbidden access;
* validation failures;
* pagination;
* conflicts;
* idempotency;
* rate limiting.

## Concurrency Tests

Explicitly test:

* duplicate reaction creation;
* simultaneous subscription requests;
* subscribe/unsubscribe races;
* playlist reorder races;
* stale playback writes;
* concurrent comment operations.

## Security Tests

Test:

* cross-user playlist access;
* cross-user history access;
* unauthorized comment editing;
* unauthorized deletion;
* cross-channel subscription manipulation;
* ID-based authorization bypasses.

---

# 47. API DOCUMENTATION

Update OpenAPI documentation for every endpoint introduced by this milestone.

Document:

* request schemas;
* response schemas;
* authorization;
* pagination;
* error cases;
* idempotency;
* representative examples.

Ensure documentation reflects actual implementation.

Do not document future notification/search/recommendation functionality as implemented.

---

# 48. OPERATIONAL DOCUMENTATION

Document:

* required environment variables;
* new migrations;
* Redis usage;
* event topics/streams;
* queue usage where applicable;
* rate-limit configuration;
* local development;
* test execution;
* debugging common comment/reaction/subscription issues;
* concurrency considerations.

Do not include secrets.

Do not claim external infrastructure is provisioned unless verified.

---

# 49. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement in this milestone:

* search indexing;
* search APIs;
* recommendation ranking;
* recommendation candidate generation;
* notification delivery;
* notification workers;
* creator analytics dashboards;
* analytics warehouses;
* moderation operator interface;
* automated content moderation;
* live-stream chat;
* live-stream ingest;
* media transcoding;
* CDN;
* payment processing;
* advertising;
* web UI;
* mobile UI.

You may emit events required by these future systems.

You may create extension interfaces where the current implementation genuinely needs them.

Do not implement future features merely to consume those events.

---

# 50. VALIDATION REQUIREMENTS

Before completing this milestone, verify:

## Comments

* comments can be created;
* replies are correctly attached;
* cross-video parent references fail;
* unauthorized editing fails;
* unauthorized deletion fails;
* deletion behavior preserves thread integrity;
* pagination is stable.

## Reactions

* duplicate reactions are prevented;
* repeated add/remove calls are idempotent;
* aggregate counts remain valid;
* concurrent mutation does not corrupt state.

## Subscriptions

* duplicate subscriptions are prevented;
* unsubscribe is idempotent;
* preference updates require correct authorization;
* subscription queries are paginated;
* subscriber/subscription ownership is correct.

## Playlists

* creation works;
* owner authorization works;
* private playlists remain private;
* item additions validate video access;
* ordering remains consistent;
* concurrent changes are safe.

## Watch History

* entries are private;
* updates are persisted correctly;
* clear/delete functions correctly;
* reads are paginated.

## Playback Progress

* progress is validated;
* stale writes cannot unexpectedly overwrite newer state;
* updates are bounded;
* reads remain private.

## Events

Verify:

* correct event types;
* correct payloads;
* correct event ownership;
* transaction/event consistency;
* no duplicate unintended publications.

## Security

Verify:

* authentication;
* authorization;
* ownership;
* rate limits;
* input validation;
* privacy.

---

# 51. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Comment persistence is implemented.
3. Comment creation is implemented.
4. Comment editing is implemented.
5. Comment deletion is implemented.
6. Threaded replies are implemented.
7. Comment retrieval is paginated.
8. Comment reactions are implemented.
9. Video reactions are implemented.
10. Reaction operations are idempotent.
11. Reaction concurrency is handled.
12. Subscription relationships are implemented.
13. Subscribe is idempotent.
14. Unsubscribe is idempotent.
15. Subscription preferences are implemented where applicable.
16. Subscription queries are implemented.
17. Subscription-feed foundation is implemented.
18. Playlist creation is implemented.
19. Playlist management is implemented.
20. Playlist items are implemented.
21. Playlist ordering is implemented.
22. Playlist visibility is enforced.
23. Watch history is implemented.
24. Playback progress is implemented.
25. Private activity data is protected.
26. Required engagement/domain events are implemented.
27. Event publication is reliable for current-scope mutations.
28. Appropriate cache usage is implemented.
29. Abuse/rate-limit protection is implemented.
30. Concurrency protections are implemented.
31. API documentation is updated.
32. Operational documentation is updated.
33. Unit tests are meaningful.
34. Integration tests are meaningful.
35. API tests are meaningful.
36. Security tests are meaningful.
37. Concurrency tests are meaningful.
38. No fake persistence exists within this scope.
39. No intentional TODO/FIXME gaps substitute for implementation.
40. No hardcoded secrets exist.
41. Known limitations are reported honestly.

---

# 52. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Domains Implemented

Summarize:

* comments;
* reactions;
* subscriptions;
* playlists;
* watch history;
* playback progress.

## Database Changes

List:

* tables/models;
* constraints;
* indexes;
* migrations.

## API Changes

List:

* endpoint families;
* authorization;
* pagination;
* errors.

## Events

List all events implemented and their producers.

## Caching and Rate Limiting

Summarize implemented cache and abuse-control behavior.

## Tests

List:

* tests created;
* suites executed;
* concurrency validation;
* security validation.

## Documentation

List documentation created or updated.

## Known Limitations

List intentionally deferred functionality.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim that future notification, search, recommendation, analytics, moderation, media, or client functionality was implemented.

# 53. FINAL EXECUTION RULE

Implement only the engagement, relationship, collection, history, and playback-progress functionality defined by this milestone.

Do not implement unrelated future backend domains.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake APIs, fake persistence, placeholders, pseudo-code, or intentionally incomplete implementations within this scope.

Produce real, tested, secure, observable, scalable backend functionality for this milestone.
