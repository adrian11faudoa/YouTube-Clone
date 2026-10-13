# YouTube-Style Video Platform — Frontend Prompt — Volume 2

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **watch experience and playback experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone within the overall project.

Your responsibility in this prompt is the **web watch experience, production video player, playback state, video-detail interactions, playback persistence, and the associated frontend infrastructure and tests** required for that scope.

Do not implement unrelated frontend domains.

Do not implement backend services.

Do not invent fake backend behavior.

Do not use placeholder implementations for required functionality.

---

# 2. Project Context

The product is a production-grade YouTube-style video platform supporting:

* long-form video;
* short-form video;
* public, unlisted, private, scheduled, and restricted content;
* channels;
* subscriptions;
* comments;
* reactions;
* playlists;
* watch history;
* playback progress;
* search and discovery;
* recommendations;
* notifications;
* creator analytics;
* live streaming;
* moderation;
* administration;
* monetization-capable infrastructure;
* web and mobile clients.

The web stack is:

* TypeScript;
* React;
* Next.js App Router;
* modern browser APIs;
* responsive desktop/tablet/mobile web;
* typed API clients;
* server/client state separation;
* production-grade observability;
* automated testing.

The target system must remain compatible with a large-scale consumer video platform.

The frontend must be designed for:

* millions of video views;
* large concurrent playback demand;
* high-frequency navigation;
* unreliable client networks;
* interrupted playback;
* adaptive media delivery;
* authenticated and unauthenticated viewers;
* accessibility requirements;
* privacy requirements;
* strong performance requirements.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh Claude conversation.

Do not assume access to:

* previous Claude conversations;
* previous AI responses;
* hidden architectural decisions;
* undocumented API behavior;
* hidden generated files;
* a shared filesystem;
* a shared repository.

If a repository is present, inspect it before modifying it.

If repository state is present and conflicts with this prompt, preserve existing compatible functionality while implementing this scope and document material contract conflicts instead of silently creating incompatible behavior.

If portable architecture or API artifacts are supplied with the project, use them as authoritative project contracts.

If those artifacts are not available, use the explicit contracts and invariants defined in this prompt.

---

# 4. Primary Objective

Implement the complete web watch experience for video playback.

The completed frontend must provide a coherent production experience for:

1. opening a video;
2. loading video metadata;
3. initializing playback;
4. selecting an appropriate media source;
5. playing and pausing;
6. seeking;
7. changing playback quality;
8. selecting playback speed;
9. captions/subtitles;
10. volume and mute;
11. fullscreen;
12. picture-in-picture where supported;
13. playback progress synchronization;
14. watch-history integration;
15. autoplay behavior;
16. related-video navigation;
17. video metadata presentation;
18. channel subscription controls;
19. video reaction controls;
20. sharing;
21. reporting entry points;
22. responsive watch layouts;
23. keyboard accessibility;
24. graceful loading and failure states;
25. telemetry and observability.

The implementation must be real and integrated.

---

# 5. Explicit Scope

This prompt includes:

* watch route;
* video data loading;
* production video-player architecture;
* media-source selection;
* playback state management;
* adaptive playback integration;
* playback controls;
* captions;
* quality selection;
* playback speed;
* fullscreen;
* picture-in-picture where supported;
* buffering state;
* playback errors;
* retry behavior;
* resume playback;
* playback progress;
* watch-history synchronization;
* autoplay;
* related-video presentation;
* video information;
* engagement controls directly attached to the watch page;
* channel identity and subscription controls;
* share functionality;
* report entry point;
* responsive behavior;
* accessibility;
* performance;
* analytics/telemetry integration;
* error boundaries;
* automated testing;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* backend video-processing services;
* transcoding workers;
* object-storage infrastructure;
* CDN infrastructure;
* search backend;
* recommendation backend;
* comment backend;
* moderation backend;
* live-stream backend;
* monetization backend;
* creator studio;
* full search UI;
* notification center;
* mobile applications;
* administrative dashboards;
* payment checkout;
* advertising exchange infrastructure;
* unrelated account-management redesign;
* new backend APIs merely to simplify frontend implementation.

Do not create duplicate APIs when an existing project contract can support the required behavior.

---

# 7. Watch Route Contract

Implement a canonical watch route equivalent to:

```text
/watch?v={videoId}
```

