# YouTube-Style Video Platform — Mobile Prompt — Volume 7

## Native Video Upload, Creation, Publishing, and Creator Analytics

### 1. Mission and Implementation Scope

Implement the production-grade **native mobile video creation, upload, publishing, video-management, and creator-analytics experience** for the YouTube-style video platform using React Native and TypeScript on iOS and Android.

The platform targets approximately 250 million registered users and 50 million daily active users. This milestone must implement its bounded mobile responsibilities while remaining compatible with a distributed, production-grade platform.

Deliver working mobile functionality, not static screens. Users must be able to select or capture eligible video content, configure video metadata, initiate uploads, track upload and processing states, recover from supported interruptions, publish or schedule content where supported, manage their own videos within the available mobile scope, and inspect creator-performance metrics exposed by the backend.

Every implemented action must have real behavior, appropriate validation, useful feedback, and an explicit success or failure state.

This prompt is independently executable in a fresh coding-agent conversation. Include all necessary implementation instructions and portable integration requirements directly in the work.

### 2. Technology and Global Constraints

Use the established project technology direction:

- **Mobile application:** React Native and TypeScript.
- **Backend:** TypeScript and NestJS.
- **Primary database:** PostgreSQL.
- **Caching and distributed state:** Redis where relevant to backend services.
- **Video infrastructure:** Object storage, upload authorization, server-side processing, transcoding, thumbnails, and adaptive streaming delivery.
- **Platform architecture:** Strongly typed contracts, modular application boundaries, secure authentication, and independently deployable services.
- **Deployment:** Production-oriented iOS and Android builds with appropriate environment configuration, telemetry, and release practices.

Inspect the repository and project artifacts actually available in the execution environment before making changes. Follow the existing navigation, component, state-management, API, authentication, storage, media, telemetry, and testing conventions.

Use authoritative project-wide contracts when supplied. Do not assume that another coding-agent conversation generated accessible files or established undocumented decisions.

If required contracts are missing, implement a coherent mobile integration layer against explicitly documented proposed contracts. Identify those contracts as proposals, rather than claiming that corresponding backend endpoints or services exist.

### 3. Required Deliverables

Implement these mobile capabilities:

1. Native media selection and supported video-capture entry points.
2. Video preparation and pre-upload validation.
3. Upload initialization, transfer, progress, retry, and interruption handling.
4. Video metadata and publishing configuration.
5. Upload processing and publishing status.
6. Creator access to their own uploaded videos and relevant management actions.
7. Mobile-facing creator analytics.
8. Safe navigation between creator workflows and the viewer application.
9. Permissions, accessibility, privacy protections, observability, and performance safeguards.
10. Automated tests and portable integration documentation.

Structure the implementation into appropriately separated screens, reusable components, domain models, API repositories, upload coordination, platform adapters, and state management.

Keep the scope coherent. Do not attempt to rebuild the entire web Creator Studio, video-processing infrastructure, or other independently owned project areas.

### 4. Creator Entry Points and Navigation

Integrate creator functionality into the established mobile application without replacing its global navigation architecture.

Provide accessible entry points for authenticated users to:

- Start a video upload.
- Select or capture video content.
- View current and recent upload jobs.
- Review their own published videos.
- Open an individual video's creator-management screen.
- View available performance analytics.
- Return to ordinary viewing, channel, and library experiences.

Respect account permissions and any backend-provided creator eligibility restrictions. Users without the required permissions must receive an appropriate explanation and recovery path instead of accessing unauthorized operations.

Support both new and existing accounts, expired sessions, account switching, and logout.

Preserve established viewer functionality, including home, search, video playback, channels, subscriptions, comments, playlists, and account settings.

### 5. Native Media Selection and Capture

Implement media acquisition using established, maintained React Native libraries and appropriate native platform APIs.

#### 5.1 Media selection

Support selecting eligible video files through the appropriate iOS and Android media-picker interfaces.

Handle:

- User cancellation.
- Permission denial or restricted access.
- Temporary or inaccessible file references.
- Unsupported formats.
- Large source files.
- Source-video duration and file-size restrictions.
- Insufficient storage where detectable.
- Interrupted selection or app lifecycle changes.

