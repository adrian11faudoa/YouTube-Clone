# YouTube-Style Video Platform — Backend Prompt — Volume 1

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the first bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone establishes the production backend foundation and implements the core identity, account, channel, video metadata, publication lifecycle, and upload-control functionality required for the platform's subsequent backend domains.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of all product capabilities described by the global project specification.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that another AI prompt was executed.

Do not fabricate previous implementation state.

Preserve compatible existing code where it exists.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent, production-grade YouTube-style video platform supporting:

* viewers;
* creators;
* channels;
* long-form and short-form video;
* uploads;
* media processing;
* adaptive playback;
* subscriptions;
* comments;
* reactions;
* playlists;
* search;
* recommendations;
* notifications;
* analytics;
* moderation;
* administration;
* live-streaming;
* monetization-capable integrations.

This milestone covers only the foundational backend domains defined below.

## 2.2 Scale Direction

The completed platform is intended to evolve toward approximately:

* 250 million registered accounts;
* 50 million daily active users;
* millions of concurrent playback sessions;
* hundreds of thousands of uploaded videos per day;
* petabyte-scale media storage;
* globally distributed CDN delivery.

The current implementation does not need to operate at that maximum scale immediately.

However, this milestone must avoid architecture choices that fundamentally prevent future scaling.

## 2.3 Backend Technology

Use:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* REST;
* OpenAPI;
* background job infrastructure where required;
* structured logging;
* OpenTelemetry-compatible tracing and metrics.

Use the repository's existing compatible versions when present.

Do not replace the established backend stack merely for convenience.

---

# 3. CURRENT MILESTONE SCOPE

This milestone implements:

1. Backend application foundation.
2. Configuration validation.
3. Database foundation and migration infrastructure.
4. Global error handling.
5. Request validation.
6. Request/correlation identifiers.
7. Authentication foundation.
8. Session management.
9. Account management.
10. Authorization foundation.
11. User profile foundation.
12. Channel management.
13. Video metadata.
14. Video lifecycle state management.
15. Video visibility management.
16. Video ownership.
17. Upload-session control plane.
18. Secure upload authorization.
19. Upload finalization.
20. Media-processing job creation for finalized uploads.
21. Video publication controls.
22. Core audit/security logging required by these domains.
23. Unit/integration/API tests for all implemented behavior.
24. API documentation for this milestone.
25. Operational documentation for the implemented backend foundation.

This milestone does not implement media transcoding itself.

This milestone does not implement CDN delivery itself.

This milestone does not implement search.

This milestone does not implement recommendations.

This milestone does not implement comments or reactions.

This milestone does not implement subscriptions.

This milestone does not implement playlists.

This milestone does not implement notifications.

This milestone does not implement analytics pipelines.

This milestone does not implement moderation tooling.

This milestone does not implement live-streaming media ingest.

This milestone does not implement payments or advertising.

---

# 4. REPOSITORY INSPECTION

Before implementation:

1. Inspect the repository structure.
2. Inspect package manifests.
3. Inspect TypeScript configuration.
4. Inspect existing NestJS modules.
5. Inspect existing environment/configuration files.
6. Inspect database configuration.
7. Inspect migrations.
8. Inspect existing authentication code.
9. Inspect existing API controllers and DTOs.
10. Inspect existing shared utilities.
11. Inspect existing tests.
12. Inspect existing architecture and contract documentation.
13. Inspect existing logging and telemetry setup.
14. Inspect existing infrastructure configuration relevant to the backend.

Determine what already exists.

Reuse compatible infrastructure rather than generating duplicates.

If an existing implementation conflicts with the required contracts, resolve the conflict within this milestone where it belongs and document the resulting compatibility decision.

Do not assume that files absent from the repository were created in another AI conversation.

---

# 5. BACKEND ARCHITECTURE

Implement a modular NestJS backend.

The initial backend may remain a coherent deployable application while maintaining explicit domain boundaries.

Create clear modules for at least:

* configuration;
* health/readiness;
* identity;
* accounts;
* authentication;
* sessions;
* authorization;
* channels;
* videos;
* uploads;
* shared infrastructure.

