# YouTube-Style Video Platform — Mobile Prompt — Volume 6

## Notifications, Account Settings, Privacy, Personalization, and Security

### 1. Mission and Implementation Scope

Implement the production-grade **notifications, account settings, privacy, personalization, security, and account-management experience** for the YouTube-style video platform's native iOS and Android applications using React Native and TypeScript.

The application is intended to serve a global platform targeting approximately 250 million registered users and 50 million daily active users. The mobile application must be designed for this scale while keeping the implementation scope of this milestone focused on the client experience and its integration boundaries.

Build complete, usable screens and supporting application logic rather than static mockups. Every included interaction must perform its intended action, use real application state, integrate with the appropriate API contract, and communicate its result honestly to the user.

This prompt is independently executable. It includes the product requirements, technical expectations, integration boundaries, testing obligations, and completion criteria necessary to implement the assigned scope in a fresh coding-agent conversation.

### 2. Technology and Engineering Constraints

Use the following project direction:

- **Mobile:** React Native and TypeScript, targeting iOS and Android.
- **Backend:** TypeScript and NestJS.
- **Primary database:** PostgreSQL.
- **Caching and distributed state:** Redis.
- **Media:** Video delivery through the platform's established media infrastructure.
- **Notifications:** Backend-managed notification services with native push delivery through Apple Push Notification service (APNs) and Firebase Cloud Messaging (FCM), where configured.
- **Architecture:** Modular, strongly typed, testable, and compatible with independently implemented services and clients.
- **Deployment:** Production-oriented mobile builds, environment configuration, crash reporting, telemetry, and release practices.

Inspect any repository, project files, API specifications, design-system artifacts, or integration contracts actually available in the execution environment before changing code. Preserve existing conventions and working functionality.

If the necessary project artifacts are not available, do not pretend to have inspected them or assume that other AI conversations shared files. Implement a coherent, self-contained mobile feature structure and produce explicit portable integration contracts for the missing dependencies.

Use supplied authoritative API and architecture contracts whenever available. The concrete requirements in this prompt establish the expected mobile behavior; they must not be used to silently override an authoritative project-wide contract.

### 3. Required Deliverable

Implement the complete mobile experience for the following areas:

1. In-app notifications and notification actions.
2. Native push-notification permission and device-registration lifecycle.
3. Notification preferences.
4. Account and application settings.
5. Viewing and personalization preferences.
6. Privacy and activity controls.
7. Account security and session management.
8. Account lifecycle and supported data-management requests.
9. Navigation, deep links, accessibility, loading states, and error recovery for all included screens.

Include supporting typed models, API integration, state management, reusable components, platform-specific behavior, automated tests, and documentation.

Organize the implementation using the application's existing architecture where available. Keep screens, components, state, API repositories, navigation, native integrations, and business rules appropriately separated.

### 4. Notification Center

Implement a complete, authenticated notification center.

#### 4.1 Notification list

Display notifications returned by the backend, including applicable types such as:

- New videos and posts from subscribed channels.
- Live-stream notifications.
- Replies to comments and creator interactions.
- Mentions and relevant community interactions.
- Subscription and account-related updates.
- Platform announcements, where supported.

Each notification must support the fields provided by its authoritative contract, such as:

- Stable notification identifier.
- Notification type.
- Title and message.
- Actor, channel, or associated content metadata.
- Thumbnail or avatar where applicable.
- Creation timestamp.
- Read or unread state.
- A typed navigation target or actionable destination, where applicable.

Do not assume that every notification has an image, actor, content item, or actionable target. Render incomplete optional metadata safely without breaking the item.

#### 4.2 List behavior

Implement:

- Cursor-based pagination when supported by the notification API.
- Pull-to-refresh.
- Loading, empty, error, and retry states.
- Unread visual treatment and accessible unread indicators.
- Stable list keys and efficient rendering for long lists.
- Correct deduplication when refreshed or paginated results overlap.
- Consistent timestamp formatting and localization-ready strings.
- A visible, accessible way to return to the main application navigation.

Do not load an unbounded notification history into memory. Preserve the backend's pagination semantics.

#### 4.3 Notification actions

Support applicable actions such as:

- Opening the associated video, Short, live stream, channel, comment, or other supported destination.
- Marking an individual notification as read or unread when the contract permits it.
- Marking all notifications as read when supported.
- Opening related account settings.
- Dismissing or deleting a notification only where the backend contract defines that operation.

Use optimistic updates only where appropriate. Preserve enough prior state to roll back failed mutations, show a useful error, and prevent duplicate requests.

A successful visual change must correspond to a successful backend mutation or an explicitly documented optimistic state awaiting confirmation. Never present an unconfirmed operation as permanently successful.

### 5. Native Push-Notification Integration

Implement the mobile application layer for push notifications across iOS and Android.

#### 5.1 Permission lifecycle

Use the appropriate native permission APIs and the project's approved notification library to:

- Determine the current notification-permission status.
- Request permission only at an appropriate point in the user experience.
- Explain the value of enabling notifications before requesting permission when appropriate.
- Distinguish granted, denied, provisional, unavailable, and not-yet-requested states where supported by the OS and integration library.
- Detect when a user must visit system settings to change a previously denied permission.
- Provide an accessible route to the relevant application settings where supported.

Do not repeatedly prompt users who have already made a permission decision. Do not claim that notifications are enabled merely because the user accepted an in-app preference.

#### 5.2 Device registration and lifecycle

Integrate with the existing backend device-registration contract to register or refresh the device's push token and associate it with the authenticated account where required.

Handle:

- Token availability and token refresh.
- Authentication changes.
- Logout and account switching.
- Registration failures and retries.
- OS permission changes.
- App reinstall or token replacement where detectable.
- Device deregistration when the backend contract requires it and the operation is appropriate.

Avoid duplicate registration, stale account associations, and leaking tokens into logs or analytics.

Do not build or replace APNs, FCM, notification delivery services, backend token storage, or server-side notification dispatch in this prompt. Do not fabricate native delivery credentials or commit them to the repository.

If the required native credentials are unavailable, implement and test the client integration paths that can be validated locally, document the missing environment configuration, and do not claim a real-device delivery test was completed.

#### 5.3 Notification routing

Support notification taps and in-app navigation from foreground, background, and cold-start states where the native platform and libraries allow it.

Requirements:

- Parse and validate incoming notification payloads.
- Route only to supported, well-defined destinations.
- Wait for navigation readiness and authentication restoration before navigating.
- Avoid duplicate navigation when the same notification event is delivered more than once.
- Handle deleted content, inaccessible channels, expired live streams, invalid identifiers, and unsupported destinations gracefully.
- Preserve appropriate navigation history.
- Avoid displaying sensitive notification contents on the wrong account after logout or account switching.

Notification payloads are untrusted input. Never execute arbitrary navigation instructions or accept arbitrary URLs as privileged actions.

### 6. Notification Preferences

Implement an account-facing notification settings screen organized into understandable categories.

Where supported by the project contract, provide preferences for:

- Subscriptions and newly published videos.
- Recommended content.
- Live streams.
- Comments, replies, and mentions.
- Creator or community activity.
- Product announcements and account updates.
- Email notifications, if the mobile API exposes those preferences.
- Push notifications and device-level permission status.
- Per-channel notification behavior if that capability is part of the platform's existing product scope.

Represent each preference with an appropriate control, clear explanatory text, and accessible labels.

Requirements:

1. Load the authenticated user's actual preference values.
2. Display loading, unavailable, and error states distinctly.
3. Save changes through the designated API.
4. Prevent stale responses from overwriting newer user changes.
5. Reconcile optimistic updates and failed requests correctly.
6. Respect any server-enforced restrictions or immutable settings.
7. Keep backend preferences distinct from OS-level permission status.
8. Support any authoritative global or category-level settings and inheritance behavior.
9. Provide a clear indication when changes are saved or could not be saved.

Do not implement server-side preference storage or notification dispatch here.

If preference categories differ in an authoritative API contract, adapt the UI to that contract rather than inventing incompatible persisted fields.

### 7. Account and Application Settings

Implement a dedicated settings area accessible through the application's existing account navigation.

Organize it into clear sections, as appropriate to the established product design:

- Account.
- Notifications.
- Privacy and activity.
- Playback and viewing preferences.
- Personalization.
- Security.
- Data and account lifecycle.
- About, legal information, and support links when supplied by project configuration.

