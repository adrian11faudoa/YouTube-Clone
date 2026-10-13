# YouTube-Style Video Platform — Mobile Prompt — Volume 5

## 1. Prompt Identity

You are the senior React Native/mobile engineer responsible for implementing the **native channel pages, subscription management, playlists, viewer library, watch history, and saved-content experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone for iOS and Android.

Your responsibility is to deliver a coherent native browsing and personal-library experience integrated with the platform's canonical video, channel, subscription, playlist, authentication, privacy, and analytics contracts.

The implementation includes:

- public channel pages;
- channel identity and metadata;
- channel content navigation;
- channel video and playlist lists;
- channel subscription controls;
- playlist viewing;
- playlist creation and editing where supported;
- playlist item management;
- playlist item ordering where supported;
- viewer library;
- watch history;
- watch-later/saved-video collections where supported;
- liked-video collections where supported;
- viewer-owned playlists;
- pagination and refresh;
- privacy-aware state management;
- accessibility;
- performance;
- automated testing;
- documentation.

Do not implement unrelated mobile domains.

Do not implement backend channel, subscription, playlist, history, or saved-content services.

Do not fabricate playlists, videos, subscription state, history records, permissions, or persistence.

---

# 2. Project Context

The product is a production-grade YouTube-style video platform supporting:

- long-form video;
- short-form video;
- channels;
- subscriptions;
- comments;
- reactions;
- playlists;
- watch history;
- saved content;
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
- the application's established navigation and state-management libraries;
- typed API clients;
- secure authentication/session integration;
- native accessibility;
- production-quality testing;
- privacy-conscious analytics.

The mobile application must use the same canonical domain models and backend contracts as the rest of the platform.

Do not establish incompatible mobile-specific definitions for videos, channels, subscriptions, playlists, identifiers, or timestamps.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- previous mobile prompts;
- hidden architectural decisions;
- undocumented backend APIs;
- generated files unavailable in the current execution environment;
- a repository shared with another AI conversation.

If a repository is available, inspect it before modifying it.

If portable architecture, API, authentication, channel, subscription, playlist, history, or privacy contracts are supplied, use them as authoritative.

If the repository already contains compatible screens, components, or integrations, preserve and extend them instead of creating competing implementations.

If an expected backend capability is missing, document the specific integration dependency. Do not replace production functionality with fake data.

---

# 4. Primary Objective

Implement the native channel, subscription, playlist, and viewer-library experience.

An eligible viewer must be able to:

1. open a public channel;
2. view channel identity and metadata;
3. browse channel videos;
4. browse supported channel sections;
5. subscribe and unsubscribe;
6. inspect subscription state;
7. open a playlist;
8. browse ordered playlist items;
9. navigate from a playlist to a video;
10. create and edit playlists where supported;
11. add or remove playlist items where supported;
12. reorder playlist items where supported;
13. access their viewer library;
14. browse watch history where supported;
15. remove history entries where supported;
16. clear history where supported;
17. browse watch-later/saved content where supported;
18. browse liked videos where supported;
19. manage their playlists;
20. recover from network failures and conflicting mutations;
21. preserve privacy and account isolation;
22. use native-accessible controls;
23. maintain smooth scrolling and predictable navigation.

---

# 5. Explicit Scope

Implement:

- canonical channel screen;
- channel header;
- channel navigation and supported tabs;
- channel video lists;
- channel playlist lists;
- channel content pagination;
- subscription/unsubscription controls;
- playlist detail screen;
- playlist metadata presentation;
- playlist item list;
- playlist creation where supported;
- playlist editing where supported;
- playlist visibility controls where supported;
- playlist item addition/removal where supported;
- playlist item reordering where supported;
- viewer library screen;
- library navigation;
- watch-history screen;
- history item removal/clear controls where supported;
- watch-later/saved-content screen where supported;
- liked-video screen where supported;
- viewer-owned playlist collection;
- refresh and pagination;
- account-specific state isolation;
- native accessibility;
- loading, empty, and error states;
- telemetry;
- automated testing;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- backend channel services;
- subscription persistence services;
- playlist persistence services;
- backend watch-history services;
- backend saved-content services;
- recommendation ranking;
- search infrastructure;
- native video playback internals;
- complete comments and replies;
- notification center;
- creator studio;
- live-stream management;
- monetization and purchases;
- moderation console;
- backend analytics aggregation;
- infrastructure provisioning.