Do not split every module into a separate microservice.

Define clear internal boundaries so future extraction remains possible without forcing premature distributed-system complexity.

Use dependency direction that keeps domain logic independent from transport details where practical.

---

# 6. PROJECT-WIDE CONTRACTS FOR THIS MILESTONE

The implementation must use the following canonical concepts.

## Identifier

Use the project's authoritative stable identifier model for:

* user;
* account;
* session;
* channel;
* video;
* media asset;
* upload session;
* processing job;
* audit record.

Do not introduce competing public ID formats.

## Timestamps

Use the project-wide UTC timestamp convention with consistent serialization.

At minimum support:

* `createdAt`;
* `updatedAt`;
* `deletedAt` where applicable.

Use server-generated timestamps as authoritative.

## Error Contract

Use one API error envelope containing, as applicable:

* stable error code;
* message;
* status;
* request ID;
* retryable flag;
* validation details.

Do not expose internal stack traces.

## Pagination

Use the established cursor-based contract for collections where applicable.

## Idempotency

Use the established idempotency contract for operations that can safely be retried, especially upload finalization and other externally retried mutations.

---

# 7. CONFIGURATION FOUNDATION

Implement strongly validated configuration.

Create a configuration layer that handles:

* environment;
* database connection;
* Redis connection;
* authentication secrets/configuration;
* session configuration;
* storage provider configuration;
* upload limits;
* API configuration;
* observability configuration;
* application URLs;
* CORS configuration where applicable.

Configuration must be validated at startup.

Required configuration must fail startup clearly when absent or invalid.

Do not silently use insecure production defaults.

Never commit secrets.

Never hardcode credentials.

Public frontend configuration must not accidentally expose backend secrets.

---

# 8. DATABASE FOUNDATION

Implement PostgreSQL integration and migration support.

Create or update the database layer to support:

* connection management;
* migrations;
* transaction support;
* clean shutdown;
* connection pooling;
* test database configuration;
* structured database errors.

The implementation must provide a reliable migration workflow.

Do not use destructive schema synchronization as a substitute for versioned migrations in production.

Implement transaction boundaries around multi-record state changes where atomicity is required.

---

# 9. CORE DATABASE MODEL

Implement the transactional models required for this milestone.

At minimum include:

## User

Fields should cover:

* user ID;
* email or login identity reference;
* password credential metadata where applicable;
* account status;
* display/profile information;
* email verification state;
* createdAt;
* updatedAt;
* deletedAt where applicable.

Do not store plaintext passwords.

## Session

Include:

* session ID;
* user ID;
* refresh/session credential representation;
* device/session metadata as appropriate;
* createdAt;
* expiresAt;
* revokedAt;
* lastSeenAt where appropriate.

Store refresh credentials using secure representations rather than plaintext long-lived secrets where the chosen session design permits.

## Channel

Include:

* channel ID;
* owner user ID;
* handle;
* name;
* description;
* avatar reference;
* banner reference;
* status;
* createdAt;
* updatedAt;
* deletedAt where applicable.

Handles must have an appropriate uniqueness constraint.

## Video

Include the authoritative video metadata and lifecycle information required by the contract.

At minimum:

* video ID;
* channel ID;
* title;
* description;
* visibility;
* lifecycle status;
* publication timestamp where applicable;
* scheduled timestamp where applicable;
* duration where known;
* language where applicable;
* thumbnail reference where applicable;
* media asset reference;
* createdAt;
* updatedAt;
* deletedAt where applicable.

Keep system-controlled lifecycle state separate from creator-authored metadata.

## Upload Session

Include:

* upload session ID;
* video ID;
* owner;
* storage reference;
* expected size where applicable;
* received/completed state;
* expiration;
* creation/update timestamps;
* finalization state.

Do not store raw media bytes in PostgreSQL.

---

# 10. DATABASE CONSTRAINTS AND INDEXING

Implement appropriate constraints.

At minimum enforce:

* unique user identity requirements;
* unique channel handles;
* channel ownership;
* video-to-channel relationship;
* upload-session ownership;
* state integrity;
* non-null requirements;
* valid enum/state values.

