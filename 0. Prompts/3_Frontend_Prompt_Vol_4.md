# YouTube-Style Video Platform — Frontend Prompt — Volume 4

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web comments, discussions, viewer interactions, moderation-facing controls, and community engagement experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

* comments;
* threaded replies;
* comment reactions;
* comment creation/editing/deletion;
* comment sorting and pagination;
* viewer blocking interactions;
* reporting;
* moderation-aware comment states;
* deleted and unavailable content states;
* comment composer;
* interaction feedback;
* optimistic mutation handling where safe;
* accessibility;
* responsive behavior;
* analytics;
* testing;
* documentation.

Do not implement unrelated frontend domains.

Do not implement backend moderation, comment persistence, abuse detection, or community-ranking infrastructure.

Do not fabricate backend behavior.

---

# 2. Project Context

The product is a production-grade YouTube-style video platform supporting:

* long-form video;
* short-form video;
* channels;
* subscriptions;
* comments;
* threaded replies;
* reactions;
* playlists;
* watch history;
* search;
* personalized discovery;
* notifications;
* creator analytics;
* live streaming;
* moderation;
* administration;
* monetization-capable architecture;
* web and mobile clients.

The web technology direction is:

* TypeScript;
* React;
* Next.js App Router;
* responsive web;
* typed API clients;
* production state management;
* server/client state separation;
* accessibility;
* observability;
* automated testing.

Comments are high-volume user-generated content and must be treated as untrusted, mutable, privacy-sensitive data.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

* a previous AI response;
* another Claude conversation;
* another frontend prompt;
* undocumented backend behavior;
* hidden generated files;
* hidden architecture decisions.

If a repository is available, inspect it before modifying it.

If portable project contracts are available, use them as authoritative.

If the repository already contains compatible comment infrastructure, preserve and extend it rather than duplicating it.

Do not assume that every moderation or community feature described in the complete product has already been implemented.

---

# 4. Primary Objective

Implement the production web experience for viewer discussion and comment interaction.

The completed scope must allow an eligible viewer to:

1. read comments;
2. load additional comments;
3. sort comments using supported ordering;
4. create a comment;
5. edit their own comment;
6. delete their own comment;
7. reply to a comment;
8. expand/collapse replies;
9. react to comments;
10. remove/change a reaction;
11. report a comment;
12. block a user where the project contract supports viewer blocking;
13. see their own comment state;
14. handle deleted comments;
15. handle moderated or unavailable comments;
16. recover from mutation failures;
17. use the composer accessibly;
18. navigate comments efficiently on mobile and desktop;
19. receive correct analytics/telemetry;
20. preserve privacy and security boundaries.

---

# 5. Explicit Scope

Implement:

* comment section;
* comment list;
* comment pagination;
* comment sorting;
* comment composer;
* reply composer;
* edit flow;
* delete flow;
* comment reactions;
* reply expansion;
* comment loading states;
* comment empty states;
* comment error states;
* moderation-aware UI states;
* report flow;
* user-blocking UI integration where supported;
* optimistic interaction handling where safe;
* authenticated/anonymous behavior;
* comment telemetry;
* accessibility;
* responsive behavior;
* caching/state management;
* automated tests;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* backend comment persistence;
* comment ranking algorithms;
* abuse-detection models;
* toxicity classification;
* spam-detection services;
* moderation queues;
* moderator dashboards;
* administrative enforcement systems;
* notification backend;
* search backend;
* creator studio;
* mobile applications;
* live chat;
* payment or monetization systems;
* recommendation ranking;
* backend API redesign.

Use the established API and domain contracts.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository;
2. identify the web application;
3. inspect existing watch-page components;
4. inspect video/detail components;
5. inspect authentication/session state;
6. inspect API-client conventions;
7. inspect error normalization;
8. inspect existing modal/dialog primitives;
9. inspect shared form/input components;
10. inspect existing analytics;
11. inspect testing infrastructure;
12. inspect existing comment-related code if present.

