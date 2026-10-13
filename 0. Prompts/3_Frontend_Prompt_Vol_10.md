# YouTube-Style Video Platform — Frontend Prompt — Volume 10

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **short-form video viewing, vertical feed, gesture-based navigation, rapid engagement, and short-form discovery experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

- short-form video feed;
- vertical video player presentation;
- continuous feed navigation;
- gesture-based interactions;
- playback lifecycle management;
- short-form engagement controls;
- creator/channel access;
- captions and audio presentation where supported;
- feed loading and pagination;
- personalized short-form discovery;
- playback progress and telemetry;
- responsive mobile-first layouts;
- accessibility;
- performance and resource management;
- automated testing;
- documentation.

Do not implement unrelated frontend domains.

Do not implement recommendation algorithms, media-processing infrastructure, or backend short-form services.

Do not fabricate videos, playback sources, feed ranking, or engagement results.

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
- search and discovery;
- personalized recommendations;
- notifications;
- creator studio and analytics;
- live streaming;
- moderation;
- paid memberships and monetization-capable functionality;
- web and mobile clients.

The web technology direction is:

- TypeScript;
- React;
- Next.js App Router;
- responsive web;
- typed API clients;
- production server/client state management;
- browser media APIs;
- established playback contracts;
- accessibility;
- observability;
- automated testing.

Short-form video is a distinct viewing experience, not merely a smaller version of the standard watch page. Its interaction model, media layout, navigation, performance, and playback lifecycle must be designed specifically for continuous vertical consumption.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- earlier frontend prompts;
- hidden architectural decisions;
- undocumented media contracts;
- undocumented recommendation endpoints;
- hidden generated files.

If a repository is available, inspect it before modifying it.

If portable architecture, API, playback, discovery, or analytics contracts are supplied, use them as authoritative.

If these artifacts are unavailable, inspect the repository for compatible implementations and follow the explicit invariants in this prompt.

Preserve compatible existing behavior. Do not implement a duplicate player architecture or a separate, incompatible content model.

---

# 4. Primary Objective

Implement a production-quality short-form viewing experience that allows viewers to:

1. open the short-form feed;
2. watch vertically oriented videos;
3. move between videos using supported gestures and controls;
4. navigate through a feed of server-provided video candidates;
5. start and stop playback appropriately;
6. pause and resume;
7. react to videos;
8. open comments;
9. subscribe to creators;
10. share videos;
11. open creator/channel pages;
12. view captions when available;
13. handle unavailable and restricted content;
14. recover from playback and network errors;
15. load additional feed items efficiently;
16. maintain the correct playback state during navigation;
17. use the interface on mobile, tablet, and desktop;
18. preserve privacy and authorization boundaries;
19. emit appropriate telemetry;
20. avoid memory leaks and uncontrolled network/media consumption.

---

# 5. Explicit Scope

Implement:

- canonical short-form feed route;
- short-form feed container;
- vertical video card/player presentation;
- feed candidate loading;
- pagination or incremental loading;
- active-video selection;
- swipe/navigation gestures;
- keyboard navigation;
- playback lifecycle coordination;
- autoplay behavior where supported by browser policy;
- mute and volume controls;
- captions;
- supported quality selection;
- reaction controls;
- comment entry point;
- subscription control;
- share functionality;
- creator identity;
- video metadata;
- unavailable/restricted states;
- playback failure recovery;
- watch-history/progress integration where supported;
- analytics and telemetry;
- responsive behavior;
- accessibility;
- performance;
- resource cleanup;
- automated tests;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- mobile-native applications;
- recommendation ranking algorithms;
- personalized candidate-generation services;
- transcoding workers;
- media-processing infrastructure;
- upload infrastructure;
- object storage;
- CDN infrastructure;
- backend reactions;
- comment persistence;
- subscription persistence;
- moderation backend;
- live-stream infrastructure;
- monetization backend;
- creator analytics computation.