Create indexes for common access paths including:

* user identity lookup;
* channel owner;
* channel handle;
* video by channel;
* video by visibility/state;
* video publication ordering;
* active upload sessions;
* session lookup/revocation.

Do not add indexes indiscriminately.

Each index must have a justified query or constraint purpose.

---

# 11. AUTHENTICATION FOUNDATION

Implement real authentication.

Support:

* account registration;
* login;
* logout;
* refresh/session renewal;
* email-verification boundary;
* password recovery boundary if included in the repository's authentication architecture;
* session revocation.

Use secure password hashing such as Argon2id.

Never store plaintext passwords.

Implement authentication using the project's established token/session contract.

The system must be able to distinguish:

* unauthenticated;
* authenticated;
* revoked;
* expired.

Authentication failures must use the canonical API error contract.

---

# 12. SESSION MANAGEMENT

Implement secure session handling.

Support:

* session creation;
* session listing where appropriate;
* session revocation;
* logout;
* refresh/renewal;
* expiry;
* invalidation following security-sensitive account events where appropriate.

Prevent refresh-token/session replay according to the chosen architecture.

Do not reveal session secrets through normal account APIs.

Do not log access tokens or refresh tokens.

Use secure hashing or equivalent protection for long-lived session credentials when applicable.

---

# 13. ACCOUNT MANAGEMENT

Implement account endpoints and domain behavior for:

* account retrieval;
* profile update;
* email verification state;
* password change;
* account deletion initiation/handling according to the current lifecycle design;
* session management.

Account mutation must require appropriate authentication.

Use optimistic concurrency or equivalent safeguards where simultaneous updates can create correctness problems.

Do not allow users to modify server-controlled security state through ordinary profile fields.

---

# 14. AUTHORIZATION FOUNDATION

Implement server-side authorization.

At minimum support:

* authenticated user;
* resource owner;
* channel owner;
* administrative privilege boundary hooks;
* privileged role checks required by the current modules.

Authorization must be performed in backend domain/application logic.

Do not rely on hidden frontend controls.

For a resource owned by a user or channel, verify ownership before mutation.

Return the canonical authorization error when access is denied.

Do not leak whether sensitive resources exist when the contract requires indistinguishable not-found/forbidden behavior.

---

# 15. USER PROFILE FOUNDATION

Implement the public/private user profile boundary needed by channels and account features.

Support profile fields appropriate to the current domain, such as:

* display name;
* profile image reference;
* locale;
* timezone;
* basic account metadata.

Do not expose:

* password hashes;
* session data;
* refresh credentials;
* sensitive recovery data;
* internal security metadata.

Separate public profile representation from private account representation.

---

# 16. CHANNEL MANAGEMENT

Implement channel creation and management.

Support:

* create channel;
* get channel;
* get public channel profile;
* update channel;
* update channel branding references;
* delete/deactivate channel according to the lifecycle contract;
* owner authorization.

Enforce:

* unique handle;
* ownership;
* valid naming constraints;
* input validation;
* appropriate length limits;
* safe text handling.

A user may have only the channel relationships allowed by the product rules established in the repository.

Do not invent multiple-channel rules if they conflict with the authoritative repository contract.

If the current implementation does not yet define the exact multiplicity rule, encode it as an explicit configuration/domain rule rather than making it silently inconsistent across endpoints.

---

# 17. CHANNEL PUBLICATION BOUNDARY

Public channel responses must return only data intended for public consumption.

Do not expose:

* private account data;
* internal moderation data;
* administrative metadata;
* secrets;
* storage credentials;
* internal object paths.

Channel visibility and lifecycle state must influence public responses.

Deleted/deactivated channels must have predictable behavior.

---

# 18. VIDEO CREATION

Implement creation of video metadata owned by a channel.

Support:

* create draft video;
* retrieve own video;
* retrieve public video metadata when allowed;
* update editable metadata;
* set visibility;
* delete video;
* publish when publication prerequisites are satisfied.

At minimum support metadata including:

* title;
* description;
* visibility;
* language;
* category or equivalent metadata;
* scheduling metadata where included;
* thumbnail reference where compatible.

Validate title and description lengths.

Reject invalid visibility transitions.

---

# 19. VIDEO OWNERSHIP

Every video must belong to exactly one canonical channel owner.

For every protected mutation:

1. authenticate the actor;
2. resolve the video;
3. verify channel ownership or appropriate privileged authorization;
4. validate lifecycle state;
5. execute mutation;
6. record resulting state;
7. emit required domain events where this milestone owns the producer.

Do not authorize a mutation merely because the client supplies the channel or video identifier.

Ownership must be derived from trusted persisted relationships.

---

# 20. VIDEO LIFECYCLE

Implement the video lifecycle states defined by the project contract.

At minimum distinguish:

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

Implement valid transition guards.

Examples:

* draft → uploading;
* uploading → uploaded;
* uploaded → processing;
* processing → ready;
* processing → failed;
* ready → scheduled;
* ready → published;
* scheduled → published;
* published → restricted;
* published → blocked;
* applicable states → deleted.

Do not allow clients to arbitrarily assign lifecycle states.

System transitions must be triggered by domain operations or processing events.

---

# 21. VIDEO VISIBILITY

Implement canonical visibility values such as:

* public;
* unlisted;
* private;
* restricted where applicable.

Visibility must influence:

* public API access;
* discovery eligibility;
* publication;
* playback authorization;
* future search indexing;
* future recommendation eligibility.

This milestone does not implement search or recommendations.

However, the video domain must publish sufficient state changes for later subsystems to consume.

---

# 22. VIDEO PUBLICATION RULES

Implement publication preconditions.

At minimum, a video must not become publicly published unless required prerequisites are satisfied.

The backend must distinguish:

* metadata exists;
* media upload completed;
* processing complete;
* video is publishable;
* video is published.

Do not permit a creator to set `published` solely through an arbitrary status field.

The publication operation must validate the current lifecycle state.

If media processing has not completed, publication must fail with a deterministic domain error or remain in an explicitly scheduled/pending state according to the established contract.

---

# 23. SCHEDULED PUBLICATION

Implement scheduled publication metadata and backend scheduling boundaries where included in this milestone.

Support:

* scheduled timestamp;
* validation that the timestamp is in the future when required;
* transition into scheduled state;
* transition to published at the appropriate time.

The scheduling mechanism may use the project's background job infrastructure.

Scheduling must be idempotent.

A video must not be published multiple times because a scheduling job is retried.

If the repository does not yet contain the complete job infrastructure, create only the scheduling integration contract and the minimum infrastructure required for this milestone. Do not implement unrelated background-job categories.

---

# 24. UPLOAD SESSION CONTROL PLANE

Implement the backend control plane for media uploads.

Support:

1. Create upload session.
2. Authorize upload.
3. Return secure upload instructions/reference.
4. Track upload state.
5. Finalize upload.
6. Validate that finalization belongs to the correct video and owner.
7. Transition video state.
8. Queue media processing.
9. Return processing state.

The backend should not proxy large media payloads unnecessarily.

Use the project's storage abstraction.

The API must not expose long-lived provider credentials to clients.

---

# 25. STORAGE ABSTRACTION

Create or use an abstraction for object storage.

The abstraction must support the operations required by this milestone:

* create upload target;
* resolve object reference;
* finalize/verify uploaded object;
* delete object when required;
* retrieve metadata;
* generate controlled upload authorization.

Do not scatter provider-specific storage SDK calls throughout domain logic.

Keep provider-specific code behind the storage boundary.

Do not hardcode bucket names, credentials, or cloud-specific secrets.

---

# 26. UPLOAD SECURITY

Protect upload operations against:

* unauthorized ownership;
* excessive file size;
* unsupported content type;
* expired upload sessions;
* upload-session reuse;
* cross-user access;
* object-path manipulation;
* arbitrary storage target selection.

The client must not be able to choose an arbitrary storage object path outside the authorized resource boundary.

Validate upload metadata server-side.

Do not trust the client to declare that a media file has been successfully uploaded.

