# YouTube-Style Video Platform — Frontend Prompt — Volume 5

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web channel, playlist, subscription-management, and viewer-library experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

* public channel pages;
* channel content navigation;
* channel subscription management;
* playlists;
* playlist viewing;
* playlist creation/editing where authorized;
* viewer library;
* watch history;
* watch-later functionality where supported;
* liked-content library where supported;
* saved playlists;
* playlist ordering where supported;
* library loading/pagination;
* viewer-specific state;
* privacy-aware library behavior;
* accessibility;
* responsive behavior;
* analytics;
* testing;
* documentation.

Do not implement unrelated frontend domains.

Do not implement backend channel, playlist, history, or subscription services.

Do not fabricate backend behavior.

---

# 2. Project Context

The product is a production-grade YouTube-style video platform supporting:

* long-form video;
* short-form video;
* channels;
* subscriptions;
* comments;
* reactions;
* playlists;
* watch history;
* watch-later/saved content where supported;
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
* production server/client state management;
* accessibility;
* observability;
* automated testing.

The channel and library experiences contain significant authenticated and privacy-sensitive data and must not leak viewer-specific information across accounts.

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

If compatible channel, subscription, playlist, or library components already exist, extend them rather than duplicating them.

Do not assume that a feature described in the complete product has already been implemented.

---

# 4. Primary Objective

Implement the production web experience for public channels and authenticated viewer libraries.

The completed scope must allow viewers to:

1. open a public channel;
2. view channel identity and metadata;
3. browse channel videos;
4. browse channel shorts where supported;
5. browse channel playlists where supported;
6. subscribe and unsubscribe;
7. see appropriate subscription state;
8. open playlists;
9. browse playlist items;
10. create/manage viewer playlists where authorized;
11. add/remove videos from supported playlists;
12. reorder playlist items where supported;
13. access watch history;
14. clear/remove history where supported;
15. access watch-later/saved content where supported;
16. access liked-content/library surfaces where supported;
17. navigate from library content to the canonical video experience;
18. receive appropriate authenticated/anonymous behavior;
19. maintain privacy boundaries;
20. use responsive accessible interfaces;
21. receive correct analytics/telemetry.

---

# 5. Explicit Scope

Implement:

* public channel page;
* channel header;
* channel tabs/navigation;
* channel video lists;
* channel short-form presentation where contracted;
* channel playlists presentation where contracted;
* subscription control;
* subscription state handling;
* playlist pages;
* playlist item lists;
* playlist owner controls;
* playlist creation;
* playlist editing;
* playlist visibility controls where supported;
* playlist item addition/removal where supported;
* playlist item ordering where supported;
* viewer library route;
* watch-history UI;
* watch-later/saved-video UI where supported;
* liked-content UI where supported;
* library pagination;
* loading/error/empty states;
* viewer-specific caching;
* analytics;
* accessibility;
* responsive behavior;
* testing;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* backend channel services;
* backend subscription persistence;
* backend playlist persistence;
* recommendation ranking;
* search infrastructure;
* video playback internals;
* media-processing services;
* creator studio;
* creator analytics;
* live-stream backend;
* monetization;
* moderation backend;
* notification backend;
* mobile applications;
* administrative dashboards.

Do not redesign backend contracts merely to simplify the frontend.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository;
2. identify the web application;
3. inspect existing routes/layouts;
4. inspect shared header/sidebar/navigation;
5. inspect video/channel card components;
6. inspect the authentication/session system;
7. inspect API-client conventions;
8. inspect server-state and caching conventions;
9. inspect existing watch-page integration;
10. inspect existing playlist/channel/library code;
11. inspect analytics/telemetry;
12. inspect tests.

Reuse compatible shared components.

Avoid introducing another routing or state-management architecture.

---

# 8. Channel Route

Implement a canonical public channel experience.

A route may be equivalent to:

```text
/channel/{channelId}
```

Preserve an existing project convention if one is already established.

The route must support:

* direct navigation;
* refresh;
* deep linking;
* back/forward navigation;
* public access;
* unavailable channel state;
* restricted/private channel state where supported.

Do not rely solely on client-side navigation state.

---

# 9. Channel Data Contract

Consume the canonical channel contract.

A conceptual representation may contain:

```text
channelId
name
handle
avatar
banner
description
verificationState
subscriberCount
videoCount
visibility
viewerSubscriptionState
viewerPermissions
createdAt
```

The actual contract must determine concrete field names.