Do not rebuild the standard long-form watch page.

Use the established watch, channel, comment, reaction, subscription, and media contracts wherever they apply.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. identify the web application;
3. inspect Next.js routes and layouts;
4. inspect existing video-player components;
5. inspect media-source integration;
6. inspect discovery/feed APIs;
7. inspect authentication/session handling;
8. inspect reaction and subscription integrations;
9. inspect comment entry points and dialogs;
10. inspect analytics conventions;
11. inspect existing gesture utilities;
12. inspect responsive design primitives;
13. inspect state management and caching;
14. inspect automated tests.

Reuse compatible existing components.

Do not introduce a second global state-management solution, media engine, API client, or authentication framework without a documented technical reason.

---

# 8. Short-Form Route

Implement a canonical short-form viewing route compatible with the project.

A conceptual route may be:

```text
/shorts/{videoId}
```

A short-form feed entry point may also exist at a route equivalent to:

```text
/shorts
```

Preserve existing routing conventions when available.

The route must support:

- direct navigation to a specific video;
- refresh;
- deep linking;
- browser back/forward;
- authenticated viewers;
- anonymous viewers where allowed;
- deleted videos;
- restricted videos;
- unavailable playback;
- transitions between feed items.

Do not rely solely on in-memory navigation state to identify the current video.

---

# 9. Short-Form Domain Contract

Consume the canonical video model and short-form discovery contract.

The frontend must distinguish a short-form presentation from an ordinary long-form video without inventing an incompatible video entity.

A conceptual feed response may contain:

```text
items
nextCursor
hasMore
feedContext
```

Each video item may expose fields equivalent to:

```text
videoId
title
description
channel
thumbnail
duration
visibility
availability
playbackAvailability
viewerReaction
viewerSubscriptionState
viewerPermissions
captionsAvailability
```

Use actual project contract fields when available.

Do not assume every item contains every optional property.

---

# 10. Feed Data Ownership

The backend is authoritative for:

- candidate generation;
- feed ordering;
- personalization;
- eligibility;
- visibility;
- safety filtering;
- restricted-content filtering.

The frontend is responsible for:

- requesting feed candidates;
- presenting them;
- navigating through the current feed;
- loading further candidates;
- coordinating player state;
- collecting permitted client telemetry.

Do not implement recommendation ranking in the browser.

Do not rearrange returned items to simulate a better feed.

---

# 11. Short-Form Feed Layout

Implement a mobile-first vertical viewing surface.

The active video should be the visual focus.

The layout must accommodate:

- video viewport;
- creator identity;
- description/title;
- supported audio information;
- reaction controls;
- comment entry point;
- share action;
- subscription action;
- feed navigation;
- playback state;
- loading/error states.

The interface must account for:

- mobile browser chrome;
- device safe areas;
- dynamic viewport height;
- touch input;
- overlays;
- captions;
- accessible controls.

Do not rely exclusively on a fixed `100vh` layout when it causes clipping on mobile browsers.

Use appropriate modern viewport and safe-area handling.

---

# 12. Responsive Behavior

Support:

- mobile web;
- tablet;
- desktop;
- large desktop.

On mobile:

- use a vertical, immersive layout;
- keep essential interactions reachable;
- prevent controls from being obscured by browser chrome;
- account for safe-area insets;
- avoid accidental horizontal scrolling.

On desktop:

- preserve the vertical video presentation;
- center the active viewing region where appropriate;
- make navigation controls available;
- use surrounding space without shrinking the video into an unusable viewport.

Do not simply scale the mobile interface across every viewport.

---

# 13. Vertical Video Presentation

Render the video using the actual media dimensions and playback contract.

Support vertical media and any other supported aspect ratios.

For videos that do not match the feed's presentation ratio:

- apply the project's intended fit/crop behavior;
- avoid distortion;
- avoid unintended overflow;
- preserve important content as much as practical.