The implementation may use the project's established routing convention if one already exists, but the user-facing route must support direct navigation to a specific video.

The route must correctly handle:

* missing video ID;
* malformed video ID;
* inaccessible video;
* deleted video;
* private video;
* unavailable video;
* processing/not-ready video;
* age/restriction states where applicable;
* published video;
* scheduled-but-not-yet-public video;
* authenticated viewer;
* anonymous viewer.

The route must be deep-linkable and refresh-safe.

Do not depend exclusively on client-side navigation state for identifying the video.

---

# 8. Video Data Contract

The watch page must consume a typed video-detail representation.

At minimum, the frontend representation must support:

```text
videoId
title
description
channel
channelId
channelDisplayName
channelAvatar
channelVerificationState
thumbnail
duration
publishedAt
visibility
availability
viewCount
likeCount
dislikeState or equivalent reaction state
viewerReaction
viewerSubscriptionState
viewerPermissions
mediaAvailability
playbackPolicy
captionsAvailability
liveState
restrictionState
relatedVideoCandidates
```

The actual property names must match the project's authoritative API contract when available.

Do not create parallel incompatible domain models for the same backend entity.

Normalize external API responses into the frontend domain layer only when that improves maintainability.

---

# 9. Watch API Integration

Create a typed watch-page data-access layer.

It must distinguish between:

* video metadata;
* playback authorization/media information;
* viewer-specific state;
* related-video information;
* playback progress;
* watch-history behavior.

Do not combine unrelated requests into an unmaintainable single client abstraction.

The data layer must support:

* cancellation;
* request deduplication where appropriate;
* aborting stale requests;
* typed success responses;
* typed error responses;
* authentication-aware behavior;
* retry policies appropriate to operation type.

Do not automatically retry deterministic authorization failures or invalid requests.

---

# 10. Server and Client Rendering Strategy

Use Next.js App Router appropriately.

The implementation must deliberately decide which watch-page content is:

* server-rendered;
* client-rendered;
* progressively hydrated.

Video playback itself must remain client-side because it depends on browser media APIs.

Metadata that benefits from server rendering should remain server-renderable where practical.

Avoid converting the entire watch page into an unnecessary client-only application.

The implementation must preserve:

* initial navigation performance;
* metadata discoverability;
* stable URL behavior;
* predictable hydration;
* fast time to interactive.

---

# 11. Watch Page Layout

Implement a responsive watch layout consisting of:

### Primary content area

* video player;
* title;
* channel identity;
* subscription control;
* view/date metadata;
* reactions;
* sharing;
* additional video actions;
* expandable description.

### Secondary content area

* related/recommended video list;
* compact video cards;
* navigation to another video.

The layout must support:

* desktop;
* tablet;
* mobile web.

At desktop widths, the player and primary watch content must remain visually dominant.

At smaller widths, the experience must collapse naturally into a single-column layout.

Do not create fixed-width desktop behavior.

---

# 12. Production Video Player Architecture

Implement the player as a reusable component system rather than a monolithic page component.

Use separations such as:

```text
VideoPlayer
  ├── MediaEngine
  ├── PlayerState
  ├── PlayerControls
  ├── ProgressBar
  ├── QualityMenu
  ├── CaptionMenu
  ├── PlaybackRateMenu
  ├── VolumeControl
  ├── FullscreenControl
  ├── PictureInPictureControl
  └── PlayerErrorOverlay
```

The exact file structure may vary, but responsibilities must remain clear.

The player architecture must permit:

* source replacement;
* adaptive streaming;
* telemetry;
* controlled playback state;
* testability;
* future DRM or protected-content integration if required by the platform architecture;
* browser capability detection.

---

# 13. Media Source Integration

The frontend must consume the media/playback contract rather than constructing media URLs from undocumented conventions.

The playback contract must support, where supplied by the backend:

* HLS manifests;
* DASH manifests where applicable;
* progressive fallback only where explicitly supported;
* signed media URLs;
* tokenized access;
* playback authorization metadata;
* expiration;
* available renditions.

Create a media-source abstraction such as:

```text
PlaybackSource
PlaybackManifest
PlaybackAuthorization
PlaybackRendition
CaptionTrack
```

Use the authoritative backend naming when available.

Do not expose privileged storage credentials to the browser.

Do not generate unsigned private media URLs client-side.

---

# 14. Adaptive Streaming