Reuse compatible primitives.

Do not introduce a new component framework or state-management system unnecessarily.

---

# 8. Comment Domain Contract

Consume the project's canonical comment contract.

A conceptual comment representation may include:

```text
commentId
videoId
author
authorId
authorAvatar
authorChannel
authorVerificationState
text
createdAt
updatedAt
isEdited
likeCount
viewerReaction
replyCount
viewerPermissions
moderationState
visibilityState
```

The actual field names must follow the authoritative project contract.

Do not create a competing comment entity.

Do not assume every field is always present.

---

# 9. Comment Visibility States

Support the states defined by the backend contract.

Examples may include:

```text
visible
deleted
removed
hidden
restricted
pending
unavailable
blocked
```

Only implement states actually defined by the project.

Do not expose internal moderation terminology directly to users when a safer product-facing message is appropriate.

The UI must distinguish:

* deleted by author;
* removed by moderation;
* unavailable;
* inaccessible because of viewer permissions;

when the backend provides enough information to do so.

---

# 10. Comment Section Layout

Implement a reusable comment-section architecture.

A recommended conceptual structure is:

```text
CommentSection
  ├── CommentHeader
  ├── CommentComposer
  ├── CommentSortControl
  ├── CommentList
  │   └── CommentThread
  │       ├── CommentItem
  │       ├── CommentActions
  │       └── ReplyList
  └── CommentPagination
```

The exact repository structure may vary.

Maintain clear separation between:

* data loading;
* state management;
* rendering;
* mutations;
* analytics.

---

# 11. Comment Loading

When the watch page loads:

* load comments according to the established API contract;
* preserve the current video ID as part of the request key;
* display loading state;
* handle empty state;
* handle failures.

Do not block video playback merely because comments are loading.

Comment loading should be independently recoverable.

---

# 12. Comment Pagination

Support the backend's pagination model.

Prefer cursor pagination when provided.

Support:

* initial page;
* next page;
* loading-more state;
* end of list;
* retry after failure;
* duplicate prevention.

Do not request the same cursor concurrently.

Do not append results from the wrong video.

Do not lose existing comments because one subsequent page failed.

---

# 13. Comment Sorting

Implement comment ordering options supported by the backend.

Potential examples include:

* top comments;
* newest comments.

Only expose sorting modes that are part of the actual project contract.

When the sort order changes:

* reset pagination appropriately;
* invalidate incompatible cached pages;
* preserve the current video;
* avoid mixing result sets from different sort modes.

---

# 14. Comment Composer

Implement the primary comment composer.

Support:

* authenticated viewer;
* unauthenticated state;
* text entry;
* validation;
* character limits from backend/product configuration;
* submit;
* cancel where appropriate;
* loading;
* success;
* failure.

The composer must not allow empty submissions after normalization.

Do not enforce a client-side maximum that conflicts with the canonical backend limit.

Where the backend exposes a length limit, use that contract.

---

# 15. Comment Text Handling

Comments are untrusted user-generated content.

The frontend must:

* render user text safely;
* avoid unsafe HTML injection;
* avoid executing embedded markup;
* safely display URLs if the product explicitly supports link recognition;
* preserve normal user-entered text and line breaks as required.

Do not render comment text using unsafe HTML APIs merely to support formatting unless the project has an explicit sanitized rich-text contract.

---

# 16. Comment Creation

Submitting a comment must:

1. validate the input;
2. submit through the canonical API;
3. handle loading state;
4. handle success;
5. reconcile returned server data;
6. handle failure;
7. avoid duplicate submissions.

The returned server representation is authoritative.

Do not manufacture IDs or timestamps for production state when the backend provides them.

---

# 17. Safe Optimistic Creation

An optimistic comment can be used only if rollback is correctly implemented.

If optimistic creation is used:

* assign an explicit temporary client state;
* never pretend the temporary ID is the authoritative server ID;
* prevent duplicate submission;
* replace temporary content with the server response after success;
* remove/rollback the temporary item after failure.

