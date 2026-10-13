# YouTube-Style Video Platform — Backend Prompt — Volume 6

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the sixth bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **trust & safety, moderation, abuse-prevention, and administrative backend foundations**.

It is responsible for:

* user/content reporting;
* moderation cases;
* moderation decisions;
* content restrictions;
* comment moderation;
* account/channel enforcement;
* blocking;
* abuse signals;
* moderation queues;
* moderation audit trails;
* appeals/workflow boundaries where applicable;
* administrator authorization;
* administrative operations;
* operational audit logging;
* privileged administrative APIs;
* moderation events;
* abuse-prevention controls;
* moderation-related observability;
* security and privacy protections;
* comprehensive testing.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of full live-streaming media infrastructure, payments, advertising, advanced recommendation models, or client applications.

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

This milestone implements the trust-and-safety and administrative control plane required to operate that product safely.

## 2.2 Scale Direction

The completed platform is intended to evolve toward:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* very large comment and report volume;
* large-scale automated and human moderation workloads;
* globally distributed content and users.

The current milestone does not need to implement every global-scale moderation mechanism immediately.

However, the design must avoid:

* synchronous human-review dependencies in normal content requests;
* unbounded moderation queues;
* authorization decisions based only on frontend state;
* irreversible destructive operations without explicit policy;
* missing audit trails for privileged actions.

---

# 3. TECHNOLOGY DIRECTION

Use the existing compatible backend stack:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* durable queues;
* event streaming;
* REST;
* OpenAPI;
* OpenTelemetry-compatible observability.

Do not introduce a separate moderation platform unless the repository already requires one.

Keep automated detection, moderation workflows, and administrative tooling behind clear domain boundaries.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Reporting domain.
2. User reporting.
3. Video reporting.
4. Comment reporting.
5. Channel reporting.
6. Moderation-case creation.
7. Case state management.
8. Moderation evidence references.
9. Moderation decision records.
10. Content restriction controls.
11. Comment hide/remove controls.
12. Video restrict/block controls.
13. Channel/account enforcement foundations.
14. User blocking.
15. Abuse-prevention signals.
16. Moderation queues.
17. Moderator role and permission enforcement.
18. Moderator assignment/state tracking.
19. Administrative audit logging.
20. Administrative user/channel/content operations within scope.
21. Moderation action idempotency.
22. Moderation events.
23. Abuse/rate-limit extensions.
24. Moderation cache invalidation where required.
25. Security and privacy controls.
26. Moderation and administration observability.
27. Unit, integration, API, concurrency, and security tests.
28. API documentation.
29. Operational documentation.

This milestone does not implement:

* automated machine-learning content classification;
* full legal/compliance workflow;
* live-stream ingest;
* advertising;
* payment processing;
* advanced recommendation models;
* web administration UI;
* mobile administration UI;
* complete analytics warehouse.

Interfaces may be created for future automated moderation or external safety providers, but external systems must not be fabricated.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect authentication and authorization.
2. Inspect users/accounts.
3. Inspect channels.
4. Inspect videos.
5. Inspect comments.
6. Inspect reactions.
7. Inspect notifications.
8. Inspect events.
9. Inspect queues.
10. Inspect rate limiting.
11. Inspect audit/logging infrastructure.
12. Inspect API errors.
13. Inspect visibility/content-state handling.
14. Inspect existing administration interfaces or contracts.
15. Inspect database migrations.
16. Inspect tests.
17. Inspect observability.

Reuse existing authorization and domain contracts.

Do not create a second user-role system.

Do not create a second visibility model.

Do not duplicate audit infrastructure if an existing implementation is suitable.

---

# 6. DOMAIN BOUNDARIES

Create or extend clear backend modules for:

* reports;
* moderation;
* enforcement;
* blocking;
* administration;
* audit.

## Reports

Own:

* report submission;
* report lifecycle;
* report reason;
* reporter;
* target;
* evidence reference;
* deduplication.

## Moderation

Own:

* cases;
* queues;
* moderator assignment;
* decisions;
* actions;
* enforcement state.

