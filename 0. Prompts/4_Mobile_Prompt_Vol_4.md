# YouTube-Style Video Platform — Mobile Prompt — Volume 4

## 1. Prompt Identity

You are the senior React Native/mobile engineer responsible for implementing the **native comments, threaded replies, viewer reactions, community interactions, reporting, and user-blocking experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone for iOS and Android.

Your responsibility is to deliver the native social-interaction experience integrated with the platform's canonical video, comment, authentication, authorization, moderation, and analytics contracts.

The implementation includes:

- comment viewing;
- comment pagination;
- comment sorting;
- comment creation;
- threaded replies;
- comment editing and deletion;
- comment reactions;
- video-reaction integration;
- subscription controls where required by the shared engagement experience;
- reporting;
- viewer blocking where supported;
- moderation-aware content states;
- accessible native dialogs and bottom sheets;
- optimistic mutation handling where safe;
- loading, empty, and failure states;
- privacy and security;
- automated testing;
- documentation.

Do not implement unrelated mobile domains.

Do not implement backend comment persistence, moderation engines, or abuse-detection services.

Do not fabricate comments, authors, reaction counts, permissions, or mutation results.

---

# 2. Project Context

The product is a production-grade YouTube-style video platform supporting:

- long-form video;
- short-form video;
- channels;
- subscriptions;
- comments and replies;
- reactions;
- playlists;
- watch history;
- search and discovery;
- notifications;
- creator studio and analytics;
- live streaming;
- moderation;
- paid memberships and monetization-capable functionality;
- web and native mobile clients.

The mobile technology direction is:

- React Native;
- TypeScript;
- iOS and Android;
- the existing navigation and state-management libraries;
- typed API clients;
- secure authentication/session integration;
- native accessibility;
- production-quality testing;
- privacy-conscious analytics.

The mobile interaction model must be appropriate for native devices, including touch input, keyboard behavior, focus management, modal presentation, text scaling, and network interruptions.

The mobile application must use the same canonical comment, video, channel, reaction, and identity contracts as the wider platform.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- previous mobile prompts;
- hidden architecture decisions;
- undocumented APIs;
- generated files unavailable in the current environment;
- a repository shared with another AI conversation.

If a repository is available, inspect it before modifying it.

If portable architecture, API, authentication, comment, reaction, moderation, or analytics contracts are supplied, use them as authoritative.

If the repository already contains compatible comment or engagement infrastructure, preserve and extend it.

If an expected backend capability is unavailable, define the integration boundary and document the missing dependency. Do not replace real production functionality with fake data.

---

# 4. Primary Objective

Implement a production-quality mobile engagement experience that allows viewers to:

1. read comments associated with a video;
2. load additional comments;
3. sort comments using supported options;
4. create comments;
5. read threaded replies;
6. create replies;
7. edit their own comments where permitted;
8. delete their own comments where permitted;
9. react to comments;
10. interact with video reactions through compatible shared components;
11. report comments or users where supported;
12. block users where supported;
13. understand deleted, removed, or restricted content states;
14. recover from network and mutation failures;
15. use the comment interface with native accessibility tools;
16. retain appropriate draft text during recoverable interruptions;
17. avoid duplicate mutations;
18. maintain privacy and account isolation.

---

# 5. Explicit Scope

Implement:

- native comment section;
- comment list;
- comment sorting;
- comment pagination;
- comment composer;
- reply composer;
- expandable/collapsible replies;
- reply pagination;
- comment edit flow;
- comment delete flow;
- comment reaction controls;
- safe mutation handling;
- video-reaction integration where necessary for shared engagement consistency;
- reporting interface;
- viewer-blocking interface where supported;
- permissions-aware actions;
- moderation-state rendering;
- authenticated and anonymous behavior;
- loading, empty, and error states;
- account-specific cache isolation;
- native keyboard handling;
- accessible dialogs and bottom sheets;
- telemetry;
- security and privacy;
- automated tests;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- backend comment storage;
- comment-ranking algorithms;
- toxicity classification;
- spam-detection services;
- moderation decision engines;
- moderation queues;
- administrator dashboards;
- full notification center;
- live-chat infrastructure;
- playlist management;
- creator studio;
- native short-form playback;
- payment and monetization functionality;
- backend reactions;
- backend reporting services;
- backend blocking services;
- web frontend functionality.