Use the least-privilege platform permissions necessary. Prefer system-mediated selection when it avoids broad media-library access.

Do not assume media files reside at stable absolute file paths. Handle platform-specific content URIs, temporary files, security-scoped resources where applicable, and file-access lifecycles correctly.

#### 5.2 Video capture

Where supported by the project's existing mobile capabilities and dependencies, provide an entry point to record a video using the device camera.

Implement appropriate camera and microphone permission handling, capture cancellation, recording errors, and returning the resulting media into the standard upload preparation workflow.

If an existing recording capability is already available, reuse it rather than creating a competing native capture system.

Do not build a full professional video-editing application in this milestone. Keep recording and editing bounded to what is needed for a functional mobile publishing workflow.

### 6. Pre-Upload Validation and Video Preparation

Before starting a transfer, validate the selected video against the constraints provided by the backend contract and supported upload capabilities.

Validate applicable properties such as:

- File readability and availability.
- Supported media formats.
- File size.
- Video duration.
- Required metadata.
- Account upload restrictions.
- Required user permissions.
- Available local resources where detectable.

Do not rely exclusively on filename extensions or file-picker filters to validate content.

When media inspection is needed, use a maintained media library or platform capability and avoid unnecessary full-file reads.

Display clear, actionable validation errors. Do not silently discard user selections or fabricate media metadata.

If local compression or preparation is part of the existing architecture, implement the required integration and manage temporary files, cancellation, resource use, and cleanup. Do not add expensive transcoding dependencies without a justified project requirement.

### 7. Video Metadata and Publishing Configuration

Implement a creator form for configuring video publication.

Support the fields exposed by the authoritative backend contract, including relevant properties such as:

- Video title.
- Description.
- Thumbnail selection or upload.
- Visibility settings, such as public, unlisted, or private, when supported.
- Audience designation and age-related declarations required by the platform.
- Category or content classification where supported.
- Tags or other discovery metadata where supported.
- Comment availability or other applicable moderation settings.
- Scheduling or publication time where supported.
- Captions or subtitle attachment where supported.
- Applicable licensing and distribution choices exposed to creators.

Do not invent additional persisted fields or enumerate unsupported visibility modes.

Implement:

- Field-level validation.
- Character limits and required-field feedback.
- Keyboard-safe form behavior.
- Draft metadata state.
- Cancellation and discard confirmation where necessary.
- Clear separation between a saved draft, an upload in progress, processing, and successful publication.
- Useful validation messages returned by the backend.
- Time-zone-aware scheduling controls if scheduling is supported.

Users must understand which metadata has been saved, which changes remain local, and which changes were actually accepted by the server.

If draft recovery or server-side draft persistence exists in the authoritative contract, integrate with it. Otherwise, do not pretend that a local form is a server-backed draft.

### 8. Upload Lifecycle and Transfer Architecture

Implement a robust mobile upload coordinator rather than embedding transfer logic directly in the screen components.

The coordinator must support the phases required by the actual upload contract:

1. Validate the source media and user input.
2. Request upload initialization or authorization.
3. Receive the backend's upload identifier and authorized transfer details.
4. Transfer the video using the prescribed upload protocol.
5. Report progress where the protocol and client library allow it.
6. Finalize or complete the upload as required.
7. Retrieve the resulting upload or processing status.
8. Reflect the authoritative server status in the UI.

Use the supplied upload protocol. If it defines resumable or multipart uploads, follow its session, part, checksum, offset, completion, and retry semantics precisely.

Do not replace an established secure upload protocol with an improvised one.

#### 8.1 Progress reporting

Show meaningful upload status, including the available information about:

- Pending upload.
- Upload initialization.
- Transfer progress.
- Paused, interrupted, or waiting state.
- Transfer completion.
- Server-side processing.
- Publication readiness.
- Successful publication.
- Recoverable failure.
- Terminal failure.

Display byte counts, estimated remaining time, or transfer speed only when sufficiently reliable information is available.

Do not fabricate progress percentages or claim that a video is published merely because the local transfer reached 100 percent.

Keep transfer progress separate from server-side processing progress.

#### 8.2 Upload concurrency