## Enforcement

Own or coordinate:

* content restrictions;
* comment restrictions;
* channel/account enforcement;
* blocking relationships.

## Administration

Own:

* privileged operational actions;
* controlled administrative queries;
* administrative workflow boundaries.

## Audit

Own:

* security-sensitive and administrative audit records.

Do not allow moderation to become the canonical owner of video metadata or account identity.

---

# 7. REPORTING MODEL

Implement a canonical report model.

At minimum include:

* report ID;
* reporter ID where applicable;
* target type;
* target ID;
* reason;
* description;
* status;
* priority;
* createdAt;
* updatedAt;
* resolvedAt;
* deduplication key;
* assigned case ID where applicable.

Support target types such as:

* video;
* comment;
* channel;
* user.

Do not allow arbitrary target types not defined by the contract.

---

# 8. REPORT REASONS

Implement controlled report reason codes.

Examples may include:

* spam;
* harassment;
* hate/abuse;
* sexual content;
* dangerous content;
* violence;
* impersonation;
* copyright-related complaint boundary;
* privacy violation;
* misleading content;
* other policy category.

The exact set must be represented as stable configuration/enum values.

Do not accept arbitrary free-form policy categories from clients.

User-provided descriptions may accompany a controlled reason code.

---

# 9. REPORT SUBMISSION

Implement authenticated reporting for supported targets.

A report submission must:

1. authenticate the reporter where authentication is required;
2. validate target existence and eligibility;
3. validate reason;
4. validate description limits;
5. prevent obvious duplicate spam;
6. create the report;
7. assign appropriate initial status/priority;
8. emit `report.created`;
9. make the report available to moderation workflows.

Do not reveal confidential moderation information to reporters.

Do not allow users to submit reports that mutate target state directly.

---

# 10. REPORT DEDUPLICATION

Prevent obvious duplicate report flooding.

Define deduplication using appropriate combinations of:

* reporter;
* target;
* reason;
* active/reporting window.

Repeated identical reports must not create unlimited duplicate cases.

However, the system must still preserve meaningful independent reports when different users report the same target.

Define how multiple reports aggregate onto one moderation case.

---

# 11. REPORT PRIVACY

Report submissions are sensitive.

Do not expose:

* reporter identity to ordinary public users;
* internal moderation notes;
* case assignment;
* other users' reports;
* moderator identities where policy does not require disclosure.

Moderators and administrators may access report information according to explicit authorization.

Audit access to sensitive moderation information where appropriate.

---

# 12. MODERATION CASE MODEL

Implement a moderation case model.

At minimum include:

* case ID;
* associated report(s);
* target;
* priority;
* status;
* assigned moderator;
* category;
* evidence references;
* decision;
* createdAt;
* updatedAt;
* resolvedAt.

Case states should explicitly include concepts such as:

* open;
* queued;
* assigned;
* under_review;
* actioned;
* dismissed;
* appealed;
* closed.

Use stable state values.

Do not allow arbitrary client state transitions.

---

# 13. CASE CREATION

When reports are received:

1. determine whether an existing open case already covers the target;
2. associate the report where appropriate;
3. otherwise create a new case;
4. assign initial priority;
5. emit moderation events.

Case creation must be idempotent.

Concurrent reports for the same target must not create uncontrolled duplicate cases when the policy calls for aggregation.

---

# 14. MODERATION QUEUES

Implement moderation queues with explicit ownership.

Queue fields may include:

* queue type;
* priority;
* target type;
* target ID;
* case ID;
* state;
* assigned moderator;
* createdAt;
* updatedAt.

Support queues such as:

* general content review;
* comment review;
* abuse/account review;
* high-priority safety review.

Do not build a UI.

Provide backend APIs and domain behavior that a future moderator interface can consume.

---

# 15. MODERATOR ASSIGNMENT

Implement controlled case assignment.

Support:

* assign;
* unassign;
* reassign;
* claim where authorized.

Assignment mutations must be:

* authenticated;
* authorized;
* audited;
* concurrency-safe.