Integrate with these domains through existing reusable components and explicit contracts only.

Do not absorb unrelated mobile features into this milestone.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. locate the React Native application;
3. identify its Expo or bare React Native workflow;
4. inspect navigation and routing conventions;
5. inspect the canonical video and channel models;
6. inspect authentication/session handling;
7. inspect API-client conventions;
8. inspect server-state and caching infrastructure;
9. inspect reusable video and channel cards;
10. inspect existing subscription controls;
11. inspect playlist and viewer-library code;
12. inspect history and saved-content APIs where available;
13. inspect privacy and account-switch handling;
14. inspect accessibility primitives;
15. inspect analytics and testing infrastructure.

Reuse compatible components and dependencies.

Do not create another API client, navigation framework, global state store, authentication system, or design system without a documented technical justification.

---

# 8. Navigation Architecture

Integrate the following native destinations through the application's established navigation system:

- channel details;
- channel content sections;
- playlist details;
- viewer library;
- library subsections;
- canonical video watch destination.

Use stable route parameters based on canonical identifiers.

Do not depend exclusively on an entity object passed from the previous screen. Screens must be able to retrieve the authoritative entity using its canonical ID.

Support:

- native back navigation;
- tab navigation where applicable;
- direct navigation from supported deep links;
- refresh/reconstruction where the application supports it;
- navigation from search/discovery results;
- navigation from the watch screen.

Do not create duplicate route formats for the same channel, video, or playlist.

---

# 9. Channel Domain Contract

Consume the canonical channel API and model.

A conceptual channel representation may contain:

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

Use exact project-defined fields and values when available.

Do not create an incompatible mobile-only channel entity.

Do not assume every channel has a banner, handle, description, or verification status.

Do not invent counts, creator identities, or permissions.

---

# 10. Channel Screen

Implement the public channel screen.

The screen must provide:

- channel identity;
- avatar;
- banner where available;
- channel name and handle;
- subscriber count where supplied;
- description;
- subscription control;
- supported channel sections;
- channel content.

Support:

- initial loading;
- public channel access;
- missing channel;
- deleted/unavailable channel;
- restricted/private channel;
- network failure;
- retry.

Do not show stale channel details after navigation to a different channel.

---

# 11. Channel Header

Implement a responsive native channel header.

Support:

- image loading and fallback;
- long channel names;
- long descriptions;
- optional verification indicators;
- subscriber count;
- subscription button;
- more-actions menu where supported.

The header must adapt to compact phone screens and accessibility text scaling.

Do not hide essential channel identity or subscription controls behind inaccessible hover behavior.

Do not assume an avatar or banner will always be available.

---

# 12. Channel Navigation

Render only channel sections supported by the project.

Possible sections include:

- Home;
- Videos;
- Shorts;
- Live;
- Playlists;
- About.

Use canonical section routing or the repository's established tab/navigation convention.

Do not render a tab as functional unless its content or destination is genuinely implemented or already exists.

The active section must remain consistent with back navigation and screen restoration where supported.

---

# 13. Channel Content

Implement channel video lists using the canonical video model.

Each item may display:

- thumbnail;
- title;
- duration;
- channel identity when needed;
- views;
- publication information;
- live/short-form indicator where supplied.

Use existing video-card components where compatible.

Selecting a video must navigate to the canonical mobile watch destination using the video ID.

Do not construct video playback URLs directly from channel data.

---

# 14. Channel Playlists and Shorts

Where supported, provide channel-specific playlist and short-form sections.