Do not leave failed optimistic comments visible as though they were published.

---

# 18. Reply Architecture

Support threaded replies according to the backend contract.

A reply must remain associated with:

* parent comment;
* video ID;
* author;
* canonical reply ID.

Support:

* reply count;
* expand replies;
* collapse replies;
* pagination inside large reply sets;
* reply loading;
* reply errors.

Do not create unlimited nested levels if the backend contract only supports one reply level.

---

# 19. Reply Loading

Replies should be loaded independently from top-level comments where appropriate.

Support:

* loading on expansion;
* empty reply state;
* pagination;
* retry;
* caching;
* collapse.

Avoid downloading thousands of replies for every visible comment.

---

# 20. Reply Composer

A reply composer must:

* identify the parent comment;
* preserve the target parent ID;
* support authentication requirements;
* validate content;
* submit through the canonical API;
* handle success/failure;
* close or reset appropriately after success.

Do not allow rapid interactions to submit a reply to the wrong parent.

---

# 21. Edit Comments

Users may edit comments they own when the backend contract permits it.

Support:

* edit control only when authorized;
* transition into editing mode;
* current text;
* validation;
* save;
* cancel;
* loading;
* server reconciliation;
* failure rollback.

Do not expose an edit control solely because the current client believes the viewer owns the comment.

Use backend-provided permissions when available.

---

# 22. Delete Comments

Support author deletion where permitted.

Before destructive actions, use the established confirmation interaction if the product requires one.

After successful deletion:

* reconcile using the server response;
* update appropriate reply/comment counts if the response provides authoritative values;
* render the proper deleted state.

Do not permanently remove related reply structure from local state unless the backend contract requires that representation.

---

# 23. Comment Reactions

Implement supported comment reactions.

Support:

* no reaction;
* active reaction;
* removing a reaction;
* changing reaction;
* loading;
* failure.

The current viewer's reaction state is distinct from aggregate counts.

Do not assume counts increment successfully merely because the mutation request was sent.

---

# 24. Reaction Mutation Behavior

For optimistic reactions:

* update the local UI immediately only when the operation can be safely rolled back;
* preserve previous reaction state;
* preserve previous count;
* restore on failure;
* reconcile with server response after success.

Rapid repeated clicks must not create race conditions.

Requests must not result in a stale response restoring an older reaction state.

---

# 25. Comment Action Menu

Implement an accessible action menu supporting actions permitted by viewer state and comment state.

Possible actions include:

* reply;
* edit;
* delete;
* react;
* report;
* block user;
* other project-defined actions.

Do not display unauthorized controls simply because the component exists.

Actions must be driven by explicit permissions or policy data.

---

# 26. Reporting

Implement a frontend reporting flow for comments when supported.

Support:

* report entry;
* reason selection;
* validation;
* submission;
* loading;
* success;
* failure;
* close/cancel.

Use the canonical moderation/report contract.

Do not implement moderation decisions.

Do not expose internal reviewer data.

---

# 27. Blocking Users

Where the project supports viewer-level blocking, integrate the blocking UI.

After a successful block:

* update affected visible comment state according to the product contract;
* do not silently mutate unrelated users;
* invalidate relevant cached content if required;
* present clear feedback.

Do not assume that blocking a user automatically removes all of their content unless the backend contract explicitly defines that behavior.

---

# 28. Moderation-Aware Comments

The frontend must correctly render server-provided moderation states.

Examples:

* comment removed;
* comment under review;
* comment hidden from this viewer;
* comment unavailable;
* comment restricted.

Do not attempt to infer moderation state from missing data.

Do not create a client-side moderation engine.

---

# 29. Viewer Permissions

Comment controls must respect explicit viewer permissions.

Potential permissions include:

```text
canComment
canReply
canEdit
canDelete
canReact
canReport
canBlock
```

Use the canonical authorization representation supplied by the API.

Client-side permissions are a UI optimization only.

