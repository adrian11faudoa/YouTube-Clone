# YouTube-Style Video Platform — Mobile Prompt — Volume 8

## Live Streaming, Real-Time Chat, Interactive Viewing, and Creator Live Controls

### 1. Mission and Implementation Scope

Implement the production-grade **native mobile live-streaming experience** for the YouTube-style video platform using React Native and TypeScript on iOS and Android.

This milestone covers the viewer's live-stream discovery and playback experience, real-time chat, live-stream interactions, moderation-aware controls, and mobile creator controls for starting, monitoring, and ending live streams where supported by the platform's established broadcasting architecture.

The platform targets approximately 250 million registered users and 50 million daily active users. Mobile components must be engineered for high concurrency, unreliable networks, changing application lifecycle states, and real-time interactions without moving backend responsibilities into the client.

Deliver real, functional application behavior. Users must be able to open available live streams, watch the live video through the established delivery infrastructure, participate in authorized live chat, handle playback and connection failures, and use applicable creator controls. Do not simulate an active live broadcast, invent chat messages, or display fabricated viewer counts as production data.

This prompt is independently executable in a fresh coding-agent conversation. Include the implementation details, integration boundaries, tests, and documentation required by its scope.

### 2. Technology and Engineering Constraints

Use the established project technology direction:

- **Mobile application:** React Native and TypeScript.
- **Backend:** TypeScript and NestJS.
- **Primary database:** PostgreSQL.
- **Distributed cache and coordination:** Redis where applicable to backend services.
- **Realtime infrastructure:** The platform's established WebSocket or equivalent realtime transport.
- **Live video:** The platform's established ingest, transcoding, packaging, and delivery infrastructure.
- **Streaming delivery:** HLS, DASH, or the exact supported delivery protocol defined by the platform.
- **Authentication:** The shared platform authentication and authorization contracts.
- **Observability:** The existing structured logging, telemetry, and error-reporting conventions.

Inspect the repository and available project artifacts before changing the implementation. Follow existing mobile navigation, player, API, realtime, design-system, media, authentication, and testing conventions.

Use authoritative architecture and API contracts when supplied. Do not assume access to files generated in another AI conversation. If a required integration contract is unavailable, define a concrete, portable proposed contract and document the missing dependency rather than pretending the service exists.

### 3. Required Deliverables

Implement the following mobile functionality:

1. Live-stream entry points and supported live content discovery.
2. Native live-stream playback and playback-state coordination.
3. Real-time live-chat rendering and interaction.
4. Chat connection, reconnection, synchronization, and backpressure handling.
5. Viewer interaction controls supported by the platform.
6. Reporting, blocking, and moderation-aware viewer controls.
7. Creator live-stream preparation and start controls, where supported.
8. Creator monitoring, stream-health information, and live-session termination.
9. Navigation, app lifecycle, background/foreground, and connection recovery.
10. Tests, observability, security safeguards, and portable integration documentation.

Keep the player, realtime client, chat state, creator controls, stream metadata, and screen components appropriately separated. Reuse the existing video player and domain models rather than introducing competing implementations.

### 4. Live-Stream Entry Points and Discovery

Integrate live-stream navigation into the existing mobile platform.

Provide appropriate entry points from existing surfaces, where supported by the project:

- Home and discovery feeds.
- Search results.
- Channel pages.
- Subscription feeds.
- Notifications.
- Direct links to live streams.
- Existing creator video-management screens.

Live-stream cards and rows should display only available authoritative information, such as the stream title, channel, thumbnail, live status, and viewer count where provided.

Support loading, empty, error, and unavailable states. Follow established API pagination and refresh semantics.

When a stream is no longer live, no longer accessible, or has been removed, provide a useful fallback. Do not direct users to a non-existent player route or show a stream as active because a stale local cache says so.

Do not rebuild home, search, channel, or subscription systems in this milestone. Integrate through their established navigation and data contracts.

### 5. Live-Stream Viewer Experience

Implement a complete mobile live-stream viewing screen.

The screen must support:

- Live video playback using the existing shared player infrastructure.
- Stream title, creator identity, and applicable channel navigation.
- Live-status presentation.
- Viewer-count display where provided.
- Full-screen playback and appropriate orientation behavior.
- Playback controls appropriate to the live-stream delivery protocol.
- Loading, connecting, buffering, reconnecting, and playback-error states.
- A clear distinction between live playback and any available DVR or time-shifted playback.
- Supported stream-ended and stream-unavailable states.
- Recovery when the device network or delivery service becomes temporarily unavailable.

Keep live-stream metadata synchronized with authoritative backend state. Update dynamic fields only through supported API responses, realtime events, or a justified refresh mechanism.

Do not fabricate viewer counts, stream duration, creator status, or live playback position.

#### 5.1 Playback behavior

Reuse the project's video player abstraction when available.

Integrate with the established live playback URL and authorization mechanism. Do not hardcode permanent media URLs, expose private stream keys, or bypass access controls.

Handle the player states required by the actual streaming library, including initialization, ready, playing, buffering, paused where supported, failed, and ended.

Implement appropriate retry behavior and prevent concurrent reconnect loops.

Where a live stream's delivery format does not support seeking, do not present ordinary on-demand seek controls as functional. Where DVR functionality is supported, respect the backend's permitted time-shift window.

Maintain correct behavior when the device changes network, the application enters the background, or the user navigates away from the player.

### 6. Picture-in-Picture and Background Playback

Support picture-in-picture or background playback only to the extent that it is compatible with the established product policy, player library, operating-system capabilities, and native configuration.

Where picture-in-picture is supported:

- Integrate with the native lifecycle.
- Preserve stream identity and player state.
- Handle returning to the application.
- Avoid creating duplicate player instances.
- Respect user-initiated termination and stream termination.

Where background playback is not supported by product policy or platform constraints, transition cleanly and release unnecessary resources.

Do not claim that background playback or picture-in-picture works on a platform where the required configuration or native capability is absent.

### 7. Real-Time Live Chat

Implement an authenticated or guest-capable live-chat experience according to the established platform's permissions.

Use the existing realtime client where possible. Follow its authentication, connection, event, heartbeat, error, and reconnection conventions.

#### 7.1 Rendering

Display chat messages with supported information, such as:

- Stable message ID.
- Author or channel identity.
- Message content.
- Server-authoritative timestamp.
- Applicable creator, moderator, or system-message designation.
- Moderation or visibility state where the contract exposes it.
- Relevant reply or interaction metadata, if supported.

Handle messages with missing optional fields safely.

Use an efficient list implementation appropriate for a sustained stream of incoming events. Avoid unbounded history retention, unnecessary rerenders, and layout work that harms playback performance.

#### 7.2 Message composition

Allow authorized users to submit messages through a validated input field.

Implement:

- Input validation and limits from the authoritative contract.
- Clear submission and delivery states.
- Appropriate keyboard behavior.
- Duplicate-submission prevention.
- Server-side rejection feedback.
- Rate-limit feedback.
- Connection-unavailable feedback.
- Accessible controls and screen-reader labels.

Treat a message as sent only when the relevant contract confirms the appropriate delivery state. If the UI optimistically displays a pending message, visually distinguish it and reconcile it after the server response.

Do not silently retry a chat submission in a way that can create duplicate messages.

#### 7.3 Reactions and supported interactions

If the backend provides live reactions, message replies, creator recognition, or other stream interactions, implement the corresponding controls using authoritative contracts.

Do not add unsupported interactive features simply because they are common on other streaming platforms.

Keep interactions rate-limited according to the server rules. If a reaction animation is optimistic, ensure that it cannot be confused with server-confirmed activity when confirmation matters.

### 8. Realtime Connection and Message Consistency

Implement robust connection management for live chat and other realtime stream state.

Handle:

- Initial connection.
- Authentication and authorization failures.
- Network loss and restoration.
- Server-initiated disconnects.
- Heartbeat or keepalive requirements.
- Bounded retry with backoff and jitter where appropriate.
- App foregrounding and backgrounding.
- Stream termination.
- Chat closure or temporary unavailability.
- Repeated or duplicated events.
- Out-of-order events where the contract permits them.