The backend must verify the expected storage-side state according to the storage abstraction before finalization.

---

# 27. UPLOAD FINALIZATION

Implement idempotent upload finalization.

A finalization operation must:

1. authenticate the principal;
2. resolve the upload session;
3. verify ownership;
4. verify upload-session state;
5. verify object existence and required metadata;
6. transition the upload session;
7. transition the video into the appropriate processing state;
8. create or enqueue the media-processing job;
9. publish the appropriate domain event;
10. return the canonical resulting state.

Repeated finalization requests must not enqueue duplicate processing jobs.

Conflicting finalization attempts must return a deterministic conflict/domain error.

---

# 28. MEDIA PROCESSING JOB CONTRACT

This milestone does not implement transcoding workers.

It must, however, create the backend-side processing job contract required for later media infrastructure.

The job must carry enough information for a future worker to process the correct asset, including:

* job ID;
* video ID;
* media asset/upload reference;
* owner/channel context where required;
* input object reference;
* processing profile/version;
* correlation ID;
* idempotency key;
* createdAt.

Do not place the raw video bytes in the job payload.

Do not create a fake transcoding implementation.

---

# 29. DOMAIN EVENTS

This milestone is responsible for publishing the events owned by the implemented domains.

At minimum implement the authoritative producers for events such as:

* user.created;
* user.updated;
* session.revoked;
* channel.created;
* channel.updated;
* channel.deleted where applicable;
* video.created;
* video.upload.initiated;
* video.upload.completed;
* video.processing.started;
* video.processing.failed where this backend owns the state transition;
* video.published;
* video.unpublished where applicable;
* video.restricted;
* video.deleted.

Use the authoritative event envelope.

Every event must contain:

* event ID;
* event type;
* version;
* occurredAt;
* producer;
* correlation context where applicable;
* payload.

Consumers for unrelated future domains are out of scope.

---

# 30. EVENT DELIVERY

Use the repository's event infrastructure when present.

If event streaming has already been implemented, use the established transport and contracts.

If it has not, create the minimal reusable event-publishing abstraction needed by this milestone while preserving the architecture contract.

Do not build a complete event platform in this milestone.

Events must be published only after the corresponding transactional state is safely committed.

Use an outbox or equivalent reliability mechanism when required to avoid losing events between database commit and event publication.

Do not publish a business event that can later contradict committed state because of transaction ordering.

---

# 31. REDIS USAGE

Use Redis only for responsibilities that belong to this milestone.

Potential uses include:

* rate limiting;
* short-lived session/security state;
* ephemeral upload state where justified;
* idempotency state;
* short-lived cache where justified.

Every Redis key must:

* have a namespace;
* have a documented ownership;
* have an explicit TTL where appropriate;
* have defined failure behavior.

Redis must not become the authoritative store for users, channels, or videos.

If Redis becomes unavailable, the backend must fail safely according to each use case.

---

# 32. RATE LIMITING

Implement rate limiting for sensitive operations introduced by this milestone.

At minimum protect:

* registration;
* login;
* password/recovery operations;
* session refresh;
* channel creation;
* video creation;
* upload-session creation;
* upload finalization;
* privileged account mutations.

Use the project's canonical rate-limit contract.

Return the canonical rate-limit response, including retry metadata where defined.

Do not use one unlimited public mutation path.

---

# 33. INPUT VALIDATION

All incoming data must be validated at the API boundary.

Validate:

* IDs;
* emails;
* handles;
* text fields;
* enum values;
* visibility;
* timestamps;
* pagination;
* upload metadata;
* scheduling;
* request size;
* required relationships.

Do not rely on database constraints as the only validation layer.

Use shared validation schemas where appropriate.

Validation behavior must be consistent across endpoints.

---

# 34. SECURITY REQUIREMENTS

Implement security appropriate to the current scope.

At minimum:

* secure password hashing;
* secure session/token handling;
* server-side authorization;
* rate limiting;
* input validation;
* safe error responses;
* secret isolation;
* audit logging for sensitive account/security actions;
* secure upload authorization;
* ownership enforcement;
* no credential leakage;
* no sensitive logging.