The backend remains authoritative.

---

# 30. Anonymous Viewer Behavior

Anonymous users may read public comments unless the product policy says otherwise.

For anonymous viewers:

* allow public comment browsing;
* require authentication for comment creation if required;
* require authentication for reactions if required;
* require authentication for reports where required;
* provide appropriate sign-in entry points.

Do not redirect the entire watch page to authentication merely because a user tries to comment.

---

# 31. Comment Count

If the watch page displays a comment count:

* prefer authoritative server-provided data;
* update it only from confirmed mutation results where possible;
* avoid blindly incrementing/decrementing based on UI intent.

Do not claim exact consistency if the underlying system is eventually consistent.

---

# 32. Cache and State Management

Use the project's established server-state system.

Cache keys must include:

* video ID;
* comment sort;
* pagination cursor where appropriate;
* viewer-sensitive context where the response varies by viewer.

Replies must include:

* parent comment ID;
* video ID;
* pagination state.

Do not share private viewer-specific comment state between users.

---

# 33. Cache Invalidation

After mutations, invalidate or update:

* relevant comment queries;
* affected reply queries;
* viewer reaction state;
* comment counts;
* moderation state;
* block-related views where required.

Avoid invalidating the entire application cache after a single comment reaction.

Use the smallest useful invalidation scope.

---

# 34. Concurrent Mutation Safety

Protect against:

```text
Edit comment
Delete comment
React to comment
Report comment
```

being triggered in conflicting combinations.

The UI should serialize or disable incompatible operations where appropriate.

Do not allow an outdated mutation response to overwrite a newer state.

---

# 35. Pagination and Mutation Reconciliation

Consider the case:

1. page 1 loaded;
2. page 2 loaded;
3. user creates a comment;
4. user edits another comment;
5. page 3 is requested.

The implementation must avoid:

* duplicate items;
* misplaced temporary comments;
* deleted items reappearing;
* stale page results overwriting confirmed mutations.

Where necessary, use stable IDs and query invalidation/revalidation.

---

# 36. Loading States

Implement clear states for:

* comments loading;
* replies loading;
* comment submission;
* reply submission;
* edit;
* delete;
* reaction;
* report;
* block;
* pagination.

Avoid replacing the entire comment tree with a spinner for a mutation affecting one item.

Prefer localized loading indicators.

---

# 37. Error States

Every mutation must distinguish between:

* validation failure;
* authorization failure;
* rate limit;
* network failure;
* temporary server failure;
* moderation/policy restriction;
* deleted/unavailable comment.

User-facing messages must remain understandable.

Do not expose raw server stack traces.

---

# 38. Retry Behavior

Retries must be deliberate.

For idempotent reads:

* retry transient network failures where appropriate.

For mutations:

* do not blindly retry non-idempotent requests.

If the backend supports idempotency keys for comment creation or mutations, integrate them according to the canonical contract.

Never create duplicate comments because a network timeout caused the user to retry.

---

# 39. Rate Limits and Abuse Prevention

The frontend must cooperate with server-side anti-abuse mechanisms.

Handle:

* comment submission rate limits;
* reaction rate limits;
* report limits;
* block limitations.

When the API returns a rate-limit response:

* show a useful user-facing message;
* avoid repeated automatic retries;
* respect server-provided retry metadata where appropriate.

Do not attempt to bypass server rate limits.

---

# 40. Comment Ordering and Live Updates

Do not assume comments remain in a static order after mutations.

After:

* new comment creation;
* deletion;
* editing;
* moderation changes;

reconcile with server state.

Do not artificially reorder comments unless the product contract explicitly requires it.

If real-time comment updates are supported later by project architecture, the component boundaries should permit their integration without replacing the entire comment system.

---

# 41. Accessibility

The comment system must be accessible.

Implement:

* semantic article/list structures where appropriate;
* accessible comment author labels;
* accessible reaction controls;
* accessible action menus;
* accessible dialogs;
* keyboard navigation;
* visible focus;
* screen-reader feedback;
* accessible composer validation;
* accessible reply nesting;
* accessible loading/error announcements.