For each section:

- request the corresponding canonical data;
- maintain proper channel ownership;
- render the correct item type;
- handle pagination;
- display empty/error states.

Short-form section items must navigate to the canonical short-form experience when available.

This prompt only integrates the entry point and listing behavior. It does not implement the short-form player or gesture-based feed.

---

# 15. Channel Pagination and Refresh

Implement backend-defined pagination for channel content.

Support:

- initial page;
- next page;
- loading state;
- end-of-results;
- retry;
- duplicate prevention;
- stale-request protection.

Use cursor pagination where the backend provides it.

Do not request the same cursor concurrently.

If refresh is supported, reconcile the updated result set without leaving duplicate content behind.

Do not load every channel video upfront.

---

# 16. Subscription Domain Contract

Consume the canonical subscription model.

The frontend must distinguish:

- free channel subscription;
- paid channel membership;
- any additional relationship types defined by the backend.

These must not be treated as interchangeable.

A conceptual subscription state may include:

```text
channelId
viewerId
isSubscribed
subscriptionPreferences
updatedAt
```

Use actual contract fields.

Do not create a second subscription representation.

---

# 17. Subscribe and Unsubscribe

Implement subscription controls.

Support:

- subscribed;
- not subscribed;
- loading;
- success;
- failure;
- unauthenticated viewer;
- inaccessible channel.

Use the canonical API.

Prevent conflicting concurrent subscribe/unsubscribe requests.

On failure, restore the prior state if optimistic UI was used.

Reconcile the final state with the server response.

Do not assume a subscription succeeded merely because the user tapped the button.

---

# 18. Subscription State Consistency

Channel subscription state must be consistent across channel screens and any compatible shared card/control already in the mobile application.

Use shared subscription logic and cache invalidation where appropriate.

Do not implement a separate channel-screen-only subscription service.

Subscriber counts are aggregate data. Do not blindly increment or decrement them without an authoritative response or appropriate revalidation.

Do not claim exact real-time count consistency unless the backend supports it.

---

# 19. Playlist Domain Contract

Consume the canonical playlist model.

A conceptual playlist representation may contain:

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

Use the actual project-defined fields.

Do not assume every playlist is owned by the current viewer.

Do not expose private playlist data to unauthorized users.

Do not create a separate mobile-only playlist entity.

---

# 20. Playlist Detail Screen

Implement the playlist detail screen.

Where supplied by the contract, display:

- title;
- description;
- owner identity;
- thumbnail;
- visibility;
- item count;
- ordered video list;
- supported owner actions.

Support:

- loading;
- empty playlist;
- unavailable playlist;
- deleted playlist;
- private/restricted playlist;
- error and retry.

Use the canonical playlist ID for navigation and requests.

Do not render a private playlist's contents when authorization is denied.

---

# 21. Playlist Items

Render playlist items in the order supplied by the backend.

Each item may display:

- thumbnail;
- title;
- duration;
- channel;
- position;
- publication information;
- deleted/unavailable state.

Use stable item IDs and appropriate React Native list rendering.

Do not sort playlist items on the client unless the project contract explicitly requires it.

Do not drop unavailable items silently if the backend provides a defined placeholder state.

---

# 22. Playlist Playback Navigation

When an item is selected, navigate to the canonical watch destination.

If the project contract supports contextual playlist playback, include only the approved navigation context, such as the playlist ID and selected item position.

Do not invent unsupported route parameters.

Do not pass signed media URLs, authorization credentials, or private metadata through navigation state.

The watch screen remains responsible for playback and playback authorization.

---

# 23. Playlist Creation

Where supported, implement creation of viewer-owned playlists.

The interface must support:

- title;
- description where available;
- visibility;
- validation;
- submission;
- loading;
- success;
- failure;
- cancellation.

Use the canonical creation API.

Do not create local-only playlists that appear persisted.

Do not assign a fabricated playlist ID.

Prevent duplicate submissions.

