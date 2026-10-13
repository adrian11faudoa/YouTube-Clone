# YouTube-Style Video Platform — Mobile Prompt — Volume 10

## Short-Form Video Feed, Vertical Playback, Interactive Engagement, and Discovery

### 1. Mission and Implementation Scope

Implement the production-grade **native short-form video experience** for the YouTube-style video platform using React Native and TypeScript on iOS and Android.

This milestone delivers the mobile experience for discovering, watching, navigating, and interacting with short-form videos through an immersive, vertically swipeable feed. It must integrate with the platform's established video delivery, recommendation, engagement, authentication, social-interaction, moderation, and analytics contracts.

The platform targets approximately 250 million registered users and 50 million daily active users. The mobile implementation must handle large feeds, frequent video transitions, unreliable mobile networks, constrained device resources, and high interaction rates without introducing incompatible backend behavior.

The application must support actual short-form videos and real platform interactions. Every visible control must behave as advertised, every engagement mutation must use the appropriate API, and the feed must reflect genuine server-provided content and state. Do not fabricate videos, likes, comments, view counts, recommendation results, or sharing outcomes.

This prompt is independently executable in a fresh coding-agent conversation. Implement the defined scope directly, preserve the project's established architecture, and produce the required tests and portable integration documentation.

### 2. Technology and Engineering Constraints

Use the established project direction:

- **Mobile:** React Native and TypeScript.
- **Backend:** TypeScript and NestJS.
- **Database:** PostgreSQL.
- **Caching:** Redis where applicable to backend services.
- **Media:** The platform's existing video storage, processing, CDN, and delivery infrastructure.
- **Playback:** The established mobile video-player abstraction and supported delivery protocols.
- **Realtime:** Existing realtime infrastructure where a short-form interaction requires it.
- **Authentication:** The shared account, session, and authorization contracts.
- **Observability:** The project's established telemetry, structured logging, and error-reporting conventions.

Inspect the actual repository, application navigation, player implementation, design system, feed architecture, API contracts, and relevant mobile dependencies before changing code.

Reuse existing video playback, comment, engagement, channel, sharing, reporting, and authentication functionality whenever appropriate. Do not create parallel implementations of systems already owned by other mobile modules.

When the necessary architecture or API artifacts are unavailable, implement clearly bounded integration interfaces and document concrete proposed contracts. Do not assume that independent coding-agent conversations share files or established implementation state.

### 3. Required Deliverables

Implement the following mobile capabilities:

1. A dedicated, vertically swipeable short-form video feed.
2. Full-screen or appropriately immersive portrait-video playback.
3. Feed pagination, refresh, and content replenishment.
4. Playback coordination, preloading, buffering, and recovery.
5. Short-form engagement actions, including supported likes and comments.
6. Creator and channel navigation.
7. Sharing and deep-link handling.
8. Feed personalization and supported discovery controls.
9. Reporting, blocking, and safety-aware content handling.
10. Integration with watch history, subscriptions, and recommendation tracking where supported.
11. Accessibility, performance, mobile lifecycle management, and reliable state handling.
12. Automated tests, integration documentation, and a factual completion report.

The implementation must integrate with the existing application rather than replacing the global mobile architecture or duplicating the ordinary video player.

### 4. Short-Form Feed Entry Points

Integrate the short-form experience into the established mobile navigation.

Provide appropriate entry points from existing surfaces where supported, including:

- Main application navigation.
- Home and discovery feeds.
- Search results.
- Channel pages.
- Subscription feeds.
- Short-form video links.
- Existing video or content recommendation surfaces.

Use the project's authoritative navigation conventions and route parameters.

The dedicated feed must open with a valid initial position and load real short-form content from the appropriate service. If a specific short is opened from a deep link, resolve and display that item through the established content API, then continue the feed using the supported continuation contract.

Handle missing, deleted, private, unavailable, and unauthorized content gracefully. Do not display an inaccessible item indefinitely because a stale navigation parameter or local cache references it.

Do not rebuild home, search, subscriptions, channels, or the global navigation system in this milestone.

### 5. Immersive Vertical Feed