Do not store or log:

* passwords;
* access tokens;
* refresh tokens;
* private signing keys;
* cloud credentials;
* raw authentication secrets.

---

# 35. AUDIT AND SECURITY EVENTS

Create appropriate audit records or security events for:

* account creation;
* password/security changes;
* session revocation where appropriate;
* channel ownership changes;
* sensitive video visibility changes;
* publication;
* deletion;
* administrative/security events within this milestone.

Audit records must identify:

* actor;
* action;
* target;
* timestamp;
* correlation/request ID where appropriate;
* result.

Do not place sensitive credential material in audit records.

---

# 36. OBSERVABILITY

Implement observability for the backend functionality in this milestone.

At minimum include:

* structured logging;
* request IDs;
* correlation IDs;
* traces;
* request duration metrics;
* error metrics;
* authentication failure metrics;
* database latency metrics;
* Redis operation metrics where appropriate;
* upload-session metrics;
* media-processing job enqueue metrics;
* video lifecycle transition metrics.

Create health checks covering:

* application process;
* database;
* required Redis dependency where health semantics require it.

Distinguish:

* liveness;
* readiness.

Do not expose sensitive dependency credentials in health responses.

---

# 37. ERROR HANDLING

Implement centralized error handling.

Map domain failures to stable API errors.

Handle at minimum:

* invalid input;
* unauthenticated;
* unauthorized;
* not found;
* conflict;
* expired resource;
* invalid lifecycle transition;
* rate limited;
* dependency unavailable;
* duplicate/idempotent request;
* internal error.

Never return raw ORM errors to clients.

Never expose stack traces in production API responses.

Include request identifiers for troubleshooting.

---

# 38. API SURFACE

Implement the API surface necessary for this milestone.

Representative endpoint families include:

## Authentication

* register;
* login;
* logout;
* refresh;
* session management.

## Account

* get current account;
* update profile;
* change password;
* delete/deactivate account according to the defined lifecycle;
* list/revoke sessions where supported.

## Channels

* create channel;
* get channel;
* update channel;
* delete/deactivate channel;
* get current user's owned channel.

## Videos

* create draft;
* get owned video;
* get public video metadata when accessible;
* update metadata;
* update visibility;
* schedule;
* publish;
* delete.

## Uploads

* create upload session;
* get upload status;
* finalize upload;
* cancel upload where applicable.

Use the project's canonical API conventions.

Do not add unrelated endpoint families.

---

# 39. API AUTHORIZATION MATRIX

Create or update an implementation-level authorization matrix covering the endpoints introduced by this milestone.

At minimum distinguish:

| Endpoint Family     | Anonymous | Authenticated User             | Channel Owner | Moderator/Admin |
| ------------------- | --------- | ------------------------------ | ------------- | --------------- |
| Public channel read | Allowed   | Allowed                        | Allowed       | Allowed         |
| Create channel      | No        | Allowed                        | Allowed       | Allowed         |
| Update own channel  | No        | Owner only                     | Allowed       | Privileged      |
| Create video        | No        | Allowed with channel ownership | Allowed       | Privileged      |
| Update video        | No        | Owner only                     | Allowed       | Privileged      |
| Publish video       | No        | Owner only                     | Allowed       | Privileged      |
| Create upload       | No        | Allowed with ownership         | Allowed       | Privileged      |
| Finalize upload     | No        | Owner only                     | Allowed       | Privileged      |
| View private video  | No        | Owner/authorized principal     | Owner         | Privileged      |
| Manage sessions     | No        | Own sessions                   | Own sessions  | Privileged      |

Refine permissions to match the exact implemented routes and domain rules.

---

# 40. DATABASE TRANSACTIONS AND CONCURRENCY

Implement explicit transaction boundaries for operations that require atomic state transitions.

At minimum consider transactions around:

* channel creation;
* video creation;
* publication;
* deletion;
* upload finalization;
* session revocation;
* security-sensitive account changes.

Protect against:

* duplicate requests;
* concurrent publication;
* concurrent deletion;
* simultaneous upload finalization;
* race conditions between state transitions.