Implement adaptive streaming through a maintainable browser-compatible playback layer.

The implementation must account for:

* browsers with native HLS support;
* browsers requiring JavaScript-based streaming support;
* manifest loading failures;
* rendition errors;
* network changes;
* buffering;
* stalled playback;
* unsupported formats.

Select a mature maintained playback implementation appropriate for the technology stack.

Do not write a custom HLS/DASH engine.

The player must be capable of beginning playback without waiting for every possible rendition to download.

---

# 15. Playback State Model

Define a typed player state model.

At minimum support states equivalent to:

```text
idle
loading
ready
playing
paused
buffering
seeking
ended
error
unsupported
```

Track at minimum:

```text
currentTime
duration
bufferedTime
volume
muted
isFullscreen
isPictureInPicture
playbackRate
selectedQuality
selectedCaptionTrack
isAutoplayEnabled
isPlaying
isBuffering
```

Player state must have one clear owner.

Avoid duplicated state between:

* React component state;
* global state;
* media element state;
* server cache.

The HTML media element remains the authoritative source for actual browser playback position/state where appropriate.

---

# 16. Playback Controls

Implement production playback controls for:

* play/pause;
* seek forward/backward;
* progress timeline;
* volume;
* mute;
* fullscreen;
* picture-in-picture;
* playback rate;
* quality;
* captions;
* autoplay;
* remaining-duration/current-time display.

Controls must correctly respond to:

* mouse;
* touch;
* keyboard;
* media-element events;
* programmatic navigation.

Controls must not trigger accidental duplicate actions caused by bubbling or repeated event subscriptions.

---

# 17. Progress Timeline

Implement a high-quality progress timeline supporting:

* current playback position;
* buffered range;
* seeking;
* keyboard navigation;
* pointer interaction;
* touch interaction;
* accessible labels;
* duration display.

The timeline must not generate an API call for every animation frame.

Separate high-frequency local playback state from lower-frequency persistence.

Do not persist playback position on every render.

---

# 18. Seeking Behavior

Seeking must support:

* forward seeks;
* backward seeks;
* drag seeking;
* keyboard seeking;
* programmatic resume;
* source changes.

During an active seek:

* prevent stale progress persistence from overwriting the new target;
* display coherent UI state;
* synchronize the player once the seek completes;
* recover cleanly when the media engine rejects a seek.

For remote streams or partially available content, respect the media source's seekability constraints.

---

# 19. Playback Quality

Implement a quality-selection UI when the media contract exposes multiple renditions.

Support:

* Auto;
* available video qualities;
* currently selected rendition;
* unavailable/unsupported options;
* loading state when quality changes;
* graceful fallback to Auto.

Do not invent quality levels.

Use the actual available renditions returned by the playback contract.

Quality switching must avoid unnecessary playback interruption.

---

# 20. Playback Speed

Implement playback-rate selection.

Support a sensible set of rates exposed through the player configuration, for example:

```text
0.25x
0.5x
0.75x
1x
1.25x
1.5x
1.75x
2x
```

The final supported set may be restricted by product requirements or browser capabilities.

Persist the user's preferred playback speed locally where appropriate.

Do not persist sensitive account data in uncontrolled storage.

---

# 21. Captions and Subtitles

Implement caption-track discovery and selection.

Support:

* captions off;
* available caption languages;
* active track;
* loading/failure state;
* keyboard-accessible selection.

Use the playback contract for available caption tracks.

The UI must not assume every video has captions.

Caption-track availability must be represented independently from video metadata so that the player can respond to the actual playback manifest.

---

# 22. Fullscreen

Implement browser fullscreen behavior.

Handle:

* entering fullscreen;
* exiting fullscreen;
* browser/browser-engine differences;
* orientation behavior where applicable;
* keyboard escape behavior;
* state synchronization when fullscreen changes outside the component.

The UI must reflect actual browser fullscreen state rather than assuming the requested action succeeded.

---

# 23. Picture-in-Picture

Support Picture-in-Picture where browser capability exists.

The implementation must:

* detect browser support;
* expose the control conditionally;
* handle enter/exit events;
* remain stable when unavailable;
* avoid throwing when the API is unsupported.

Do not polyfill unsupported browser APIs with unsafe hacks.

---

# 24. Autoplay

Implement controlled autoplay behavior.