Do not create an alternate channel entity.

Do not infer private viewer permissions from public channel fields.

---

# 10. Channel Header

Implement a production channel header containing, where available:

* channel avatar;
* banner;
* channel name;
* handle;
* verification indicator;
* subscriber count;
* description;
* subscription control;
* additional channel actions.

Support:

* loading;
* unavailable;
* restricted;
* error;
* responsive layouts.

Do not assume every channel has a banner, handle, verification state, or subscriber count.

---

# 11. Channel Navigation

Implement channel-level navigation for supported sections.

Potential sections include:

* Home;
* Videos;
* Shorts;
* Live;
* Playlists;
* Community/about where actually supported.

Only render sections represented by the project's product/API contract.

Active tab state must be synchronized with routing.

Do not create frontend-only channel tabs that have no implementation behind them.

---

# 12. Channel Content

Render channel content using typed lists.

Video items should support:

* thumbnail;
* title;
* duration;
* views;
* publication information;
* restricted/live indicators where supplied.

The frontend must not infer ranking or publication order unless the API explicitly guarantees it.

---

# 13. Channel Pagination

Support contract-defined pagination for channel content.

Implement:

* initial load;
* next-page loading;
* end-of-results;
* retry;
* duplicate prevention;
* stale-request protection.

Use cursor pagination when provided by the backend.

Do not request the same cursor concurrently.

---

# 14. Channel Error Isolation

A channel header failure must not unnecessarily break navigation.

A playlist tab failure should not destroy the entire channel shell.

A single content-section failure should produce a localized recoverable state where possible.

The channel page must remain structurally usable even if one downstream endpoint fails.

---

# 15. Subscription Control

Implement channel subscription controls.

Support:

* subscribed;
* not subscribed;
* pending/loading;
* authentication required;
* operation failure;
* unavailable/restricted state.

Use canonical subscription state returned by the backend.

Do not determine subscription status solely from subscriber counts.

---

# 16. Subscription Mutation

For subscription/unsubscription:

* disable conflicting actions while a mutation is active;
* use the canonical API contract;
* reconcile with the server response;
* rollback optimistic state on failure if optimistic UI is used.

Do not issue multiple conflicting mutations concurrently.

Do not assume subscriber counts change synchronously.

---

# 17. Subscriber Count Handling

Subscriber counts are aggregate data.

The UI may display a server-provided count, but should not assume that:

```text
subscribe → displayed count += 1
unsubscribe → displayed count -= 1
```

is always correct.

Prefer authoritative server responses or normal revalidation.

Do not create false precision around eventually consistent counters.

---

# 18. Channel Privacy States

Support channel states defined by the backend.

Examples:

```text
public
private
restricted
deleted
unavailable
```

Do not expose unavailable channel metadata that the viewer is not authorized to see.

The UI should provide appropriate user-facing explanations.

---

# 19. Playlist Domain Contract

Consume the canonical playlist contract.

A conceptual playlist may contain:

```text
playlistId
ownerId
title
description
thumbnail
visibility
itemCount
createdAt
updatedAt
owner
viewerPermissions
viewerSavedState
```

The actual backend contract determines concrete fields and permissions.

Do not redefine the playlist domain in the frontend.

---

# 20. Playlist Route

Implement a canonical playlist experience.

A supported route may be equivalent to:

```text
/playlist?list={playlistId}
```

Preserve existing routing conventions if different.

The route must support:

* direct access;
* refresh;
* deep links;
* unavailable playlists;
* private playlists;
* deleted playlists;
* authenticated owner state;
* public viewer state.

---

# 21. Playlist Header

Display:

* title;
* description;
* owner;
* visibility;
* item count where supplied;
* thumbnail;
* relevant playlist actions.

Support:

* loading;
* unavailable;
* empty;
* error.

Do not assume playlists always contain videos.

---

# 22. Playlist Items

Implement playlist item presentation.

Each item should support:

* thumbnail;
* title;
* duration;
* channel;
* position where appropriate;
* publication information;
* unavailable/deleted item state.

The playlist UI must preserve item order returned by the backend.

Do not sort playlist items on the client unless explicitly required.

---

# 23. Playlist Pagination

If playlists are paginated:

* support the canonical pagination model;
* preserve item order;
* prevent duplicate items;
* prevent concurrent cursor loads;
* isolate pagination failures;
* preserve already loaded items after later-page failures.

---

# 24. Playlist Playback Navigation