Implement a polished, vertically swipeable feed optimized for mobile short-form video.

Each feed item must present the video prominently and display the applicable metadata and interaction controls supplied by the platform.

Support:

- Vertical swipe navigation.
- Correct selection of the active video.
- Clear active-item state.
- Loading and buffering indicators.
- Playback-error recovery.
- Creator and channel identity.
- Video description or caption text.
- Audio information where available.
- Like, comment, share, and other supported actions.
- Access to the creator's channel.
- Accessible reporting and additional-action menus.

Use a native-feeling interaction model consistent with the existing mobile design system.

#### 5.1 Active-item behavior

At any given time, only the intended active feed item should ordinarily own active playback.

When the active index changes:

- Pause or release the previously active video as appropriate.
- Stop inappropriate audio leakage from off-screen videos.
- Activate the selected item when playback conditions permit.
- Preserve valid playback state when temporarily interrupted.
- Ensure item-specific metadata and engagement controls update to the selected video.
- Prevent stale callbacks from an old player instance from changing the new active item's UI.

The player must not continue playing a previous video behind the visible item.

When a video becomes unavailable or fails terminally, present a useful recovery path and allow the user to continue through the feed.

### 6. Video Playback and Player Coordination

Reuse the established player implementation and supported native playback libraries.

Integrate with the platform's authoritative video metadata and playback-source resolution.

Requirements include:

- Video initialization and readiness.
- Buffering and playback progress.
- Player errors and retry.
- Audio mute and unmute behavior where supported.
- Playback pause and resume.
- Correct transition between consecutive feed items.
- Network changes and interrupted delivery.
- Application foreground and background behavior.
- Device audio interruptions.
- Supported full-screen, orientation, and accessibility behavior.
- Safe release of native playback resources.

Do not hardcode permanent media URLs or bypass the established video-access rules.

Do not assume every short-form video uses the same codec, dimensions, stream protocol, or available playback controls. Use the player capabilities and media metadata actually provided by the platform.

Where adaptive delivery is supported, allow the existing playback infrastructure to select or adjust delivery quality according to the established strategy.

### 7. Preloading, Buffering, and Feed Continuity

Optimize the feed so users can swipe between videos without unnecessary blank screens, excessive delays, or resource exhaustion.

Implement a bounded strategy for preloading upcoming content through the shared player and media infrastructure.

Requirements:

- Preload only a controlled number of nearby feed items.
- Prioritize the next likely item while preserving resources for the active video.
- Avoid loading entire videos into memory.
- Reuse validated metadata and existing media caches where appropriate.
- Cancel obsolete preloads after rapid swipes.
- Prevent duplicate requests for the same media resource.
- Release unused player instances and native resources.
- Apply reasonable timeouts and retry limits.
- Recover gracefully when preloading fails.
- Avoid allowing preloading to degrade playback of the active item.

Use actual device and player constraints when selecting the preload window. Do not allocate an unlimited set of player instances or introduce a separate caching subsystem without architectural justification.

Do not claim that an item is ready merely because its metadata has loaded. Distinguish metadata readiness, media availability, and playable-buffer readiness according to the capabilities of the player library.

### 8. Feed Retrieval and Pagination

Integrate the short-form feed with the platform's established discovery or recommendation API.

Support the feed retrieval behavior exposed by its contract, including:

- Initial page loading.
- Cursor-based pagination.
- Pull-to-refresh where applicable.
- Feed continuation.
- Deduplication across overlapping pages.
- Refresh and pagination race handling.
- Recovery from request failures.
- Empty and exhausted-feed states.
- Removal or skipping of unavailable items.

Preserve authoritative ordering from the backend unless the product contract explicitly permits client-side adjustments.

Do not invent a recommendation algorithm or reorder feed items through unsupported local heuristics.

Avoid unboundedly growing the in-memory feed. Implement an appropriate item-retention and cleanup strategy that preserves the active item and necessary navigation continuity while maintaining manageable memory usage.

When the feed's cursor becomes invalid or the backend requests a reset, follow the documented recovery behavior rather than fabricating continuation data.