Use these domains only through their existing contracts and reusable integrations.

Do not silently absorb unrelated mobile features into this milestone.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. locate the React Native application;
3. identify whether the project uses Expo or a bare React Native workflow;
4. inspect the native watch-screen integration;
5. inspect existing video and channel models;
6. inspect the API client;
7. inspect authentication and session handling;
8. inspect server-state management;
9. inspect existing reaction and subscription components;
10. inspect dialog, modal, and bottom-sheet primitives;
11. inspect keyboard-handling utilities;
12. inspect accessibility conventions;
13. inspect moderation/report contracts;
14. inspect analytics and telemetry;
15. inspect testing infrastructure.

Reuse compatible components and libraries.

Do not create competing API, authentication, state-management, navigation, or design-system infrastructure without a documented technical reason.

---

# 8. Comment Domain Contract

Consume the project's canonical comment contract.

A conceptual comment representation may include:

```text
commentId
videoId
parentCommentId
author
authorId
authorAvatar
authorChannel
text
createdAt
updatedAt
isEdited
likeCount
viewerReaction
replyCount
visibilityState
moderationState
viewerPermissions
```

Use the exact field names from the authoritative contract when available.

Do not create a competing mobile-only comment entity.

Do not assume every optional field is present.

Do not invent author identities, creation timestamps, reply counts, or reactions.

---

# 9. Comment Identity and Thread Structure

All comment state must be associated with canonical IDs.

The implementation must correctly distinguish:

- video ID;
- top-level comment ID;
- reply ID;
- parent comment ID;
- author ID.

Use the project's established thread-depth rules.

If the backend supports only one level of replies, do not invent unlimited nested comments.

If deeper nesting is supported, preserve the canonical parent-child relationships.

Do not derive parentage from array position or display order.

---

# 10. Comment Section Architecture

Implement a modular comment component system.

A conceptual structure may be:

```text
CommentSection
  ├── CommentHeader
  ├── CommentComposer
  ├── CommentSortControl
  ├── CommentList
  │   └── CommentItem
  │       ├── CommentAuthor
  │       ├── CommentContent
  │       ├── CommentActions
  │       ├── ReplyComposer
  │       └── ReplyList
  └── CommentPagination
```

The exact file layout may follow repository conventions.

Keep separate responsibilities for:

- API access;
- server-state management;
- local input state;
- mutation handling;
- presentation;
- accessibility;
- telemetry.

Do not put the entire comment system inside a single screen component.

---

# 11. Native Comment Presentation

The comment experience must work naturally on:

- compact phones;
- large phones;
- tablets;
- portrait and landscape layouts where relevant.

If comments use a bottom sheet or modal, ensure it:

- respects native safe areas;
- supports an appropriate close action;
- handles dynamic height;
- accommodates the software keyboard;
- prevents accidental background interaction where necessary;
- preserves the context of the active video;
- remains accessible.

If the repository already has an established comment-screen navigation pattern, preserve it rather than introducing an unnecessary new presentation model.

---

# 12. Comment Loading

Load comments using the canonical API.

Support:

- initial loading;
- successful loading;
- empty comment section;
- unavailable comments;
- network failure;
- authorization failure;
- retry.

Comment loading must not block video playback.

A comment-service failure must not make the watch screen unusable.

Do not display old-video comments while a new video's comment request is pending.

---

# 13. Comment Sorting

Implement only backend-supported sorting options.

Possible modes may include:

- top comments;
- newest comments;
- other canonical sort modes.

When the viewer changes sorting:

- send the canonical sort identifier;
- reset pagination appropriately;
- invalidate incompatible cached pages;
- prevent stale responses from replacing the newly selected result set;
- preserve the current video and comment context.

Do not sort only the currently loaded page when the user expects server-wide sorting.

Do not invent a client-side comment ranking algorithm.

---

# 14. Comment Pagination

Implement the project's canonical pagination model.

Prefer cursor pagination when provided by the backend.

Support:

- initial page;
- next page;
- loading indicator;
- retry;
- end-of-results state;
- duplicate prevention;
- stale-request protection.

Do not request the same cursor concurrently.

Do not fetch an unlimited comment history.

Do not discard previously loaded comments merely because a later page failed.

---

# 15. Comment Composer

