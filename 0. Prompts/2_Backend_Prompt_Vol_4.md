# YouTube-Style Video Platform — Backend Prompt — Volume 4

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the fourth bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **search and content-discovery backend foundations**, including:

* search indexing;
* search document generation;
* search querying;
* autocomplete/suggestion infrastructure;
* content discovery feeds;
* related-video retrieval;
* deterministic ranking;
* recommendation candidate generation;
* recommendation filtering;
* personalization inputs;
* discovery fallback behavior;
* search/discovery caching;
* indexing and recommendation events;
* search/discovery observability;
* search/discovery security and privacy;
* tests and operational documentation.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of the complete notification system, analytics platform, moderation system, live-stream system, monetization system, or client applications.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier AI prompt was executed merely because the prompt exists in the user's conversation.

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

This milestone implements backend retrieval and discovery capabilities that consume canonical content, channel, engagement, subscription, and media-readiness information.

## 2.2 Scale Direction

The completed platform is intended to evolve toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* large search-index volume;
* high request volume for home/discovery feeds;
* high recommendation-read volume.

The current milestone does not need to implement the maximum theoretical scale immediately.

However, it must avoid architectural choices that make large-scale indexing or discovery fundamentally impractical.

---

# 3. TECHNOLOGY DIRECTION

Use the repository's established compatible technology direction:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* OpenSearch or equivalent search engine;
* REST;
* durable event consumption;
* asynchronous workers;
* OpenAPI;
* OpenTelemetry-compatible observability.

Do not replace the established backend stack without a repository-driven reason.

Do not introduce a second search engine without justification.

Do not build a separate recommendation platform when the current milestone can remain a bounded backend module/worker architecture.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Search domain/module.
2. Search document model.
3. Video indexing.
4. Channel indexing.
5. Index-update event consumers.
6. Search document lifecycle.
7. Search query API.
8. Search filtering.
9. Search sorting.
10. Search pagination.
11. Search access-control filtering.
12. Search autocomplete/suggestion foundation.
13. Search cache strategy where justified.
14. Index rebuild/reconciliation tooling.
15. Discovery domain/module.
16. Home-feed candidate retrieval.
17. Subscription-based feed retrieval.
18. Related-video retrieval.
19. Candidate filtering.
20. Deterministic ranking.
21. Cold-start discovery.
22. Personalized ranking inputs where available.
23. Negative feedback signals already represented by current backend contracts.
24. Discovery cache strategy.
25. Recommendation/discovery events.
26. Search/discovery failure fallback behavior.
27. Search/discovery observability.
28. Security and privacy protections.
29. Unit, integration, API, concurrency, and performance tests.
30. API and operational documentation.

This milestone does not implement:

* advanced machine-learning ranking;
* model training infrastructure;
* feature stores;
* notification delivery;
* analytics warehouses;
* moderation operator dashboards;
* live-stream infrastructure;
* payments;
* advertising;
* web UI;
* mobile UI.

The architecture must, however, create clean interfaces that allow those systems to consume search/discovery outputs later.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect the existing backend architecture.
2. Inspect video and channel modules.
3. Inspect visibility and authorization logic.
4. Inspect media-readiness state.
5. Inspect subscriptions.
6. Inspect reactions and engagement state.
7. Inspect watch history and playback progress.
8. Inspect event infrastructure.
9. Inspect queue/job infrastructure.
10. Inspect Redis.
11. Inspect configuration.
12. Inspect existing OpenAPI definitions.
13. Inspect tests.
14. Inspect observability.
15. Inspect architecture and contract documentation.

Reuse compatible existing services and contracts.

Do not duplicate the video ownership model, authentication model, or visibility model.

---

# 6. DOMAIN BOUNDARIES

Create explicit backend boundaries for:

## Search

Own:

* search indexes;
* search document mappings;
* search query interpretation;
* search filtering;
* search ranking configuration;
* autocomplete/suggestion retrieval;
* index maintenance.

Search does not own canonical video or channel state.

## Discovery

Own:

* feed candidate retrieval;
* ranking;
* discovery policy;
* related-content selection;
* recommendation result assembly;
* fallback strategies.