After successful creation, reconcile with the authoritative server response and navigate or update the library according to the product flow.

---

# 24. Playlist Editing

Where supported, allow an authorized owner to edit playlist information.

Potential fields include:

- title;
- description;
- visibility.

The editor must:

- load authoritative initial values;
- validate fields;
- track changes;
- save;
- cancel/reset;
- handle conflicts;
- reconcile the server response.

Do not assume a viewer may edit a playlist because it appears in their recently opened list.

Use canonical permissions.

---

# 25. Playlist Visibility

Expose only visibility modes supported by the backend.

Potential modes include:

```text
public
unlisted
private
```

The actual model takes precedence.

When changing visibility:

- use canonical values;
- explain the effect where required;
- show pending state;
- handle failure;
- reconcile authoritative state.

Do not locally expose a private playlist as public before the server confirms the change.

Do not make privacy guarantees that contradict the actual backend access model.

---

# 26. Playlist Item Addition

Where supported, allow a viewer to add a video to an authorized playlist.

Implement a native-friendly playlist selector.

Support:

- loading available authorized playlists;
- current membership state;
- playlist selection;
- add action;
- success/failure;
- restricted/private playlist handling.

Use the canonical playlist-item mutation contract.

Do not expose playlists belonging to another viewer without authorization.

Do not assume every video may be added to every playlist.

---

# 27. Playlist Item Removal

Where supported, allow authorized viewers to remove a video from a playlist.

The implementation must:

- identify the correct playlist and item;
- submit the canonical mutation;
- prevent double submission;
- update state after confirmed success;
- preserve correct ordering;
- reconcile item counts;
- recover safely from failures.

Removing an item from one playlist must not remove it from unrelated playlists.

Do not delete the underlying video when only a playlist relationship should be removed.

---

# 28. Playlist Item Reordering

If the backend supports explicit playlist ordering, implement a native-accessible ordering interaction.

Support:

- current order;
- drag/reorder where suitable;
- keyboard/accessibility alternative where applicable;
- submit of the resulting order;
- loading;
- success;
- failure;
- reconciliation.

Do not send a mutation for every minor drag movement if a final-order submission is supported.

Do not create fake local ordering without persistence.

Do not use the visual order as proof that the backend accepted the change.

---

# 29. Playlist Mutation Concurrency

Handle conflicting operations such as:

```text
Add item
Remove item
Reorder items
Edit playlist
Change visibility
```

The UI must:

- disable incompatible actions where appropriate;
- maintain a consistent item identity;
- prevent stale responses from restoring an outdated list;
- refetch or reconcile server state after a conflict.

Do not allow a delayed reorder response to reintroduce a removed item.

Use version fields or concurrency tokens where provided.

---

# 30. Viewer Library

Implement a native viewer library for authenticated viewers.

A conceptual library may contain:

- History;
- Watch later;
- Liked videos;
- Personal playlists;
- Saved playlists where supported.

Only expose library categories backed by actual product contracts.

Do not populate empty library sections with fake content.

Do not confuse a viewer's personal library with the creator's public channel.

---

# 31. Library Navigation

Provide accessible native navigation between implemented library categories.

Support:

- active section;
- back navigation;
- refresh;
- direct navigation where supported;
- appropriate loading state;
- empty state;
- error state.

The selected subsection should remain consistent with the application's navigation conventions.

Do not present a nonfunctional category as a completed feature.

For categories that are part of later work, integrate an already existing implementation if available; otherwise keep this milestone bounded to supported behavior.

---

# 32. Watch History

Where supported, implement the native watch-history list.

Display authoritative history entries using the canonical model.

Support:

- appropriate ordering;
- video navigation;
- pagination;
- refresh;
- removal of individual entries where supported;
- clearing history where supported.

Do not create a separate mobile-only watch-history store.

Do not generate history from locally remembered navigation when the backend history contract is the authoritative source.

---

# 33. History Privacy

Watch history is sensitive viewer-specific data.