Implement a native-friendly comment composer.

Support:

- authenticated viewer;
- unauthenticated viewer;
- text entry;
- keyboard submission;
- character limits;
- validation;
- submit;
- cancel/reset where appropriate;
- pending state;
- success;
- failure.

Use the project's canonical limits and validation rules.

The composer must reject empty input after the normalization rules applicable to the backend have been applied.

Do not introduce a conflicting client-side character limit.

---

# 16. Native Keyboard Handling

The comment composer must behave correctly with the iOS and Android software keyboards.

Handle:

- keyboard appearance;
- keyboard dismissal;
- screen resizing;
- input focus;
- submit action;
- bottom-sheet resizing where applicable;
- safe-area adjustments.

Do not allow the keyboard to permanently obscure the send control.

Avoid automatically dismissing the keyboard after every failed submission.

Do not change the active video or navigate unexpectedly merely because the keyboard is shown.

---

# 17. Comment Creation

Submitting a comment must:

1. validate the input;
2. use the canonical API;
3. prevent duplicate concurrent submissions;
4. display pending state;
5. handle the authoritative response;
6. reconcile the rendered comment;
7. clear the composer only after the appropriate success condition;
8. handle failure without silently losing meaningful input.

Do not generate authoritative server IDs or timestamps on the client.

Do not mark a comment as published before the canonical operation confirms the result when confirmation is required.

---

# 18. Optimistic Comment Creation

Optimistic UI may be used only if the complete rollback and reconciliation behavior is implemented.

If used:

- represent the item as pending;
- distinguish temporary local identity from canonical server identity;
- prevent duplicate submission;
- replace temporary state with the server response;
- deduplicate the realtime/server response if both arrive;
- remove or mark failure after rejection.

Do not leave failed comments looking successfully published.

Do not insert the same server-confirmed comment twice.

---

# 19. Draft Preservation

Preserve entered text when a submission fails for recoverable reasons.

Where appropriate, retain the draft while the user:

- dismisses a transient error;
- reconnects to the network;
- reopens the comment composer;
- refreshes a safely retained local interaction state.

Do not persist drafts indefinitely without a product requirement.

If local draft persistence is supported, scope it correctly to the video and authenticated identity, and follow the approved storage policy.

Do not store credentials or sensitive session material alongside drafts.

---

# 20. Threaded Replies

Implement reply presentation according to the canonical comment model.

Support:

- reply count;
- expand replies;
- collapse replies;
- initial reply loading;
- pagination where supported;
- retry;
- reply creation;
- unavailable/deleted reply state.

Loading replies must not require fetching every reply to every top-level comment.

Use stable comment and parent IDs.

Do not let expanding one thread show another comment's replies.

---

# 21. Reply Loading and Caching

Replies must use cache keys associated with:

- video ID;
- parent comment ID;
- sort/context where required;
- pagination cursor;
- viewer context when authorization or visibility differs by viewer.

When expanding a thread:

- load the appropriate replies;
- prevent duplicate requests;
- handle repeated expansion;
- preserve valid cached replies according to the cache policy.

Do not retain unbounded reply collections indefinitely.

---

# 22. Reply Composer

A reply composer must identify the correct parent comment.

Support:

- opening reply mode;
- entering a reply;
- validation;
- authenticated/anonymous state;
- submission;
- success;
- failure;
- cancellation.

Protect against race conditions where a user opens one reply composer, switches context, and accidentally submits to a different parent.

Do not assume the viewer may reply to every comment.

Use the canonical permission model.

---

# 23. Editing Comments

Implement editing for comments the backend confirms the viewer can edit.

Support:

- entering edit mode;
- loading original text;
- validating the new text;
- save;
- cancel;
- pending state;
- success;
- failure;
- reconciliation.

After a successful edit, display the canonical server response.

Do not assume local authorship or local ownership checks override backend permissions.

Do not discard the original text when the update fails.

---

# 24. Deleting Comments

Implement deletion where permitted.

The experience must:

- identify the target comment;
- explain the action where appropriate;
- require confirmation when the product requires it;
- disable conflicting actions during submission;
- submit the canonical mutation;
- reconcile the server-confirmed state;
- handle failures.

Do not mark a comment permanently deleted simply because the user tapped Delete.

