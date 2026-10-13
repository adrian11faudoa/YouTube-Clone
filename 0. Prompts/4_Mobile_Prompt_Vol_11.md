# YouTube-Style Video Platform — Mobile Prompt — Volume 11

## Offline Downloads, Download Management, and Offline Video Playback

### 1. Mission and Implementation Scope

Implement the production-grade **offline video downloading, download management, and offline playback experience** for the YouTube-style video platform's native iOS and Android applications using React Native and TypeScript.

The platform targets approximately 250 million registered users and 50 million daily active users. This milestone focuses on the mobile device's download lifecycle, protected media storage, download queues, offline playback, storage management, network-aware behavior, and synchronization with the platform's video and entitlement systems.

Users must be able to discover whether a video is eligible for offline viewing, initiate supported downloads, monitor download progress, pause or cancel supported operations, manage downloaded videos, play eligible content without connectivity, and understand when downloaded content becomes unavailable.

All behavior must be connected to the platform's actual media-download, authorization, entitlement, and playback contracts. Do not simulate downloaded videos, claim that unavailable content can be played offline, or treat a cached streaming URL as a valid offline copy.

This prompt is independently executable in a fresh coding-agent conversation. Implement the defined scope, preserve the established mobile architecture, and deliver appropriate automated tests and portable integration documentation.

### 2. Technology and Engineering Constraints

Use the established project direction:

- **Mobile:** React Native and TypeScript.
- **Backend:** TypeScript and NestJS.
- **Database:** PostgreSQL.
- **Caching:** Redis where relevant to backend services.
- **Media:** The platform's established object storage, media-processing, delivery, and authorization infrastructure.
- **Playback:** The existing mobile video-player abstraction.
- **Authentication:** The shared account, session, and authorization contracts.
- **Entitlements:** The platform's authoritative premium and other applicable access-entitlement contracts.
- **Observability:** Existing mobile telemetry, structured logging, and error-reporting conventions.

Inspect the actual repository, mobile player, existing library screens, storage abstractions, API contracts, entitlement integration, supported media libraries, and native build configuration before changing code.

Reuse existing player, video metadata, authentication, account settings, library, and download-related components whenever appropriate. Do not create competing implementations of global functionality.

If the architecture, DRM requirements, offline authorization contract, or required native dependencies are unavailable, implement a clearly bounded integration layer and document the missing dependencies. Never invent a media-protection mechanism and describe it as equivalent to an authoritative production DRM or licensing system.

### 3. Required Deliverables

Implement the following mobile capabilities:

1. Offline-download eligibility and authorization handling.
2. A download action for supported video content.
3. Download initialization, queueing, progress, pausing, cancellation, and recovery where supported.
4. Protected, device-local media storage.
5. Offline playback of eligible downloaded videos.
6. A dedicated downloads library and individual download details.
7. Storage usage, available-space handling, and cleanup.
8. Expiration, licensing, entitlement, and content-availability synchronization.
9. Network-aware download settings and resource management.
10. Account isolation, security safeguards, and privacy-aware local storage.
11. Automated testing and portable integration documentation.

The intended result is a functional offline-viewing system integrated into the existing native mobile application, not a collection of static download screens.

### 4. Download Eligibility and User Experience

Integrate the download action into the existing video-detail, watch, and other supported mobile content surfaces.

A download must be offered only when the relevant video, user, device, region, content policy, and current entitlement satisfy the established platform rules.

Depending on the authoritative product contract, eligibility may depend on:

- Video availability.
- Content-owner permissions.
- Account or geographic restrictions.
- Current premium or other access entitlements.
- Video format and media-delivery capabilities.
- Device storage.
- Offline-download limits.
- License availability.
- Expiration or retention restrictions.

Use actual authorization and eligibility responses. Do not infer that a user may download a video merely because streaming playback is permitted.

When downloading is unavailable, show the actual supported reason or a useful generic explanation. Do not expose confidential licensing or internal authorization details.

Provide accessible actions to start a download, inspect its status, open the downloaded video, or manage an existing copy where appropriate.

Prevent repeated taps from creating duplicate downloads for the same eligible video unless the product explicitly supports multiple download variants.

### 5. Download Initialization and Queue Management

Implement a dedicated download coordinator separated from screen components.

Where supported by the platform, the lifecycle should include:

1. Validate local eligibility prerequisites.
2. Request authoritative download eligibility and authorization.
3. Retrieve the required media manifest, download instructions, or protected media resources.
4. Obtain the necessary offline license or authorization when required.
5. Reserve and validate local storage.
6. Enqueue the download.
7. Transfer media through the approved protocol.
8. Validate integrity and completion conditions.
9. Complete the required license, manifest, or metadata operations.
10. Commit the downloadable item to the offline library.
11. Make it available for offline playback only after all required conditions have succeeded.

Represent intermediate states explicitly, including pending, preparing, queued, downloading, paused, verifying, completed, interrupted, expired, and failed where applicable.

The exact state model must follow the platform's authoritative download contract. Do not invent conflicting states when equivalent values already exist.

If multiple downloads are supported, implement a bounded queue with a deliberate concurrency policy. Keep queue operations stable when the application restarts, the network changes, or an individual download fails.

A partially downloaded or invalid file must not be presented as a playable offline video.

### 6. Transfer Progress, Pause, Resume, and Cancellation

Provide useful and accurate progress information.

Where reliable data is available, display:

- Download status.
- Transfer progress.
- Downloaded and expected byte counts.
- Approximate remaining time.
- Current queue position or waiting reason.
- Relevant recoverable errors.

Do not fabricate percentages, speeds, or estimated completion times.

Support pause, resume, and cancellation where the selected download protocol and native implementation permit them.

#### 6.1 Pause and resume

Pause must stop or suspend transfer work using the supported mechanism and update the correct job state.

Resume must validate the existing transfer state and follow the authoritative resume protocol, including any required session validation, offsets, checksums, or resource reauthorization.

Do not assume every media endpoint supports HTTP range requests, permanent download URLs, or resumable transfers.

If a download can no longer be resumed, show the supported recovery action rather than pretending that the previous byte offset remains valid.

#### 6.2 Cancellation

Cancellation must:

- Stop ongoing transfer work where supported.
- Prevent stale callbacks from restoring a cancelled job.
- Clean up incomplete local data safely.
- Release reserved storage.
- Release temporary credentials or transfer resources when required.
- Reconcile server-side download state when the contract requires it.
- Avoid deleting an already completed download when cancelling a different job.

Distinguish cancellation of an in-progress download from removal of an existing offline copy.

### 7. Download Storage Architecture

Implement a secure, predictable local-storage strategy appropriate for large media files.

Do not store complete videos inside ordinary React Native state, large serialized application stores, or an unrestricted cache directory that the application cannot manage reliably.

Use established native filesystem and media libraries to handle:

- Large-file transfer.
- Temporary files.
- Partial-download storage.
- Completion verification.
- Atomic promotion or equivalent safe finalization.
- Media metadata.
- Cleanup.
- Available-space checks.
- Application restart recovery.
- Native resource release.

Use stable download identifiers and an appropriate local metadata index. Keep the metadata index consistent with the actual files.

A completed download must not become visible as available until the required file, metadata, integrity, and licensing conditions are satisfied.

If a file has been deleted outside the download coordinator, detect the missing media and reconcile the corresponding download entry safely.

Avoid copying large video files unnecessarily. Use streaming or chunked transfer mechanisms appropriate to the underlying library and protocol.

### 8. Media Protection and Offline Licensing

Follow the platform's authoritative media-protection and offline-licensing architecture.

If downloaded media requires DRM, protected key storage, signed licenses, expiration enforcement, or periodic authorization renewal, integrate with the approved native player and license mechanism.

Requirements:

- Store media and licensing artifacts using the platform's prescribed security model.
- Avoid exposing decryption keys or license credentials to ordinary application state.
- Keep authorization material out of logs, telemetry, and crash reports.
- Prevent playback when required licensing conditions are not satisfied.
- Respect licensing expiration and content-revocation behavior.
- Release protected media resources safely.
- Avoid allowing the download library to be treated as a public media directory when the content is protected.

Do not invent custom encryption and claim that it replaces production DRM.

Do not place authentication credentials, permanent private media URLs, or reusable license secrets in source code or unprotected storage.

If protected offline playback cannot be implemented because the required native DRM or licensing integration is missing, document the exact dependency and avoid falsely marking protected content as available offline.

### 9. Offline Playback Integration

Integrate completed downloads with the existing mobile video player.