Autoplay rules must respect browser restrictions.

The application must not assume that autoplay is always permitted.

Support:

* initial autoplay where policy allows;
* muted autoplay behavior where appropriate;
* autoplay enable/disable state;
* transition to the next recommended video only when the product behavior explicitly requires it;
* cancellation when the user navigates away.

User-initiated interaction must take precedence over an automated autoplay transition.

---

# 25. Resume Playback

For authenticated viewers, retrieve stored playback progress using the project's playback-progress contract.

For anonymous viewers, use a local persistence mechanism appropriate for non-sensitive playback progress.

Implement:

* resume prompt or automatic resume according to product UX;
* reset-to-beginning behavior;
* near-end handling;
* stale progress handling;
* video-version/source changes;
* progress belonging to the correct video ID.

Do not resume a different video's position accidentally because of cache-key collisions.

---

# 26. Playback Progress Persistence

Persist playback progress using a controlled cadence.

The implementation must support:

* initial progress retrieval;
* progress updates;
* paused-state persistence;
* page visibility changes;
* player unmount;
* navigation away;
* near-end completion;
* retry after transient network failure.

Use throttling/debouncing where appropriate.

Do not issue a request on every `timeupdate` event.

The client must preserve the most recent meaningful progress locally until the server acknowledges it where appropriate.

---

# 27. Watch History Integration

Integrate the watch experience with the watch-history contract.

The implementation must distinguish:

* opening a video;
* beginning playback;
* meaningful viewing;
* completion;
* explicit history updates.

History writes must be idempotent or otherwise safely repeatable according to the backend contract.

Do not record multiple duplicate history entries merely because React re-rendered or the page remounted.

For privacy-sensitive behavior, honor the viewer's configured history state.

---

# 28. Playback Telemetry

Implement structured playback telemetry using the project's analytics contract.

Relevant events may include:

```text
video_watch_opened
video_play_started
video_played
video_paused
video_seek_started
video_seek_completed
video_buffer_started
video_buffer_recovered
video_playback_error
video_quality_changed
video_caption_changed
video_playback_rate_changed
video_entered_fullscreen
video_exited_fullscreen
video_entered_picture_in_picture
video_completed
video_watch_abandoned
```

Use the project's canonical event names when they are provided.

Every telemetry event must include sufficient context to be useful without leaking unnecessary personal data.

Avoid sending excessively high-frequency telemetry.

Aggregate or sample events where appropriate.

---

# 29. Engagement Controls

Implement watch-page controls for:

* like;
* dislike or equivalent negative reaction if supported by the product contract;
* subscription;
* share;
* additional actions;
* report entry point.

The UI must accurately represent:

* current viewer state;
* loading state;
* success state;
* failure state;
* unauthenticated state;
* authorization restrictions.

Do not optimistically change state unless rollback behavior is fully implemented.

For optimistic operations, preserve the previous state and restore it on failure.

---

# 30. Subscription Control

The watch page must expose the channel subscription control.

Support:

* subscribed;
* not subscribed;
* pending request;
* failure;
* unauthenticated interaction;
* channel-disabled/restricted cases where applicable.

The UI must use the canonical subscription contract rather than deriving subscription state from cached channel counts.

Channel subscriber counts should not be assumed to be perfectly synchronized with an individual viewer's subscription state.

---

# 31. Reaction Controls

Implement video reactions according to the project's canonical reaction model.

Support:

* current viewer reaction;
* loading;
* success;
* failure;
* removal/change of reaction;
* inaccessible video.

Do not blindly increment server-provided counts locally without handling concurrency or failed mutations.

Where counts are presented optimistically, establish clear rollback behavior.

---

# 32. Share Experience

Implement sharing behavior appropriate to the web application.

Support:

* copying the watch URL;
* native Web Share API when available;
* fallback copy behavior;
* success feedback;
* failure feedback.

The copied URL must represent the canonical watch route.

Never expose internal API URLs, signed storage URLs, or authorization tokens through sharing.

---

# 33. Report Entry Point

Expose a report action when the viewer has permission to report the content.

The watch frontend must provide the entry point and interaction shell required by the moderation/reporting contract.

Support:

* unauthenticated restriction if required;
* authenticated report flow;
* category selection if the API requires it;
* validation;
* submission;
* success state;
* failure state.

Do not implement moderation decisions inside the frontend.