Preserve reply structure or render deleted-comment placeholders according to the backend's canonical contract.

Do not delete other comments or all replies merely because the parent is removed, unless the backend defines that behavior.

---

# 25. Comment Reactions

Implement supported comment reactions through the canonical reaction API.

Support:

- no current reaction;
- active reaction;
- reaction removal;
- reaction change;
- pending state;
- failure;
- current viewer state.

Do not assume a comment reaction is identical to a video reaction merely because both use a like-style control.

Use the correct entity type and canonical identifiers.

---

# 26. Safe Optimistic Reactions

If reactions use optimistic state:

- retain the previous viewer reaction;
- retain any displayed count required for rollback;
- prevent conflicting mutations;
- update the UI;
- restore prior state on failure;
- reconcile the confirmed server response.

Protect against stale responses reversing a newer reaction.

Do not increment or decrement authoritative aggregate counts blindly.

Do not treat a network timeout as definite failure if the backend may have processed the mutation. Reconcile state according to the canonical API contract.

---

# 27. Video-Reaction Integration

Where the shared watch experience needs video reactions, consume the same canonical reaction model and reusable integration.

The comment milestone must not create a second incompatible video-reaction implementation.

Use consistent:

- identifiers;
- API error handling;
- loading states;
- optimistic-update rules;
- telemetry conventions.

Do not expand this prompt into unrelated playback functionality.

---

# 28. Comment Action Menu

Implement an accessible native action menu or bottom sheet for comment actions.

Actions may include, when supported and authorized:

- reply;
- edit;
- delete;
- react;
- report;
- block user;
- other project-defined operations.

Only display actions permitted by the canonical viewer permissions and product policy.

Do not invent administrative actions for ordinary viewers.

Do not treat hidden UI controls as an authorization mechanism.

---

# 29. Reporting

Where the backend supports reporting, implement a native report flow.

Support:

- opening the report interface;
- reason selection;
- validation;
- submission;
- pending state;
- success;
- failure;
- close/cancel.

Use the canonical reporting contract.

Do not create a separate report entity or reporting API.

Do not expose internal moderation queue details or reviewer information.

---

# 30. Blocking Users

Where the platform supports viewer blocking, integrate with the canonical block contract.

The UI must:

- identify the target user;
- explain the action;
- obtain confirmation where appropriate;
- submit through the backend;
- reconcile affected visible content;
- handle failure.

Do not invent the effects of blocking.

Do not assume blocking a user automatically deletes all historical comments unless that behavior is explicitly defined by the project.

Do not modify unrelated viewers' data locally.

---

# 31. Moderation-Aware Comment States

Render canonical server-provided states for comments and replies.

Possible conceptual states include:

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

Use only states supported by the actual backend.

Distinguish between:

- deleted by the author;
- removed by moderation;
- unavailable;
- hidden from the current viewer;
- inaccessible due to viewer permissions;

only when the API provides sufficient information.

Do not infer moderation outcomes from missing comments.

---

# 32. Authentication-Aware Interaction

Anonymous viewers may read public comments where permitted.

Require authentication only for operations that actually require it, according to the product policy.

Possible authenticated actions include:

- creating comments;
- replying;
- reacting;
- editing;
- deleting;
- reporting;
- blocking.

Do not redirect the entire watch experience to sign-in because an anonymous viewer opens comments.

For unauthenticated actions, present the established authentication entry point and preserve the active video context.

---

# 33. Comment Counts

Where the watch screen displays comment counts:

- use authoritative server data;
- reconcile count changes from confirmed responses;
- avoid blindly incrementing counts after submission;
- avoid double-counting optimistic and confirmed comments.

If counts are eventually consistent, do not claim exact immediate synchronization.

Do not calculate global counts from only loaded pages.

---

# 34. Cache Invalidation

After mutations, invalidate or update only the appropriate data:

- top-level comments;
- replies for the affected parent;
- viewer reaction state;
- comment counts;
- moderation/visibility state;
- block-related data where supported.

Avoid invalidating every video and account query after one comment is edited.

Use the smallest scope that keeps the client consistent with authoritative server state.

---

# 35. Concurrent Mutation Safety

Protect against conflicting actions such as:

```text
Edit comment
Delete comment
React to comment
Report comment
Block author
```

The UI must disable or reconcile incompatible actions as appropriate.