### 9. Engagement: Likes and Supported Reactions

Implement short-form engagement controls using the platform's established video-engagement APIs.

Where supported, display:

- Current user's like state.
- Authoritative like count.
- Applicable reaction or interaction controls.
- Pending or failed state for engagement mutations.

Requirements:

- Use stable video identifiers.
- Prevent accidental duplicate submissions.
- Apply optimistic updates only where appropriate.
- Retain enough prior state to roll back failed changes.
- Reconcile the result with authoritative server responses.
- Handle stale data and concurrent mutations.
- Refresh or invalidate relevant engagement state according to the shared architecture.

If the user rapidly toggles a like, ensure the final intended state is reconciled correctly rather than allowing out-of-order requests to overwrite the latest state.

Do not invent reaction types or use local counters as the authoritative production count.

Where a metric is unavailable, omit it or display an appropriate unavailable state instead of displaying zero as though it were confirmed.

### 10. Comments and Discussion Integration

Integrate the short-form feed with the platform's existing comments experience.

When the user opens a video's comments:

- Identify the exact video through the established route contract.
- Open the shared comment screen, sheet, or supported presentation.
- Preserve enough playback and feed state to return to the correct item.
- Restore appropriate scroll and navigation state.
- Follow the existing comment pagination and submission behavior.
- Handle deleted, restricted, or disabled comments appropriately.

Where comments are composed in a bottom sheet, ensure the keyboard, gesture navigation, safe areas, and scroll behavior work on both mobile platforms.

New comments must use the actual comment API, respect established validation and authorization, and display confirmed success or actionable failure states.

Do not implement a second comment storage system, duplicate moderation semantics, or a separate short-form-only comment engine.

### 11. Creator and Channel Interactions

Display the video's actual creator or channel identity and integrate with existing channel functionality.

Implement relevant supported actions, including:

- Opening the creator's channel.
- Viewing existing subscription state.
- Subscribing or unsubscribing where supported.
- Displaying the corresponding confirmed subscription state.
- Accessing supported creator or channel content.
- Navigating to the associated long-form video or other linked media when explicitly supported.

Reuse the established channel model, subscription APIs, and global account state.

Prevent duplicate subscription actions, reconcile failures, and ensure the visible state reflects the authenticated user's actual relationship with the channel.

Do not invent channel identifiers, creator information, subscription counts, or unavailable channel-management capabilities.

### 12. Sharing and Deep Links

Implement supported sharing actions for short-form videos.

Use the platform's authoritative share payload and deep-linking conventions.

Where supported, share a stable, canonical video link with any permitted content-specific routing information.

Requirements:

- Open the native sharing interface through the established library or platform API.
- Handle cancellation without treating it as a failed share.
- Avoid claiming that a recipient received the link.
- Support opening a shared short link inside the application when the app and content permit it.
- Validate incoming identifiers and route parameters.
- Handle application cold starts and authenticated navigation restoration.
- Provide an appropriate web or in-app fallback when supported content cannot open natively.

Do not place private credentials, session tokens, or sensitive account identifiers in shared URLs.

Do not fabricate a successful share result or use arbitrary user-controlled destinations as trusted internal routes.

### 13. Personalization and Discovery Controls

Integrate with the existing recommendation and personalization contracts wherever the platform exposes the corresponding controls.

Supported actions may include:

- Indicating that a video is not interesting.
- Hiding or reducing recommendations from a particular creator.
- Reporting inappropriate content.
- Managing supported recommendation preferences.
- Providing feedback to the recommendation system.

Implement only the actions available through the authoritative API.

Each action must:

1. Be accessible from the relevant item menu.
2. Communicate its meaning clearly.
3. Submit the actual corresponding operation.
4. Show progress when appropriate.
5. Reflect confirmed success or display a recoverable error.
6. Update or remove the affected feed item only according to documented response semantics.

Do not build the recommendation engine, user-embedding system, ranking model, experimentation service, or recommendation backend in this milestone.

Do not silently treat dismissal of an item from the current local list as a persisted global recommendation preference.

### 14. Reporting, Blocking, and Safety