---

# 34. Description and Metadata

Implement expandable video metadata.

At minimum show:

* title;
* channel;
* publication date;
* views;
* reactions;
* description;
* relevant restrictions/disclosures supplied by the backend.

The description must support:

* long text;
* links according to safe URL rules;
* truncation/expansion;
* responsive layouts.

Do not render untrusted HTML directly.

Apply safe text rendering and URL handling.

---

# 35. Related Videos

Implement the related-video presentation area.

The frontend consumes candidates supplied by the discovery/recommendation contract.

Each card must support:

* thumbnail;
* duration where applicable;
* title;
* channel;
* view count;
* relative/absolute publication information;
* navigation.

The frontend must not implement recommendation ranking logic.

Support:

* loading;
* empty;
* partial;
* error;
* fallback states.

A recommendation service failure must not make the current video unplayable.

---

# 36. Navigation Between Videos

When a related video is selected:

* update the canonical route;
* dispose or replace the previous player source safely;
* reset video-specific local state;
* fetch the new video's data;
* load the new playback source;
* restore applicable viewer preferences;
* prevent stale telemetry from being attributed to the new video.

Race conditions between previous and new video requests must be prevented.

---

# 37. Player Cleanup and Resource Management

Ensure complete cleanup when a video changes or the page unmounts.

Clean up:

* media-source instances;
* event listeners;
* timers;
* animation frames;
* subscriptions;
* abort controllers;
* telemetry flush timers;
* progress persistence timers;
* object URLs where created;
* player-library resources.

Memory leaks are unacceptable.

Repeated navigation between many videos must not cause unbounded browser memory growth.

---

# 38. Playback Failure Handling

Create explicit error categories for:

* unsupported media;
* authorization failure;
* expired media authorization;
* manifest failure;
* network failure;
* decoding failure;
* playback stalled;
* source unavailable;
* restricted content;
* unknown player failure.

User-facing messages must be understandable without exposing internal diagnostics.

Provide appropriate retry behavior.

Do not endlessly retry a permanently unavailable source.

Where practical, distinguish recoverable from terminal playback failures.

---

# 39. Network and Offline Behavior

The watch experience must handle:

* slow connections;
* temporary disconnections;
* network changes;
* background/foreground transitions;
* offline navigation.

Do not claim that video can continue offline unless the architecture explicitly supports offline media.

Playback progress and telemetry should degrade gracefully while disconnected and reconcile when connectivity returns, subject to the project's contracts.

---

# 40. Authentication-Aware Behavior

The watch page must work for anonymous viewers when the content is public.

Anonymous viewers must still be able to:

* navigate;
* play public videos;
* use supported non-authenticated features.

Authentication should only be required for operations that actually require an account, such as:

* subscription;
* reactions;
* private history synchronization;
* protected playback;
* reporting where policy requires authentication.

Do not redirect public viewers to login simply because an authenticated-only control is present.

---

# 41. Loading, Empty, and Error States

Every asynchronous watch-page section must define:

### Loading

Use meaningful skeletons or reserved layout regions.

### Empty

Examples:

* no related videos;
* no description;
* no captions.

### Error

Examples:

* metadata unavailable;
* playback unavailable;
* related videos failed;
* viewer state unavailable.

Each failure must be isolated where possible.

A related-video error must not replace the entire watch page.

A reaction API error must not destroy the player.

---

# 42. Accessibility

The watch experience must meet production accessibility expectations.

Implement:

* semantic controls;
* keyboard navigation;
* visible focus states;
* screen-reader labels;
* accessible menus;
* accessible sliders;
* accessible dialogs;
* captions controls;
* appropriate live-region feedback;
* sufficient touch targets;
* reduced-motion support where relevant.

The player must remain usable without a mouse.

Keyboard shortcuts must not interfere with text-entry fields.

---

# 43. Responsive Behavior

Support at minimum:

* mobile web;
* tablet;
* desktop;
* large desktop.

Do not depend on fixed viewport dimensions.

The player must preserve appropriate aspect ratio.

The watch page must avoid cumulative layout shift caused by late image or player sizing.

Related-video cards must adapt to available width.

Controls must remain usable on touch devices.

---

# 44. Performance

Optimize for:

* fast initial navigation;
* low JavaScript cost before playback;
* minimal unnecessary hydration;
* lazy loading of below-the-fold related content where appropriate;
* stable player initialization;
* efficient image loading;
* efficient state updates;
* no unnecessary global rerenders.

Do not use expensive React state updates for every media-element event when a lower-level mechanism is sufficient.

Measure and avoid:

* excessive renders;
* long tasks;
* memory leaks;
* event-listener accumulation;
* unnecessary API calls;
* duplicate requests.

---

# 45. Caching

Use the project's established server-state/cache mechanism.

Cache behavior must distinguish between:

* relatively stable video metadata;
* rapidly changing viewer state;
* playback progress;
* related-video results;
* reaction state;
* subscription state;
* playback authorization.

Do not cache signed playback URLs beyond their valid lifetime.

Do not use stale viewer-specific state as if it were authoritative.

Cache keys must include all relevant identifiers and viewer context.

---

# 46. URL and State Synchronization

The watch page must maintain stable URL semantics.

Do not encode large amounts of transient player state into the URL.

The URL may represent durable navigation state such as:

* video ID;
* supported watch parameters explicitly defined by the product.

Player state such as volume, playback speed, and fullscreen status should not unnecessarily mutate browser history.

Back/forward navigation must remain predictable.

---

# 47. Security Requirements

The frontend implementation must:

* never expose secrets;
* never expose privileged storage credentials;
* avoid unsafe HTML injection;
* validate untrusted URL values;
* handle API errors without leaking sensitive backend details;
* use secure authentication mechanisms already defined by the project;
* respect authorization state;
* avoid storing sensitive credentials in insecure browser storage;
* prevent accidental disclosure of signed media URLs through logs or analytics.

Do not log access tokens.

Do not log authorization headers.

Do not emit sensitive query parameters to analytics.

---

# 48. Privacy

Respect project-wide privacy controls.

Playback telemetry must minimize personal information.

Watch history must follow user privacy settings.

Authenticated viewer identifiers must not be embedded into publicly visible URLs.

Local persistence must only contain data appropriate for browser storage.

Do not persist private video metadata unnecessarily.

---

# 49. Observability

Integrate frontend observability for:

* watch-page load errors;
* player initialization failures;
* playback failures;
* API failures;
* major user interaction failures;
* unhandled exceptions.

Use structured diagnostics.

Where the project supports correlation/request IDs, propagate them through API requests appropriately.

Do not capture secrets or sensitive media authorization values in diagnostics.

---

# 50. Error Boundaries

Implement appropriate React/Next.js error boundaries around:

* watch page;
* player;
* related-video area;
* engagement controls where isolation is useful.

The player failure state must remain recoverable where technically possible.

Provide a clear retry path.

Avoid replacing the entire application shell because one watch-page child failed.

---

# 51. Testing Strategy

Implement tests for the complete scope.

At minimum include:

### Unit tests

* player state transitions;
* playback utilities;
* quality selection logic;
* caption selection;
* playback-rate persistence;
* progress-throttling logic;
* watch-history rules;
* URL handling;
* telemetry event construction;
* retry classification.

### Component tests

* player controls;
* progress timeline;
* quality menu;
* caption menu;
* player error state;
* reaction controls;
* subscription control;
* share UI;
* metadata expansion;
* related-video cards.

### Integration tests

* watch-page data loading;
* playback-source initialization;
* authenticated viewer state;
* playback progress synchronization;
* watch-history integration;
* video navigation;
* failure recovery.

### End-to-end tests

Cover at minimum:

1. open a public video;
2. start playback;
3. pause;
4. seek;
5. change quality;
6. change playback speed;
7. enable captions where available;
8. subscribe;
9. react to the video;
10. share the video;
11. navigate to a related video;
12. recover from a transient API/playback failure;
13. preserve accessibility-critical player operations;
14. verify authenticated playback-progress behavior where test infrastructure permits.

Do not replace tests with screenshots alone.

---

# 52. Browser Compatibility

Validate behavior across the browser support matrix established by the project.

Where browser media APIs differ:

* isolate browser-specific code;
* use feature detection;
* avoid user-agent sniffing where capability detection is sufficient;
* provide safe fallbacks.

The application must not crash when optional APIs such as Picture-in-Picture are unavailable.

---

# 53. Data Race Prevention

Protect against stale asynchronous results.

Example race:

```text
Video A request starts
Video B request starts
Video B completes
Video A completes later
```