Discovery does not own user history, subscriptions, or video metadata.

It consumes those domains through explicit contracts.

---

# 7. SEARCH ARCHITECTURE

Implement OpenSearch or the repository's established search infrastructure as a derived read system.

The search index must never become the canonical source of truth for:

* videos;
* channels;
* users;
* visibility;
* moderation state;
* publication state.

Search documents are rebuildable projections.

The search system must be able to recreate its indexes from authoritative domain data and events.

---

# 8. SEARCH DOCUMENT MODEL

Implement a canonical search document for videos.

At minimum include searchable/returnable information such as:

* video ID;
* channel ID;
* title;
* description;
* tags or keywords where supported;
* language;
* category;
* publication timestamp;
* duration;
* visibility eligibility;
* moderation/indexing eligibility;
* channel name;
* channel handle;
* thumbnail reference;
* engagement signals useful for ranking;
* search-document version.

Do not duplicate sensitive private user information into the search index.

Do not store unnecessary internal fields.

---

# 9. CHANNEL SEARCH DOCUMENT

Implement a channel search document containing, as appropriate:

* channel ID;
* public channel name;
* handle;
* description;
* avatar reference;
* publication/activity signals;
* subscriber-related ranking signal where authorized;
* indexing eligibility;
* document version;
* updatedAt.

Do not index:

* account credentials;
* private account data;
* internal security data;
* private moderation details.

---

# 10. INDEX NAMING AND VERSIONING

Define deterministic index names that support versioned mappings.

Use a model such as:

```text
videos-v{version}
channels-v{version}
```

and aliases such as:

```text
videos-current
channels-current
```

where the selected search engine supports aliases.

Document:

* index version;
* mapping version;
* analyzer version;
* migration strategy;
* reindex strategy.

Do not perform destructive in-place mapping changes when an index-rebuild strategy is required.

---

# 11. INDEXING EVENT CONSUMER

Implement event consumers for relevant authoritative changes.

At minimum consume:

* video.created;
* video.published;
* video.unpublished;
* video.restricted;
* video.deleted;
* channel.created;
* channel.updated;
* channel.deleted;
* media.ready where search eligibility depends on playback readiness.

When a video becomes ineligible for search, remove or update its search document appropriately.

Do not trust event arrival order blindly.

Use:

* entity version;
* event version;
* updatedAt;
* sequence information where available

to prevent stale events from overwriting newer indexed state.

---

# 12. INDEXING IDEMPOTENCY

Indexing consumers must be idempotent.

A repeated event must not:

* duplicate search documents;
* corrupt mappings;
* regress document state;
* re-enable deleted content.

Use the canonical entity ID as the search document ID.

Where an event is stale, ignore it safely rather than allowing it to overwrite newer state.

---

# 13. SEARCH ELIGIBILITY

Before indexing any content, evaluate canonical eligibility.

A video should only be searchable when appropriate conditions such as these are satisfied:

* published;
* searchable visibility;
* media/content state allows discovery;
* not deleted;
* not blocked;
* not restricted from search.

Do not reproduce authorization logic independently.

Use the authoritative content-access and moderation contracts.

Search must never become a bypass around private-content protection.

---

# 14. INDEXING WORKERS

Implement asynchronous indexing workers where necessary.

A worker should:

1. consume the relevant event/job;
2. resolve the canonical entity;
3. validate index eligibility;
4. generate the document;
5. write/update/remove the document;
6. record success/failure;
7. emit appropriate operational telemetry.

Bound worker concurrency.

Use retries and backoff for transient search-engine failures.

Do not retry permanent validation failures indefinitely.

---

# 15. INDEX REBUILD

Implement a controlled index-rebuild/reconciliation capability.

It must support:

* selecting target index version;
* bulk indexing authoritative records;
* progress tracking;
* retry;
* failure reporting;
* validation;
* alias swap or equivalent cutover;
* rollback strategy.

Do not perform an uncontrolled full-database scan from an HTTP request.

Use background processing or administrative tooling.

Index rebuilds must be safe to repeat.

---