Integrate short-form content with the project's existing reporting, blocking, and moderation systems.

Where supported, allow users to:

- Report a short-form video.
- Report a creator or account.
- Block an account.
- Hide content or creator recommendations using the approved contract.
- Access other established safety controls appropriate to the item.

Use existing report categories, validation rules, confirmation requirements, and server-side moderation semantics.

Requirements:

- Validate report input.
- Prevent duplicate submissions.
- Show the result of the actual request.
- Handle inaccessible or already-deleted content.
- Remove or refresh blocked content according to the established policy.
- Avoid displaying private moderation details beyond the user's permissions.
- Preserve safety-control access for users with accessibility needs.

Do not treat client-side hiding as a replacement for backend authorization or moderation enforcement.

Do not implement a new moderation engine or administrative moderation console.

### 15. Watch History, Analytics, and Recommendation Signals

Integrate short-form viewing with the shared viewing-history and analytics architecture.

Where applicable, record the client-observable events defined by the platform contract, such as:

- A video becoming the active item.
- Playback beginning.
- Meaningful playback progress.
- Playback completion.
- A swipe to another item.
- Engagement actions.
- Playback errors.

Use the project's established event schemas and measurement conventions.

Do not independently redefine view-count qualification, watch-time calculations, completion thresholds, or recommendation-ranking rules. These are authoritative platform definitions.

Requirements:

- Avoid emitting duplicate lifecycle events from stale player instances.
- Distinguish actual playback from a video merely becoming visible.
- Avoid counting media that never started as a completed viewing event.
- Batch or debounce telemetry only where supported and appropriate.
- Handle network interruptions according to the established analytics contract.
- Avoid blocking playback while telemetry requests complete.
- Never put sensitive account data or unnecessary personal information into event payloads.

Do not fabricate analytics or calculate platform-wide metrics from local session state.

If watch-history or analytics contracts are unavailable, document the required events and ownership boundaries instead of inventing a new production tracking service.

### 16. Authentication and Entitlement Integration

Respect the shared authentication model and the platform's existing premium and membership entitlements.

Where supported by the product contract, a short-form experience may adapt to:

- Ad-free playback.
- Premium playback behavior.
- Background playback.
- Other explicitly defined entitlement-based capabilities.

Requirements:

- Use the shared authenticated API client.
- Handle session expiry centrally.
- Respect content-access restrictions.
- Avoid presenting premium access based solely on local flags.
- Prevent user-scoped feed or engagement state from leaking across accounts.
- Refresh relevant server-owned state following login, logout, or account switching.
- Preserve guest-access behavior where explicitly supported.

Do not rebuild authentication, billing, subscription management, or entitlement verification in this milestone.

### 17. State Management and Navigation Consistency

Use the established application and server-state management infrastructure.

Represent the feed as a coordinated set of states for retrieval, active-item selection, playback, engagement, and navigation.

Requirements:

- Keep active item identity separate from list position.
- Prevent stale callbacks from updating a different video.
- Avoid redundant copies of authoritative video metadata.
- Reconcile overlapping page requests.
- Preserve correct video identity after list refreshes.
- Prevent duplicate mutations.
- Restore the intended feed position after returning from comments or channel pages where appropriate.
- Handle removed or reordered items safely.
- Clear or isolate account-specific cached content where necessary.

The feed should remain coherent when a user interacts rapidly, opens nested screens, changes accounts, or returns from the background.

Do not replace the global navigation or state-management architecture to implement this isolated feature.

### 18. Mobile Lifecycle, Network, and Resource Management

Implement explicit behavior for mobile application lifecycle transitions.

Handle:

- App entering the background.
- App returning to the foreground.
- Incoming calls and system audio interruptions where applicable.
- Device audio-focus changes.
- Network loss and reconnection.
- Playback interruptions.
- Rapid feed navigation.
- Memory pressure.
- Native player initialization or release failures.
- User leaving the feed.

Pause, resume, or release playback according to the established product behavior and platform lifecycle.

Do not assume React Native JavaScript will execute continuously while the app is suspended.