Do not permanently hardcode an aspect ratio that clips all nonvertical media.

Use an appropriate poster or thumbnail during initialization where available.

---

# 14. Player Architecture

Reuse the project's established media engine and playback contracts.

The short-form experience must coordinate:

- active video selection;
- media-source initialization;
- playback state;
- buffering;
- source replacement;
- visibility;
- resource cleanup;
- telemetry.

Conceptually, separate:

```text
ShortFormFeed
  ├── FeedState
  ├── ActiveVideoController
  ├── ShortFormPlayer
  ├── VideoOverlay
  ├── EngagementControls
  ├── FeedNavigation
  └── FeedTelemetry
```

The repository's structure may differ, but the responsibilities must remain clearly separated.

Do not create a custom HLS/DASH playback engine.

---

# 15. Active-Video Selection

The feed must maintain one clear active-video identity.

When the active item changes:

- update the canonical route where appropriate;
- initialize the new media source;
- dispose of the previous media source;
- reset video-specific UI state;
- load the correct engagement state;
- preserve appropriate viewer preferences;
- prevent stale responses from overwriting the new video.

Do not allow two feed videos to play audio simultaneously.

---

# 16. Playback Lifecycle

Model relevant player states, including:

```text
idle
loading
ready
playing
paused
buffering
ended
error
unsupported
```

Use the existing player-state model where one already exists.

The browser media element or established player library remains authoritative for actual playback state.

Do not maintain competing sources of truth in local state and the media engine.

---

# 17. Visibility-Based Playback

Use an appropriate visibility mechanism to determine which feed item is active.

The implementation must:

- identify the active item as the viewer scrolls;
- avoid simultaneous playback of multiple items;
- pause items that leave the active viewing area;
- avoid rapid repeated source creation during small scroll fluctuations;
- clean up observers when the feed changes or unmounts.

Do not assume that mounting a video element means the viewer is actually watching it.

---

# 18. Autoplay and Browser Restrictions

Implement autoplay according to browser policies and project behavior.

The frontend must:

- attempt autoplay only under appropriate conditions;
- handle autoplay rejection;
- support muted autoplay where appropriate;
- provide a visible play control when autoplay is blocked;
- avoid falsely displaying a playing state when the browser rejected the request;
- respect explicit user pause intent.

Do not repeatedly call `play()` in response to every render.

User interactions must take precedence over automatic playback transitions.

---

# 19. Playback Controls

Implement controls appropriate for short-form viewing.

Where supported, include:

- play/pause;
- mute/unmute;
- volume;
- captions;
- quality selection;
- fullscreen;
- supported progress indication.

Controls must respond correctly to:

- touch;
- mouse;
- keyboard;
- media-element events;
- route changes;
- visibility changes.

Do not expose unsupported seek or quality controls merely because they exist on the standard watch page.

---

# 20. Gesture Navigation

Implement vertical feed navigation where appropriate.

Support:

- touch swipe to advance;
- touch swipe to return to a previous item where available;
- keyboard next/previous controls;
- visible navigation affordances where appropriate.

Gesture handling must:

- distinguish vertical feed gestures from horizontal content interaction;
- avoid preventing all normal page scrolling;
- avoid trapping browser navigation;
- handle interrupted gestures;
- avoid changing video when the gesture starts over an interactive control.

Do not make swiping the only method of navigation.

---

# 21. Keyboard Navigation

Support keyboard-accessible feed navigation.

At minimum, provide a coherent method to:

- move to the next video;
- move to the previous available video;
- play/pause;
- mute/unmute where appropriate;
- enter/exit available viewing modes;
- activate engagement controls.

Do not capture keyboard input when focus is in:

- text fields;
- comment composers;
- dialogs;
- menus;
- other interactive controls where the shortcut would interfere with normal use.

Provide visible focus indicators.

---

# 22. Feed Pagination

Load candidates through the canonical feed contract.