When opening a video, select the offline media source only after validating that the local download is complete, eligible, accessible, and properly licensed.

The playback source selection must respect the platform's content and authorization rules.

Implement:

- Launching an eligible downloaded video.
- Offline playback when the network is unavailable.
- Correct association between the downloaded item and its canonical video identifier.
- Playback progress persistence where supported.
- Offline loading and error states.
- Handling expired or revoked offline access.
- Falling back to streaming when policy permits and connectivity is available.
- Clear user feedback when a required offline resource is missing.

Do not blindly prioritize a stale local file over a newer authoritative restriction.

A local copy must not automatically bypass a content deletion, legal restriction, account restriction, or revoked license when the platform's policy requires those restrictions to be enforced.

When the device is offline, distinguish a genuinely playable downloaded video from an online-only item that merely appears in the ordinary viewing history.

### 10. Downloaded Videos Library

Implement a dedicated downloads library integrated with the existing viewer library and navigation.

Display actual locally stored download records.

Depending on supported metadata, show:

- Video title.
- Creator or channel.
- Thumbnail.
- Download status.
- Download date.
- Local size.
- Duration where known.
- Expiration or license status where applicable.
- Available actions.

Support:

- Opening a completed download.
- Refreshing and reconciling the local download index.
- Filtering or grouping by available status where useful.
- Removing a downloaded copy.
- Inspecting applicable download details.
- Recovering or retrying failed jobs when supported.
- Handling unavailable media and missing files.
- Opening the associated online video when allowed and useful.

Separate locally stored downloaded content from streaming history, liked videos, playlists, and other online-only library items.

Do not mark an ordinary saved video or playlist as downloadable merely because the user saved it.

When a video has both an online library entry and a local download, maintain a consistent relationship without duplicating the logical video identity.

### 11. Storage Management and Device Constraints

Provide an appropriate download-management view that allows users to understand and manage local storage.

Display storage information using actual filesystem measurements and app-owned metadata where available.

Support:

- Total space consumed by managed downloads.
- Per-video local size.
- Incomplete-download usage where practical.
- Removal of selected downloads.
- Removing all eligible downloads when supported.
- Insufficient-storage detection.
- Cleanup of abandoned temporary files.
- Recovery after externally removed files.

Before a download begins, check available storage when the platform provides an appropriate capability. Avoid reserving space based on unreliable or stale measurements.

When storage becomes insufficient:

- Pause or fail the relevant job safely.
- Explain the problem.
- Preserve completed downloads.
- Avoid deleting user-managed content automatically.
- Offer supported cleanup actions.

Do not implement a general-purpose device cleaner or delete arbitrary user files.

Treat operating-system-reported storage capacity as approximate where the platform can change it while the application is running.

### 12. Network and Power-Aware Downloads

Implement mobile network settings and transfer behavior appropriate to the established product design.

Where supported, allow users to configure:

- Download over Wi-Fi only.
- Whether cellular downloads are permitted.
- Automatic download behavior, if explicitly supported.
- Video-quality or storage-size preference.
- Whether downloads should pause under specified power or connection conditions.

Use the platform's actual network-connectivity APIs. Do not infer a stable connection type from a failed request.

Requirements:

- Respect explicit user restrictions.
- Avoid repeated automatic restart loops.
- Reevaluate queued jobs when connectivity changes.
- Handle captive portals and unstable connections gracefully.
- Apply bounded retries and appropriate backoff.
- Avoid unnecessary background polling.
- Avoid keeping the device awake indefinitely without justification.

Any automatic-download feature must follow an explicit product contract and user preference. Do not implement an unrequested background-download policy that unexpectedly consumes cellular data or device storage.

### 13. Background Execution and Application Lifecycle

Downloaded media may require transfers lasting longer than an ordinary screen session.

Use the appropriate supported native background-transfer mechanisms where the architecture requires them and where iOS and Android permit them.

Handle:

- App moving to the background.
- App returning to the foreground.
- Operating-system suspension or termination.
- Device restart where supported recovery exists.
- Network transitions.
- Permission or authorization changes.
- Transfer completion while the application UI is not visible.
- Native job callbacks arriving after the associated screen has been destroyed.

Do not assume React Native JavaScript will continue running indefinitely while suspended.

Persist the minimum state required to restore safe transfer progress. On application startup, reconcile persisted jobs with the actual files and authoritative transfer state instead of blindly trusting the last locally recorded status.