Do not allow a stale edit response to restore content after deletion.

Do not allow a reaction response to recreate a comment that has been removed.

Use request identity and canonical IDs to ensure mutations apply to the correct comment.

---

# 36. Pagination and Mutation Reconciliation

The implementation must safely handle:

1. loading a page of comments;
2. loading another page;
3. adding a new comment;
4. editing an existing comment;
5. deleting a comment;
6. loading additional replies;
7. receiving a delayed response.

Prevent:

- duplicate items;
- deleted items reappearing;
- replies attached to the wrong parent;
- stale page data overwriting confirmed changes;
- comments from one video entering another video's list.

Use stable IDs and appropriate cache invalidation.

---

# 37. Native Dialogs and Bottom Sheets

Use existing native-compatible dialog/bottom-sheet components where available.

For dialogs:

- move focus appropriately;
- provide an accessible title;
- expose appropriate action labels;
- handle cancellation;
- restore focus where possible;
- prevent accidental repeated confirmation.

For bottom sheets:

- handle safe areas;
- handle dynamic content;
- accommodate the keyboard;
- preserve the active video context.

Do not introduce a new presentation library without first inspecting the repository.

---

# 38. Offline and Network Recovery

Handle temporary loss of connectivity during:

- comment loading;
- reply loading;
- comment creation;
- reply creation;
- editing;
- deletion;
- reactions;
- reporting;
- blocking.

Do not assume that network failure proves a mutation was not processed by the backend.

For operations with uncertain outcomes:

- inspect the contract's idempotency/reconciliation capabilities;
- fetch authoritative state when appropriate;
- avoid automatically repeating non-idempotent requests;
- preserve draft text where safe.

Do not claim that comments can be created offline unless offline creation is explicitly supported by the project architecture.

---

# 39. Rate Limits and Abuse Prevention

Respect server-side rate limits for:

- comment creation;
- replies;
- reactions;
- reports;
- blocking actions.

When a rate-limit response occurs:

- display a meaningful message;
- prevent aggressive resubmission;
- honor server-provided retry metadata where applicable.

Do not bypass rate limits with multiple concurrent requests.

Do not implement a client-only system that claims to replace server-side abuse prevention.

---

# 40. Native Accessibility

The comment experience must support native accessibility on iOS and Android.

Implement:

- accessible comment author labels;
- accessible reaction controls;
- semantic action menus;
- accessible composer labels;
- keyboard/send actions;
- clear form validation;
- screen-reader feedback for successful or failed operations;
- adequate touch-target sizes;
- accessible reply expansion;
- readable author/content hierarchy;
- visible focus or focus feedback where applicable.

Do not rely on color alone to communicate reactions, deletion, or moderation state.

Avoid announcements that repeatedly overwhelm assistive-technology users.

---

# 41. Text Scaling and Layout

The interface must remain usable with platform accessibility text scaling enabled.

Handle:

- long usernames;
- long comments;
- long reply chains;
- large text;
- multiline text entry;
- narrow viewports;
- dynamic keyboard dimensions.

Prevent horizontal overflow.

Do not truncate critical moderation or failure messages without a way to inspect the full text where needed.

Ensure touch actions remain discoverable even when text becomes larger.

---

# 42. Performance

Optimize for:

- large comment lists;
- frequent reply expansion;
- text-entry responsiveness;
- reaction updates;
- mutation reconciliation;
- scrolling;
- limited memory retention.

Use an appropriate React Native list component for long lists.

Use stable keys.

Avoid rerendering every comment when one composer changes.

Do not load every reply for every comment upfront.

Virtualization may be used where necessary, but must preserve:

- scroll behavior;
- interaction state;
- accessibility;
- focus;
- correct pagination.

---

# 43. State Ownership

Separate state into clear categories.

### Server state

- comment pages;
- reply pages;
- canonical comment content;
- moderation state;
- viewer permissions;
- reaction state;
- server-provided counts.

### Local UI state

- composer text;
- reply composer state;
- edit state;
- open action menu;
- dialog visibility;
- expansion/collapse state;
- temporary validation messages.

### Persistent local state

Only data explicitly permitted for local persistence.

Do not place all comments, drafts, and actions into one global store.

Do not let cached server state overwrite a newer native interaction state without reconciliation.

---