Use the established event identifiers, sequence numbers, cursors, or timestamps to deduplicate or reconcile events where supported.

Do not assume realtime delivery guarantees that the server contract does not provide. When history reconciliation is supported, recover missed messages without inserting duplicates.

Apply backpressure and bounded in-memory retention. Under heavy message throughput, keep playback responsive and avoid rendering every event as an unbatched state update if the architecture provides a safer approach.

The client must not create its own competing authoritative chat history.

### 9. Chat Modes, Access Rules, and Moderation

Implement chat behavior according to the platform's established chat modes and permission model.

Supported settings may include:

- Normal chat.
- Slow mode.
- Subscribers-only chat.
- Members-only chat.
- Restricted or closed chat.
- Moderator and creator permissions.
- Stream-ended chat state.

The actual list of modes must come from the authoritative contract.

Display relevant restrictions clearly. A disabled composer should explain the applicable reason when the server provides that information.

Handle rejected messages without losing unrelated typed content unnecessarily.

Where the platform supports blocking, reporting, muting, or hiding participants, implement the viewer-facing interactions using established APIs and moderation semantics.

Requirements:

- Confirm destructive or consequential actions when appropriate.
- Prevent duplicate submissions.
- Reflect moderation changes only through confirmed responses or explicitly managed optimistic state.
- Handle already blocked, deleted, inaccessible, or suspended users safely.
- Avoid disclosing sensitive moderation signals beyond the authorized user's visibility.
- Do not rely on local filtering as the sole enforcement of backend moderation policies.

Do not implement backend moderation engines, automated abuse detection, or the moderator administration system in this milestone.

### 10. Stream Lifecycle and Synchronization

Treat the backend's stream lifecycle as authoritative.

Support the applicable transitions defined by the platform, such as:

- Scheduled.
- Preparing.
- Starting.
- Live.
- Temporarily interrupted.
- Ending.
- Ended.
- Failed.
- Unavailable.

Do not introduce new enum values if an authoritative state machine already exists.

When stream status changes:

- Update the UI through established events or refresh behavior.
- Handle transitions while the viewer is actively watching.
- Stop or adapt playback when the stream ends.
- Close the chat connection when required.
- Preserve suitable navigation behavior.
- Prevent reconnect loops for terminal stream states.
- Avoid continuing to display stale live controls after the stream has ended.

Handle delayed events and out-of-order lifecycle notifications according to the server's versioning or sequence semantics.

### 11. Creator Live-Stream Preparation

Implement the mobile-facing creator setup flow only for broadcasting methods supported by the platform.

Where available, allow an authorized creator to configure supported fields such as:

- Stream title.
- Description.
- Thumbnail.
- Visibility or audience restrictions.
- Chat configuration.
- Scheduling metadata.
- Other creator-controlled live-stream properties supplied by the authoritative contract.

Validate user input and permissions before attempting to create or start a session.

Provide clear setup, validation, authorization, and initialization states.

Do not introduce unsupported publishing settings or duplicate existing creator metadata models.

#### 11.1 Broadcasting method

Determine the platform's supported broadcasting approach from the authoritative architecture and APIs.

If the project supports native camera broadcasting, implement integration with its documented ingest protocol and native media-capture requirements.

If the architecture supports streaming from another source but not from the mobile camera, implement only the mobile controls compatible with that architecture.

If the platform has no actual live-broadcast ingest contract, implement the supported creator setup and monitoring flows only, document the missing ingest capability, and do not pretend to transmit a real live video stream.

Never embed stream keys or ingest secrets in source code, telemetry, application logs, or ordinary persisted preferences.

### 12. Creator Broadcast Controls

Where mobile-originated broadcasting is supported, implement the required native camera and microphone lifecycle.

Capabilities should include the subset established by the platform architecture, potentially:

- Requesting camera and microphone permissions.
- Previewing the camera before broadcasting.
- Selecting supported front and rear cameras.
- Starting and stopping capture.
- Applying supported orientation and video configuration.
- Starting the broadcast using the approved ingest session.
- Displaying connection and stream-health state.
- Recovering from network interruption.
- Ending the broadcast safely.