Define a deliberate policy for simultaneous uploads based on supported resource limits and the authoritative contract.

Avoid uncontrolled concurrent transfers that exhaust device memory, battery, networking resources, or local storage.

If multiple queued uploads are supported, provide a clear queue and ensure each upload has independent lifecycle state.

### 9. Interruption, Retry, and Recovery

Mobile uploads must account for unreliable connectivity and application lifecycle transitions.

Handle:

- Network disconnection.
- Connection restoration.
- Request timeout.
- Expired authorization.
- Process or app interruption.
- App moving into the background.
- User cancellation.
- Upload-session expiration.
- Partial-transfer failure.
- Finalization failure.
- Server-side processing failure.
- Repeated or stale status responses.

Retry only when allowed by the upload protocol. Use bounded retries, appropriate backoff, and idempotent operations when supported.

For resumable uploads, persist only the minimal metadata necessary to resume, such as a server-provided session identifier and required transfer state. Store sensitive session information using an appropriate protected-storage mechanism and the security requirements of the protocol.

Do not persist permanent credentials or expose upload authorization secrets in logs, analytics, crash reports, or ordinary application state.

If an upload cannot be resumed safely, communicate the problem and offer the supported recovery path.

Do not assume the operating system will keep JavaScript running indefinitely in the background. Use platform-supported background-transfer capabilities where required and compatible with the established architecture. Accurately document any OS restrictions that prevent uninterrupted transfers.

### 10. Upload Cancellation and Cleanup

Implement upload cancellation for every state where the server and transfer protocol permit it.

Cancellation must:

- Stop local transfer work where possible.
- Cancel pending requests safely.
- Prevent stale callbacks from mutating the current UI.
- Reconcile or abort the server-side session through the prescribed contract.
- Clean up temporary local media when it is no longer needed and deletion is safe.
- Preserve media still owned by the user's library.
- Prevent a late completion response from incorrectly restoring a cancelled upload.

Distinguish cancellation of a transfer from deletion of an already uploaded video.

If cancellation cannot guarantee immediate termination of backend processing, show the actual status and explain the limitation instead of displaying a false terminal state.

### 11. Thumbnail Selection and Processing Status

Implement thumbnail functionality exposed by the established mobile and backend contracts.

Where custom thumbnail selection is supported:

- Allow the creator to select an eligible image or video frame.
- Validate size, format, and dimensions against the authoritative constraints.
- Display a preview.
- Upload through the approved media flow.
- Track the actual upload outcome.
- Handle rejected images or processing failures.
- Keep the selected thumbnail associated with the correct video.

Where the backend automatically generates thumbnails, display the generated thumbnail when available and render appropriate placeholders while processing.

Do not implement a new thumbnail-generation or image-processing backend service here.

### 12. Upload Queue and Creator Video Management

Create an upload-management screen displaying active, queued, recently completed, and failed jobs according to the product's supported history and persistence model.

For each upload, show available information such as:

- Video title or source filename.
- Thumbnail when available.
- Upload and processing status.
- Transfer progress when active.
- Last-updated time.
- Recoverable error summary.
- Available actions appropriate to the current state.

Support retry, cancel, resume, review, or dismissal only where the current state and backend contract permit those actions.

Do not remove server-side records merely because a row was dismissed from the mobile UI.

Implement a creator-facing list of the user's existing uploaded or published videos by consuming the authoritative creator/video-list API.

Support:

- Pagination.
- Refresh.
- Loading and empty states.
- Server-provided status labels.
- Opening a video's management view.
- Editing supported metadata.
- Changing visibility where authorized.
- Opening the published video in the viewer experience.
- Deleting a video only when supported by the backend, with appropriate confirmation and error handling.

Do not create separate mobile definitions of video ownership, publication status, or deletion rules. Reuse the platform's authoritative entities, permissions, and lifecycle semantics.

### 13. Mobile Creator Analytics

Implement a focused creator-analytics experience using metrics exposed by the existing backend.

Display applicable metrics such as:

- Views.
- Watch time.
- Subscriber changes.
- Performance over a selected period.
- Video-level performance.
- Published content summaries.
- Other creator metrics explicitly supported by the API.