Do not allow two moderators to silently overwrite each other's assignments.

Use optimistic concurrency or another appropriate mechanism.

---

# 16. MODERATION EVIDENCE

Implement evidence references rather than copying arbitrary sensitive data into moderation records.

Evidence may reference:

* target resource;
* relevant snapshot;
* media asset;
* comment;
* report description;
* event;
* moderation signal.

Store enough metadata to identify what was reviewed.

Do not store unnecessary copies of sensitive media.

If evidence snapshots are necessary, use controlled storage and lifecycle rules.

---

# 17. MODERATION DECISION MODEL

Implement explicit moderation decisions.

At minimum represent:

* decision;
* decision reason;
* moderator;
* target;
* createdAt;
* expiration where applicable;
* enforcement action;
* appeal status where supported.

A moderation decision must be distinct from the target's canonical content state.

The moderation system requests/enforces changes through explicit domain actions.

---

# 18. MODERATION ACTIONS

Support controlled actions such as:

## Content

* hide;
* restrict;
* block;
* remove from discovery;
* restore.

## Comments

* hide;
* remove;
* restore.

## Channels

* restrict;
* suspend;
* restore.

## Accounts

* warn;
* restrict;
* suspend;
* restore.

Do not allow arbitrary state injection.

Every action must map to a controlled action type.

---

# 19. VIDEO ENFORCEMENT

Implement moderation controls for videos.

The moderation domain must be able to cause a video to become:

* restricted;
* blocked;
* removed from discovery;
* restored where authorized.

The video domain remains authoritative for canonical video ownership and lifecycle.

Enforcement changes must propagate through established domain interfaces/events.

Do not directly manipulate unrelated domain tables from moderation code merely for convenience.

---

# 20. COMMENT ENFORCEMENT

Implement moderation actions for comments.

Support:

* hide;
* remove;
* restore.

Maintain thread integrity.

A removed comment must not expose original content publicly.

Moderation deletion is distinct from user-requested comment deletion where policy/audit semantics differ.

Preserve the appropriate audit and decision records.

---

# 21. CHANNEL AND ACCOUNT ENFORCEMENT

Implement foundations for:

* channel restriction;
* channel suspension;
* account restriction;
* account suspension;
* restoration.

Differentiate:

* account status;
* channel status;
* content status;
* moderation case status.

Do not overload a single `status` field with unrelated meanings.

---

# 22. USER BLOCKING

Implement user-to-user blocking.

Support:

* block;
* unblock;
* block-state query.

Blocking must affect appropriate interaction capabilities defined by the product contract.

At minimum consider:

* comments;
* replies;
* direct interaction where future domains consume the block state.

Do not make blocking a moderation action unless performed by an authorized moderator.

A user's personal block must remain distinct from platform enforcement.

---

# 23. BLOCKING PRIVACY

Users must only be able to retrieve their own blocking state.

Do not expose a public "who blocked whom" endpoint.

Backend authorization must prevent users from querying another user's block list by ID substitution.

---

# 24. ABUSE SIGNALS

Implement structured abuse signals appropriate to this milestone.

Potential signals include:

* repeated report creation;
* comment flooding;
* reaction flooding;
* rapid subscribe/unsubscribe cycling;
* repeated failed authentication;
* suspicious upload behavior;
* repeated moderation-triggering activity.

Signals must be stored or emitted through a controlled abstraction.

Do not create a machine-learning fraud platform.

The objective is to establish high-quality signals and enforcement hooks for future anti-abuse systems.

---

# 25. ABUSE ESCALATION

Create a controlled mechanism for turning abuse signals into actions where deterministic policy is sufficient.

Examples:

* temporary rate restriction;
* interaction cooldown;
* report throttling;
* comment throttle;
* account review flag.

High-impact account suspension should require explicit policy/action boundaries unless automated enforcement is intentionally configured.

Do not silently implement permanent bans based on a single heuristic.

---

# 26. RATE LIMITING

Extend rate limits for abuse-sensitive operations:

* reports;
* comment interactions;
* reactions;
* subscription changes;
* block/unblock operations;
* moderator APIs;
* administrative APIs.

Moderator/admin endpoints need their own protection even though they are authenticated.

Do not assume privileged users should have unlimited request rates.

---

# 27. ADMINISTRATIVE AUTHORIZATION

Implement explicit administrative authorization.

At minimum distinguish:

* standard user;
* creator/channel operator;
* moderator;
* administrator;
* platform operations role where applicable.

Use permissions rather than one giant `isAdmin` boolean where the existing architecture supports granular authorization.

Sensitive actions must require the specific permission needed.

---

# 28. ADMINISTRATIVE API BOUNDARIES

Implement backend APIs for controlled administrative workflows such as:

* inspect user;
* inspect channel;
* inspect video;
* inspect moderation case;
* search moderation cases;
* update moderation case;
* assign moderator;
* apply approved enforcement;
* restore moderated content;
* inspect audit records according to privilege.

Do not expose unrestricted database search.

Do not expose internal credentials.

Do not expose arbitrary command execution.

---

# 29. ADMINISTRATIVE ACTION SAFETY

Administrative mutations must:

1. authenticate the actor;
2. verify explicit permission;
3. validate target;
4. validate requested action;
5. validate current target state;
6. execute within a transaction where required;
7. record an audit event;
8. emit relevant domain events;
9. return the canonical resulting state.

A privileged role does not bypass domain invariants.

---

# 30. AUDIT LOG MODEL

Implement a durable administrative/security audit record.

At minimum include:

* audit ID;
* actor ID;
* actor role/permission context;
* action;
* target type;
* target ID;
* reason;
* request ID;
* correlation ID;
* timestamp;
* result;
* metadata safe for audit storage.

Do not store secrets.

Do not store raw authentication credentials.

Audit records must be append-oriented and protected from ordinary user modification.

---

# 31. AUDIT IMMUTABILITY

Audit records must not be editable through normal administrative APIs.

Corrections must be represented as additional audit events rather than silently rewriting history, where the product's audit model requires immutable history.

Administrative deletion of audit records should be prohibited from normal application workflows.

Retention must be explicit.

---

# 32. MODERATION EVENTS

Publish events such as:

* report.created;
* moderation.case.created;
* moderation.case.assigned;
* moderation.case.updated;
* moderation.action.applied;
* moderation.action.reversed;
* moderation.case.closed;
* user.blocked;
* user.unblocked;
* enforcement.applied;
* enforcement.removed;
* audit.record.created.

Use the project's canonical event envelope.

Consumers must be idempotent.

Do not create duplicate events for retries.

---

# 33. MODERATION EVENT ORDERING

Where ordering matters:

* case creation must precede case resolution;
* enforcement application must precede enforcement removal;
* assignment must not silently overwrite a newer assignment;
* restore operations must not resurrect content that was subsequently deleted.

Use versioning, optimistic concurrency, or explicit state transitions.

Do not rely exclusively on timestamps to protect ordering.

---

# 34. MODERATION CACHE INVALIDATION

When enforcement changes content visibility or interaction behavior, invalidate appropriate caches.

At minimum consider:

* video-access cache;
* playback metadata;
* discovery/search eligibility;
* comment visibility;
* channel/account status;
* user-block state.

Do not leave stale cached content accessible after a high-priority enforcement action.

Where immediate invalidation is impossible, define the acceptable propagation delay.

---

# 35. SEARCH/DISCOVERY INTEGRATION

Moderation state must propagate to search/discovery.

When content becomes:

* restricted;
* blocked;
* deleted;
* restored;

publish the required events.

Do not directly manipulate search-index documents from unrelated moderation logic unless an explicit shared contract requires it.

Search/discovery consumers should remain responsible for their derived representations.

---

# 36. NOTIFICATION INTEGRATION

This milestone may emit events for future notification workflows when moderation or administrative state changes warrant user notification.

Do not implement a second notification pipeline.

Examples may include:

* moderation action applied;
* account suspension;
* restoration.