Respect device constraints and supported encoder capabilities. Avoid starting a broadcast before all required permissions and resources are available.

Prevent duplicated session creation during repeated taps or retries.

Handle permissions being denied, changed, or revoked while the setup screen is active.

Do not build a full professional broadcast production suite or require unsupported advanced features such as multi-camera switching, external ingest, live scene compositing, or complex overlays.

### 13. Creator Live Dashboard

Implement a creator-facing live dashboard while a session is active.

Display information returned by the server or supported native broadcasting components, such as:

- Stream title and current status.
- Elapsed time where the source is reliable.
- Viewer count where supplied.
- Connection health or ingest status.
- Relevant stream warnings.
- Current chat state.
- Applicable moderation or chat controls.

Provide a clear, accessible end-stream action with confirmation where appropriate.

After ending a stream, reflect the actual server and broadcasting state. Close active capture and release native resources safely.

Do not equate a successful end-session request with confirmed completion when the server reports a different state or the response is ambiguous.

If the connection drops during stream termination, reconcile status using the appropriate API rather than creating an additional stream session.

### 14. Creator Chat and Moderation Controls

For creators and users granted the required permissions, expose supported controls for managing their live chat.

Depending on the established contract, these may include:

- Enabling or disabling chat.
- Selecting supported chat modes.
- Managing message restrictions.
- Removing a message.
- Muting or restricting a participant.
- Reviewing reports related to the live session where authorized.

Clearly distinguish ordinary viewer controls from creator or moderator operations.

Require backend authorization for every privileged mutation. Reflect success or failure through server responses and avoid showing controls that grant a user permissions they do not possess.

Do not implement the backend moderation policy engine or administrative moderation console.

### 15. API and Portable Integration Contracts

Use the application's centralized typed API client and established realtime abstractions.

Use authoritative contracts for:

- Live-stream discovery.
- Stream metadata and lifecycle.
- Playback URL resolution and access.
- Viewer counts or other live metrics.
- Chat connection and event schemas.
- Chat message submission and history reconciliation.
- Chat restrictions and moderation.
- Creator stream setup and initialization.
- Ingest authorization and session metadata.
- Stream-health status.
- Creator broadcast termination.
- Live-session chat configuration.

Possible mobile-facing responsibilities include:

- Retrieving stream details.
- Resolving an authorized playback source.
- Connecting to the live-chat channel.
- Submitting a chat message.
- Fetching or reconciling recent chat history.
- Applying supported moderation actions.
- Fetching creator livestream settings.
- Initializing an authorized live session.
- Retrieving stream status and health.
- Ending a live session.

These are capability requirements, not permission to invent endpoint paths or event names that conflict with project contracts.

Respect authoritative:

- Identifier formats.
- API versioning.
- Authentication and authorization rules.
- Pagination and history-reconciliation behavior.
- WebSocket or realtime event schemas.
- Error structures and status codes.
- Rate limits.
- Idempotency rules.
- Stream lifecycle values.
- Ingest and playback authorization.
- Delivery and retry guarantees.

If required contracts are absent, produce a portable integration specification with concrete proposed schemas, operations, authorization requirements, state transitions, event names, retry semantics, and unresolved dependencies. Mark these definitions as proposals rather than existing functionality.

Do not ship fake playback, fabricated chat streams, mock creator sessions, or hardcoded stream metadata as production functionality.

### 16. Security and Privacy

Treat stream metadata, realtime events, URLs, chat content, notification payloads, and route parameters as untrusted input.

Implement the following safeguards:

- Require authentication for actions that need an account.
- Respect guest access only where explicitly supported.
- Enforce creator and moderator permissions on the backend.
- Validate identifiers and deep links.
- Use the approved media authorization mechanism.
- Do not log access tokens, stream keys, signed URLs containing secrets, or private ingest metadata.
- Prevent one account's creator-session data from appearing after account switching.
- Clear protected creator state on logout where appropriate.
- Avoid storing unnecessary private chat history.
- Apply server-defined rate limits.
- Handle session expiry and authorization failures centrally.
- Avoid exposing private streams through guessed or manipulated navigation parameters.