Do not rely on color alone to indicate reaction or moderation state.

---

# 42. Focus Management

After opening:

* reply composer;
* edit mode;
* report dialog;
* confirmation dialog;

focus must move predictably.

After closing a modal or popup, return focus to the invoking control where appropriate.

When a comment is deleted, focus must not disappear into a removed DOM subtree.

---

# 43. Mobile Behavior

On small screens:

* comment actions must remain touch-friendly;
* action menus must fit the viewport;
* reply indentation must remain readable;
* long comments must wrap correctly;
* composers must accommodate mobile keyboards;
* dialogs must remain usable;
* nested replies must not create excessive horizontal indentation.

Do not create an unrelated separate mobile comment implementation.

Use responsive behavior on the shared components.

---

# 44. Desktop Behavior

On larger screens:

* comments should remain readable;
* reply nesting should be visually clear;
* action controls should not create excessive horizontal noise;
* long threads should remain navigable.

Do not let the comment section dominate the entire watch page to the detriment of primary video content.

---

# 45. Comment Composer Performance

Avoid expensive rerenders while typing.

Do not place the entire comment tree behind a form state update that causes every comment to rerender for each keystroke.

Use localized state and memoization where it provides measurable value.

Do not prematurely introduce a global state system for simple composer state.

---

# 46. Accessibility of Rich Interaction

Menus, dialogs, and expandable reply sections must correctly implement appropriate accessibility states.

For example:

```text
aria-expanded
aria-controls
aria-haspopup
aria-selected
aria-disabled
```

Use semantics appropriate to the actual control.

Do not add ARIA attributes without matching behavior.

---

# 47. Analytics and Telemetry

Instrument behavior using the project's analytics contract.

Relevant events may include:

```text
comment_section_viewed
comment_loaded
comment_created
comment_creation_failed
comment_reply_opened
comment_reply_created
comment_edited
comment_deleted
comment_reaction_changed
comment_report_opened
comment_report_submitted
comment_block_submitted
comment_pagination_loaded
comment_sort_changed
```

Use canonical event names when available.

Do not include raw comment text in analytics unless explicitly authorized by the privacy architecture.

Do not transmit private user identifiers unnecessarily.

---

# 48. Analytics Duplication Prevention

Ensure events are not duplicated because of:

* React Strict Mode;
* component remounts;
* retries;
* optimistic updates;
* pagination revalidation.

Separate:

* user action;
* server mutation result;
* impression/visibility events.

Do not interpret every render as user behavior.

---

# 49. Privacy

Comments and reactions are user-generated social data.

Protect:

* private account information;
* moderation metadata;
* internal enforcement reasons;
* report details;
* viewer identity;
* private comment history.

Do not place moderation information into analytics unless explicitly required and authorized.

Do not log raw comment content into application logs.

---

# 50. Security

The implementation must:

* safely render untrusted comment content;
* validate links before navigation;
* avoid open redirects;
* avoid unsafe HTML;
* use secure API integration;
* avoid exposing secrets;
* respect server authorization;
* avoid leaking hidden comments;
* avoid logging private report details.

The frontend must never treat client-side permissions as authoritative security.

---

# 51. Error Isolation

The failure of one comment must not break the entire discussion.

For example:

```text
Comment A reaction fails
Comment B remains usable
Reply thread remains usable
Video player remains usable
```

Likewise:

```text
Comments fail to load
Watch player remains functional
Video metadata remains functional
```

Use localized error boundaries and mutation states.

---

# 52. Navigation and Deep Linking

Where product requirements support direct access to a comment or reply, provide a stable mechanism using canonical IDs.

Do not expose internal database identifiers if the project uses a public identifier abstraction.

If comment deep linking is part of the product contract:

* scroll to the target comment;
* highlight it temporarily where appropriate;
* expand the necessary reply tree;
* handle unavailable/deleted comments gracefully.