Selecting a playlist item should navigate to the canonical watch experience using the proper playlist context if the product contract supports contextual playback.

Where supported, the frontend may pass:

* playlist ID;
* current playlist item;
* supported playback position/context.

Do not expose private playlist identifiers or internal service data unnecessarily.

Do not create unsupported query parameters.

---

# 25. Playlist Owner Permissions

Owner controls must be driven by explicit backend permissions.

Possible capabilities include:

```text
canEdit
canDelete
canAddItems
canRemoveItems
canReorderItems
canChangeVisibility
```

Do not assume ownership solely from matching client-side IDs.

The backend remains the authority.

---

# 26. Playlist Creation

Where the project contract supports user-created playlists, implement playlist creation.

Support:

* title;
* description where supported;
* visibility;
* validation;
* submit;
* loading;
* success;
* failure;
* cancellation.

Do not create a playlist locally and treat it as persisted before the backend confirms success.

---

# 27. Playlist Editing

Support editing permitted fields for owned playlists.

Potential fields include:

* title;
* description;
* visibility.

The UI must:

* load existing values;
* validate changes;
* prevent duplicate submissions;
* reconcile server responses;
* handle conflicts/errors.

Do not allow editing controls when the viewer lacks permission.

---

# 28. Playlist Visibility

Where supported, expose the backend-defined visibility choices.

Potential values may include:

```text
public
unlisted
private
```

Only expose actual project-supported values.

Changing visibility must use the canonical mutation contract.

The UI must warn appropriately when a change materially affects discoverability.

---

# 29. Playlist Item Addition

If the viewer can add a video to a playlist:

* open an accessible playlist-selection UI;
* retrieve the viewer's authorized playlists;
* display membership state;
* add/remove according to the backend contract;
* handle loading and failure states.

Do not show playlists the viewer is not authorized to modify.

Do not expose private playlist metadata through unrelated caches.

---

# 30. Playlist Item Removal

Support removal where authorized.

After success:

* update the correct playlist state;
* preserve correct item ordering;
* update item count from authoritative data where available.

Do not remove a video from every playlist merely because it was removed from one.

---

# 31. Playlist Item Ordering

Where reordering is supported:

* provide an accessible ordering interaction;
* preserve stable item IDs;
* avoid sending one request per pointer movement;
* submit meaningful order changes;
* handle failed reordering;
* reconcile with authoritative server order.

If drag-and-drop is used, provide a keyboard-accessible alternative.

Do not make drag-and-drop the only way to reorder items.

---

# 32. Playlist Mutation Concurrency

Protect against conflicting actions such as:

```text
remove item
reorder playlist
add item
change visibility
```

The UI must serialize or reconcile these operations.

Do not allow stale responses to restore an outdated playlist state.

---

# 33. Viewer Library Route

Implement the authenticated viewer library.

A route may be equivalent to:

```text
/feed/library
```

Preserve established routing conventions if different.

The library should provide appropriate access to supported viewer-owned content collections.

---

# 34. Library Sections

Where supported, expose:

* History;
* Watch later;
* Liked videos;
* Saved playlists;
* Personal playlists.

Only render sections backed by real project contracts.

Do not create fake collections to fill an empty library.

---

# 35. Library Navigation

The library should provide clear navigation between supported collections.

Navigation state must:

* survive refresh;
* support direct links;
* support browser back/forward;
* remain accessible;
* remain responsive.

Do not hide important library functionality behind inaccessible interaction patterns.

---

# 36. Watch History

Implement authenticated watch-history presentation.

Support:

* chronological or backend-defined ordering;
* pagination;
* video navigation;
* remove individual item where supported;
* clear history where supported;
* empty state;
* loading;
* errors.

Do not assume the client is authoritative for history.

---

# 37. History Privacy

Watch history is sensitive viewer data.

Ensure:

* only the current viewer can access it;
* viewer-specific cache keys are used;
* logout invalidates appropriate state;
* account switching does not leak previous history;
* analytics do not accidentally transmit the complete history.

Do not store complete authenticated history in uncontrolled browser storage unless explicitly required.

---

# 38. Remove History Item

Where supported, provide removal of individual history entries.

The implementation must:

* submit the canonical mutation;
* localize loading state;
* reconcile success;
* restore or refetch on failure;
* prevent duplicate removal requests.

Do not silently delete history locally without server confirmation.

---

# 39. Clear Watch History

Where the backend supports full history clearing:

* provide a clear action;
* use an appropriate confirmation step;
* display progress;
* handle failure;
* reconcile after success.