Avoid uncontrolled polling, excessive network requests, unbounded video preloading, stale native handles, and resource leaks.

Where telemetry or prefetching runs asynchronously, ensure its cancellation and failure do not block essential user interactions.

### 19. Accessibility and Visual Quality

Deliver a production-quality user interface consistent with the existing mobile design system.

Implement:

- Accessible play, pause, like, comment, share, and additional-action controls.
- Correct screen-reader labels and interaction hints.
- Announcements for meaningful playback or action-state changes.
- Adequate touch targets.
- Dynamic font support where applicable.
- Readable creator and caption overlays.
- Safe-area and orientation support.
- Accessible reporting and preference controls.
- Reduced-motion behavior where appropriate.
- High-contrast and light/dark-theme support when provided by the application.
- Localization-ready text and locale-aware metadata.
- Appropriate keyboard behavior for comments and other interactive overlays.

Ensure that core actions remain discoverable even when video overlays, captions, or comments are visible.

Do not make essential functionality accessible only through gestures. Provide equivalent accessible actions for vertical navigation and important item controls.

Avoid obstructing the video with excessive UI. Keep essential interaction controls visually clear and consistent with the product's established design.

### 20. Security and Data Handling

Treat feed responses, media URLs, deep links, engagement payloads, and creator metadata as untrusted input.

Implement these safeguards:

- Validate identifiers and supported navigation destinations.
- Use approved media authorization and playback resolution.
- Respect server-side access control for restricted videos.
- Avoid logging authentication credentials or signed media URLs containing secrets.
- Prevent account-specific interaction state from leaking between users.
- Sanitize or safely render user-generated text using the application's existing conventions.
- Enforce authorization through backend APIs rather than UI visibility alone.
- Avoid persisting unnecessary private watch or engagement data.
- Respect report and block semantics.
- Handle deleted or restricted content consistently across cached and refreshed feed states.

Do not use arbitrary deep-link parameters to authorize privileged navigation or bypass media restrictions.

### 21. Performance and Reliability Validation

Optimize the feed with measurable, device-appropriate constraints.

Focus on:

- Time to first playable video.
- Time between a swipe and the next playable item.
- Dropped or frozen playback during rapid navigation.
- Memory use from active and preloaded player instances.
- Excessive feed rerenders.
- Duplicate metadata and media requests.
- Engagement mutation latency.
- Responsiveness while loading comments or submitting interactions.

Use existing performance instrumentation where available. Run appropriate profiling or tests for the supported environment.

Do not invent numeric performance results or claim production-scale capacity without actual evidence.

Implement safe fallbacks when preloading or media delivery is unavailable. A failed preload must not prevent the user from accessing the selected video through ordinary playback.

### 22. Required Automated Tests

Use the established project test framework.

#### 22.1 Unit tests

Test:

- Feed item parsing and stable identity.
- Cursor pagination and deduplication.
- Active-item selection.
- Player-state synchronization.
- Preload-window calculation and cancellation.
- Stale callback prevention.
- Engagement mutation and rollback.
- Subscription-state mapping.
- Comment and creator navigation parameters.
- Deep-link validation.
- Report and block action handling.
- Analytics-event deduplication.
- Account-switching and cached-state isolation.

#### 22.2 Component and screen tests

Test:

- Initial feed loading and error states.
- Empty and exhausted feeds.
- Vertical item transitions.
- Playback buffering and failure.
- Rapid consecutive swipes.
- Like controls and mutation errors.
- Comment opening and return navigation.
- Creator navigation and subscription controls.
- Native sharing cancellation and failure.
- Personalization actions.
- Report and block confirmation.
- Restricted and unavailable videos.
- Accessibility labels and non-gesture alternatives.

#### 22.3 Integration and platform tests

Where available, test:

- Feed API integration.
- Video metadata and playback-source resolution.
- Active-player cleanup.
- Network disconnect and recovery.
- App foreground/background behavior.
- Engagement API consistency.
- Comment-screen navigation continuity.
- Shared-link routing.
- Native player resource release.
- Relevant iOS and Android build behavior.