Do not represent local permission checks as replacements for backend enforcement.

### 17. Performance and Resource Management

Live video and real-time chat compete for device resources. Keep playback smooth while handling sustained chat traffic.

Requirements:

- Reuse the shared player implementation.
- Avoid duplicate player instances.
- Release playback, audio, camera, and microphone resources when no longer needed.
- Batch or throttle high-frequency state updates when appropriate.
- Bound retained chat history and pending messages.
- Avoid uncontrolled polling and retry loops.
- Use pagination or bounded retrieval for recent chat history.
- Avoid keeping unnecessary realtime connections open.
- Reconcile app foreground and background transitions.
- Respect OS audio-focus and interruption behavior.
- Handle network changes without leaking resources.
- Avoid unnecessary screen renders driven by high-frequency viewer-count updates.

Measure or test critical performance-sensitive behavior to the extent supported by the existing environment. Do not make unsupported claims about production-scale concurrent-stream capacity based solely on client tests.

### 18. Accessibility and Mobile User Experience

Deliver a polished native experience consistent with the established visual system.

Provide:

- Accessible player controls.
- Clear chat connection and stream-status indicators.
- Screen-reader labels for interactive chat controls.
- Keyboard-safe message composition.
- Accessible start and end broadcast controls.
- Readable presentation for connection failures.
- Responsive layouts for different device sizes and orientations.
- Safe-area support.
- Dynamic text support.
- Reduced-motion behavior where appropriate.
- Accessible text alternatives for important live metrics and charts.
- Platform-appropriate permission explanations.
- Loading, empty, reconnecting, offline, and terminal states.
- Localization-ready text and locale-aware timestamps.
- Dark and light theme compatibility if supported.

The viewer should be able to understand whether a stream is loading, live, buffering, disconnected, ended, or unavailable without ambiguity.

Do not use static screenshots, fake chat rows, or nonfunctional controls as substitutes for the required implementation.

### 19. Observability and Failure Recovery

Use established mobile telemetry and error-reporting infrastructure.

Capture privacy-safe diagnostic information for:

- Playback initialization and playback failures.
- Live-stream reconnection.
- Realtime connection failures.
- Chat submission errors.
- Session authorization failures.
- Creator-session initialization.
- Broadcast start and termination errors.
- Native capture errors where supported.
- Stream-status reconciliation failures.

Use correlation IDs where permitted and available.

Do not log raw chat payloads unnecessarily, credentials, stream keys, signed URLs, or sensitive account data.

Implement bounded retries and clear recovery paths. Do not create duplicate sessions or repeat privileged mutations when the previous request's outcome is uncertain.

Where an operation may have succeeded despite a lost response, query the authoritative state before initiating an unsafe duplicate operation.

### 20. Required Automated Tests

Use the project's established test framework and native testing setup.

#### 20.1 Unit tests

Test:

- Stream metadata and lifecycle parsing.
- Playback-state transitions.
- Live-status synchronization.
- Chat event parsing and deduplication.
- Chat input validation.
- Connection-retry policies.
- Realtime event ordering where relevant.
- Rate-limit and authorization errors.
- Creator session-state transitions.
- Broadcast initialization and termination behavior.
- Account switching and state cleanup.
- Safe handling of malformed stream destinations.

#### 20.2 Component and screen tests

Test:

- Live-stream loading and unavailable states.
- Playback error and reconnecting presentation.
- Live-status transitions.
- Chat connection and reconnection.
- Message composition, pending, success, and failure states.
- Chat permission and restricted-mode presentation.
- Supported blocking, reporting, and moderation controls.
- Creator preparation and validation.
- Camera and microphone permission-denied flows.
- Creator dashboard status.
- Stream termination confirmation and error handling.

#### 20.3 Integration and platform tests

Test applicable behavior involving:

- Live metadata and playback-source repository contracts.
- Realtime connection and history reconciliation.
- Network disconnection and restoration.
- App foreground/background transitions.
- Stream-ended events during playback.
- Authorization failures.
- Duplicate action prevention.
- Creator-session recovery.
- Native media-capture resource cleanup.
- Navigation to and from live-stream screens.