Support:

- initial page;
- next page;
- end of feed;
- retry;
- empty feed;
- duplicate prevention;
- stale-request cancellation.

Use cursor pagination when supplied by the backend.

Do not request all feed candidates upfront.

Do not trigger several concurrent requests for the same cursor.

---

# 23. Feed Preloading

Use controlled preloading to reduce transitions between videos.

The implementation may prepare limited upcoming feed metadata or media resources where appropriate.

Requirements:

- prioritize the active video;
- bound the amount of preloaded media;
- cancel obsolete requests;
- avoid unnecessary network consumption;
- avoid preloading protected content before authorization;
- respect browser data/resource constraints where practical.

Do not download every video in the feed.

Do not make aggressive preload behavior cause increased playback failures for the active video.

---

# 24. Resource and Memory Management

Short-form feed navigation must remain stable across many consecutive videos.

Clean up:

- media-source instances;
- event listeners;
- intersection observers;
- timers;
- animation frames;
- request controllers;
- playback telemetry timers;
- temporary object URLs;
- gesture handlers.

Bound the amount of media and component state retained in memory.

Do not keep every previously visited video mounted indefinitely.

---

# 25. Playback Failure Recovery

Handle:

- unavailable playback source;
- expired media authorization;
- manifest errors;
- unsupported format;
- network interruptions;
- decoding failures;
- buffering timeouts;
- source replacement failures.

Use understandable user-facing messaging.

Provide a retry path where safe.

If a feed item is permanently unavailable, support a contract-consistent transition or unavailable state.

Do not invent a replacement video.

---

# 26. Active Video and Route Synchronization

The current short-form video must remain identifiable through navigation.

When moving between feed items:

- update the canonical path or supported URL state;
- preserve browser history behavior according to the product convention;
- support direct opening of a specific item;
- handle browser back/forward;
- prevent stale previous-video responses from resetting the current route.

Do not add a separate history entry for every tiny scroll movement unless that is the explicit navigation design.

---

# 27. Video Metadata Overlay

Display appropriate video metadata, such as:

- title or description;
- creator/channel name;
- creator avatar;
- supported audio information;
- visibility or availability messaging where appropriate.

Long descriptions must not obstruct the main viewing experience.

Where text expands or collapses, use accessible controls.

Do not render untrusted rich content without safe handling.

---

# 28. Creator Navigation

Provide navigation from the active short-form video to the canonical creator/channel page.

Support:

- creator avatar;
- channel identity;
- verification where supplied;
- subscription state;
- channel navigation.

Use the existing channel and subscription models.

Do not create a separate short-form-only subscription implementation.

---

# 29. Reaction Controls

Integrate video reaction controls using the project's canonical reaction contract.

Support:

- current viewer reaction;
- active/inactive state;
- loading;
- success;
- failure;
- sign-in requirements where applicable.

Use authoritative server state.

If optimistic UI is used:

- retain the previous state;
- roll back on failure;
- reconcile with server response;
- protect against stale conflicting mutations.

Do not blindly increment counts when a request is submitted.

---

# 30. Comment Entry Point

Provide a way to open or navigate to comments associated with the current short-form video.

Use the project's canonical comment domain and API contracts.

Where a shared comment dialog or comment route exists, reuse it.

Support:

- loading;
- empty comments;
- error;
- authenticated comment creation where supported;
- reply navigation where supported.

Do not implement a separate comment persistence model.

Do not let the comment interface accidentally change the active video without an explicit navigation action.

---

# 31. Comment Overlay Behavior

If comments are presented in an overlay or sheet:

- manage focus appropriately;
- support close/cancel;
- prevent unwanted background interactions;
- adapt to mobile keyboard behavior;
- preserve the active video identity;
- pause playback where product policy requires it;
- resume only when appropriate to the viewer's explicit intent.

Do not automatically resume playback after closing comments if the viewer had explicitly paused the video before opening them.