# 16. SEARCH QUERY API

Implement a search API.

Support at minimum:

* query text;
* search scope;
* cursor pagination;
* page size;
* safe filtering;
* sorting;
* result type;
* optional language/region context where supported.

Search should support at least:

* videos;
* channels.

Do not expose arbitrary raw OpenSearch query JSON through the public API.

Translate user-facing filters into controlled backend search expressions.

---

# 17. SEARCH FILTERING

Support filters appropriate to the product contract, such as:

* content type;
* duration range;
* publication period;
* category;
* language.

Filtering must operate on indexed fields only when those fields are explicitly part of the contract.

Do not create a public endpoint that accepts unrestricted field names or raw query clauses.

Validate every filter.

---

# 18. SEARCH SORTING

Support controlled sorting such as:

* relevance;
* newest;
* view/engagement-related ranking where explicitly supported.

Do not expose arbitrary database/search-engine sort fields.

Define stable secondary ordering to ensure cursor pagination remains deterministic.

---

# 19. SEARCH PAGINATION

Use the project's cursor pagination contract.

Cursor pagination must be deterministic with respect to:

* ranking;
* secondary sort;
* document ID.

Avoid offset pagination for large indexes.

Do not expose internal search-engine cursor state directly if it compromises portability or security.

---

# 20. SEARCH RANKING

Implement a deterministic initial ranking strategy.

Ranking may combine:

* textual relevance;
* title relevance;
* description relevance;
* freshness;
* engagement;
* channel relevance;
* content quality signals available from current backend domains.

Keep ranking weights configurable.

Do not hardcode ranking values across multiple services.

Do not implement machine-learning ranking in this milestone.

The ranking interface must allow future model-based ranking without changing the public search API.

---

# 21. AUTOCOMPLETE

Implement an autocomplete/suggestion foundation.

Support:

* prefix queries;
* controlled result count;
* normalization;
* safe handling of abusive or oversized input;
* caching.

Suggestions may derive from:

* channel names;
* public video titles;
* normalized search terms;
* curated suggestion sources when configured.

Do not expose private or unlisted content through autocomplete.

Do not index sensitive user input without an explicit privacy policy.

---

# 22. SEARCH CACHE

Use Redis for search caching where justified.

Cache keys must include all relevant query dimensions, including:

* normalized query;
* filters;
* sort;
* locale where applicable;
* page/cursor context where applicable.

Define:

* TTL;
* invalidation;
* cache size;
* stale behavior.

Do not cache private authorization decisions globally.

Search-cache responses must not leak restricted content between users.

---

# 23. SEARCH SECURITY

Protect against:

* oversized queries;
* query injection;
* unrestricted filter fields;
* expensive wildcard expressions;
* regular-expression abuse;
* search-engine resource exhaustion;
* private-content disclosure.

Normalize and validate search input.

Set query timeouts.

Limit result sizes.

Do not expose raw OpenSearch errors.

---

# 24. SEARCH API DOCUMENTATION

Document:

* query syntax;
* filters;
* sorting;
* pagination;
* result schema;
* error conditions;
* rate limits;
* authorization/visibility behavior.

Do not document unsupported raw search-engine features.

---

# 25. DISCOVERY ARCHITECTURE

Create a discovery service/module that can assemble content candidates for:

* home feed;
* subscriptions feed;
* related videos;
* short-form discovery;
* fallback discovery.

The service must distinguish:

1. candidate generation;
2. eligibility filtering;
3. ranking;
4. diversity;
5. response shaping.

Do not collapse all discovery logic into one untestable query.

---

# 26. HOME-FEED CANDIDATES

Implement deterministic home-feed candidate generation.

Candidates may come from:

* subscriptions;
* recent content;
* popular content;
* category/topic signals;
* previously engaged content;
* related content;
* creator freshness.

Candidate sources must be independently testable.

Do not require an ML model.

The service must continue functioning when one candidate source is unavailable.

---

# 27. SUBSCRIPTIONS FEED

Implement a dedicated subscriptions-feed backend endpoint.

It must return recent eligible videos from channels the user is subscribed to.