Use deterministic test fixtures and test doubles at appropriate boundaries. They must not become the production source of feed items, playback content, or engagement results.

Execute the available type checks, linting, tests, and build validations. State the commands executed and their actual outcomes.

### 23. Documentation and Portable Integration Contracts

Create or update documentation covering:

- Short-form module responsibilities.
- Navigation and deep-link contracts.
- Feed retrieval and pagination.
- Active-item and player-lifecycle behavior.
- Preloading and resource-management policy.
- Engagement operations.
- Comment and creator integration.
- Sharing and safety-control contracts.
- Recommendation and watch-history integration.
- Authentication and entitlement boundaries.
- Telemetry events and privacy safeguards.
- Supported native player capabilities.
- Testing and validation commands.
- Known limitations and external dependencies.

When authoritative contracts are missing, document concrete proposed request and response schemas, event names, identifiers, permissions, errors, and state transitions. Mark them as proposed so an independent integration environment can reconcile them explicitly.

Do not claim that a proposed endpoint or unavailable backend service is already functional.

### 24. Explicitly Out of Scope

Do not implement:

- A new recommendation-ranking engine.
- Backend short-form feed generation.
- Video storage, transcoding, or CDN infrastructure.
- A replacement for the shared mobile video player.
- A new comments service.
- A separate engagement or subscription backend.
- A moderation engine or administrative moderation console.
- A complete video editor or creator production suite.
- Backend analytics aggregation.
- Payment, subscription, or entitlement systems.
- Unrelated account settings, upload, live-stream, or creator functionality.
- Additional architecture, QA, integration, or production-readiness prompt phases.

Implement only the assigned short-form mobile experience, its integration with established systems, required tests, and documentation.

### 25. Definition of Done

This milestone is complete when all applicable requirements below are satisfied:

1. A dedicated short-form feed retrieves real platform content through the established API.
2. Users can move vertically between videos while active playback follows the correct item.
3. The shared player correctly handles initialization, buffering, failures, transitions, and cleanup.
4. Preloading is bounded, cancellable, and does not compromise active playback.
5. Feed pagination, refresh, and deduplication follow the authoritative contract.
6. Supported engagement actions use actual API operations and reconcile success or failure.
7. Comments, creator navigation, subscription state, and sharing integrate with their established modules.
8. Supported discovery feedback, reporting, and blocking behave correctly.
9. Watch-history and analytics integrations conform to the platform's established contracts.
10. Authentication, entitlements, restricted content, and account-specific state remain secure and consistent.
11. Mobile lifecycle transitions and network failures are handled without persistent playback or resource leaks.
12. The interface meets the applicable accessibility and design-system requirements.
13. Automated tests cover the major success paths, failure paths, race conditions, and navigation transitions.
14. Available static checks, tests, and build validations have been executed and accurately reported.
15. Documentation describes implemented behavior, authoritative contracts, and unresolved dependencies.
16. No fabricated production content, fake engagement, hardcoded secrets, placeholder functionality, or undocumented integration assumptions remain within the defined scope.

### 26. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Short-form feed implementation**
- **Playback and preloading behavior**
- **Feed pagination and recovery**
- **Engagement and comment integration**
- **Creator navigation and sharing**
- **Safety and personalization controls**
- **Analytics and history integration**
- **Security and resource-management safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **iOS and Android build results**
- **Documentation created or updated**
- **External configuration requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Clearly distinguish actual implemented behavior from proposed contracts and unavailable services. Do not claim performance improvements, real production recommendation behavior, or end-to-end playback success unless supported by executed validation.

### 27. Final Execution Directive

Treat this prompt as the active implementation assignment for the mobile short-form video experience of the YouTube-style video platform.

Inspect the project artifacts genuinely available in the execution environment. Implement the complete bounded scope, preserve the existing architecture and contracts, run applicable tests and validations, and document the actual outcome.

Do not respond with a plan alone. Do not ask the user to choose which task to implement. Do not rebuild unrelated platform functionality, invent backend capabilities, or create unplanned project phases.

Deliver a complete, secure, accessible, and verifiably working implementation within the defined boundaries.

**Begin implementation now.**