Use row locks, optimistic concurrency, unique constraints, or other appropriate mechanisms where necessary.

Do not solve concurrency problems only in frontend code.

---

# 41. TESTING REQUIREMENTS

Create tests covering actual behavior.

## Unit Tests

Test:

* authentication services;
* password validation;
* authorization rules;
* channel ownership;
* video lifecycle transitions;
* visibility rules;
* upload lifecycle;
* idempotency behavior;
* error mapping.

## Integration Tests

Test:

* PostgreSQL persistence;
* migrations;
* transactions;
* Redis-backed behavior where used;
* session management;
* upload control plane;
* event publication;
* job creation.

## API Tests

Test:

* successful requests;
* validation failures;
* authentication failures;
* authorization failures;
* not-found behavior;
* conflict behavior;
* rate limits;
* pagination;
* lifecycle transitions.

## Security Tests

Test at minimum:

* password handling;
* unauthorized access;
* ownership bypass;
* session revocation;
* upload ownership;
* sensitive response-field exclusion;
* rate-limit enforcement.

## Concurrency Tests

Test scenarios such as:

* duplicate publication;
* duplicate upload finalization;
* concurrent session revocation;
* concurrent video mutation where applicable.

Do not inflate test counts with meaningless assertions.

---

# 42. API DOCUMENTATION

Generate or update OpenAPI documentation for all endpoints introduced by this milestone.

Document:

* request schemas;
* response schemas;
* authentication requirements;
* authorization requirements;
* status codes;
* error structures;
* pagination;
* idempotency;
* representative examples.

The OpenAPI contract must match the actual implementation.

Do not document endpoints that do not exist.

---

# 43. OPERATIONAL DOCUMENTATION

Document:

* local backend setup;
* required environment variables;
* database migration commands;
* test commands;
* seed/development data behavior if any;
* Redis requirements;
* storage configuration;
* observability;
* troubleshooting;
* common authentication/session failures;
* upload-control-plane troubleshooting.

Do not include real secrets.

Do not claim external cloud infrastructure has been provisioned.

---

# 44. FILE AND MODULE QUALITY

Organize code according to coherent backend boundaries.

Prefer a structure that clearly separates:

* controllers;
* DTOs;
* application services;
* domain logic;
* persistence;
* entities/models;
* infrastructure adapters;
* guards;
* authentication;
* authorization;
* configuration;
* shared contracts.

Do not create large controllers containing business logic.

Do not bury authorization in database queries without an explicit policy model.

Do not put provider-specific storage code inside domain entities.

Do not duplicate validation logic unnecessarily.

---

# 45. PERFORMANCE REQUIREMENTS

This milestone must remain efficient for substantial growth.

Avoid:

* N+1 queries;
* loading unbounded user/video collections;
* synchronous calls to future media-processing services;
* storing large media payloads in the database;
* repeated password/session lookups when safely cacheable;
* unbounded Redis keys;
* unbounded request bodies.

Paginate collection endpoints.

Index common queries.

Use connection pooling correctly.

Set timeouts for external operations.

Use background processing for work that does not belong in request latency.

---

# 46. PRIVACY REQUIREMENTS

Do not expose private account data through public APIs.

Protect:

* account credentials;
* session state;
* private videos;
* unlisted video access;
* internal moderation/security metadata.

Respect deletion state.

When account or video deletion occurs, ensure the current domain state prevents unauthorized access immediately even if derived systems have not yet processed cleanup.

Do not retain sensitive credentials in ordinary logs.

---

# 47. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement in this milestone:

* comments;
* comment replies;
* reactions/likes;
* subscriptions;
* playlists;
* search indexing;
* search queries;
* recommendations;
* creator analytics;
* notification delivery;
* moderation queues;
* administrator dashboards;
* live-stream media ingest;
* transcoding workers;
* CDN infrastructure;
* payment processing;
* advertising systems;
* mobile applications;
* frontend UI;
* full production Kubernetes infrastructure.

You may create the contracts, interfaces, and event producers required for later milestones where this prompt explicitly requires them.

Do not implement future behavior merely because its event or contract appears in this prompt.

---