Use appropriate date ranges, trend visualizations, loading states, and empty-data presentation.

Requirements:

- Consume actual backend analytics.
- Display the selected time range and relevant metric definitions.
- Respect backend aggregation and attribution windows.
- Avoid presenting estimates as finalized metrics without indicating their status.
- Handle missing, delayed, or unavailable measurements safely.
- Use accessible alternatives for charts and trend visualizations.
- Avoid excessive polling and unnecessary repeated data retrieval.
- Apply pagination or bounded result sizes to video-performance lists where appropriate.

Do not calculate platform analytics from incomplete local viewing events. Do not invent values, fabricate chart datasets in the production application, or build the backend analytics pipeline in this milestone.

When the analytics API is unavailable or not yet implemented, document the exact dependency and integration contract. Do not ship mock metrics as real creator performance.

### 14. API and Portable Integration Contracts

All requests must use the centralized, typed API infrastructure established by the project.

Use existing contracts for authentication, authorization, video metadata, media storage, upload sessions, processing status, thumbnails, creator video lists, publication, scheduling, deletion, and analytics.

Implement appropriately typed models and repository interfaces for operations such as:

- Initializing an upload.
- Obtaining authorized transfer instructions.
- Sending or resuming media data.
- Completing or aborting an upload.
- Querying upload and processing status.
- Creating or updating video metadata.
- Uploading or selecting a thumbnail.
- Publishing a video or scheduling publication where supported.
- Listing the authenticated creator's videos.
- Editing supported video properties.
- Performing supported deletion operations.
- Retrieving creator analytics.

These are required client responsibilities, not permission to invent incompatible endpoint paths.

Respect the authoritative contract's:

- Authentication and authorization requirements.
- Identifier formats.
- Request and response schemas.
- Upload protocols.
- Pagination.
- Error structures and status codes.
- Idempotency rules.
- Session expiration behavior.
- Status transitions.
- Rate limits.
- API versioning and compatibility requirements.

Where authoritative definitions are missing, create explicit portable integration documentation containing the proposed operation names, payload schemas, protocol expectations, error handling, ownership rules, lifecycle transitions, and unresolved dependencies.

Keep proposed contracts clearly distinguished from verified, implemented endpoints.

Do not create fake successful uploads, placeholder storage adapters, fabricated processing status, or an in-memory mock repository as the real production application path.

### 15. Authentication, Authorization, and Privacy

All creator operations must use the application's established authenticated API client.

Implement or preserve these safeguards:

- Enforce creator permissions exposed by the backend.
- Prevent editing or deleting videos owned by another account.
- Associate every upload session with the correct authenticated account.
- Handle expired sessions through the centralized authentication flow.
- Clear or isolate account-specific upload metadata when users log out or switch accounts.
- Prevent a new account from accidentally inheriting a previous account's pending upload identity or private drafts.
- Avoid logging raw media paths, authorization headers, upload tokens, or sensitive account data.
- Validate identifiers and deep links before opening creator screens.
- Avoid exposing private videos through unintended public navigation.
- Use secure handling for upload session credentials and temporary signed URLs.
- Respect user cancellation and applicable platform permission restrictions.

Upload authorization and ownership must remain enforced by the backend. Client-side controls are not substitutes for server authorization.

Do not log complete signed URLs if they contain bearer credentials or other sensitive query parameters.

### 16. Media and Device Resource Management

Uploads can involve large files and extended network operations. Implement resource management appropriate for mobile devices.

Requirements include:

- Avoid reading an entire large video into JavaScript memory.
- Use streaming or chunked transfers when required by the upload protocol and available libraries.
- Avoid duplicate copies of large media files.
- Clean up generated temporary files safely.
- Release native media resources when they are no longer needed.
- Handle interrupted file access.
- Prevent memory leaks and stale upload callbacks.
- Apply reasonable concurrency and retry limits.
- Avoid excessive battery consumption and background polling.
- Display a recoverable error when required local storage or media access becomes unavailable.

Do not delete the user's original selected media as part of upload cleanup.

If the backend requires checksums, media inspection results, or integrity metadata, implement the client responsibility according to the authoritative contract.

### 17. State Management and Application Lifecycle

Use the project's established state-management and server-state libraries.