The implementation must ensure:

- only the authorized viewer can retrieve private history;
- user-specific cache keys are used;
- account switching invalidates the appropriate state;
- logout does not leave private history accessible through cached screens;
- history-related telemetry does not unnecessarily reveal viewing behavior.

Do not persist the complete authenticated history in ordinary local storage unless the project architecture explicitly requires and secures that behavior.

---

# 34. Remove History Item

Where supported, implement removal of individual history entries.

Support:

- an action associated with the correct entry;
- pending state;
- confirmed success;
- error handling;
- retry or revalidation as appropriate.

Do not permanently remove the item locally when the mutation has not succeeded, unless the interaction explicitly uses optimistic state with full rollback.

Do not accidentally remove an entire video's unrelated data or playlist membership.

---

# 35. Clear Watch History

Where the backend supports clearing history, implement the operation with appropriate confirmation.

The interface must:

- explain the action;
- require confirmation where appropriate;
- prevent duplicate submissions;
- show loading;
- submit the canonical request;
- reconcile the result;
- handle failures.

Do not clear local cache and treat that as confirmation that server history was deleted.

Do not assume the operation also pauses future history collection unless the backend defines that behavior.

---

# 36. Watch Later and Saved Content

Where supported, implement the watch-later or saved-video collection.

Support:

- loading;
- pagination;
- video navigation;
- remove saved item;
- empty state;
- error recovery.

Use the canonical saved-content contract.

Do not treat watch-later as a playlist unless the backend domain explicitly models it as one.

Do not create fake saved items.

---

# 37. Liked Videos

Where supported, implement the liked-video collection.

Support:

- loading;
- pagination;
- canonical video navigation;
- deleted or unavailable video states;
- reaction updates where the contract supports them.

The liked-video collection must remain consistent with the canonical video-reaction model.

Do not fabricate membership in the collection from a client-only reaction toggle.

Reconcile saved list state after confirmed reaction changes where necessary.

---

# 38. Viewer-Owned Playlists

Where supported, display playlists created or owned by the current viewer.

Each playlist item should display available fields such as:

- title;
- thumbnail;
- visibility;
- item count;
- updated time.

Support:

- creation entry point;
- opening a playlist;
- editing where permitted;
- deletion where explicitly supported.

Do not expose another user's private playlist because it appears in a stale cache.

Do not assume ownership without the authoritative permission or owner context.

---

# 39. Library Pagination

Use the backend's established pagination contract.

Support:

- initial page;
- next page;
- loading indicator;
- retry;
- end-of-collection;
- duplicate prevention;
- stale-response protection.

Do not load unlimited history or saved-video collections in one request.

Do not mix entries from different viewers or collection types.

Keep previously loaded items usable when a subsequent page fails.

---

# 40. Refresh and Cache Strategy

Use the application's established server-state library.

Implement appropriate refresh behavior for:

- channel data;
- channel content;
- playlists;
- history;
- watch later;
- liked videos;
- viewer-owned playlists.

Use targeted invalidation after mutations.

Do not refetch every channel, playlist, and library collection after a single item is removed.

Keep cache keys associated with the relevant canonical entity IDs and viewer context.

Do not serve private viewer data through a public/shared cache.

---

# 41. Account Switching

When authentication changes from one user to another:

- invalidate subscription state;
- invalidate viewer-owned playlists;
- invalidate watch history;
- invalidate saved/watch-later state;
- invalidate liked-video state;
- clear pending private mutations;
- clear private screen state where necessary;
- reload the correct viewer's library.

No private collection from the previous account may remain visible after another account signs in.

Do not rely solely on route remounting to guarantee cache isolation.

---

# 42. Authentication Expiration

Handle session expiration during:

- opening a library category;
- loading history;
- updating a subscription;
- creating or modifying a playlist;
- removing saved content;
- deleting history entries.

Use the canonical session-refresh or logout flow.

Do not retry an unauthorized mutation indefinitely.