Provide clear navigation, screen titles, back behavior, and account-aware loading states.

Use reusable settings rows, section headers, switches, selectors, navigation rows, confirmation dialogs, and form components consistent with the existing design system.

Ensure that settings remain understandable on small screens, large text sizes, and both supported mobile platforms.

Do not duplicate complete functionality already implemented in another mobile area merely to make the settings section appear more substantial. Link to existing screens when that is the correct user experience.

### 8. Viewing and Personalization Preferences

Implement user-facing preferences for video viewing and content personalization when supported by the established backend contract.

Potential controls include:

- Preferred video quality on Wi-Fi.
- Preferred video quality on cellular connections.
- Autoplay behavior.
- Captions and subtitles preferences where supported.
- Playback-related accessibility preferences.
- Restricted Mode or equivalent content-filtering controls when supported.
- Personalized recommendation controls.
- Relevant watch-history and search-history controls.

The actual control set must reflect the platform's established product scope, available API fields, and capabilities.

For settings that affect playback, use the shared playback-preference contract rather than introducing mobile-only settings that conflict with other clients.

For settings that affect recommendations, distinguish the user's explicit preference from inferred recommendation state. Explain relevant effects in user-facing language without making guarantees that the backend cannot enforce.

Requirements:

- Load the persisted preference state.
- Save supported changes through the designated API.
- Validate enumerations and values according to the authoritative contract.
- Handle save failures without silently losing the previous state.
- Update affected mobile behavior only after the change is accepted, or use a reversible optimistic update.
- Preserve preferences across restarts and authentication restoration according to their documented ownership.
- Respect account and age-related restrictions exposed by the backend.

Do not build the recommendation engine, playback engine, caption-processing system, or backend personalization services in this milestone.

### 9. Privacy and Activity Controls

Implement a mobile privacy and activity area with the functionality actually supported by the platform.

Where present in the API contract, cover:

- Watch-history visibility and management.
- Search-history visibility and management.
- Pause or resume supported history collection.
- Clear watch history.
- Clear search history.
- Available activity deletion requests.
- Privacy-related account controls.
- Relevant data-retention explanations or account privacy documentation.

For destructive history-clearing actions:

1. Explain the scope and consequence of the action.
2. Require an explicit confirmation.
3. Call the actual corresponding API.
4. Prevent accidental repeated submissions.
5. Reflect completion only after the operation succeeds.
6. Display an actionable error if the operation fails.

Where the platform supports granular deletion, implement the controls exposed by the API rather than presenting an unrelated generic deletion button.

Do not claim that data has been permanently deleted merely because a client-side list was cleared. The server remains authoritative for persisted history and deletion completion.

Respect privacy preferences across accounts and cached state. A history belonging to one account must never appear when another account signs in.

### 10. Account Security

Implement a security section for authenticated users.

Include the relevant capabilities supported by the backend contract:

- Current account identity and security status.
- Password change for password-based accounts.
- Reauthentication before sensitive operations where required.
- Password-reset navigation through the approved recovery flow.
- Multi-factor authentication status and management, if the backend supports it.
- Active session or device management.
- Revocation of supported sessions.
- Security notifications or related account-security information when available.

#### 10.1 Sensitive forms

Password or credential forms must:

- Use secure input components.
- Support show/hide controls without exposing values unnecessarily.
- Validate fields and report field-specific errors.
- Avoid logging credentials.
- Avoid persisting secret form values in local storage or analytics.
- Clear sensitive values when the form is completed, cancelled, or abandoned where practical.
- Handle reauthentication, expired sessions, and server-side validation failures appropriately.

Do not invent multi-factor authentication behavior, password policies, or identity-verification workflows. Enforce authoritative rules supplied by the backend.

#### 10.2 Session management

When supported by the API, display identifiable active sessions or devices with useful fields such as device type, last activity, and current-session status.

Provide an appropriate session-revocation action with confirmation and reliable mutation handling.

For revoking the current session, immediately transition through the application's supported logout and credential-clearing workflow when required. For revoking another device, update the visible state only after the backend operation is confirmed.

Do not expose session secrets, refresh tokens, private authentication metadata, or sensitive device identifiers.

Do not implement authentication servers, account identity services, or session-revocation backend logic in this prompt.