Implement explicit state transitions for uploads, creator metadata, processing, publishing, and analytics.

Do not make screen components responsible for all networking, upload orchestration, native file handling, and state reconciliation.

Requirements:

- Maintain stable upload identities.
- Prevent duplicate submissions.
- Deduplicate or reconcile overlapping status responses.
- Handle stale requests and cancelled operations.
- Keep transfer and processing states distinct.
- Invalidate or refresh affected creator-video caches after successful mutations.
- Preserve the actual operation result when navigating away from a screen.
- Restore only upload jobs whose state can be recovered safely.
- Avoid leaking user-scoped state across account changes.
- Handle app foregrounding and backgrounding without assuming JavaScript remains continuously active.

Use persistent local job state only where it is necessary and justified by the supported recovery model. Do not persist sensitive credentials or unsafe raw media data merely to make recovery easier.

### 18. Accessibility and User Experience

Produce a polished, native-feeling creator workflow consistent with the established design system.

Implement:

- Accessible upload progress indicators.
- Screen-reader announcements for meaningful status changes.
- Clear labels and validation for metadata forms.
- Keyboard-safe layouts.
- Appropriate touch targets.
- Dynamic type and readable layouts.
- Loading, empty, error, retry, and disabled states.
- Confirmation dialogs for destructive actions.
- Safe-area support.
- Localization-ready strings.
- Locale-aware date and time handling.
- Accessible charts or equivalent text summaries.
- Light and dark themes if supported by the application.
- Platform-appropriate permission prompts and navigation behavior.

Make it clear which stage a video has reached. A user must not have to infer whether a video is transferring, processing, failed, private, published, or scheduled.

Use the existing component library where available. Do not introduce a conflicting design system or temporary-looking controls.

### 19. Observability and Operational Readiness

Integrate with the project's existing telemetry and error-reporting conventions.

Record useful, privacy-safe signals for:

- Upload initialization failures.
- Transfer failures.
- Retry attempts.
- Resume and recovery outcomes.
- Upload cancellation.
- Upload finalization.
- Server-processing failure states surfaced to the client.
- Metadata-save failures.
- Publication failures.
- Creator-analytics API errors.

Include relevant operation correlation identifiers when permitted by the contract.

Never include raw media contents, credentials, signed upload URLs, passwords, or unnecessary personal data in logs.

Use client-side metrics only for behavior the client can observe reliably. Do not claim end-to-end server-processing timings or successful publication based on client-side events alone.

### 20. Required Automated Tests

Add tests using the established project testing framework.

#### 20.1 Unit tests

Cover:

- Video metadata validation.
- Supported upload-state transitions.
- Upload progress calculation.
- Upload retry and cancellation decisions.
- Resumable-upload state restoration where supported.
- Duplicate-submission prevention.
- Processing-status reconciliation.
- Account changes and user-scoped job isolation.
- Thumbnail selection and metadata mapping.
- Scheduling validation when supported.
- Creator-video mutation handling.
- Analytics time-range and response mapping.

#### 20.2 Component and screen tests

Test:

- Media-selection cancellation and permission-denied states.
- Video-preparation validation errors.
- Metadata form validation.
- Upload progress and failure presentation.
- Retry, resume, and cancellation controls.
- Processing and publication states.
- Creator video list loading, refresh, and pagination.
- Editing and visibility-change flows.
- Destructive-action confirmation.
- Analytics loading, error, empty, and populated states.
- Authentication expiry during creator operations.

#### 20.3 Integration and platform tests

Test where the environment supports them:

- Upload repository serialization and error handling.
- Authorized upload initialization and completion workflows against test fixtures or controlled integration environments.
- Retry behavior and idempotency expectations.
- Cancellation races and late responses.
- Interrupted transfer recovery.
- App foreground/background transitions.
- Temporary-file cleanup.
- Authorization failures and account switching.
- Cache invalidation following metadata or visibility changes.
- iOS and Android media-picker and permission behavior.

Automated tests may use deterministic fixtures and mock network boundaries for test isolation. Such mocks must not be shipped as the production upload implementation.

Execute the relevant type-checking, linting, unit tests, integration tests, and build checks available in the environment. Report what was actually run.