Honor:

* current subscription relationship;
* video publication state;
* visibility;
* restrictions;
* deletion;
* pagination;
* stable ordering.

Do not rank subscription feed items using arbitrary personalized recommendations in this milestone.

The purpose is to provide a deterministic and reliable subscriptions view.

---

# 28. RELATED VIDEOS

Implement a related-video retrieval capability.

Candidates may use:

* same channel;
* category;
* tags;
* language;
* textual similarity;
* co-engagement signals already available;
* recent engagement;
* freshness.

Apply eligibility filtering before ranking.

Never return:

* deleted videos;
* inaccessible private videos;
* blocked content;
* media that is not ready for playback.

The service should gracefully degrade to simpler candidate sources if some signals are unavailable.

---

# 29. SHORT-FORM DISCOVERY

Implement the backend foundation for short-form discovery.

Identify short-form content using the canonical video metadata/model.

Candidate generation must support:

* vertical/short-form eligibility;
* freshness;
* engagement;
* creator diversity;
* user personalization signals where available.

Do not build a separate unrelated content model.

Short-form discovery must use the same canonical video ownership and visibility contracts.

---

# 30. CANDIDATE ELIGIBILITY FILTER

Before ranking any candidate, filter by:

* publication state;
* visibility;
* moderation state;
* media readiness;
* deletion state;
* viewer authorization;
* content eligibility;
* age/region restrictions where the current contract supports them.

The filter must run before candidates are returned.

Do not rely on search-index state alone to enforce access control.

---

# 31. PERSONALIZATION INPUTS

Use available backend signals such as:

* subscriptions;
* watch history;
* playback progress/completion;
* reactions;
* playlists;
* recent interactions;
* category preferences;
* language;
* session context where supported.

Do not copy all watch-history data into the recommendation service.

Use controlled interfaces/read models.

Do not expose private viewing history to other users.

---

# 32. COLD-START DISCOVERY

Implement deterministic cold-start behavior.

For users with insufficient history, use signals such as:

* popular content;
* fresh content;
* category diversity;
* region/language where available;
* broad engagement quality;
* creator diversity.

Cold-start behavior must not return restricted/private content.

It must remain operational when personalization data is unavailable.

---

# 33. DETERMINISTIC RANKING

Implement an initial ranking function using configurable signals.

Potential inputs:

* freshness;
* engagement quality;
* completion rate if available;
* subscription affinity;
* textual/topic relevance;
* creator diversity;
* viewer interaction history.

Keep the ranker isolated behind an interface.

Do not scatter scoring formulas throughout controller code.

Store ranking configuration in validated configuration or a controlled data source.

---

# 34. DIVERSITY AND REPETITION CONTROL

Implement basic diversity controls.

Avoid returning excessive consecutive results from:

* the same creator;
* the same video;
* the same narrow category.

Do not recommend content the viewer has just consumed repeatedly unless the ranking policy deliberately permits it.

Define deterministic tie-breaking.

---

# 35. NEGATIVE SIGNALS

Consume available negative signals such as:

* explicit negative reactions;
* removed subscriptions;
* hidden/blocked content where represented.

Negative signals must reduce eligibility/ranking appropriately without overriding authoritative moderation or privacy rules.

Do not invent hidden user-profile attributes.

---

# 36. DISCOVERY RESULT CONTRACT

Define a canonical discovery result.

At minimum include:

* content ID;
* video metadata required by the client;
* rank position;
* source category;
* optional ranking metadata;
* freshness information where appropriate.

Do not expose internal model scores directly unless explicitly required.

Do not expose private recommendation features.

---

# 37. DISCOVERY CACHE

Cache expensive discovery results where justified.

Define:

* cache key;
* viewer context;
* query/feed type;
* TTL;
* invalidation;
* stale behavior.

Do not allow one user's personalized feed to be returned to another user.

Separate:

* public/global feed caches;
* personalized caches.

---

# 38. DISCOVERY FALLBACKS

Implement graceful degradation.

Examples:

* personalized ranking unavailable → deterministic popular/fresh feed;
* subscription candidate source unavailable → recent globally eligible content;
* related-video signal unavailable → same-channel/category fallback;
* Redis unavailable → direct computation where safe;
* search unavailable → discovery endpoints remain functional.

Do not allow a non-critical discovery dependency failure to take down core playback or content access.

---

# 39. DISCOVERY EVENTS

Publish events required by future analytics/recommendation systems.

At minimum define or emit appropriate events for:

* search.performed;
* search.result.selected;
* recommendation.impression;
* recommendation.selected;
* subscription_feed.impression;
* related_video.impression.

Do not claim these events form a complete analytics pipeline.

They are product events for later consumers.

Use the canonical event envelope.

---

# 40. EVENT CONSUMPTION

The search/discovery modules may consume:

* video lifecycle events;
* media-ready events;
* channel updates;
* subscription changes;
* engagement changes;
* moderation state changes.

Consumers must be idempotent.

Stale events must not revert current state.

Do not consume future event types that are not defined.

---

# 41. SEARCH/DISCOVERY DATA FRESHNESS

Define freshness expectations.

Search:

* should react quickly to publication/update changes where operationally reasonable.

Discovery:

* may use eventually consistent derived signals.

Document:

* expected freshness;
* stale-data tolerance;
* rebuild behavior;
* failure mode.

Do not promise strong consistency where derived systems are asynchronous.

---

# 42. RATE LIMITING

Rate-limit:

* search;
* autocomplete;
* home feed;
* related videos;
* subscription feed;
* personalized discovery endpoints.

Use limits appropriate to read-heavy endpoints.

Prevent abusive query patterns from exhausting search infrastructure.

Do not apply one global limit that makes ordinary feed scrolling unusable.

---

# 43. OBSERVABILITY

Implement search/discovery observability.

Track:

## Search

* query latency;
* result count;
* zero-result rate;
* error rate;
* index lag;
* indexing failures;
* cache hit rate;
* autocomplete latency.

## Discovery

* feed-generation latency;
* candidate counts;
* filtering rate;
* ranking latency;
* fallback frequency;
* cache hit rate;
* empty-feed rate;
* source availability;
* recommendation/discovery errors.

Use:

* request ID;
* correlation ID;
* trace ID;
* index version;
* ranking version where appropriate.

Do not log sensitive personalized recommendation inputs.

---

# 44. PERFORMANCE REQUIREMENTS

Search and discovery are read-heavy systems.

Avoid:

* loading huge candidate sets into application memory;
* querying PostgreSQL once per candidate;
* making synchronous calls to multiple slow services for every result;
* rebuilding personalized feeds from unbounded watch history;
* returning excessive page sizes;
* running unrestricted full-text queries.

Use:

* batched reads;
* bounded candidate sets;
* indexed data;
* caching;
* cursor pagination;
* precomputed derived data where appropriate.

Define timeouts for downstream calls.

---

# 45. DATABASE ACCESS PATTERNS

Search and discovery must respect canonical domain ownership.

Do not query another domain's tables with arbitrary SQL merely because it is convenient.

Use:

* domain APIs;
* read models;
* event-derived views;
* carefully defined shared read interfaces

where appropriate.

For large-scale discovery, document any intentional denormalized read models.

Do not make PostgreSQL the long-term high-volume feed-ranking engine without an explicit capacity justification.

---

# 46. SEARCH INDEX CONSISTENCY

Implement reconciliation mechanisms that can detect:

* missing documents;
* stale documents;
* orphaned documents;
* documents referencing deleted content;
* mapping/version mismatches.

Provide operational tooling to report discrepancies.

Where possible, reconciliation must be safe to run repeatedly.

Do not silently repair data without recording the operation when administrative auditability is required.

---

# 47. DISCOVERY CONSISTENCY

Discovery results must never bypass canonical access controls.

Before final response:

* filter deleted content;
* filter private content;
* filter blocked/restricted content;
* filter media-not-ready content;
* enforce applicable visibility rules.

Do not trust stale cache entries to override current authoritative access state.

---

# 48. SECURITY AND PRIVACY

Protect:

* search query privacy where applicable;
* watch-history signals;
* subscription signals;
* personalized rankings;
* private content;
* unlisted content;
* recommendation context.

Do not expose:

* hidden recommendation features;
* private viewing history;
* internal ranking scores;
* security flags;
* moderation-only fields.

Do not log complete personalized feed inputs unless explicitly justified.

---

# 49. API SURFACE

Implement API families for:

## Search

* search videos;
* search channels;
* autocomplete.

## Discovery

* home feed;
* subscriptions feed;
* related videos;
* short-form discovery.

Use common:

* authentication;
* pagination;
* error;
* rate-limit;
* response contracts.

Do not expose raw search-engine queries.

Do not expose internal ranking controls.

---

# 50. AUTHORIZATION MATRIX

Create an implementation-level authorization matrix.

At minimum:

| Operation                   | Anonymous                      | Authenticated User | Creator/Owner     | Moderator/Admin |
| --------------------------- | ------------------------------ | ------------------ | ----------------- | --------------- |
| Search public content       | Allowed                        | Allowed            | Allowed           | Allowed         |
| Autocomplete public content | Allowed                        | Allowed            | Allowed           | Allowed         |
| Home feed                   | Limited/public policy          | Allowed            | Allowed           | Allowed         |
| Subscription feed           | No                             | Own subscriptions  | Own subscriptions | Privileged      |
| Related videos              | Allowed when content is public | Allowed            | Allowed           | Allowed         |
| Personalized discovery      | No or limited                  | Own context        | Own context       | Privileged      |

Exact behavior must match the established API/product contract.

---

# 51. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* search eligibility;
* query normalization;
* ranking;
* filters;
* candidate generation;
* diversity rules;
* cold-start behavior;
* fallback selection.

## Integration Tests

Test:

* search indexing;
* index updates;
* index deletion;
* reconciliation;
* OpenSearch integration;
* Redis caching;
* discovery data retrieval;
* event consumption.

## API Tests

Test:

* search;
* autocomplete;
* home feed;
* subscriptions feed;
* related videos;
* short-form discovery;
* pagination;
* filtering;
* rate limiting;
* authorization.

## Consistency Tests

Test:

* deleted content disappears from search;
* private content is not searchable publicly;
* restricted content is filtered;
* stale events do not regress search documents;
* media-not-ready videos are not returned for playback discovery.

## Concurrency/Recovery Tests

Test:

* repeated indexing events;
* concurrent indexing;
* worker retry;
* search-engine temporary failure;
* cache failure;
* index rebuild interruption;
* discovery dependency failure.

---

# 52. PERFORMANCE VALIDATION

Perform realistic benchmark/measurement work for:

* search latency;
* autocomplete latency;
* indexing throughput;
* index update lag;
* home-feed latency;
* related-video latency;
* subscriptions-feed latency;
* cache effectiveness.

Test bounded concurrent load appropriate to the available environment.

Do not claim global-scale capacity from a local benchmark.

Report measured results and environmental limitations honestly.

---

# 53. API DOCUMENTATION

Update OpenAPI documentation for:

* search;
* autocomplete;
* home feed;
* subscriptions feed;
* related videos;
* short-form discovery.

Document:

* query parameters;
* filters;
* sorting;
* pagination;
* response schemas;
* authorization;
* error cases;
* rate limits.

Do not expose implementation-specific search-engine APIs.

---

# 54. OPERATIONAL DOCUMENTATION

Document:

* search index setup;
* mappings;
* index versions;
* alias strategy;
* reindex procedure;
* reconciliation procedure;
* queue/worker setup;
* discovery configuration;
* ranking configuration;
* cache configuration;
* failure behavior;
* troubleshooting;
* important metrics.

Do not document fictitious production resources.

---

# 55. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement in this milestone:

* machine-learning model training;
* feature-store infrastructure;
* advanced ML ranking;
* online model serving;
* analytics warehouse;
* complete creator analytics;
* notifications;
* moderation dashboards;
* automated moderation;
* live-stream media infrastructure;
* payments;
* advertising;
* web UI;
* mobile UI.

The architecture must remain extensible for these future milestones.