Document platform-specific constraints and any background-execution limitations that remain.

### 14. Download Expiration, Revocation, and Synchronization

Integrate downloads with the server-authoritative availability and authorization policies.

Some offline videos may require a valid license, periodic renewal, account verification, or continued eligibility. Follow the exact contract.

Support the applicable lifecycle events, such as:

- Download authorization expiration.
- License expiration.
- Entitlement changes.
- Video availability changes.
- Content deletion or revocation.
- Account logout.
- Region or policy restrictions.
- Required reauthorization.
- Local media removal.

Use online reconciliation when connectivity permits and the contract requires it.

When the application is offline, apply the documented local-license behavior and do not invent authorization rules.

If the server or DRM system revokes a download, reflect that outcome according to the platform's policy. Do not continue presenting the video as permanently playable simply because bytes remain on disk.

Distinguish between deleting the media file, removing its library entry, expiring its license, and temporarily losing the ability to verify its current status.

### 15. Authentication, Account Isolation, and Premium Entitlements

Integrate with the shared authentication and entitlement architecture.

Use the same account identity and authorization conventions as the rest of the application.

Requirements:

- Associate downloads with the correct platform account when required.
- Prevent one user's private download metadata from appearing under another account.
- Clear or isolate sensitive account-scoped metadata during account switching.
- Apply the established logout policy to protected downloads.
- Refresh eligibility after authentication restoration.
- Respect premium or other required entitlements.
- Reconcile entitlement changes according to the authoritative offline-access policy.
- Avoid assuming that an expired paid subscription always requires immediate deletion of local files.
- Avoid assuming that already-downloaded media remains playable forever.

The actual post-logout and post-expiration behavior must follow the backend, product, and licensing contracts. Do not silently define a contradictory local policy.

Do not implement backend entitlements, payment systems, identity services, or subscription management here.

### 16. Download and Offline State Management

Use the project's established state-management infrastructure. Keep transfer coordination separate from screen-level state.

Implement explicit, typed models for the relevant information, such as:

- Download identity.
- Canonical video identifier.
- Local file and metadata references.
- Transfer status.
- Transfer progress.
- Expected size where known.
- Source or session metadata required for recovery.
- Download timestamps.
- License or authorization status where appropriate.
- Available user actions.

Avoid persisting sensitive transfer credentials unnecessarily.

Requirements:

- Prevent duplicate active downloads for the same logical item unless explicitly supported.
- Reconcile job state with local files.
- Handle stale callbacks.
- Cancel obsolete requests.
- Keep local metadata consistent with completed media.
- Handle partial writes and failed finalization.
- Isolate account-scoped state.
- Update the library after confirmed download or removal operations.
- Avoid unnecessary re-renders driven by frequent progress updates.
- Keep completed media separate from incomplete transfer artifacts.

A completed download record must not survive as a falsely playable item when the underlying media and required license are missing.

### 17. Security and Privacy

Treat server responses, file paths, download URLs, license data, and locally persisted metadata as sensitive or untrusted where appropriate.

Implement these safeguards:

- Use approved authorization mechanisms for protected media.
- Never log raw credentials, signed download URLs, decryption keys, or private license payloads.
- Validate metadata before opening a local or remote media resource.
- Avoid exposing protected downloads through public file-sharing mechanisms.
- Ensure user-scoped download records do not leak across accounts.
- Follow the established content-access and DRM rules.
- Avoid collecting unrelated filesystem information.
- Do not use arbitrary paths received from an API as unrestricted filesystem write destinations.
- Handle corrupted or unexpected downloaded data safely.
- Clean up temporary files and authorization resources where required.
- Prevent unauthorized navigation from opening protected downloads.

Do not represent locally hiding an item as equivalent to revoking its authorization.

### 18. Performance and Reliability

Optimize the download system for mobile devices with constrained storage, memory, power, and network availability.

Requirements include:

- Efficient large-file transfer.
- Bounded concurrent downloads.
- Bounded in-memory queue state.
- Efficient progress updates.
- Safe player-resource management.
- Minimal duplicate media storage.
- Controlled preallocation or storage checks where supported.
- Cleanup of orphaned transfer artifacts.
- Recoverable handling of corrupted media and interrupted transfers.
- Reliable reconciliation after restart.
- No unlimited polling or automatic retry loops.
- No blocking of ordinary browsing while the downloads library is loading.