Never make destructive actions one accidental click away when confirmation is part of product expectations.

---

# 40. Watch Later / Saved Videos

Where supported, implement the viewer's watch-later/saved-video collection.

Support:

* list loading;
* pagination;
* add/remove actions;
* empty state;
* video navigation;
* synchronization with other add/remove controls.

The frontend must use the canonical saved-content contract.

Do not treat watch-later as a playlist unless the backend domain explicitly models it as one.

---

# 41. Liked Videos

Where supported, implement the liked-video library.

Support:

* list loading;
* pagination;
* canonical video navigation;
* unavailable/deleted video states;
* reaction changes where applicable.

The liked-video library must not be treated as an arbitrary locally generated list.

---

# 42. Personal Playlists

Where supported, display playlists owned by the viewer.

Support:

* playlist list;
* visibility;
* item count;
* thumbnail;
* navigation;
* editing controls where authorized;
* empty state.

Private playlists must remain isolated to the current viewer.

---

# 43. Library Pagination

Use cursor-based pagination when available.

Support:

* initial load;
* next page;
* retries;
* duplicate prevention;
* empty state;
* end of collection;
* stale-request protection.

Do not mix history entries from one viewer/account with another.

---

# 44. Library Cache Isolation

Viewer-specific library queries must include the authenticated identity or equivalent server-state isolation.

Examples:

```text
history:userA
history:userB
likes:userA
playlists:userA
```

The actual cache-key implementation should use the project's state-management conventions.

Never allow viewer-specific data to come from a public shared cache.

---

# 45. Account Switching

When authentication changes from one user to another:

* invalidate viewer-specific channel/subscription state;
* invalidate library state;
* invalidate private playlist lists;
* invalidate history;
* invalidate liked/saved collections;
* clear stale mutation state;
* reload viewer-specific content.

This must also work across logout/login transitions.

---

# 46. Loading and Empty States

Implement meaningful states for:

* channel loading;
* channel section loading;
* playlist loading;
* library loading;
* mutation loading;
* empty playlists;
* empty history;
* empty watch-later;
* empty liked videos;
* no subscriptions where applicable.

Do not show a generic endless spinner.

Empty states should explain what the viewer can do next without fabricating content.

---

# 47. Error States

Differentiate:

* unavailable channel;
* unavailable playlist;
* authorization failure;
* network failure;
* temporary backend error;
* empty collection;
* deleted item;
* restricted item.

A failure in one library collection should not break the rest of the library shell.

---

# 48. Responsive Design

Support:

* mobile web;
* tablet;
* desktop;
* large desktop.

Channel pages should adapt banner/header content.

Playlist and library lists should remain usable on narrow screens.

Controls must remain touch-friendly.

Do not rely on horizontal overflow for critical actions.

---

# 49. Accessibility

Implement:

* semantic headings;
* accessible channel tabs;
* accessible playlist controls;
* keyboard navigation;
* accessible dialogs;
* accessible drag/reorder alternatives;
* screen-reader labels;
* visible focus;
* proper expanded/collapsed states;
* meaningful error announcements.

For playlist reordering, keyboard users must have a mechanism equivalent to the pointer interaction.

---

# 50. URL State and Navigation

Durable state should be represented in canonical URLs where appropriate:

* channel ID;
* channel section;
* playlist ID;
* library subsection.

Do not place transient UI state into URLs unnecessarily.

Back/forward navigation must restore durable page state.

---

# 51. Search/Discovery Integration

Channel, playlist, and library surfaces must use the same canonical cards and navigation conventions established throughout the project.

Selecting:

* channel → canonical channel page;
* playlist → canonical playlist page;
* video → canonical watch route.

Do not introduce duplicate URL conventions.

---

# 52. Subscription Integration

Subscription actions from:

* channel page;
* video page;
* channel cards;
* discovery surfaces

must use the same subscription state model.

Avoid separate incompatible implementations of subscription status.

The canonical viewer subscription state must remain consistent after mutations.

---

# 53. Playlist Integration with Watch Experience

Where product contracts support it, provide playlist context when navigating from playlist items to playback.

The watch experience must remain responsible for media playback.

This prompt only provides the navigation/context information required by the playlist UI.

Do not duplicate the playback engine.

---

# 54. Analytics and Telemetry

Instrument relevant behavior according to the project's analytics contract.

Potential events include:

```text
channel_page_viewed
channel_section_selected
channel_video_clicked
channel_subscription_changed
playlist_opened
playlist_item_clicked
playlist_created
playlist_updated
playlist_item_added
playlist_item_removed
playlist_reordered
library_opened
library_section_viewed
history_item_removed
history_cleared
watch_later_item_added
watch_later_item_removed
liked_library_opened
```

Use canonical event names where defined.

Do not transmit:

* authentication tokens;
* private playlist contents unnecessarily;
* complete watch history;
* sensitive private account information.

---

# 55. Analytics Deduplication

Prevent duplicate events caused by:

* hydration;
* route remounts;
* Strict Mode;
* cache revalidation;
* optimistic updates;
* pagination refetches.

Separate user interactions from server reconciliation events.

Do not treat every server-state update as a user action.

---

# 56. Security

The implementation must:

* respect server-side authorization;
* avoid exposing private playlist data;
* safely handle channel/user-provided text;
* validate navigation targets;
* prevent open redirects;
* avoid unsafe HTML;
* avoid logging sensitive viewer library data;
* protect session state.

Never trust client-side ownership checks as authoritative authorization.

---

# 57. Privacy

The library contains highly sensitive behavioral information.

Protect:

* watch history;
* liked videos;
* private playlists;
* saved content;
* subscription state.

Do not accidentally expose private content through:

* static rendering;
* shared caches;
* browser prefetching;
* analytics;
* URL metadata;
* client-side persistence.

When private data is rendered, make sure the route and data-fetching behavior match the project's authentication model.

---

# 58. Prefetching Safety

Be careful with Next.js/router/data prefetching.

Do not prefetch private viewer data in a way that could create cross-user leakage through:

* shared caches;
* publicly reusable artifacts;
* incorrect static rendering.

Public channel data may be prefetched according to the project strategy.

Viewer-specific data must remain properly isolated.

---

# 59. Component Boundaries

Maintain conceptual boundaries such as:

```text
channels/
  data
  hooks
  header
  navigation
  sections
  components
  analytics

playlists/
  data
  hooks
  header
  items
  editor
  reorder
  components
  analytics

library/
  data
  hooks
  history
  watch-later
  liked
  playlists
  components
  analytics
```

The exact file structure may follow existing repository conventions.

Avoid a single page component containing every channel, playlist, and library behavior.

---

# 60. State Ownership

Separate:

### Server state

* channel metadata;
* channel content;
* subscription state;
* playlist data;
* playlist permissions;
* library collections;
* history;
* saved/liked content.

### Local UI state

* open menus;
* editor state;
* confirmation dialogs;
* temporary form values;
* drag/reorder state.

### URL state

* channel section;
* playlist ID;
* library section.

Do not place all state into one global store.

---

# 61. Mutation Safety

Protect against stale or conflicting operations.

Examples:

```text
subscribe
unsubscribe
subscribe
```

or:

```text
playlist item reorder
playlist item removal
playlist visibility update
```

The client must prevent or reconcile conflicting operations.

Do not allow older responses to overwrite newer confirmed state.

---

# 62. API Error Normalization

Use the project's standard error model.

At minimum distinguish:

```text
authentication
authorization
validation
notFound
conflict
rateLimited
temporarilyUnavailable
network
unknown
```

Map each category to the appropriate UI.

Do not expose internal stack traces.

---

# 63. Testing Strategy

Implement tests for actual behavior.

### Unit tests

Cover:

* route-state serialization;
* subscription mutation state;
* playlist permission handling;
* playlist reorder logic;
* library cache-key isolation;
* account-switch invalidation;
* pagination;
* mutation reconciliation;
* analytics event construction.

### Component tests

Cover:

* channel header;
* channel navigation;
* subscription control;
* playlist header;
* playlist item;
* playlist editor;
* playlist reorder interaction;
* library navigation;
* history item;
* watch-later item;
* liked-video item;
* empty/error states.

### Integration tests

Cover:

* loading a channel;
* switching channel sections;
* subscribing/unsubscribing;
* loading a playlist;
* creating/editing a playlist;
* adding/removing an item;
* reordering items;
* opening history;
* removing history;
* loading watch-later;
* loading liked videos;
* authentication-state changes.

### End-to-end tests

At minimum:

1. open a public channel;
2. navigate channel sections;
3. subscribe to a channel;
4. unsubscribe;
5. open a playlist;
6. navigate to a playlist video;
7. create a playlist where supported;
8. add a video to it;
9. remove a video;
10. reorder playlist items where supported;
11. open viewer library;
12. inspect watch history;
13. remove a history item;
14. open another library collection;
15. verify authenticated/private data isolation;
16. verify anonymous access to public channel content;
17. verify keyboard-accessible channel/playlist navigation.

Do not replace functional testing with snapshots alone.

---

# 64. Browser Compatibility

Validate across the supported browser matrix.

Pay particular attention to:

* responsive channel headers;
* touch controls;
* playlist editors;
* keyboard-based reordering;
* dialogs;
* focus restoration;
* browser navigation.

Do not rely on unsupported browser APIs without appropriate fallbacks.

---

# 65. Performance

Optimize for:

* public channel page loading;
* image-heavy channel banners;
* channel video lists;
* playlist lists;
* library pagination;
* private viewer-state queries.

Use:

* responsive images;
* lazy loading;
* appropriate server rendering;
* efficient caching;
* localized rerenders.

Do not make the entire library client-rendered unnecessarily.

Do not fetch every library collection when only one collection is visible.

---

# 66. Image Optimization

Channel banners, avatars, playlist thumbnails, and video thumbnails must:

* reserve layout space;
* use appropriate responsive sources;
* avoid full-resolution downloads when unnecessary;
* provide fallback states;
* avoid cumulative layout shift.

---

# 67. No Fake Channel/Playlist/Library Behavior

Do not create:

* hardcoded channels;
* fake subscription counts;
* fake playlists;
* fake history items;
* simulated private playlists;
* fake saved videos;
* fake persistence.

Mocks may exist only inside automated tests.

The actual application must use real project contracts.

---

# 68. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* fake editor controls;
* nonfunctional reorder controls;
* placeholder history;
* incomplete subscription mutations;
* empty mutation handlers;
* unsupported tabs pretending to work.

Everything within the current scope must be implemented.

---

# 69. Documentation

Update documentation describing:

* channel routes;
* channel sections;
* subscription integration;
* playlist architecture;
* playlist permissions;
* playlist ordering;
* library architecture;
* viewer-specific cache isolation;
* history/privacy behavior;
* analytics;
* accessibility;
* account-switch handling.

Documentation must describe actual behavior.

---

# 70. Validation

Before completion, validate:

* TypeScript;
* linting;
* unit tests;
* component tests;
* integration tests;
* end-to-end tests where available;
* production build;
* channel navigation;
* subscription mutations;
* playlist loading;
* playlist editing;
* playlist item mutations;
* ordering;
* library loading;
* history operations;
* authenticated/private-data isolation;
* account switching;
* responsive behavior;
* accessibility-critical interaction;
* stale-request protection.

Fix issues found within this scope.

Do not merely report them.

---

# 71. Definition of Done

This prompt is complete only when:

* public channel pages work;
* channel sections work where supported;
* channel content pagination works;
* subscription state and mutations work;
* playlist pages work;
* playlist item navigation works;
* playlist creation works where supported;
* playlist editing works where supported;
* playlist visibility works where supported;
* playlist item addition/removal works where supported;
* playlist ordering works where supported;
* viewer library works;
* watch history works where supported;
* history removal/clearing works where supported;
* watch-later/saved content works where supported;
* liked-content library works where supported;
* personal playlists work where supported;
* viewer-specific cache isolation works;
* account switching does not leak data;
* private data is not exposed publicly;
* mutations are race-safe;
* loading/error/empty states are implemented;
* responsive behavior works;
* accessibility requirements are implemented;
* security/privacy requirements are respected;
* analytics are implemented appropriately;
* tests cover the defined behavior;
* documentation is updated;
* no fake production behavior remains;
* no current-scope placeholders remain;
* validation passes.

---

# 72. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize channel, subscription, playlist, and library functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List channel, subscription, playlist, history, saved-content, liked-content, pagination, authorization, and analytics contracts consumed.

### State and Caching

Summarize viewer-specific cache isolation, mutation reconciliation, account-switch handling, and pagination.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, production build, and runtime validation.

### Integration Notes

Identify material backend-contract assumptions, compatibility considerations, or external dependencies.

### Out of Scope

Confirm that backend services, creator studio, mobile, moderation backend, search infrastructure, recommendation ranking, live streaming, and monetization were not improperly implemented.

---

# 73. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe the channel, playlist, or library experience.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate backend behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web channel, playlist, subscription, and viewer-library experience** that can be integrated with the independently generated backend and other project components through explicit contracts.