---

# 32. Subscription Integration

Use the same subscription contract and state model as other channel surfaces.

Support:

- subscribed;
- not subscribed;
- pending;
- unavailable;
- authentication required;
- error.

Disable conflicting actions while a request is pending.

Do not assume the displayed subscriber count is immediately consistent with the mutation.

Do not duplicate subscription logic inside every video card.

---

# 33. Share Functionality

Implement sharing through supported web capabilities.

Support:

- canonical short-form URL;
- native Web Share API where available;
- fallback copy behavior;
- success feedback;
- failure handling.

The shared link must open the specific video through the canonical route.

Do not include internal API URLs, signed media URLs, or authorization tokens.

---

# 34. Captions

Where captions are available, integrate with the established caption model.

Support:

- caption availability;
- enabled/disabled state;
- track selection where supported;
- loading/failure;
- caption rendering by the approved player.

Do not assume captions exist for every video.

Do not create a separate incompatible subtitle engine.

Make caption controls accessible.

---

# 35. Audio Attribution

If the platform supports audio metadata or source attribution, present the backend-provided information.

The frontend must not infer an audio track's rights, origin, licensing, or reuse status from its title or filename.

Only show supported attribution fields.

Do not expose internal storage locations or media-processing metadata.

---

# 36. Short-Form Restrictions

Respect visibility and restriction states supplied by the backend.

Support appropriate presentation for:

- public;
- unlisted;
- private;
- deleted;
- unavailable;
- age/restriction state where supported;
- blocked or removed content where defined.

Do not assume a video is public merely because a feed candidate was previously available.

Do not expose media authorization data when access is denied.

---

# 37. Privacy-Aware History and Progress

Integrate with the existing watch-history and playback-progress contracts where supported.

Do not create a separate incompatible short-form history model.

Respect viewer privacy controls.

Progress and watch-history updates must:

- use canonical IDs;
- avoid duplicate entries;
- avoid excessive request frequency;
- be scoped to the correct active video;
- stop after navigation as appropriate.

Do not send progress updates for videos the viewer did not meaningfully view unless the product contract explicitly requires that behavior.

---

# 38. Playback Telemetry

Instrument appropriate short-form playback events.

Potential events include:

```text
short_form_feed_opened
short_form_video_impression
short_form_play_started
short_form_paused
short_form_video_completed
short_form_feed_advanced
short_form_feed_reversed
short_form_playback_failed
short_form_playback_recovered
short_form_reaction_changed
short_form_comments_opened
short_form_creator_opened
short_form_share_started
short_form_caption_changed
```

Use canonical event names when supplied by the platform.

Do not infer a valid impression from mounting alone.

Use an appropriate visibility and engagement threshold when the analytics contract defines one.

Do not emit excessive high-frequency telemetry.

---

# 39. Analytics Privacy

Do not include:

- passwords;
- access tokens;
- signed media URLs;
- private account information;
- raw comment content;
- unnecessary personal identifiers.

Use only the context required by the canonical analytics contract.

Do not independently invent new analytics semantics that conflict with backend aggregation.

---

# 40. State Ownership

Separate state into clear categories.

### Server state

- feed candidates;
- canonical video metadata;
- playback authorization;
- viewer reaction;
- viewer subscription;
- comment data;
- privacy preferences.

### Local player state

- active playback state;
- mute/volume;
- control visibility;
- transient media state.

### Feed UI state

- active index;
- loading state;
- gesture state;
- visible menu/dialog;
- pagination state.

### Persisted preferences

Only preferences that the product permits storing locally or through the existing user settings contract.

Do not place every feed and player state variable into a global store.

---

# 41. Request Race Prevention

Protect against stale asynchronous responses.

Example:

```text
Video A becomes active
Video A playback request starts
Viewer advances to Video B
Video B request starts
Video B succeeds
Video A finishes afterward
```