# 44. Account-Specific Cache Isolation

Ensure that viewer-specific comment permissions, reactions, blocks, and other account-sensitive state are scoped correctly.

When the authenticated viewer changes:

- invalidate viewer-specific reaction state;
- invalidate relevant permissions;
- invalidate block-related state;
- clear private or viewer-specific comment data;
- reset pending mutation state;
- preserve public comment data only where safe.

Do not display one user's reaction, permissions, or block status to another account.

---

# 45. Authentication Expiration

Handle session expiration while a viewer is:

- composing a comment;
- replying;
- reacting;
- editing;
- deleting;
- reporting;
- blocking.

The implementation must:

- use the established session-refresh flow;
- avoid infinite refresh loops;
- preserve draft text where safe;
- stop unauthorized mutations;
- show the correct authentication state.

Do not blindly repeat a mutation after session refresh if its original outcome is uncertain.

---

# 46. Security

The implementation must:

- safely render untrusted user-generated text;
- avoid unsafe HTML rendering;
- validate links before opening them;
- prevent open redirects;
- use secure authentication/session integration;
- respect backend authorization;
- avoid exposing moderation metadata;
- avoid logging raw comment text or report content unnecessarily;
- protect private data;
- prevent cross-account cache leakage.

Do not treat client-side permissions as authoritative.

The backend must remain the source of truth for comment access, moderation state, and enforcement.

---

# 47. Privacy

Comments and reports may contain sensitive personal information.

Do not:

- transmit raw comment text to analytics unless explicitly authorized;
- include private report reasons in telemetry;
- expose hidden moderation state;
- store private drafts indefinitely;
- persist authentication credentials with composer data;
- put private user information into navigation parameters.

Respect the platform's privacy policy and user settings.

---

# 48. Analytics and Telemetry

Instrument meaningful comment interactions using the project's canonical analytics contract.

Potential event categories include:

```text
comment_section_opened
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

Use the canonical event names where supplied.

Prevent duplicate telemetry due to:

- remounts;
- retries;
- optimistic updates;
- cache revalidation;
- duplicate delivery.

Do not transmit raw comment text, access tokens, private report details, or unnecessary personal identifiers.

Separate user intent from confirmed backend outcomes.

---

# 49. Testing Strategy

Implement tests for real behavior.

### Unit tests

Cover:

- permission mapping;
- comment/reply state transitions;
- query and pagination state;
- comment mutation payloads;
- stale-response protection;
- reaction rollback;
- comment deduplication;
- parent/reply association;
- cache-key generation;
- account-switch invalidation;
- error classification;
- telemetry event construction.

### Component tests

Cover:

- comment item;
- reply item;
- comment composer;
- reply composer;
- edit mode;
- delete confirmation;
- reaction control;
- action menu;
- reporting form;
- blocking confirmation;
- deleted/removed comment presentation;
- loading/empty/error states.

### Integration tests

Cover:

- loading top-level comments;
- sorting;
- pagination;
- creating a comment;
- creating a reply;
- editing a comment;
- deleting a comment;
- reacting to comments;
- report submission;
- user blocking where supported;
- authorization failures;
- session expiration;
- mutation rollback;
- stale-response handling;
- cache invalidation;
- network recovery.

### End-to-end tests

At minimum:

1. open a video with comments;
2. load comments;
3. change the supported comment sort;
4. load additional comments;
5. expand a reply thread;
6. create a comment while authenticated;
7. create a reply;
8. edit an owned comment;
9. react to a comment;
10. delete an owned comment;
11. report a comment where supported;
12. block a user where supported;
13. test comment pagination failure and recovery;
14. test an anonymous viewer attempting a restricted action;
15. verify comments do not block playback when the comment service fails;
16. verify comment data does not leak across accounts;
17. verify keyboard and screen-reader interactions on both platforms where test infrastructure permits.

Use controlled mocks for isolated tests only. Production code must use the actual project integration interfaces.

---

# 50. iOS and Android Compatibility

Validate the implemented experience on supported iOS and Android environments.

Pay particular attention to:

- keyboard appearance/dismissal;
- bottom-sheet behavior;
- native navigation;
- touch interactions;
- accessibility;
- text scaling;
- long comments;
- scrolling;
- focus restoration.

Do not assume a UI validated on one platform is automatically correct on the other.

Use platform-specific code only when required by actual native behavior.

---

# 51. Dependency Discipline

Before adding dependencies:

- inspect the existing component libraries;
- verify React Native compatibility;
- verify iOS/Android support;
- avoid duplicate modal, bottom-sheet, list, and form frameworks;
- consider native build configuration requirements.

Do not introduce a new dependency merely to implement a simple comment interaction already supported by the project.

Document material dependency or native configuration changes.

---

# 52. Documentation

Update documentation describing:

- comment architecture;
- API contract integration;
- reply loading and pagination;
- comment sorting;
- mutation handling;
- optimistic-update rollback;
- moderation states;
- report/block integrations;
- cache isolation;
- keyboard and bottom-sheet behavior;
- accessibility;
- analytics/privacy requirements;
- test strategy.

Documentation must reflect the implementation that actually exists.

Do not document unsupported backend features as completed functionality.

---

# 53. No Fake Comment Behavior

Do not create:

- hardcoded production comments;
- fake authors;
- fake replies;
- fabricated reactions;
- simulated report success;
- fabricated block results;
- fake persistence;
- hardcoded viewer permissions;
- invented moderation outcomes.

Mocks are permitted only within controlled automated tests.

The production application must use real API and integration contracts.

---

# 54. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- nonfunctional comment submission;
- empty reply handlers;
- placeholder reaction buttons;
- fake report controls;
- fake block actions;
- incomplete keyboard handling;
- incomplete error recovery;
- incomplete cache isolation;
- “implement later” functionality within the current scope.

Everything required by this prompt must be genuinely implemented.

---

# 55. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- native build where available;
- comment loading;
- sorting;
- pagination;
- comment creation;
- reply creation;
- editing;
- deletion;
- reactions;
- report flow;
- blocking where supported;
- authorization-sensitive actions;
- session expiration;
- mutation rollback;
- stale-request protection;
- cache isolation;
- keyboard handling;
- accessibility;
- responsive layouts;
- privacy/security requirements.

Fix issues discovered within the current scope.

Do not claim that a native build, backend service, or external integration passed validation unless the check actually ran.

If a platform toolchain is unavailable, report the exact blocker and complete all feasible local checks.

---

# 56. Definition of Done

This prompt is complete only when:

- the native comment section works;
- comments load from real contracts;
- sorting works where supported;
- pagination works;
- comment submission works;
- reply loading and creation work;
- editing works where authorized;
- deletion works where authorized;
- reaction behavior is correct;
- optimistic interactions roll back correctly where used;
- reporting works where supported;
- blocking works where supported;
- moderation-aware states render correctly;
- authenticated and anonymous behavior is correct;
- duplicate mutations are prevented;
- stale responses cannot overwrite current state;
- mutation/cache reconciliation works;
- account-specific state is isolated;
- session expiration is handled safely;
- keyboard and bottom-sheet behavior works;
- accessibility requirements are implemented;
- performance remains usable with large comment lists;
- security/privacy requirements are respected;
- telemetry is implemented without prohibited sensitive data;
- automated tests cover the defined behavior;
- documentation is updated;
- no fake production behavior remains;
- no current-scope placeholders remain;
- validation passes to the extent possible in the available environment.

---

# 57. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize comments, replies, reactions, reporting, blocking, and moderation-aware interactions actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List comment, reply, reaction, report, block, authorization, pagination, and analytics contracts consumed.

### State and Caching

Summarize mutation reconciliation, optimistic rollback, stale-request protection, account isolation, and cache invalidation.

### Testing

List tests created and tests executed.

### Validation

Report TypeScript, linting, native builds, and runtime tests performed for iOS and Android.

### Integration Notes

Identify missing backend contracts, external dependencies, platform-specific limitations, or required configuration.

### Out of Scope

Confirm that backend comment persistence, moderation engines, abuse detection, live-chat infrastructure, monetization, administration, and other excluded domains were not improperly implemented.

---

# 58. Final Execution Directive

Execute this prompt as a concrete native mobile implementation task.

Do not merely describe the comment system.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate comments, reactions, persistence, permissions, reports, or moderation outcomes.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated mobile or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style native mobile comments, replies, reactions, and community-interaction experience for iOS and Android**, integrated with the project's canonical backend contracts.