Do not implement them now.

---

# 56. VALIDATION REQUIREMENTS

Before completion, verify:

## Search

* publication creates searchable content;
* deleted content is removed;
* private content is protected;
* restricted content is excluded;
* filters work;
* sorting works;
* cursors are stable;
* autocomplete does not expose private content;
* index rebuilding works.

## Discovery

* home feed produces valid candidates;
* subscription feed contains eligible subscribed-channel content;
* related videos are relevant enough for deterministic initial behavior;
* short-form discovery respects content type;
* personalized inputs remain private;
* cold-start works;
* fallback behavior works.

## Reliability

Verify:

* search-engine failure does not corrupt canonical content;
* cache failure does not make discovery permanently unavailable;
* indexing retries are bounded;
* stale events do not overwrite newer indexed content;
* index reconciliation can recover missing/stale documents.

## Security

Verify:

* no private content is searchable;
* no private feed is returned to another user;
* raw search-engine queries are not exposed;
* sensitive ranking data is not leaked;
* rate limits are enforced.

## Observability

Verify:

* search latency metrics;
* indexing failures;
* feed latency;
* fallback metrics;
* cache metrics;
* correlation IDs.

---

# 57. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Search domain/module is implemented.
3. Video search documents are implemented.
4. Channel search documents are implemented.
5. Index lifecycle is implemented.
6. Search indexing consumers are implemented.
7. Indexing is idempotent.
8. Search eligibility is enforced.
9. Search query API is implemented.
10. Search filtering is implemented.
11. Search sorting is implemented.
12. Cursor pagination is implemented.
13. Autocomplete foundation is implemented.
14. Search caching is implemented where justified.
15. Index rebuild/reconciliation tooling exists.
16. Discovery domain/module is implemented.
17. Home-feed candidate generation is implemented.
18. Subscription-feed backend is implemented.
19. Related-video retrieval is implemented.
20. Short-form discovery foundation is implemented.
21. Candidate filtering is implemented.
22. Deterministic ranking is implemented.
23. Cold-start behavior is implemented.
24. Basic diversity/repetition control is implemented.
25. Discovery caching is implemented where justified.
26. Search/discovery events are emitted as required.
27. Search/discovery failures degrade safely.
28. Rate limiting is implemented.
29. Security and privacy requirements are enforced.
30. Observability is implemented.
31. Search tests are implemented.
32. Discovery tests are implemented.
33. API tests are implemented.
34. consistency/reconciliation tests are implemented.
35. recovery/concurrency tests are implemented.
36. performance validation has been performed.
37. API documentation is updated.
38. operational documentation is updated.
39. No fake search engine or fake discovery behavior substitutes for the required implementation.
40. No intentional TODO/FIXME gap substitutes for current-scope functionality.
41. No hardcoded secrets exist.
42. Known limitations are reported honestly.

---

# 58. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Search

Summarize:

* index structure;
* indexing workers;
* query APIs;
* autocomplete;
* filtering;
* sorting;
* rebuild/reconciliation.

## Discovery

Summarize:

* candidate sources;
* eligibility filtering;
* ranking;
* cold start;
* subscriptions feed;
* related videos;
* short-form discovery;
* fallback behavior.

## Caching

Summarize cache keys, TTLs, invalidation, and failure behavior.

## Events

List search/discovery events and consumers.

## Tests

List:

* unit tests;
* integration tests;
* API tests;
* consistency tests;
* recovery tests;
* performance validation.

## Documentation

List documentation created or updated.

## Known Limitations

List functionality intentionally deferred to later milestones.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim that machine-learning infrastructure, analytics warehouses, or external search infrastructure was provisioned unless it actually was.

# 59. FINAL EXECUTION RULE

Implement only the search and discovery functionality defined by this milestone.

Do not implement unrelated notification, analytics, moderation, live-stream, monetization, frontend, or mobile functionality.

Do not redesign established contracts arbitrarily.

Do not depend on another AI prompt.

Do not fabricate repository state.

Do not use fake search results, fake persistence, placeholder ranking, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, secure, observable, scalable search and discovery backend functionality