Video A must not overwrite Video B's playback or metadata state.

Apply this to:

- video detail;
- playback authorization;
- captions;
- reactions;
- subscriptions;
- comments;
- feed pagination;
- telemetry.

Use request cancellation, identity checks, generation tokens, or equivalent mechanisms.

---

# 42. Authentication and Session Expiration

The short-form feed must allow anonymous playback of public videos when supported.

Authentication should only be required for protected operations.

If a viewer's session expires while interacting:

- preserve playback where possible;
- handle authorized mutations safely;
- use the canonical session-refresh behavior;
- avoid infinite refresh loops;
- prevent stale user-specific reactions or subscriptions from remaining visible.

Do not force public viewers to sign in just to browse public short-form content.

---

# 43. Accessibility

Implement:

- keyboard navigation;
- semantic buttons;
- accessible player controls;
- visible focus;
- screen-reader labels;
- accessible comment overlays;
- accessible menus;
- sufficient touch-target sizes;
- reduced-motion support where appropriate;
- meaningful playback/error announcements.

Do not rely exclusively on gesture interaction.

Do not auto-advance a video in a way that makes necessary controls unusable for keyboard or assistive-technology users.

The main feed and engagement controls must remain accessible.

---

# 44. Motion and Interaction

Use transitions that support the continuous-feed experience without blocking interaction.

Respect reduced-motion preferences.

Do not require large animated transitions to complete before the next video can start.

Avoid motion that causes nausea or prevents users from identifying the active video.

Gesture feedback must remain subtle and responsive.

---

# 45. Performance

Optimize:

- first feed-item time to playback;
- source initialization;
- next-item transitions;
- image loading;
- feed scrolling;
- player-state updates;
- engagement-control updates;
- comments overlay loading.

Do not rerender every feed item when the active video changes.

Use stable component boundaries and appropriate memoization where it provides measurable benefit.

Avoid unnecessary hydration or loading heavy secondary UI before it is needed.

---

# 46. Error Isolation

Short-form errors must not unnecessarily break the application shell.

Examples:

```text
Comments fail to load
Video playback remains usable
```

```text
Reaction request fails
The active player continues
```

```text
Feed pagination fails
Previously loaded items remain available
```

```text
Next video is unavailable
The interface presents a recoverable state
```

Use localized error handling.

Do not fabricate replacement data.

---

# 47. Security

The implementation must:

- use secure session handling;
- respect backend authorization;
- safely render video descriptions and creator-provided text;
- validate navigation targets;
- avoid open redirects;
- avoid unsafe HTML;
- avoid exposing signed media URLs;
- avoid logging tokens;
- prevent unauthorized actions.

The frontend must never be the authoritative security boundary for protected media.

---

# 48. Testing Strategy

Implement tests for actual behavior.

### Unit tests

Cover:

- active-video selection;
- feed navigation;
- route synchronization;
- playback lifecycle;
- visibility logic;
- request-race prevention;
- pagination;
- duplicate suppression;
- reaction mutation rollback;
- autoplay rejection;
- cleanup behavior;
- telemetry construction.

### Component tests

Cover:

- vertical player container;
- active-video overlay;
- feed navigation;
- reaction controls;
- subscription control;
- comments entry/overlay;
- share action;
- caption control;
- playback error state;
- loading and unavailable states.

### Integration tests

Cover:

- loading feed candidates;
- opening a specific video;
- initializing playback;
- advancing to another video;
- pagination;
- reaction state;
- subscription state;
- comment integration;
- playback-progress integration;
- source failure recovery;
- authentication changes.

### End-to-end tests

At minimum:

1. open the short-form feed;
2. verify the active video is identified correctly;
3. verify playback initialization;
4. navigate to the next video;
5. navigate to a previous video where supported;
6. verify the previous player no longer plays;
7. react to a video;
8. open comments;
9. open the creator channel;
10. share a video;
11. handle a playback failure;
12. trigger feed pagination;
13. verify anonymous viewing of public videos;
14. verify restricted-content behavior;
15. verify keyboard navigation;
16. verify repeated feed navigation does not create duplicate media or realtime resources.