The notification system remains authoritative for delivery.

---

# 37. ANALYTICS INTEGRATION

Publish moderation/abuse events for analytics consumers where appropriate.

Do not expose sensitive moderation notes as ordinary analytics data.

Use controlled event payloads.

---

# 38. MODERATION CASE QUERIES

Implement moderator-authorized query APIs.

Support:

* case list;
* queue list;
* case detail;
* reports associated with a case;
* evidence references;
* assignment;
* decision history;
* enforcement history.

Use cursor pagination.

Support controlled filtering such as:

* status;
* priority;
* target type;
* assigned moderator;
* creation range;
* category.

Do not expose unrestricted query predicates.

---

# 39. ADMINISTRATIVE SEARCH

Implement controlled administrative search over authorized resources.

Support appropriate filters for:

* user;
* channel;
* video;
* case;
* status;
* moderation state.

Do not expose raw SQL or arbitrary OpenSearch queries to administrators.

Administrative search must enforce authorization and privacy boundaries.

---

# 40. MODERATION DATA PRIVACY

Moderation data may contain highly sensitive information.

Protect:

* report descriptions;
* evidence;
* moderator notes;
* enforcement reasons;
* account risk signals;
* administrative metadata.

Do not return sensitive moderation fields to:

* ordinary users;
* creators unless explicitly permitted;
* public APIs.

Use field-level response models rather than exposing database entities directly.

---

# 41. APPEAL BOUNDARY

Where the product contract supports appeals, implement only the bounded workflow foundation:

* appeal creation;
* appeal status;
* associated moderation decision;
* appeal queue/state.

Do not create a full legal/compliance system.

Appeals must not automatically reverse moderation actions.

A reversal must be represented by an explicit authorized decision.

---

# 42. MODERATION EXPIRATION

Support time-bounded enforcement where applicable.

Examples:

* temporary restriction;
* temporary suspension;
* temporary interaction cooldown.

Use explicit:

* startsAt;
* expiresAt;
* active status.

Do not rely on background jobs alone to maintain current access state.

Authorization/enforcement checks must also account for expiration directly.

---

# 43. MODERATION CONCURRENCY

Protect concurrent moderation operations.

Test:

* two moderators claiming the same case;
* two moderators applying actions;
* action then restore;
* restore then delete;
* suspension while account deletion begins;
* moderator action while user changes content.

Use:

* optimistic versioning;
* transactions;
* state-transition validation;
* explicit conflict errors.

Do not allow last-write-wins behavior to silently erase a moderation decision.

---

# 44. DATABASE MODEL

Implement or update models for:

* reports;
* moderation cases;
* moderation evidence;
* moderation decisions/actions;
* enforcement records;
* user blocks;
* abuse signals;
* appeals where applicable;
* administrative audit records.

Use appropriate:

* foreign keys;
* unique constraints;
* status fields;
* timestamps;
* indexes.

Index:

* target;
* case status;
* priority;
* assignment;
* creation time;
* active enforcement;
* user blocks;
* audit actor;
* audit target.

---

# 45. RETENTION

Define retention behavior for:

* reports;
* cases;
* evidence references;
* audit records;
* abuse signals;
* block relationships.

Do not apply short retention to audit/security records without an explicit policy.

Do not retain sensitive evidence forever without justification.

Retention jobs must be:

* asynchronous;
* idempotent;
* observable.

---

# 46. API SURFACE

Implement API families for:

## Reporting

* create report;
* retrieve own report status where allowed.

## User Blocking

* block user;
* unblock user;
* get own block state/list where supported.

## Moderation

* list cases;
* get case;
* assign;
* unassign;
* update;
* apply action;
* reverse action where authorized;
* manage appeal state where supported.

## Administration

* inspect authorized user/channel/video;
* execute approved administrative actions;
* retrieve authorized audit records.

All privileged endpoints must enforce explicit permissions.

---

# 47. AUTHORIZATION MATRIX

Create an implementation-level matrix.

At minimum:

| Operation                          | Anonymous | User                    | Creator                                     | Moderator                     | Administrator |
| ---------------------------------- | --------- | ----------------------- | ------------------------------------------- | ----------------------------- | ------------- |
| Submit report                      | No        | Allowed                 | Allowed                                     | Allowed                       | Allowed       |
| View own report status             | No        | Allowed where supported | Allowed                                     | Allowed                       | Allowed       |
| Block user                         | No        | Own action              | Own action                                  | Privileged                    | Privileged    |
| View moderation case               | No        | No                      | Restricted                                  | Allowed                       | Allowed       |
| Assign moderation case             | No        | No                      | No                                          | Permissioned                  | Allowed       |
| Apply moderation action            | No        | No                      | No unless explicit creator moderation right | Permissioned                  | Allowed       |
| Reverse moderation action          | No        | No                      | No                                          | Permissioned                  | Allowed       |
| Inspect user administratively      | No        | No                      | No                                          | Limited                       | Permissioned  |
| Execute administrative enforcement | No        | No                      | No                                          | Only where explicitly allowed | Permissioned  |
| Read sensitive audit records       | No        | No                      | No                                          | Limited                       | Permissioned  |

Refine permissions to match the actual role model.

---

# 48. SECURITY REQUIREMENTS

Protect against:

* privilege escalation;
* IDOR;
* report abuse;
* moderator impersonation;
* administrative misuse;
* evidence disclosure;
* audit tampering;
* unauthorized enforcement;
* stale enforcement state;
* race conditions;
* cross-user block-list access.

Use:

* server-side authorization;
* explicit permissions;
* field-level response filtering;
* immutable/auditable records;
* concurrency controls;
* rate limits;
* secure internal authentication.

---

# 49. OBSERVABILITY

Implement metrics and traces for:

## Moderation

* reports submitted;
* cases created;
* queue depth;
* case age;
* assignment latency;
* action latency;
* enforcement failures;
* appeal volume;
* moderation-action conflicts.

## Abuse

* abuse-signal volume;
* throttled requests;
* repeated-report patterns;
* interaction abuse;
* automated enforcement triggers.

## Administration

* administrative operations;
* authorization failures;
* audit-write failures;
* privileged endpoint latency.

Do not emit sensitive report bodies or moderator notes into logs.

---

# 50. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* report validation;
* deduplication;
* moderation state transitions;
* authorization policies;
* enforcement expiration;
* block behavior;
* audit creation;
* action reversal.

## Integration Tests

Test:

* report persistence;
* case creation;
* queue behavior;
* enforcement propagation;
* cache invalidation;
* audit persistence;
* event publication.

## API Tests

Test:

* report submission;
* blocking;
* moderation APIs;
* administrative APIs;
* authorization;
* pagination;
* filtering;
* rate limits.

## Security Tests

Test:

* privilege escalation;
* IDOR;
* cross-user case access;
* moderator/admin permission boundaries;
* audit tampering;
* evidence leakage;
* unauthorized enforcement.

## Concurrency Tests

Test:

* simultaneous moderator assignment;
* competing moderation actions;
* action/reversal races;
* concurrent user blocking;
* enforcement/deletion races.

---

# 51. PERFORMANCE VALIDATION

Measure:

* report submission latency;
* moderation-case queries;
* queue throughput;
* moderation-action latency;
* privileged API latency;
* audit-write latency.

Test bounded concurrent access to moderation queues and privileged endpoints.

Do not claim global-scale moderation capacity from local tests.

Report environmental limitations honestly.

---

# 52. API DOCUMENTATION

Update OpenAPI documentation for:

* reporting;
* blocking;
* moderation;
* appeals where supported;
* administration.

Document:

* permissions;
* response fields;
* errors;
* pagination;
* filters;
* concurrency conflicts;
* audit semantics.

Do not expose hidden privileged fields in ordinary API schemas.

---

# 53. OPERATIONAL DOCUMENTATION

Document:

* moderation queues;
* case lifecycle;
* assignment behavior;
* enforcement actions;
* expiration;
* audit records;
* retention;
* abuse signals;
* privileged API operation;
* failure recovery;
* security incident considerations;
* observability.