### 11. Account Lifecycle and Data Requests

Implement the mobile-facing experience for account lifecycle actions that are already supported by the platform.

Potential capabilities include:

- Accessing account information.
- Initiating a data-export request.
- Viewing data-export request status or retrieving an available export.
- Initiating account deletion.
- Understanding the consequences of deletion.
- Completing any required reauthentication or explicit confirmation.
- Handling pending, successful, rejected, or failed requests.

Distinguish between an immediate client action, an accepted asynchronous server request, and a completed server-side operation.

For account deletion:

- Present a clear explanation of relevant consequences.
- Use the authoritative deletion workflow.
- Require the required level of confirmation or reauthentication.
- Prevent duplicate submissions.
- Handle cancelled and expired requests.
- Clear account-specific local state and credentials when the authoritative workflow requires it.
- Avoid leaving account-specific data visible after the account becomes unavailable.

Do not claim that a deletion or export is complete until the backend contract confirms the relevant state.

Do not implement the server-side export pipeline, retention policies, deletion orchestration, or legal compliance machinery here.

### 12. API and Domain Integration Contracts

All backend communication must use the application's centralized, typed API infrastructure.

Use the authoritative project contracts for authentication, identifiers, timestamps, pagination, errors, notifications, preferences, security, account management, and mutations whenever they are provided.

Define appropriately typed models and repository interfaces for the mobile functionality. Keep screen components separate from request serialization, response parsing, and persistence concerns.

At minimum, cover operations equivalent to:

- Fetching a paginated notification feed.
- Fetching and updating notification preferences.
- Marking supported notifications as read or unread.
- Marking all notifications as read when supported.
- Fetching and updating viewing and personalization preferences.
- Fetching and updating privacy and activity settings.
- Performing supported history-management actions.
- Fetching account security and session information.
- Executing supported session-management operations.
- Executing supported account data-management requests.
- Registering or removing a push-notification device token where required.

These are functional responsibilities, not permission to invent incompatible API routes. Bind repository operations to the supplied API specification and preserve its error structures, authentication requirements, request semantics, pagination conventions, and status codes.

When authoritative API artifacts are unavailable, document an explicit proposed mobile integration contract with the operation names, request and response schemas, error behavior, authentication requirements, pagination, and unresolved dependencies. Do not silently treat proposed contracts as implemented backend endpoints.

Do not add fake API implementations, fabricated persisted state, hardcoded successful responses, or production-inaccessible mock services to make the screens appear functional.

### 13. State Management, Caching, and Offline Behavior

Use the application's established state-management and server-state libraries when available. Avoid adding redundant state-management dependencies without a demonstrated need.

Implement behavior appropriate to this feature set:

- Explicit loading, success, empty, and error states.
- Safe cancellation or stale-response handling when requests become obsolete.
- Cache invalidation after successful mutations.
- Optimistic updates only for operations with predictable rollback behavior.
- Request deduplication where appropriate.
- Safe refresh behavior when the application returns to the foreground.
- Consistency when the authenticated account changes.
- Appropriate handling of expired credentials and authorization errors.

Offline behavior must be deliberate.

Cached, non-sensitive settings may be available for display when appropriate, but the UI must distinguish cached values from confirmed server state. Do not claim a server mutation succeeded while offline.

Do not queue destructive operations or security-sensitive mutations for later execution unless the existing product contract explicitly supports that behavior and provides appropriate safeguards.

Never persist raw credentials or expose private notification or account data through unprotected storage.

### 14. Security, Privacy, and Data Isolation

Treat notifications, deep links, API responses, device tokens, and navigation parameters as untrusted input.

Implement the following safeguards:

- Use the existing secure authentication-storage mechanism.
- Do not store passwords, access tokens, refresh tokens, or push tokens in logs.
- Prevent cross-account leakage of cached notifications, activity, or settings.
- Clear or isolate user-scoped in-memory and persisted state during logout and account switching.
- Validate identifiers and navigation destinations before acting on them.
- Avoid displaying sensitive information in debug logs, analytics events, or crash reports.
- Require backend authorization for every privileged operation.
- Do not assume that hiding a UI control provides authorization.
- Handle expired sessions and unauthorized responses through the centralized authentication flow.
- Keep secrets out of source code and client bundles.
- Respect OS privacy restrictions and notification-permission status.
- Do not place authentication credentials or personal information in deep-link query strings.
- Ensure privacy controls reflect the persisted server state rather than local presentation alone.