Do not replace behavioral tests with snapshots alone.

---

# 49. Browser Compatibility

Validate the supported browser matrix.

Pay particular attention to:

- autoplay restrictions;
- touch gestures;
- fullscreen;
- dynamic viewport sizing;
- safe-area handling;
- media cleanup;
- keyboard navigation;
- Picture-in-Picture where supported.

Use feature detection for optional browser APIs.

Do not assume identical media capabilities across browsers.

---

# 50. Documentation

Update documentation describing:

- short-form routes;
- feed API integration;
- canonical video model;
- active-video selection;
- playback lifecycle;
- gesture navigation;
- media cleanup;
- preload strategy;
- engagement integration;
- comment integration;
- privacy/history behavior;
- telemetry events;
- accessibility;
- testing strategy.

Documentation must describe the actual implementation.

---

# 51. No Fake Short-Form Behavior

Do not create:

- hardcoded feed content;
- fake recommendation ranking;
- fake playback sources;
- simulated reactions;
- fake subscription state;
- fabricated engagement counts;
- fake captions;
- fake progress persistence.

Mocks are allowed only within automated tests.

Production behavior must use the project's real contracts.

---

# 52. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- nonfunctional gestures;
- empty player handlers;
- placeholder feed items;
- fake reaction controls;
- fake navigation buttons;
- incomplete media cleanup;
- missing error handling;
- “implement later” sections.

Every requirement within the current scope must be genuinely implemented.

---

# 53. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- production build;
- feed loading;
- active-video transitions;
- playback controls;
- autoplay rejection behavior;
- captions where supported;
- reactions and subscriptions;
- comments integration;
- share behavior;
- pagination;
- stale-request protection;
- resource cleanup;
- responsive behavior;
- accessibility;
- authenticated/anonymous behavior;
- privacy and authorization constraints.

Fix issues within this scope.

Do not merely report test failures as completion.

---

# 54. Definition of Done

This prompt is complete only when:

- canonical short-form routes work;
- feed content uses real contracts;
- vertical video presentation works;
- active-video selection is deterministic;
- only the intended video plays;
- feed navigation works;
- gestures work without breaking other controls;
- keyboard navigation works;
- media initialization and cleanup work;
- feed pagination works;
- preload behavior is bounded;
- autoplay restrictions are handled;
- playback errors are recoverable;
- reaction controls work;
- subscription controls work;
- comment integration works;
- sharing works;
- creator navigation works;
- captions work where supported;
- history/progress integration respects privacy;
- telemetry is correct and not excessive;
- restricted content is handled securely;
- responsive behavior works;
- accessibility requirements are implemented;
- memory and resource use remain bounded during repeated navigation;
- tests cover the defined behavior;
- documentation is updated;
- no fake production behavior remains;
- no current-scope placeholder functionality remains;
- validation passes.

---

# 55. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize the short-form feed, player experience, navigation, engagement controls, and discovery integration actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List the feed, video, playback, reaction, subscription, comment, history, and analytics contracts consumed.

### State and Resource Management

Summarize active-video ownership, playback cleanup, feed pagination, preloading, stale-request prevention, and memory management.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, production build, and relevant browser/runtime checks.

### Integration Notes

Identify material backend-contract assumptions, browser limitations, or missing service dependencies.

### Out of Scope

Confirm that mobile-native applications, recommendation algorithms, media infrastructure, backend engagement services, and other excluded domains were not improperly implemented.

---

# 56. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe the short-form viewing experience.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate feed content, playback, reactions, subscriptions, or recommendation behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web short-form video feed and viewing experience** that integrates with the independently generated backend, media platform, and other frontend modules through explicit contracts.