# 48. VALIDATION REQUIREMENTS

Before completion, validate:

## Backend Validation

* application starts successfully;
* configuration validation works;
* migrations execute successfully;
* database constraints are enforced;
* required modules load correctly.

## Authentication Validation

* registration works;
* login works;
* session creation works;
* refresh works;
* logout/revocation works;
* expired/revoked sessions fail correctly.

## Authorization Validation

* unauthorized users cannot mutate protected resources;
* channel ownership is enforced;
* video ownership is enforced;
* private content is protected.

## Video Validation

* video creation works;
* lifecycle rules are enforced;
* visibility rules are enforced;
* publication prerequisites are enforced;
* deletion behavior is correct.

## Upload Validation

* upload sessions are authorized;
* session ownership is enforced;
* expired sessions fail;
* upload finalization is idempotent;
* duplicate processing jobs are prevented;
* processing state transitions are correct.

## Contract Validation

Verify consistency of:

* IDs;
* timestamps;
* errors;
* state enums;
* event envelopes;
* queue envelopes;
* configuration names;
* authorization semantics.

## Observability Validation

Confirm that:

* request IDs exist;
* structured logs work;
* critical failures emit metrics;
* health endpoints reflect dependency state appropriately;
* no secrets appear in telemetry.

---

# 49. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. The backend application foundation is functional.
3. Configuration is validated.
4. Database migrations are functional.
5. PostgreSQL integration is functional.
6. Authentication is implemented.
7. Session management is implemented.
8. Account management is implemented.
9. Authorization is enforced server-side.
10. User profile handling is implemented.
11. Channel creation and management are implemented.
12. Channel ownership is enforced.
13. Video metadata management is implemented.
14. Video ownership is enforced.
15. Video lifecycle transitions are implemented.
16. Video visibility rules are implemented.
17. Video publication rules are implemented.
18. Scheduled publication behavior required by this milestone is implemented.
19. Upload-session control is implemented.
20. Storage integration is abstracted and secured.
21. Upload finalization is implemented and idempotent.
22. Media-processing job creation is implemented.
23. Required domain events are implemented.
24. Rate limiting is implemented for relevant sensitive operations.
25. Centralized validation is implemented.
26. Centralized error handling is implemented.
27. Observability is implemented.
28. Security protections are implemented.
29. Database concurrency requirements are addressed.
30. API documentation is updated.
31. Operational documentation is updated.
32. Unit tests are present and meaningful.
33. Integration tests are present and meaningful.
34. API tests are present and meaningful.
35. Security tests are present and meaningful.
36. Relevant concurrency tests are present.
37. No fake implementation remains inside this milestone's scope.
38. No placeholder/TODO/FIXME gap intentionally substitutes for required functionality.
39. No hardcoded secrets exist.
40. Known limitations are documented honestly.

---

# 50. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every newly created file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Backend Modules

List implemented modules and their responsibilities.

## Database Changes

List:

* models;
* migrations;
* indexes;
* constraints.

## API Changes

List:

* endpoints;
* request/response contracts;
* authorization rules.

## Authentication and Security

Summarize implemented controls.

## Video and Upload

Summarize:

* lifecycle;
* visibility;
* upload session;
* finalization;
* processing-job integration.

## Events and Jobs

List events and jobs implemented by this milestone.

## Tests

List:

* tests created;
* test suites executed;
* validation performed.

## Documentation

List documentation created or updated.

## Known Limitations

Identify only functionality intentionally deferred to later milestones.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim external cloud resources or third-party systems were provisioned unless that actually occurred.

# 51. FINAL EXECUTION RULE

Implement only the backend foundation, identity, accounts, channels, video metadata/lifecycle, upload-control-plane, and supporting functionality defined in this prompt.

Do not implement unrelated future backend domains.

Do not redesign the architecture arbitrarily.

Do not invent incompatible API or data contracts.

Do not depend on another AI prompt.

Do not fabricate repository state.

Do not use fake persistence or fake authentication.

Do not replace required implementation with placeholders or pseudo-code.

Produce real, tested, observable, secure backend functionality within this milestone's scope.