Do not include real administrative credentials.

---

# 54. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* machine-learning moderation;
* automated image/video classification;
* full copyright-detection infrastructure;
* legal/compliance case-management systems;
* advertising;
* payments;
* live-stream media infrastructure;
* recommendation model training;
* web moderation UI;
* mobile moderation UI.

Create only the contracts/interfaces required for future integration.

Do not fabricate external trust-and-safety provider results.

---

# 55. VALIDATION REQUIREMENTS

Before completion, verify:

## Reporting

* reports validate correctly;
* duplicate-report abuse is controlled;
* sensitive report data is protected;
* reports are associated with cases correctly.

## Moderation

* state transitions are valid;
* assignment is concurrency-safe;
* decisions are auditable;
* enforcement is explicit;
* expiration works;
* reversals are controlled.

## Enforcement

* restricted content is actually restricted;
* blocked content is excluded from applicable access paths;
* comment moderation affects public visibility;
* account/channel enforcement is enforced server-side.

## Blocking

* block/unblock is idempotent;
* block state is private;
* blocked interactions are prevented where required.

## Administration

* privileged access requires correct permissions;
* administrative actions are audited;
* audit records cannot be silently modified.

## Security

* IDOR tests pass;
* privilege escalation tests pass;
* evidence leakage is prevented;
* stale enforcement cannot bypass current policy.

## Reliability

* queue failures are recoverable;
* moderation actions are idempotent;
* event publication is reliable;
* cache invalidation occurs after enforcement.

---

# 56. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Reporting is implemented.
3. Report deduplication is implemented.
4. Moderation cases are implemented.
5. Case states are implemented.
6. Moderation queues are implemented.
7. Moderator assignment is implemented.
8. Evidence references are implemented.
9. Moderation decisions are implemented.
10. Enforcement actions are implemented.
11. Video enforcement is integrated.
12. Comment enforcement is integrated.
13. Channel/account enforcement is integrated.
14. User blocking is implemented.
15. Abuse signals are implemented.
16. Deterministic abuse throttling is implemented where scoped.
17. Administrative authorization is implemented.
18. Administrative APIs are implemented.
19. Audit logging is implemented.
20. Audit records are protected from ordinary mutation.
21. Appeals foundation is implemented where required.
22. Enforcement expiration is implemented.
23. Moderation concurrency is protected.
24. Moderation events are implemented.
25. Cache invalidation is implemented where necessary.
26. Retention behavior is implemented.
27. API documentation is updated.
28. Operational documentation is updated.
29. Unit tests are implemented.
30. Integration tests are implemented.
31. API tests are implemented.
32. Security tests are implemented.
33. Concurrency tests are implemented.
34. Performance validation has been performed.
35. No fake moderation results or fabricated external provider behavior exists.
36. No intentional TODO/FIXME gap substitutes for current-scope functionality.
37. No hardcoded secrets exist.
38. Known limitations are reported honestly.

---

# 57. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Reporting

Summarize:

* report model;
* reasons;
* deduplication;
* privacy.

## Moderation

Summarize:

* case model;
* queues;
* assignment;
* decisions;
* enforcement;
* appeals.

## Abuse Prevention

Summarize:

* signals;
* throttling;
* rate limits.

## Administration

Summarize:

* permissions;
* privileged APIs;
* audit logging.

## Database Changes

List:

* models;
* migrations;
* indexes;
* constraints.

## Events

List moderation/admin events and producers.

## Tests

List:

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

Do not claim that machine-learning moderation, external safety providers, legal/compliance systems, or cloud infrastructure were provisioned unless that actually occurred.

# 58. FINAL EXECUTION RULE

Implement only the moderation, trust-and-safety, abuse-prevention, blocking, administration, audit, and supporting backend functionality defined by this milestone.

Do not implement unrelated future domains.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake moderation decisions, fake external safety results, placeholder enforcement, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, secure, privacy-aware, observable, auditable backend functionality.