Client-side controls must not be represented as substitutes for backend security enforcement.

### 15. Navigation and Cross-Feature Integration

Integrate the implemented screens with the existing mobile application navigation structure.

Preserve current app entry points, authenticated and unauthenticated navigation, account switching, and existing video-related functionality.

Implement routes for the notification center and settings sections using the project's established navigation library.

Where appropriate, expose settings through the existing account/profile area and notification access point. Do not create competing navigation systems or duplicate global navigation structures.

Support external and internal navigation to relevant destinations through validated, typed route parameters.

If a notification refers to a feature that is out of scope or unavailable on the device, show a safe, understandable fallback instead of navigating to a nonexistent screen.

Changes in these screens must not break authentication restoration, home/discovery navigation, video playback, subscriptions, comments, channel navigation, playlists, or viewer-library behavior.

### 16. UI, Accessibility, and Platform Quality

Produce a polished, production-quality native mobile experience consistent with the existing design system.

Implement:

- Reusable settings rows and section layouts.
- Clear typography and visual hierarchy.
- Accessible switches, buttons, forms, and confirmation dialogs.
- Adequate touch targets and screen-reader labels.
- Correct accessibility announcements for loading and mutation results.
- Dynamic text and appropriate layout behavior for larger font settings.
- Keyboard-safe forms and suitable input types.
- Platform-appropriate status-bar, system-navigation, and modal behavior.
- Reduced-motion accommodations where relevant.
- Consistent empty, error, retry, disabled, and permission-denied presentation.
- Localization-ready strings and locale-aware dates and times.
- Safe-area and small-screen layout handling.
- Consistent light and dark themes if supported by the application.

Do not use emoji, temporary text, or unstyled default controls as substitutes for intended production UI.

Follow the existing component library and visual language when available. Avoid introducing a competing design system within this feature area.

### 17. Performance and Reliability

Design these mobile features for high usage volume without putting platform-scale work on the device.

Requirements include:

- Paginated notification rendering.
- Efficient list item rendering.
- Minimal unnecessary rerenders.
- Appropriate caching and invalidation.
- No unbounded polling or uncontrolled network requests.
- Retry behavior consistent with operation safety.
- Correct handling of interrupted requests and app backgrounding.
- Safe push-token refresh and registration.
- No duplicate notification navigation or repeated destructive submission.
- Graceful operation when push services, the network, or individual optional endpoints are unavailable.

Instrument relevant failures and performance behavior using the project's existing observability conventions.

Never include sensitive user data, credentials, push tokens, or full notification payloads in telemetry.

### 18. Required Tests

Add meaningful automated tests appropriate to the existing test framework and the implemented functionality.

#### 18.1 Unit tests

Test:

- Notification model parsing and optional metadata.
- Preference mapping and validation.
- Notification action-state transitions.
- Pagination and deduplication logic.
- Settings persistence and failed-save rollback.
- Notification-permission status mapping.
- Push-token registration decisions.
- Authentication changes and account-scoped state cleanup.
- Deep-link validation and destination resolution.
- Session-revocation and account-lifecycle state transitions.

#### 18.2 Component and screen tests

Test:

- Notification loading, empty, error, and populated states.
- Refresh and pagination behavior.
- Read/unread actions and mutation failures.
- Notification preference changes.
- Viewing and personalization controls.
- Privacy and history-clearing confirmations.
- Security forms and validation failures.
- Session-list rendering and revocation.
- Data-export and account-deletion flows.
- Accessibility labels and important screen transitions.

Use realistic typed fixtures and mocked boundaries for tests. Mocks are acceptable for automated test isolation; they must not become the application's fake production data source.

#### 18.3 Integration and platform tests

Test applicable behavior involving:

- API repository serialization and response handling.
- Authentication expiry and authorization errors.
- Cache invalidation following mutations.
- Account switching and logout.
- Notification taps and navigation readiness.
- Cold-start notification routing where the test environment supports it.
- Permission-denied and unavailable push-registration states.
- Failure and retry behavior.