Where profiling and native tooling are available, measure important file-transfer, storage, and playback behavior.

Do not invent storage-efficiency improvements, benchmark results, or claims of uninterrupted background execution that have not been verified.

### 19. Accessibility and Mobile User Experience

Build a polished offline-viewing experience that follows the existing design system.

Implement:

- Accessible download and cancel controls.
- Clearly labeled download progress.
- Screen-reader announcements for meaningful transfer-state changes.
- Readable download-size and storage information.
- Accessible storage cleanup confirmations.
- Clear distinction between online-only and offline-available content.
- Useful retry and recovery actions.
- Safe-area-aware layouts.
- Dynamic text support.
- Localization-ready strings.
- Locale-aware dates and storage units.
- Consistent light/dark themes if supported.
- Appropriate handling of small screens and long titles.
- Accessibility support for dialogs, forms, lists, and player controls.

Do not rely exclusively on color to communicate download states.

Do not label partially downloaded content as available offline or present an expired license as a generic connectivity error.

### 20. Observability and Failure Recovery

Integrate with the project's existing client telemetry and error-reporting systems.

Capture privacy-safe diagnostic information for:

- Download initialization failures.
- Transfer failures and retries.
- Resume and recovery outcomes.
- Insufficient local storage.
- Media-integrity validation failures.
- License or authorization failures.
- Download finalization failures.
- Missing-file reconciliation.
- Offline playback failures.
- Cleanup errors.
- Native background-transfer limitations where observable.

Use correlation IDs where appropriate.

Do not log media contents, authentication credentials, signed URLs containing secrets, encryption keys, or unnecessary private file paths.

Retry only when the protocol permits it. When an operation might have succeeded despite a lost response, reconcile actual file and authorization state before repeating it.

### 21. API and Portable Integration Contracts

Use the centralized typed API infrastructure and authoritative project contracts.

Depending on the architecture, the mobile client may require operations for:

- Checking download eligibility.
- Creating or authorizing a download.
- Retrieving media-transfer instructions.
- Refreshing transfer authorization.
- Completing or cancelling a download session.
- Obtaining offline-license authorization.
- Refreshing license or entitlement state.
- Reconciling download availability.
- Reporting applicable client-side download outcomes.
- Retrieving the relevant video metadata.

These are required integration responsibilities, not permission to invent incompatible endpoint names.

Follow the authoritative contracts for:

- Authentication and authorization.
- Video identifiers and metadata.
- Transfer protocol and resumability.
- Checksums or integrity requirements.
- Offline licensing and expiration.
- Content retention and revocation.
- Entitlement requirements.
- Error formats and status codes.
- Rate limits and idempotency.
- Session expiration and retry behavior.

The local download index is a mobile persistence responsibility. Do not assume the backend stores local file paths or directly controls the mobile filesystem.

If contracts are unavailable, define explicit portable proposals describing the operations, payloads, identifiers, transfer protocol, authorization model, license lifecycle, error behavior, state transitions, and unresolved dependencies.

Clearly mark proposed contracts as proposals. Do not claim that missing backend endpoints, native DRM, or external services are already functional.

### 22. Required Automated Tests

Use the established mobile testing framework.

#### 22.1 Unit tests

Test:

- Download eligibility mapping.
- Queue ordering and concurrency limits.
- Download state transitions.
- Transfer progress mapping.
- Duplicate-download prevention.
- Pause, resume, and cancellation decisions.
- File metadata consistency.
- Local file reconciliation.
- License expiration and authorization-state mapping.
- Offline playback eligibility.
- Account switching and download isolation.
- Storage-availability error handling.
- Retry classification and backoff.
- Cleanup of incomplete downloads.

#### 22.2 Component and screen tests

Test:

- Download action availability.
- Download initialization.
- Queue display and progress.
- Pause, resume, retry, and cancellation.
- Downloads-library rendering.
- Opening completed content.
- Unavailable and expired downloads.
- Storage usage and cleanup.
- Insufficient-space errors.
- Network-restriction settings.
- Logout and account-switching behavior.
- Offline playback failure and recovery.

#### 22.3 Integration and platform tests

Where the environment supports them, test:

- Download API serialization and error handling.
- Real transfer behavior against a controlled test environment.
- Interrupted-transfer recovery.
- Large-file handling.
- Media finalization and integrity checks.
- Missing-file reconciliation.
- App foreground/background transitions.
- Native filesystem permissions.
- Offline-license integration.
- Entitlement changes and content authorization.
- iOS and Android build configurations.

Use deterministic fixtures and mocks at appropriate test boundaries. Do not make a mocked media response the production download source.

Execute the available type checking, linting, unit tests, integration tests, and build checks. Report the actual commands and outcomes.

### 23. Documentation and Portable Handoff

Create or update documentation covering:

- Download coordinator and storage architecture.
- Download state machine.
- File layout and metadata index.
- Transfer protocol and resumability.
- Offline playback selection.
- License and authorization requirements.
- Entitlement integration.
- Network and storage policy.
- Native background-transfer behavior.
- Cleanup and recovery rules.
- Account isolation and logout behavior.
- iOS and Android dependencies.
- Required environment configuration.
- API and portable integration contracts.
- Test commands and validation results.
- Known platform limitations and unresolved dependencies.

The documentation must distinguish mobile-local responsibilities from backend media, authorization, and licensing responsibilities.

Where authoritative contracts are absent, document explicit proposed contracts so another integration environment can connect independently generated project parts without relying on hidden conversation history.

### 24. Explicitly Out of Scope

Do not implement:

- Backend media-storage infrastructure.
- A new media-transcoding pipeline.
- Backend download-session orchestration.
- Server-side DRM or offline-license services.
- Subscription billing or payment processing.
- Backend entitlement persistence.
- A replacement for the shared video player.
- A general-purpose device-cleaning system.
- A new global mobile navigation or state-management architecture.
- Unrelated creator, livestream, short-form, moderation, or administration functionality.
- Unplanned architecture, QA, integration, or production-readiness prompt phases.

Implement the complete bounded mobile offline-viewing scope, including its actual client integrations, tests, and documentation.

### 25. Definition of Done

This milestone is complete only when all applicable criteria are satisfied:

1. The mobile application evaluates download eligibility through the established contract.
2. Eligible videos can be downloaded using the actual supported media-transfer mechanism.
3. Download progress and lifecycle states accurately reflect real operations.
4. Pause, resume, cancellation, and recovery behave according to the transfer protocol.
5. Completed media and its metadata are persisted safely.
6. Offline playback uses validated local media and the approved player and licensing integration.
7. The downloads library displays genuine locally managed download records.
8. Storage usage, cleanup, insufficient-space handling, and missing-file recovery work correctly.
9. Network restrictions and applicable native lifecycle behavior are implemented.
10. Content authorization, premium entitlements, account isolation, and license requirements are respected.
11. Incomplete, revoked, missing, or expired downloads are not falsely presented as playable.
12. Security and privacy safeguards protect local media and authorization data.
13. Automated tests cover critical download, recovery, storage, licensing, offline playback, and account-isolation paths.
14. Relevant available type checks, tests, and builds have been executed and accurately reported.
15. Documentation captures the actual implementation and remaining native or backend dependencies.
16. No fake production downloads, hardcoded secrets, invented DRM behavior, placeholder implementations, or undocumented integration assumptions remain within this scope.

### 26. Completion Report

After implementation, provide a factual report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Download eligibility and initialization**
- **Transfer lifecycle and recovery**
- **Local storage implementation**
- **Offline playback integration**
- **Downloads library and storage management**
- **Licensing and entitlement integration**
- **Native iOS and Android behavior**
- **Security and privacy safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **Build results**
- **Documentation created or updated**
- **External configuration and service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Clearly distinguish verified behavior from proposed contracts and unavailable external dependencies. Never claim that offline playback, DRM enforcement, or background transfer is production-ready without actual evidence.

### 27. Final Execution Directive

Treat this prompt as the active implementation assignment for offline downloads and offline video playback in the YouTube-style platform's native mobile application.

Inspect the project materials genuinely available to you. Implement the defined scope, preserve established contracts and existing functionality, run the available tests and validations, and document the actual result.

Do not respond with planning alone. Do not ask the user to choose a task. Do not implement unrelated project functionality, invent unavailable backend or DRM capabilities, or create unplanned project phases.

Deliver the strongest secure, complete, and verifiable implementation supported by the execution environment.

**Begin implementation now.**