Use mocks only at proper test boundaries. Do not replace production playback or realtime services with fabricated data paths.

Execute available type checking, linting, tests, and iOS/Android build validation. Report exactly which validations were run and their actual outcomes.

### 21. Documentation and Portable Handoff

Create or update documentation describing:

- Mobile live-stream modules and screen boundaries.
- Player integration and supported streaming protocols.
- Stream lifecycle and status mapping.
- Realtime connection management.
- Chat events and history-reconciliation behavior.
- Permission and moderation dependencies.
- Creator broadcast capabilities and ingest requirements.
- Required native libraries and platform configuration.
- Audio, video, camera, and microphone lifecycle behavior.
- API and authorization contracts.
- Retry and recovery rules.
- Test commands and validation results.
- Known platform limitations.
- Unresolved backend or native integration dependencies.

Where an authoritative contract was unavailable, include a portable proposed specification sufficiently precise for an independent integration environment to implement the corresponding service.

Do not claim a working end-to-end broadcast if the required ingest infrastructure is absent.

### 22. Explicitly Out of Scope

Do not implement:

- Backend live-stream orchestration.
- Ingest servers or transcoding pipelines.
- HLS/DASH packaging infrastructure.
- Backend chat services or WebSocket infrastructure.
- Backend viewer-count aggregation.
- Backend chat moderation engines.
- Administrative moderation consoles.
- A new global video-player framework when one already exists.
- An entire professional broadcasting and production suite.
- Payment, membership, or subscription-billing workflows.
- Unrelated viewer, library, account, or creator features.
- Unplanned architecture, QA, integration, or production-readiness prompt phases.

Implement only the assigned mobile experience, its necessary client integration, tests, and documentation.

### 23. Definition of Done

This milestone is complete only when all applicable criteria are met:

1. Supported live-stream entry points navigate to a functional mobile viewer.
2. Live playback uses the actual established playback integration.
3. Playback errors, reconnection, stream termination, and unavailable content are handled correctly.
4. Real-time chat uses the established transport and domain contracts.
5. Chat submission, reconnection, deduplication, and permission states work correctly.
6. Supported viewer interactions and moderation-aware controls use the appropriate APIs.
7. Creator setup and broadcast controls are implemented to the extent supported by the platform's real broadcasting architecture.
8. Creator monitoring and termination reflect authoritative stream state.
9. Camera, microphone, playback, and realtime resources are managed safely.
10. Navigation, authentication, and account boundaries remain compatible with the existing mobile application.
11. The implementation handles important network and application lifecycle failures.
12. Automated tests cover core behavior, important errors, state transitions, and authorization-sensitive actions.
13. Relevant available static checks, tests, and build validations have been executed.
14. Documentation describes actual functionality and missing dependencies.
15. No fake live broadcasts, fabricated production chat, hardcoded secrets, placeholder implementations, or undocumented integration assumptions remain within the assigned scope.

### 24. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Live-stream viewer implementation**
- **Playback integration**
- **Realtime and chat implementation**
- **Moderation-aware functionality**
- **Creator broadcasting capabilities**
- **API and portable integration contracts**
- **Security and resource-management safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **iOS and Android build results**
- **Documentation created or updated**
- **Native configuration and external-service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Distinguish working client functionality from proposed contracts and unavailable external services. Do not claim that a live broadcast, realtime connection, or end-to-end playback workflow was successfully verified unless it was actually tested.

### 25. Final Execution Directive

Treat this prompt as the active engineering assignment for the native mobile live-streaming experience of the YouTube-style video platform.

Inspect the project materials genuinely available in the execution environment, implement the complete bounded scope, preserve existing functionality and authoritative contracts, run applicable tests and validations, and document the actual result.

Do not respond with a plan alone. Do not ask the user to choose a task. Do not implement unrelated project functionality, invent unavailable backend services, or create unplanned project phases.

Complete the defined implementation to the strongest verifiable standard supported by the environment.

**Begin implementation now.**