Use existing iOS and Android validation tools. Run the available type checking, linting, unit tests, and build checks relevant to the changed code.

Do not claim a device-specific integration, push-delivery, or release-build test was run unless it was actually executed.

### 19. Documentation and Portable Handoff

Create or update documentation describing the implemented mobile functionality and its integration requirements.

Where applicable, document:

- Screen and module responsibilities.
- Navigation destinations and parameters.
- API repositories and operation mappings.
- Authoritative contract sources and any proposed contracts.
- Push-token lifecycle and device-registration behavior.
- Required iOS and Android capabilities.
- Required environment configuration.
- Permission behavior and platform limitations.
- State ownership, caching, and invalidation rules.
- Authentication and account-switching behavior.
- Testing and validation commands.
- Known external dependencies and operational limitations.

If project-wide contracts were unavailable, include portable documentation describing every proposed API dependency or unresolved cross-part decision so another integration environment can reconcile it without relying on hidden conversation history.

Do not silently invent backend capabilities to make the mobile handoff appear complete.

### 20. Explicitly Out of Scope

Do not implement the following in this milestone:

- Backend notification delivery or scheduling services.
- Backend device-token storage or lifecycle workers.
- Backend preference persistence.
- Recommendation algorithms.
- Authentication or identity-provider services.
- Password reset or multi-factor authentication server workflows.
- Backend session creation, tracking, or revocation.
- Backend history storage or deletion orchestration.
- Data-export generation pipelines.
- Account-deletion and retention infrastructure.
- Creator Studio or administrator moderation consoles.
- Monetization, checkout, membership, or payment workflows.
- A replacement for the existing global mobile architecture.
- Unrelated features belonging to other mobile implementation areas.
- New implementation volumes or project phases.

Use these services through the established contracts. Implement only the mobile-facing responsibilities assigned to this prompt, along with the necessary client integration, tests, and documentation.

### 21. Definition of Done

This milestone is complete only when all of the following applicable conditions are satisfied:

1. The notification center is implemented and connected to the actual API integration layer.
2. Supported notification actions work and handle failures correctly.
3. Native permission handling, push-token lifecycle integration, and notification routing are implemented to the extent supported by the available environment.
4. Notification preferences load and save through the correct API contracts.
5. Account settings and supported viewing preferences are implemented.
6. Privacy and activity controls execute their supported operations with appropriate confirmation and error handling.
7. Account-security, session-management, and data-management screens implement the supported workflows.
8. Navigation remains compatible with the existing mobile application.
9. User-scoped state and sensitive data are correctly isolated across logout and account switching.
10. Loading, empty, error, offline, denied-permission, and other relevant failure states are covered.
11. The implementation follows the existing design system and accessibility requirements.
12. Automated tests cover the main success paths, important failure paths, security-sensitive transitions, and state-management behavior.
13. Relevant type checking, linting, tests, and build validations have been executed where the environment permits.
14. Documentation reflects the actual implementation and any unresolved external dependencies.
15. No fake production APIs, hardcoded secrets, hidden integration assumptions, placeholder implementations, or intentional implementation gaps remain within the assigned scope.

### 22. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Features implemented**
- **Notification and push integration details**
- **API and contract dependencies**
- **Navigation and state-management changes**
- **Security and privacy safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **Build results**
- **Documentation created or updated**
- **External configuration or service dependencies**
- **Known limitations**
- **Unresolved issues**
- **Definition of Done status**

Distinguish implemented functionality from proposed integration contracts and environment-dependent behavior. Clearly state any validation that could not be performed and why. Never claim that a feature works in production, that push notifications were delivered, or that validation passed without evidence from actual execution.

### 23. Final Execution Directive

Treat this prompt as the active implementation assignment for the YouTube-style video platform's native mobile application.

Inspect the project materials genuinely available to you, implement the complete bounded scope described here, preserve established contracts and existing functionality, execute available tests and validations, and document the actual result.

Do not respond with a high-level plan alone. Do not ask the user to choose which part to implement. Do not implement the entire platform or expand into unrelated project scopes. Do not create another prompt or invent an additional project phase.

Make the necessary engineering decisions within the stated boundaries, document any unavoidable integration dependencies, and complete the implementation to the strongest verifiable standard supported by the execution environment.

**Begin implementation now.**