Do not silently continue showing private library data after the backend rejects the viewer's session.

Preserve safe unsaved form data when appropriate, but never preserve credentials as normal form state.

---

# 43. Offline and Network Recovery

The mobile app must handle temporary disconnection during browsing and mutations.

Support:

- network failure feedback;
- retry for safe reads;
- stale-data presentation where the caching strategy supports it;
- controlled revalidation after connectivity returns;
- duplicate-request prevention;
- preservation of safe local UI state.

Do not claim private collections can be accessed offline unless that feature has actually been implemented and validated.

If a mutation's outcome is uncertain after a timeout, reconcile with authoritative server state before repeating a potentially non-idempotent operation.

---

# 44. State Ownership

Separate state clearly.

### Server state

- channel metadata;
- channel content;
- subscription status;
- playlist records;
- playlist items;
- permissions;
- watch history;
- saved content;
- liked videos.

### Local UI state

- selected channel section;
- open menu;
- current editor values;
- confirmation dialogs;
- playlist-selection dialog;
- reorder interaction state;
- temporary validation messages.

### Navigation state

- canonical channel ID;
- canonical playlist ID;
- supported library subsection;
- supported pagination/navigation parameters.

Do not put all state into one global store.

Do not treat cached values as authoritative after a mutation succeeds.

---

# 45. Mutation Safety

Protect against conflicting operations such as:

```text
Subscribe
Unsubscribe
Subscribe again
```

or:

```text
Remove playlist item
Reorder playlist
Add the same item again
```

Use stable IDs, pending-state controls, and server reconciliation.

Prevent an older response from overwriting a newer confirmed subscription or playlist state.

Use idempotency support where provided by the backend.

Do not treat network timeouts as proof that the server rejected a mutation.

---

# 46. Native Accessibility

The channel and library experience must be accessible on iOS and Android.

Implement:

- semantic screen names;
- accessible channel tabs;
- labelled video and playlist cards;
- accessible subscription controls;
- accessible playlist editor controls;
- accessible confirmation dialogs;
- keyboard navigation where applicable;
- screen-reader announcements for important state changes;
- appropriate roles and states;
- sufficient touch targets;
- text scaling;
- visible focus feedback where supported.

For playlist ordering, provide an accessible alternative to drag-and-drop.

Do not communicate privacy, visibility, or subscription state through color alone.

---

# 47. Responsive Layout and Native Behavior

Adapt the experience to:

- compact phones;
- large phones;
- tablets;
- portrait and landscape layouts where appropriate.

Handle:

- safe areas;
- status/navigation bars;
- long text;
- dynamic font sizes;
- keyboard behavior;
- native back gestures;
- scrolling and refresh gestures.

Do not create separate iOS and Android screen implementations unless a genuine platform-specific requirement justifies them.

Use shared components where practical while respecting native platform conventions.

---

# 48. Performance

Optimize for:

- channel content lists;
- large personal playlists;
- lengthy history;
- saved-video collections;
- image-heavy cards;
- pagination;
- cache updates;
- repeated navigation between channels and playlists.

Requirements:

- use stable list keys;
- virtualize large collections appropriately;
- avoid rendering every item at once;
- avoid rerendering entire lists after a local menu change;
- bound memory retention;
- avoid fetching unrelated library categories eagerly.

Do not use expensive abstraction or virtualization where it is unnecessary.

---

# 49. Security

The implementation must:

- use secure session integration;
- respect server-side authorization;
- avoid open redirects;
- safely render untrusted channel and playlist text;
- avoid unsafe HTML;
- prevent private playlist exposure;
- protect viewer-specific state;
- avoid logging session credentials;
- validate route targets;
- avoid sharing signed media URLs.

Client-side permission checks are a UI boundary, not authoritative security.

The backend remains authoritative for channel, playlist, subscription, history, and saved-content permissions.

---

# 50. Privacy

Protect sensitive viewer information, including:

- watch history;
- liked videos;
- private playlists;
- watch-later collections;
- private subscription state.