The Video A response must not overwrite the Video B state.

Apply the same rule to:

* playback authorization;
* related videos;
* viewer reaction state;
* subscription state;
* playback progress;
* telemetry;
* player initialization.

Use request cancellation, request identity, generation tokens, or equivalent mechanisms.

---

# 54. Component and Module Boundaries

Keep responsibilities explicit.

A recommended structure is:

```text
watch/
  page
  data
  hooks
  player
  playback
  engagement
  related
  metadata
  telemetry
  components
  types
  tests
```

The exact directory structure may follow the repository's conventions, but the conceptual boundaries must remain clear.

Avoid a single multi-thousand-line watch-page component.

Avoid circular dependencies.

UI components should not directly contain transport-layer concerns when a dedicated data layer is appropriate.

---

# 55. State Ownership Rules

Classify state deliberately.

### Server state

Examples:

* video metadata;
* playback authorization;
* related videos;
* viewer subscription;
* viewer reaction;
* stored playback progress.

### Local player state

Examples:

* current time;
* buffer state;
* volume;
* mute;
* fullscreen;
* playback rate;
* active caption track.

### Navigation state

Examples:

* current video ID;
* supported watch parameters.

### Persisted client preferences

Examples:

* preferred volume;
* playback speed;
* autoplay preference.

Do not place everything in a single global store.

---

# 56. API Error Handling

Normalize API errors into a frontend-safe structure containing, where provided:

```text
code
message
status
requestId
retryable
fieldErrors
```

The player and watch page must map these errors into user-appropriate behavior.

Do not show raw backend stack traces.

Do not assume every `500` response is safely retryable.

Do not retry non-idempotent mutations blindly.

---

# 57. Authentication Expiration

Handle expired authentication during:

* reaction;
* subscription;
* history synchronization;
* playback progress synchronization;
* protected playback.

The frontend must use the project's established session-refresh or reauthentication mechanism.

Avoid infinite refresh loops.

When an authenticated action becomes unauthorized:

* preserve the user's viewing experience;
* present the appropriate authentication state;
* retry only when safe.

---

# 58. Image and Thumbnail Handling

Video thumbnails and channel avatars must:

* use responsive dimensions;
* reserve layout space;
* use appropriate loading behavior;
* support fallback states;
* avoid layout shift;
* respect image optimization conventions.

Do not load oversized source images when a smaller rendition is sufficient.

---

# 59. Mobile Web Player Behavior

On narrow screens:

* player controls must remain touch-friendly;
* metadata should stack naturally;
* related videos should remain discoverable;
* long titles must wrap safely;
* menus should not overflow the viewport;
* fullscreen behavior must work with supported mobile browser behavior.

Do not create a separate mobile implementation unless required by actual product architecture.

Prefer shared behavior with responsive presentation.

---

# 60. Documentation

Add or update documentation covering:

* watch-page architecture;
* player architecture;
* media-source integration;
* playback state model;
* playback progress strategy;
* telemetry events;
* browser compatibility;
* local development/testing requirements;
* known browser/API limitations.

Document any implementation decision that could materially affect later frontend or integration work.

Do not document behavior that the implementation does not actually provide.

---

# 61. Repository Inspection and Compatibility

Before implementation:

1. inspect the existing project structure if a repository is provided;
2. identify the frontend application;
3. inspect package manager and scripts;
4. inspect existing design-system/component conventions;
5. inspect API-client conventions;
6. inspect authentication/session handling;
7. inspect routing conventions;
8. inspect state-management conventions;
9. inspect testing infrastructure;
10. identify existing reusable components.

Reuse compatible infrastructure.

Do not introduce a competing framework or duplicate state-management solution without a strong technical reason.

Do not rewrite unrelated parts of the frontend.

---

# 62. Dependency Discipline

Use production-quality maintained dependencies.

Before introducing a player/media dependency:

* verify that it works with the project's React/Next.js architecture;
* verify browser support;
* verify SSR/client-only requirements;
* avoid unnecessary duplicate player libraries;
* isolate the dependency behind a project-owned abstraction.

Do not add a dependency merely to solve a problem that is already covered by existing project infrastructure.

---

# 63. Contract Compatibility

The implementation must remain compatible with these project-wide frontend/backend contract categories:

```text
Canonical IDs
Canonical timestamps
API response envelope
API error model
Pagination conventions
Authentication/session model
Authorization model
Video entity
Channel entity
Playback authorization
Media manifest/source model
Caption model
Reaction model
Subscription model
Watch-history model
Playback-progress model
Discovery/recommendation model
Analytics event model
Privacy model
```

When actual project artifacts are supplied, use their concrete field names and endpoint definitions.

Do not silently rename externally visible contracts.

If a supplied contract is internally inconsistent, document the conflict explicitly and choose the least-disruptive implementation consistent with the project-wide architecture.

---

# 64. No Backend Fabrication

Do not create:

* mock production APIs;
* fake playback URLs;
* hardcoded video data;
* fake authorization responses;
* fake subscriptions;
* fake reactions;
* fake progress persistence;
* static recommendation arrays masquerading as production data.

Mocks may exist only inside automated tests where they represent controlled test boundaries.

The actual application path must use real typed integration interfaces.

---

# 65. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* placeholder buttons;
* empty handlers;
* commented-out required functionality;
* fake menus;
* “implement later” notes;
* partial player controls;
* omitted error handling;
* pseudo-code.

A feature included in this prompt is complete only when its current-scope implementation is real, testable, and integrated.

---

# 66. Quality Requirements

The implementation must meet a senior production-engineering standard.

Require:

* strict TypeScript;
* clear module boundaries;
* predictable state ownership;
* safe async behavior;
* accessible UI;
* responsive behavior;
* meaningful tests;
* resilient error handling;
* observability;
* performance awareness;
* security-conscious browser behavior;
* maintainable abstractions.

Do not over-engineer speculative requirements.

Do not under-engineer the required player experience.

---

# 67. Validation

Before completion, verify:

* TypeScript compilation;
* linting;
* unit tests;
* component tests;
* integration tests;
* end-to-end tests where available;
* production build;
* route behavior;
* media-player initialization;
* authenticated and anonymous watch flows;
* responsive behavior;
* accessibility-critical interactions;
* player cleanup;
* network failure handling;
* stale-request protection;
* telemetry correctness.

Fix implementation issues rather than merely reporting them.

---

# 68. Definition of Done

This prompt is complete only when all of the following are true:

* the canonical watch experience is implemented;
* the player is a real production-capable implementation;
* playback sources are integrated through explicit contracts;
* HLS/DASH support is handled according to the project's media architecture;
* playback controls function correctly;
* seeking works;
* quality selection works where supported;
* playback-rate controls work;
* captions work where supplied;
* fullscreen works;
* Picture-in-Picture works where supported;
* buffering and error states are handled;
* resume playback works;
* playback progress synchronization works;
* watch-history integration works;
* telemetry is implemented;
* engagement controls are integrated;
* subscription controls work;
* reactions work;
* sharing works;
* reporting entry is integrated;
* related videos work;
* navigation between videos is race-safe;
* responsive layouts work;
* accessibility requirements are implemented;
* security/privacy requirements are respected;
* player resources are cleaned up correctly;
* tests cover the required behavior;
* documentation is updated;
* no fake production behavior remains;
* no required current-scope functionality is left as a placeholder;
* validation passes.

---

# 69. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize the watch and playback functionality actually completed.

### Files

List the significant files created or modified.

### Contracts

List the API/media/analytics contracts consumed by the implementation.

### Testing

Report tests executed and their results.

### Validation

Report build/type/lint and relevant runtime validation.

### Integration Notes

Identify any material contract assumptions, compatibility concerns, browser limitations, or integration work that remains outside this prompt's scope.

### Out of Scope

Confirm that backend, mobile, search, creator, live, monetization, moderation, and other excluded domains were not improperly implemented.

---

# 70. Final Execution Directive

Execute this prompt as an implementation task.

Do not merely describe the architecture.

Do not provide a tutorial instead of implementation.

Do not ask the user what should be implemented.

Do not wait for another prompt.

Do not request approval before performing the defined work.

Inspect the available project state, implement the complete bounded scope, test it, validate it, document it, and provide the completion report.

Do not silently expand the scope.

Do not silently reduce the scope.

Do not create fake backend behavior to make the frontend appear complete.

The result must be a real, production-grade **YouTube-style web watch and playback experience** that can later be integrated with independently generated backend, mobile, infrastructure, and QA project parts through explicit contracts.