Do not invent a deep-link mechanism if it is not part of the canonical product contract.

---

# 53. Component Boundaries

Maintain clear conceptual boundaries:

```text
comments/
  data
  hooks
  types
  components
  composer
  thread
  replies
  reactions
  moderation
  analytics
  tests
```

The exact file organization can follow the repository.

Avoid placing all comment functionality into a single large component.

Avoid circular dependencies.

Keep API concerns separate from presentation.

---

# 54. State Ownership

Separate:

### Server state

* comment pages;
* reply pages;
* moderation state;
* viewer permissions;
* reaction state;
* authoritative counts.

### Local UI state

* editing;
* composer text;
* open menus;
* expanded replies;
* dialog visibility;
* temporary validation messages.

### Persistent state

Only preferences appropriate for browser persistence.

Do not persist comment content automatically unless the product explicitly requires draft persistence.

---

# 55. Draft Handling

If comment drafts are persisted:

* use a clearly defined storage mechanism;
* scope drafts to the correct user and video;
* prevent data leakage;
* expire stale drafts appropriately.

If draft persistence is not part of the product contract, keep composer content local to the current session/page.

Do not silently store private comment drafts indefinitely.

---

# 56. Authentication Expiration

When an authenticated viewer's session expires while interacting with comments:

* handle the authorization failure;
* preserve the user's typed comment where safe;
* avoid clearing meaningful local input unnecessarily;
* route through the established authentication-refresh mechanism;
* avoid infinite retry loops.

A public comment-reading experience should continue where possible.

---

# 57. API Error Normalization

Use the project's standard error model.

At minimum the frontend should be able to distinguish:

```text
validation
authentication
authorization
notFound
conflict
rateLimited
temporarilyUnavailable
network
unknown
```

Map those states to meaningful UI responses.

Do not expose internal error codes directly unless they are intended for user-facing product behavior.

---

# 58. Testing Strategy

Implement tests for actual behavior.

### Unit tests

Cover:

* comment state transitions;
* permission logic;
* comment sorting serialization;
* pagination;
* reply expansion state;
* cache-key generation;
* mutation reconciliation;
* reaction rollback;
* safe text/link handling;
* stale-response protection;
* analytics event creation.

### Component tests

Cover:

* comment item;
* comment composer;
* reply composer;
* edit mode;
* delete confirmation;
* reaction control;
* action menu;
* report flow;
* moderation states;
* empty state;
* pagination;
* sorting.

### Integration tests

Cover:

* loading comments;
* loading replies;
* creating a comment;
* replying;
* editing;
* deleting;
* reacting;
* reporting;
* blocking;
* pagination;
* failure recovery;
* authentication transitions.

### End-to-end tests

At minimum:

1. open a video with comments;
2. load comment list;
3. expand replies;
4. create a comment as an authenticated viewer;
5. edit that comment;
6. react to a comment;
7. reply to a comment;
8. delete an owned comment;
9. report a comment where permitted;
10. exercise comment pagination;
11. change comment sorting;
12. verify anonymous-viewer behavior;
13. verify authorization-sensitive controls;
14. verify keyboard accessibility;
15. verify a comment failure does not break video playback.

Tests must validate real application behavior through appropriate boundaries.

---

# 59. Browser Compatibility

Validate across the project's supported browser matrix.

Pay particular attention to:

* mobile keyboard behavior;
* dialog behavior;
* focus management;
* pointer/touch interaction;
* scrolling;
* nested reply layouts.

Do not rely on browser-specific APIs without feature detection or project-approved compatibility handling.

---

# 60. Performance

The comment section can become very large.

Optimize for:

* incremental loading;
* localized rerenders;
* efficient list updates;
* stable keys;
* avoiding unnecessary recalculation;
* controlled mutation invalidation.

Consider virtualization only if actual project requirements justify it.

Do not virtualize the comment list in a way that breaks:

* accessibility;
* deep linking;
* browser find;
* focus;
* reply expansion;

without solving those behaviors.

---

# 61. Long Comment and Large Thread Handling

Support:

* very long comment text;
* many comments;
* many replies;
* long usernames/channel names;
* deleted comments;
* rapidly changing local state.

Prevent:

* horizontal overflow;
* DOM explosions caused by eagerly loading all replies;
* unbounded client-side memory growth.

---

# 62. Contract Compatibility

Remain compatible with project-wide contracts for:

```text
Canonical IDs
Canonical timestamps
API envelopes
API error model
Authentication
Authorization
Video entity
Comment entity
Reply entity
Reaction model
Report model
Block model
Moderation state
Pagination
Analytics events
Privacy rules
```

Use exact concrete contracts when project artifacts are supplied.

Do not silently redefine comment semantics.

---

# 63. No Fake Comment System

Do not create:

* static comments;
* fabricated authors;
* fake reactions;
* fake reply counts;
* fake report success;
* simulated persistence;
* hardcoded permissions.

Mocks are acceptable only inside automated tests.

The production application must use actual integration boundaries.

---

# 64. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* fake submit buttons;
* nonfunctional menus;
* empty mutation handlers;
* placeholder moderation states;
* incomplete reply pagination;
* incomplete error handling;
* “implement later” sections.

Everything in the current scope must be implemented.

---

# 65. Documentation

Update documentation for:

* comment architecture;
* comment API integration;
* reply loading;
* pagination;
* mutation handling;
* optimistic updates;
* moderation states;
* reporting;
* blocking;
* accessibility;
* telemetry;
* privacy behavior;
* testing strategy.

Documentation must reflect actual implementation.

---

# 66. Validation

Before completion, validate:

* TypeScript compilation;
* linting;
* unit tests;
* component tests;
* integration tests;
* end-to-end tests where available;
* production build;
* comment loading;
* comment creation;
* reply creation;
* editing;
* deletion;
* reactions;
* report flow;
* block flow where supported;
* pagination;
* sorting;
* authorization;
* responsive behavior;
* accessibility-critical interactions;
* stale-request protection;
* failure isolation.

Fix issues found within this scope.

Do not merely report failures as completion.

---

# 67. Definition of Done

This prompt is complete only when:

* the comment section is implemented;
* comments load from real contracts;
* pagination works;
* sorting works where supported;
* the comment composer works;
* comment creation works;
* reply creation works;
* replies expand/collapse correctly;
* edit works where authorized;
* delete works where authorized;
* comment reactions work;
* optimistic mutations roll back correctly where used;
* report flow works where supported;
* block flow works where supported;
* moderation-aware states render correctly;
* authorization-sensitive controls are correct;
* anonymous behavior is correct;
* comment errors are recoverable;
* mutation races are prevented;
* stale responses cannot overwrite newer state;
* cache invalidation is scoped correctly;
* accessibility requirements are implemented;
* mobile and desktop layouts work;
* privacy/security requirements are respected;
* analytics are implemented without prohibited sensitive data;
* tests cover the required behavior;
* documentation is updated;
* no fake production behavior remains;
* no current-scope placeholders remain;
* validation passes.

---

# 68. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize the comments, replies, reactions, moderation-facing interactions, and viewer controls completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List the comment, reply, reaction, report, block, pagination, authorization, and analytics contracts consumed.

### State and Caching

Summarize comment/reply cache strategy, mutation reconciliation, optimistic behavior, and stale-request protection.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, build validation, and relevant runtime validation.

### Integration Notes

Identify material backend-contract assumptions, compatibility concerns, or external dependencies.

### Out of Scope

Confirm that backend moderation, ranking, abuse detection, mobile, live chat, creator studio, search infrastructure, and monetization were not improperly implemented.

---

# 69. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe the comment system.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real contracts.

Do not fabricate backend behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web comments and viewer community interaction experience** that can be integrated with the independently generated backend and other project components through explicit contracts.