Do not expose private data through:

- public metadata;
- shared caches;
- navigation parameters;
- logs;
- telemetry;
- screenshots generated by automated infrastructure containing unintended sensitive test data.

Do not send complete viewing history to analytics unless explicitly authorized by the canonical privacy contract.

---

# 51. Analytics and Telemetry

Use the established analytics event model.

Potential events include:

```text
mobile_channel_opened
mobile_channel_section_selected
mobile_channel_video_selected
mobile_channel_subscribed
mobile_channel_unsubscribed
mobile_playlist_opened
mobile_playlist_created
mobile_playlist_updated
mobile_playlist_item_added
mobile_playlist_item_removed
mobile_playlist_reordered
mobile_library_opened
mobile_library_section_viewed
mobile_history_item_removed
mobile_history_cleared
mobile_watch_later_item_added
mobile_watch_later_item_removed
mobile_liked_videos_opened
```

Use canonical names where supplied by the platform.

Prevent duplicate events due to navigation remounts, cache refreshes, or mutation retries.

Do not emit credentials, private playlist contents, full watch history, or unnecessary viewer identifiers.

Separate the viewer's action from the authoritative server outcome.

---

# 52. Testing Strategy

Implement automated tests for real behavior.

### Unit tests

Cover:

- subscription-state transitions;
- playlist permission mapping;
- playlist item ordering;
- history-removal state;
- collection pagination;
- cache-key generation;
- viewer identity isolation;
- account-switch invalidation;
- mutation rollback;
- stale-response protection;
- telemetry construction.

### Component tests

Cover:

- channel header;
- channel navigation;
- video cards;
- channel cards;
- subscription control;
- playlist header;
- playlist item;
- playlist editor;
- playlist selector;
- reorder controls;
- library navigation;
- history item;
- saved-video item;
- liked-video item;
- empty/error states.

### Integration tests

Cover:

- opening a public channel;
- switching channel sections;
- loading channel content;
- subscribing and unsubscribing;
- opening a playlist;
- creating and editing a playlist;
- adding and removing playlist items;
- reordering items where supported;
- loading viewer library;
- loading watch history;
- removing a history entry;
- clearing history where supported;
- loading saved/watch-later content;
- loading liked videos;
- handling session expiration;
- account switching;
- cache invalidation.

### End-to-end tests

At minimum:

1. open a public channel;
2. browse channel content;
3. open a video from the channel;
4. subscribe to the channel;
5. unsubscribe;
6. open a playlist;
7. open a playlist item;
8. create a playlist where supported;
9. add a video to a playlist;
10. remove an item;
11. reorder items where supported;
12. open the viewer library;
13. inspect history;
14. remove a history entry;
15. open a supported saved-content collection;
16. test anonymous access to public channel content;
17. verify private library access requires authentication;
18. switch accounts and verify data isolation;
19. verify keyboard/screen-reader labels for essential controls;
20. simulate a network failure and verify safe recovery.

Use controlled mocks for isolated testing only. Production functionality must use the real project's API contracts.

---

# 53. iOS and Android Compatibility

Validate the supported iOS and Android environments.

Pay particular attention to:

- native navigation;
- scrolling;
- pull-to-refresh;
- safe areas;
- bottom sheets and dialogs;
- text scaling;
- keyboard interaction;
- large-list performance;
- accessibility;
- account-switch behavior.

Do not assume that an implementation tested on one platform is automatically correct on the other.

Use platform-specific code only when required by genuine native behavior.

---

# 54. Dependency Discipline

Before adding dependencies:

- inspect installed libraries;
- verify React Native compatibility;
- verify iOS and Android support;
- inspect native configuration requirements;
- avoid duplicate list, dialog, form, navigation, and state-management libraries.

Do not introduce a new library solely for a feature that is already supported by the existing design system.

Document required native configuration changes.

---

# 55. Documentation

Update documentation covering:

- channel routes and sections;
- subscription integration;
- playlist model and permissions;
- playlist item management;
- playlist ordering;
- viewer library;
- history and saved-content APIs;
- pagination and cache behavior;
- account-switch isolation;
- privacy/security rules;
- telemetry;
- accessibility;
- testing.

Documentation must describe the real implementation.

Do not document unsupported backend functionality as complete.

---

# 56. No Fake Channel, Playlist, or Library Behavior

Do not create:

- hardcoded production channels;
- fake subscriber counts;
- simulated subscriptions;
- fake playlists;
- fabricated playlist items;
- fake history records;
- invented liked videos;
- simulated persistence;
- fake visibility updates;
- hardcoded permissions.

Mocks are permitted only within controlled automated tests.

The actual application must use real backend integration boundaries.

---

# 57. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- fake playlist editors;
- nonfunctional reorder controls;
- placeholder history;
- empty subscription handlers;
- fake saved-content persistence;
- incomplete error states;
- dummy channel tabs;
- actions without behavior;
- “implement later” sections within the current scope.

Everything required by this prompt must be genuinely implemented.

Features unsupported by backend contracts must be documented as integration dependencies rather than represented by fake functionality.

---

# 58. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- native builds where available;
- channel-page loading;
- channel-section navigation;
- subscription mutations;
- playlist loading;
- playlist creation/editing where supported;
- playlist item addition/removal;
- item reordering where supported;
- library navigation;
- watch-history loading and mutations;
- saved-content collections where supported;
- account-switch isolation;
- cache invalidation;
- session expiration;
- privacy/security requirements;
- accessibility;
- iOS/Android behavior where the environment supports validation.

Fix issues within this scope rather than merely reporting them.

Do not claim a native build or backend capability passed validation unless it actually did.

If the available toolchain prevents platform-specific validation, report the exact blocker and complete all possible local checks.

---

# 59. Definition of Done

This prompt is complete only when:

- native channel pages work;
- channel identity and metadata render correctly;
- supported channel sections work;
- channel content pagination works;
- subscription controls work;
- subscription state is consistent;
- playlist viewing works;
- playlist items render in canonical order;
- playlist navigation works;
- playlist creation/editing works where supported;
- visibility controls work where supported;
- playlist item addition/removal works where supported;
- ordering works where supported;
- viewer library works;
- history works where supported;
- history removal/clearing works where supported;
- watch-later/saved content works where supported;
- liked-video collection works where supported;
- viewer-owned playlists work where supported;
- pagination and refresh work;
- mutations are race-safe;
- account-specific state is isolated;
- logout and account switching do not leak private data;
- privacy/security requirements are respected;
- native accessibility requirements are implemented;
- responsive layouts work;
- automated tests cover the defined behavior;
- documentation is updated;
- no fake production behavior remains;
- no current-scope placeholders remain;
- validation passes to the extent possible in the available environment.

---

# 60. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize channel pages, subscription management, playlists, library, watch history, and saved-content functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List channel, subscription, playlist, playlist-item, history, saved-content, liked-content, pagination, authorization, and analytics contracts consumed.

### State and Caching

Summarize account isolation, cache keys, mutation reconciliation, pagination, and account-switch invalidation.

### Testing

List tests created and tests executed.

### Validation

Report TypeScript, linting, native builds, and actual iOS/Android runtime checks.

### Integration Notes

Identify missing backend contracts, external dependencies, platform-specific limitations, or configuration requirements.

### Out of Scope

Confirm that backend channel, subscription, playlist, history, recommendation, media, monetization, notification, and moderation services were not improperly implemented.

---

# 61. Final Execution Directive

Execute this prompt as a concrete native mobile implementation task.

Do not merely describe the channel, playlist, or library experience.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate channels, subscriptions, playlists, history, saved content, permissions, or persistence.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated mobile or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style native mobile channel, subscription, playlist, and viewer-library experience for iOS and Android**, integrated with the platform's canonical backend contracts.