### 21. Documentation and Portable Handoff

Create or update documentation covering:

- Mobile creator module organization.
- Supported media-selection and capture behavior.
- Upload lifecycle and state transitions.
- Upload protocol and resumability requirements.
- Retry, cancellation, and cleanup behavior.
- API operations and authoritative contract sources.
- Thumbnail and metadata integration.
- Creator video-management operations.
- Analytics API dependencies.
- Required iOS and Android permissions.
- Environment configuration and native build requirements.
- Secure handling of upload authorization.
- Local state and recovery strategy.
- Test commands and results.
- Known limitations and unresolved dependencies.

If a backend or native capability is unavailable, document the precise integration dependency and the validation that remains necessary.

Portable documentation must be sufficient for an independent integration environment to connect the mobile implementation to the actual backend without needing this coding conversation.

### 22. Explicitly Out of Scope

Do not implement the following as part of this milestone:

- Backend video ingestion services.
- Backend upload-session creation, persistence, or cleanup workers.
- Video transcoding or encoding infrastructure.
- Server-side thumbnail generation.
- Video storage or CDN infrastructure.
- Backend processing orchestration and status management.
- Backend metadata or publication services.
- Backend creator analytics aggregation.
- A complete professional video-editing suite.
- A replacement for the existing mobile application architecture.
- A full web Creator Studio.
- Live-stream production controls or live chat.
- Subscription billing, memberships, or payment processing.
- Features belonging to other planned mobile implementation volumes.
- New architecture, QA, integration, or production-readiness prompt phases.

Implement the assigned mobile functionality and its required supporting tests, integration contracts, and documentation. Consume backend capabilities through their authoritative contracts rather than pretending to implement backend services.

### 23. Definition of Done

This milestone is complete when all applicable requirements below are satisfied:

1. Creators can select supported video files and enter the upload workflow.
2. Supported native capture is integrated where required by the project.
3. Media and metadata validation works and communicates actionable errors.
4. Upload initialization, transfer, progress, completion, and processing states use the established contracts.
5. Retry, cancellation, and resume behavior are safe and consistent with the actual upload protocol.
6. Upload jobs remain correctly associated with their authenticated accounts.
7. Creators can configure supported metadata and publication options.
8. Thumbnail functionality works to the extent supported by the platform contract.
9. Creators can inspect their own uploaded and published videos and perform authorized management actions.
10. Creator analytics display actual backend-provided information without fabricated production values.
11. Navigation integrates with the existing viewer application without regressions.
12. Device-resource management and sensitive-data handling follow the stated safeguards.
13. Automated tests cover the critical success paths, failure paths, state transitions, and authorization-sensitive behavior.
14. Relevant available static checks, tests, and build validations have been executed.
15. Documentation describes the implementation and identifies any unavailable backend, native, or environment dependency.
16. No fake production services, hardcoded secrets, silent contract assumptions, placeholder implementations, or intentional functionality gaps remain within this milestone's scope.

### 24. Completion Report

After completing implementation, provide a factual report covering:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Media-selection and capture functionality**
- **Upload lifecycle and recovery implementation**
- **Metadata, thumbnails, and publishing functionality**
- **Creator video-management functionality**
- **Analytics functionality**
- **API and portable integration contracts**
- **Security and resource-management safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **Build results**
- **Documentation updated**
- **Native configuration or external service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Clearly separate features implemented in the mobile client from backend dependencies that are merely specified or awaiting integration. Do not report a successful end-to-end upload, real-world publication, or background-transfer capability unless the relevant behavior was actually verified.

### 25. Final Execution Directive

Treat this prompt as the active engineering assignment for the mobile creator and video-upload experience of the YouTube-style video platform.

Inspect the materials genuinely available in the execution environment. Implement the defined scope, preserve existing application behavior, respect authoritative platform contracts, and perform all available tests and validations.

Do not respond with planning alone. Do not ask the user to choose which part to implement. Do not implement unrelated platform functionality, invent backend capabilities, or append unplanned project phases.

Make sound engineering decisions within the defined scope, document actual limitations, and deliver the strongest verifiable implementation possible.

**Begin implementation now.**
