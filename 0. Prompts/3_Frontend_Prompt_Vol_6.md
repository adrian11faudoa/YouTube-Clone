# YouTube-Style Video Platform — Frontend Prompt — Volume 6

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web notifications, viewer account settings, privacy controls, security-sensitive preferences, personalization settings, and account-management experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

* notification center;
* notification preferences;
* push/email/in-app notification settings where supported;
* account settings;
* profile settings;
* privacy settings;
* watch/privacy controls;
* personalization controls;
* playback and discovery preferences where supported;
* session/security management where supported;
* account deletion entry points;
* data/privacy controls where supported;
* authenticated account-management flows;
* accessibility;
* responsive behavior;
* analytics;
* testing;
* documentation.

Do not implement unrelated frontend domains.

Do not implement notification delivery infrastructure, identity backend services, security services, or data-deletion backend systems.

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
* personalized discovery;
* search;
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

This prompt handles viewer-facing authenticated account controls. Security-sensitive operations must remain backed by authoritative server-side contracts.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

* another Claude conversation;
* another AI response;
* an earlier frontend prompt;
* hidden API contracts;
* hidden security decisions;
* undocumented backend behavior.

If a repository is available, inspect it before modifying it.

If portable project contracts are available, use them as authoritative.

If compatible account, settings, session, or notification components already exist, extend them instead of duplicating them.

Do not infer that a backend capability exists solely because it is mentioned in the global product description.

---

# 4. Primary Objective

Implement the authenticated web experience for:

1. viewing notifications;
2. managing notification preferences;
3. controlling supported delivery channels;
4. managing profile information;
5. managing privacy preferences;
6. controlling history-related privacy;
7. managing personalization preferences;
8. reviewing security/session information where supported;
9. initiating account-sensitive operations;
10. accessing privacy/data controls where supported;
11. handling authorization and session expiry;
12. preserving sensitive account state across navigation;
13. providing responsive accessible interfaces;
14. generating appropriate telemetry without exposing sensitive information.

---

# 5. Explicit Scope

Implement:

* notification center;
* unread notification state;
* notification pagination;
* notification read/unread state;
* notification navigation;
* notification preferences;
* delivery-channel preferences where supported;
* profile settings;
* privacy settings;
* history/privacy controls;
* personalization preferences;
* viewer-facing playback/discovery preferences where supported;
* account/security settings exposed to normal viewers;
* session/device management where supported;
* account deletion entry point where supported;
* privacy/data-management entry points where supported;
* loading/error/empty states;
* authenticated route protection;
* state and cache management;
* accessibility;
* responsive behavior;
* analytics;
* tests;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* notification delivery services;
* email/SMS provider infrastructure;
* Web Push infrastructure;
* authentication backend;
* credential storage backend;
* session issuance/validation services;
* MFA backend;
* account-deletion processing backend;
* data-export processing backend;
* privacy-compliance backend;
* moderation;
* creator studio;
* mobile applications;
* live streaming;
* monetization;
* administrative dashboards;
* backend security services.

Do not create fake implementations to make unsupported settings appear functional.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository;
2. identify the web application;
3. inspect authentication/session infrastructure;
4. inspect protected-route conventions;
5. inspect header/navigation;
6. inspect existing notification UI;
7. inspect user/profile components;
8. inspect API-client conventions;
9. inspect server-state and cache configuration;
10. inspect form/validation infrastructure;
11. inspect accessibility utilities;
12. inspect analytics;
13. inspect testing infrastructure.

Preserve compatible existing behavior.

Do not introduce competing account/settings frameworks unnecessarily.

---

# 8. Authenticated Route Model

Viewer account and privacy settings must be protected.

Use the project's canonical authentication/session model.

Protected sections should support routes conceptually equivalent to:

```text
/settings
/settings/account
/settings/privacy
/settings/notifications
/settings/security
/settings/playback
/settings/history
/settings/personalization
```

The exact routing structure may follow the repository's conventions.

Do not rely exclusively on client-side checks for actual authorization.

---

# 9. Session-Aware Rendering

Authenticated settings must correctly handle:

* authenticated viewer;
* loading session;
* unauthenticated viewer;
* expired session;
* revoked session;
* insufficient permissions.

Do not render sensitive account information before authentication state is known when doing so could cause leakage.

---

# 10. Settings Shell

Implement a reusable settings layout.

Conceptually:

```text
SettingsShell
  ├── SettingsNavigation
  └── SettingsContent
```

It must support:

* desktop navigation;
* mobile navigation;
* active section;
* deep links;
* browser back/forward;
* accessible headings;
* responsive layouts.

Avoid repeating the navigation logic in every settings page.

---

# 11. Settings Categories

Expose only supported project settings.

Potential categories include:

* Account;
* Profile;
* Notifications;
* Privacy;
* Security;
* Playback;
* History;
* Personalization;
* Data and privacy.

Do not display an interactive settings section when no real backend capability exists.

---

# 12. Notification Center Route

Implement a canonical notification-center route.

A route may be equivalent to:

```text
/notifications
```

Preserve existing routing conventions if different.

It must support:

* direct navigation;
* refresh;
* browser back/forward;
* authenticated access;
* pagination;
* unread state;
* notification navigation;
* read-state mutation.

---

# 13. Notification Data Contract

Consume a typed notification representation.

A conceptual notification may contain:

```text
notificationId
type
createdAt
readAt
isRead
actor
video
channel
message
navigationTarget
metadata
```

The actual contract must determine field names.

Do not expose internal provider payloads directly to the UI.

---

# 14. Notification Types

Render only notification types defined by the project contract.

Potential examples include:

* new upload from subscribed channel;
* reply to comment;
* reaction;
* mention;
* live-stream start;
* playlist activity;
* account/security alert;
* platform/system notification.

Each type must use a dedicated presentation mapping where necessary.

Do not infer notification meaning from arbitrary strings.

---

# 15. Notification Item Architecture

Implement reusable notification items.

Conceptually:

```text
NotificationItem
  ├── NotificationIcon
  ├── NotificationContent
  ├── NotificationMetadata
  └── NotificationActions
```

The component must remain safe when optional related entities are missing.

Do not assume every notification has:

* an actor;
* a video;
* a channel;
* a thumbnail.

---

# 16. Notification Navigation

Selecting a notification must navigate to the canonical destination defined by the project.

Possible targets include:

* video;
* channel;
* comment;
* playlist;
* live stream;
* settings/security page.

Never construct privileged destinations from untrusted notification data without validation.

Avoid open redirects.

Do not navigate to arbitrary external URLs unless explicitly authorized by the contract.

---

# 17. Notification Read State

Support:

* unread state;
* read state;
* marking a notification as read;
* marking multiple/all notifications as read where supported.

When marking read:

* prevent duplicate conflicting mutations;
* reconcile with server state;
* handle failed mutations;
* do not falsely clear unread state permanently after a failed request.

---

# 18. Unread Notification Count

Where the product exposes an unread notification badge:

* consume the canonical unread count/state;
* update it after confirmed mutations where appropriate;
* avoid incrementing/decrementing purely from local assumptions;
* prevent stale notification responses from restoring incorrect counts.

The count may be eventually consistent.

Do not claim exact real-time synchronization unless supported by the actual backend contract.

---

# 19. Notification Pagination

Use the canonical notification pagination model.

Support:

* initial page;
* next page;
* loading;
* retry;
* end of results;
* duplicate prevention;
* stale-response protection.

Do not load an unbounded notification history into the browser.

---

# 20. Notification Empty State

When there are no notifications:

* explain that the notification center is empty;
* preserve normal application navigation;
* provide useful preference navigation where appropriate.

Do not generate fake notifications.

---

# 21. Notification Failure Handling

Distinguish:

* no notifications;
* network failure;
* authorization failure;
* temporary service failure;
* rate limiting.

A notification service failure must not break:

* video playback;
* search;
* channel pages;
* settings navigation.

Use localized error handling.

---

# 22. Notification Preferences

Implement viewer-facing notification preferences where supported.

Potential settings include:

* channel upload notifications;
* comment/reply notifications;
* mentions;
* recommended-content notifications;
* live-stream notifications;
* security alerts;
* product/system communications.

Only expose categories represented by the backend contract.

Do not fabricate preference categories.

---

# 23. Delivery Channels

Where supported, expose controls for:

* in-app;
* browser push;
* email;
* other project-supported channels.

The UI must distinguish:

* enabled;
* disabled;
* unavailable;
* permission not granted;
* loading;
* failure.

Do not claim that enabling a browser preference automatically grants browser permission.

---

# 24. Browser Notification Permission

Where browser push exists:

* detect browser support;
* detect permission state;
* explain permission requirements;
* invoke browser permission only from an appropriate user action;
* handle denied/default/granted states.

Do not repeatedly prompt users automatically.

Do not treat browser permission as equivalent to backend notification preference.

These are separate states.

---

# 25. Preference Persistence

Notification preference changes must:

* use the canonical API;
* validate values;
* show saving state;
* reconcile server responses;
* handle failures;
* prevent conflicting concurrent updates.

Do not mark a setting permanently changed before a required backend confirmation.

---

# 26. Preference Grouping

Group settings into understandable categories.

Avoid overwhelming users with raw backend fields.

Use product-facing labels while keeping stable internal identifiers.

Changes must map deterministically to the project's canonical preference model.

---

# 27. Profile Settings

Implement viewer profile-management UI for fields supported by the project.

Potential fields include:

* display name;
* handle;
* avatar;
* profile description;
* public-facing profile information.

Only expose fields supported by the account/profile contract.

---

# 28. Profile Editing

Profile edits must support:

* initial value loading;
* validation;
* save;
* cancel/reset;
* loading;
* success;
* error;
* server reconciliation.

Do not treat local form state as authoritative.

---

# 29. Avatar Management

Where avatar editing is supported:

* use the project's media-upload contract;
* validate file type and size according to the contract;
* display upload progress where provided;
* show preview safely;
* handle cancellation/failure;
* update the profile only after successful upload.

Do not create a separate upload backend.

Do not expose raw object-storage credentials.

---

# 30. Handle and Username Changes

Where supported:

* validate format;
* surface availability/conflict errors;
* distinguish invalid from unavailable values;
* prevent duplicate submissions;
* reconcile the server response.

Do not perform availability checks on every keystroke without a controlled debounce and explicit contract.

---

# 31. Privacy Settings

Implement viewer privacy controls supported by the product.

Potential settings include:

* public/private subscription visibility;
* watch-history behavior;
* search-history behavior;
* personalization;
* activity visibility;
* profile visibility;
* communication preferences.

Use only project-defined fields.

---

# 32. Subscription Privacy

If subscription visibility is configurable:

* expose the current server-defined value;
* provide a clear explanation;
* update through the canonical API;
* show saving/error state.

Do not infer public subscription state from unrelated channel data.

---

# 33. Watch History Controls

Where supported, expose history-related settings such as:

* enable/disable history;
* pause history;
* manage/delete history.

The UI must clearly distinguish:

* history collection;
* existing history deletion.

Changing a preference must not automatically delete existing history unless the backend contract explicitly defines that behavior.

---

# 34. Search History Controls

Where supported:

* show search-history state;
* allow pausing/enabling;
* provide management/deletion entry points where the product supports them.

Search history must be treated as sensitive behavioral data.

Do not transmit raw search history through analytics.

---

# 35. Personalization Controls

Where supported, expose viewer-facing personalization controls.

Potential controls may affect:

* recommendations;
* search personalization;
* homepage content;
* autoplay;
* contextual suggestions.

Do not implement ranking algorithms in the browser.

These settings only communicate viewer preference to the authoritative backend.

---

# 36. Playback Preferences

Where supported, expose persistent playback preferences such as:

* autoplay;
* preferred playback quality behavior;
* caption preferences;
* preferred playback speed.

The actual player remains responsible for playback execution.

This scope provides preference management and integration with the existing player contract.

---

# 37. Caption Preferences

Where the product supports persistent caption preferences:

* expose caption enable/disable;
* preferred language where supported;
* reconcile with browser/player capabilities.

Do not assume every video offers the selected language.

The player must gracefully fall back when a preferred track is unavailable.

---

# 38. Security Settings

Expose viewer-facing security settings supported by the project.

Potential functionality includes:

* active sessions/devices;
* sign-out of another session;
* password-management entry point;
* MFA settings entry point;
* account-security alerts.

Do not implement cryptographic or identity-provider infrastructure in the frontend.

---

# 39. Session and Device Management

Where the backend provides active-session information:

Display only safe user-facing fields such as:

* device/platform;
* approximate browser;
* session creation/recent activity;
* location information only when explicitly provided and appropriate.

Do not expose internal session IDs or security metadata unnecessarily.

---

# 40. Revoke Session

Where supported, allow the viewer to revoke another session.

Support:

* confirmation;
* loading;
* success;
* failure;
* reconciliation with the session list.

The currently active session must receive special handling if the backend contract permits revoking it.

Do not make assumptions about token invalidation performed by the backend.

---

# 41. Security Alerts

Display server-provided security/account alerts where the notification or security contract supports them.

Examples:

* new sign-in;
* suspicious activity;
* credential change;
* MFA change;
* session revocation.

Do not generate security alerts locally.

Do not expose sensitive authentication information in UI analytics.

---

# 42. Account Deletion Entry Point

Where account deletion is supported:

* provide a clear destructive-action entry;
* explain consequences according to product policy;
* require appropriate confirmation;
* require reauthentication if the backend contract requires it;
* submit the deletion request through the canonical API;
* handle pending/deferred deletion states;
* avoid claiming deletion is complete when processing is asynchronous.

Do not implement backend deletion processing.

---

# 43. Data Export / Privacy Requests

Where supported, provide viewer-facing entry points for:

* data export;
* privacy requests;
* account data management.

The frontend should:

* initiate the canonical request;
* display request state;
* show pending/success/failure;
* allow navigation to supported status/details.

Do not generate data exports in the browser unless that behavior is explicitly defined by the architecture.

---

# 44. Destructive Action Safety

For account deletion, history clearing, session revocation, and other destructive actions:

* use explicit confirmation where appropriate;
* make the consequence clear;
* prevent accidental double-submission;
* disable conflicting controls during submission;
* reconcile server state;
* provide clear failure feedback.

Do not hide destructive actions behind ambiguous labels.

---

# 45. Settings Forms

Use consistent form architecture.

Every supported setting/form should address:

* initial values;
* validation;
* dirty state where useful;
* submission;
* saving;
* successful persistence;
* failure;
* reset/cancel;
* accessibility.

Do not submit unchanged values unnecessarily when the API supports partial updates.

---

# 46. Form Validation

Client validation should provide immediate usability feedback, but the backend remains authoritative.

Validate:

* required values;
* supported formats;
* maximum lengths;
* invalid combinations where known.

Do not duplicate complicated business rules in the browser when those rules can change independently on the server.

---

# 47. Unsaved Changes

For multi-field settings forms:

* track dirty state;
* prevent accidental navigation where practical;
* warn before discarding meaningful unsaved changes;
* preserve typed data during recoverable errors.

Do not interrupt navigation for forms with no actual changes.

---

# 48. State and Caching

Use the project's server-state system.

Distinguish:

### Server state

* notification list;
* unread count;
* preferences;
* profile;
* security/session list;
* privacy settings.

### Local state

* form drafts;
* open menus;
* confirmation dialogs;
* temporary validation state.

### Persistent local preferences

Only values explicitly safe and appropriate for local persistence.

Do not store sensitive account settings unnecessarily in browser storage.

---

# 49. Account Switching

When the authenticated viewer changes:

* clear notification state;
* clear unread counts;
* clear settings caches;
* clear profile caches;
* clear security/session data;
* clear privacy preferences;
* clear personalization state.

No previous account's settings may remain visible after account switching.

---

# 50. Logout Integration

The settings/account experience must use the canonical logout behavior.

After logout:

* invalidate viewer-specific client state;
* invalidate notification counts;
* invalidate settings caches;
* remove protected-route access;
* navigate to the project's appropriate public destination.

Do not merely hide settings UI while retaining sensitive cached data in memory if the application lifecycle can reasonably clear it.

---

# 51. Session Expiration

When a session expires:

* preserve appropriate unsaved local form state where safe;
* stop issuing authenticated requests;
* avoid infinite retries;
* transition to the public/unauthenticated application state;
* present the correct authentication pathway.

Do not loop between refresh and logout indefinitely.

---

# 52. Notifications and Real-Time Updates

Where the project provides realtime notification updates:

* consume the established realtime contract;
* update unread count correctly;
* deduplicate notifications;
* reconcile with server state;
* clean up subscriptions on unmount/logout.

Do not implement a new WebSocket protocol.

If realtime is not currently available, use the established polling/refetch strategy only where the project's contract supports it.

---

# 53. Notification Deduplication

Prevent duplicate notifications caused by:

* realtime delivery;
* cache revalidation;
* pagination;
* retries;
* reconnects.

Use canonical notification IDs.

Do not deduplicate solely by notification text.

---

# 54. Notification Ordering

Use server-provided ordering.

Do not sort notifications on the client by an assumed timestamp format unless the contract guarantees the semantic ordering.

When new notifications arrive in realtime:

* place them according to the canonical ordering;
* avoid disturbing a currently focused item unexpectedly;
* update unread state appropriately.

---

# 55. Analytics and Telemetry

Instrument appropriate settings and notification behavior.

Potential events include:

```text
notifications_opened
notification_clicked
notification_marked_read
notifications_marked_read
notification_preferences_viewed
notification_preference_changed
profile_settings_viewed
profile_updated
privacy_settings_viewed
privacy_setting_changed
playback_preference_changed
security_settings_viewed
session_revoked
account_deletion_started
data_export_requested
```

Use canonical project event names when available.

Do not log:

* passwords;
* tokens;
* MFA secrets;
* private security details;
* complete notification contents;
* raw search history;
* sensitive account data.

---

# 56. Analytics Privacy

Analytics must not become a side channel for sensitive settings.

For example, do not emit:

```text
privacy_setting_changed("show_my_subscriptions": false)
```

if the project's privacy model does not permit that information to leave the settings system.

Use non-sensitive event categories or carefully defined metadata.

---

# 57. Accessibility

Implement:

* semantic settings sections;
* accessible tab/list navigation where applicable;
* accessible switches/checkboxes;
* keyboard navigation;
* screen-reader labels;
* status feedback;
* focus management;
* accessible destructive-action dialogs;
* understandable validation messages.

Settings controls must expose actual state to assistive technologies.

Do not use visual-only toggles without semantic control behavior.

---

# 58. Responsive Behavior

Support:

* mobile web;
* tablet;
* desktop;
* large desktop.

Settings navigation should collapse appropriately on narrow screens.

Notification lists must remain readable.

Long preference labels must wrap safely.

Destructive dialogs must fit within small viewports.

---

# 59. Security

The frontend must:

* never expose secrets;
* never log credentials;
* use secure session handling;
* respect backend authorization;
* protect sensitive settings from unauthorized rendering;
* validate navigation targets;
* avoid unsafe HTML;
* avoid open redirects;
* prevent accidental disclosure of account state.

Do not make frontend-only authorization decisions authoritative.

---

# 60. Privacy

The settings experience itself contains sensitive information.

Protect:

* notification preferences;
* security/session data;
* search-history preferences;
* watch-history state;
* personalization settings;
* private profile settings;
* account deletion status.

Do not expose protected data through:

* public metadata;
* shared caches;
* static rendering;
* analytics;
* browser URLs.

---

# 61. Error Isolation

An individual settings failure must not break the entire account-management application.

Examples:

```text
Notification preferences fail
Profile settings remain usable
```

or:

```text
Security session list fails
Privacy settings remain accessible
```

Use localized errors and retries.

---

# 62. Component Boundaries

Maintain conceptual boundaries:

```text
settings/
  shell
  navigation
  account
  profile
  privacy
  playback
  personalization
  security
  data
  components
  forms
  analytics

notifications/
  data
  center
  item
  preferences
  unread
  realtime
  analytics
```

The repository structure may differ.

Keep notification infrastructure separate from generic settings UI.

Avoid one giant settings component.

---

# 63. API Error Normalization

Use the project's canonical error representation.

Distinguish:

```text
authentication
authorization
validation
conflict
rateLimited
notFound
temporarilyUnavailable
network
unknown
```

Map each category to appropriate UI behavior.

Do not expose internal debugging information.

---

# 64. Testing Strategy

Implement tests for actual behavior.

### Unit tests

Cover:

* settings serialization;
* preference mapping;
* notification deduplication;
* unread-count reconciliation;
* session-state transitions;
* account-switch invalidation;
* destructive-action state;
* error classification;
* analytics event construction.

### Component tests

Cover:

* settings navigation;
* profile form;
* privacy controls;
* notification item;
* notification pagination;
* preference toggles;
* security/session list;
* session revoke;
* destructive confirmation dialogs;
* data/privacy controls.

### Integration tests

Cover:

* protected-route access;
* notification loading;
* notification read state;
* notification preference updates;
* profile update;
* privacy updates;
* playback/discovery preference updates;
* session listing;
* session revocation;
* account switching;
* logout;
* session-expiration handling.

### End-to-end tests

At minimum:

1. authenticate;
2. open notification center;
3. read a notification;
4. navigate from a notification;
5. change notification preference;
6. open account settings;
7. update a supported profile field;
8. change a privacy preference;
9. inspect supported security/session settings;
10. revoke a session where test infrastructure supports it;
11. verify account-specific cache/state isolation;
12. logout;
13. verify protected settings are no longer accessible;
14. verify keyboard-accessible settings controls;
15. verify destructive confirmation behavior.

Do not replace behavioral testing with snapshots alone.

---

# 65. Browser Compatibility

Validate across the supported browser matrix.

Pay particular attention to:

* responsive settings navigation;
* switches;
* dialogs;
* focus management;
* notification permission handling;
* form behavior.

Do not assume browser notification APIs are universally available.

---

# 66. Performance

Optimize:

* notification loading;
* settings navigation;
* form interactions;
* cache reuse;
* authenticated route transitions.

Do not fetch every settings category simultaneously if only one section is active and the architecture does not require it.

Notification pagination must remain bounded.

---

# 67. Documentation

Update documentation describing:

* protected settings routes;
* notification-center architecture;
* preference model;
* viewer settings model;
* privacy-sensitive state;
* security/session controls;
* notification realtime integration if present;
* account-switch behavior;
* logout cache invalidation;
* telemetry/privacy considerations;
* accessibility behavior.

Documentation must accurately reflect implementation.

---

# 68. No Fake Settings or Notifications

Do not create:

* fake notifications;
* fake unread counts;
* fake profile persistence;
* fake security sessions;
* fake privacy changes;
* fake account deletion;
* fake data export completion.

Mocks are acceptable only inside automated tests.

The application path must use real contracts.

---

# 69. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* nonfunctional switches;
* fake settings;
* placeholder notification actions;
* incomplete security controls;
* empty save handlers;
* fake destructive flows;
* “implement later” sections.

Everything inside the current scope must be genuinely implemented.

---

# 70. Validation

Before completion, validate:

* TypeScript compilation;
* linting;
* unit tests;
* component tests;
* integration tests;
* end-to-end tests where available;
* production build;
* protected routes;
* notification center;
* unread state;
* notification preferences;
* profile settings;
* privacy settings;
* personalization preferences;
* security/session settings;
* account-switch isolation;
* logout behavior;
* responsive behavior;
* accessibility-critical controls;
* notification deduplication;
* stale-request protection.

Fix issues discovered within this scope.

Do not merely report them.

---

# 71. Definition of Done

This prompt is complete only when:

* protected settings routes work;
* settings navigation works;
* notification center works;
* notification pagination works;
* notification read state works;
* notification navigation works;
* unread state is reconciled correctly;
* notification preferences work where supported;
* delivery-channel preferences work where supported;
* browser notification permission is handled correctly where supported;
* profile settings work where supported;
* profile updates are persisted through real contracts;
* privacy settings work where supported;
* history/privacy controls work where supported;
* personalization settings work where supported;
* playback preferences work where supported;
* security/session settings work where supported;
* session revocation works where supported;
* account deletion entry point behaves correctly where supported;
* data/privacy request entry points behave correctly where supported;
* logout invalidates viewer-specific state;
* account switching does not leak data;
* sensitive data is not exposed through shared caches or analytics;
* authentication expiration is handled safely;
* realtime notification integration works where supported;
* notification duplicates are prevented;
* loading/error/empty states are implemented;
* responsive behavior works;
* accessibility requirements are implemented;
* tests cover the defined behavior;
* documentation is updated;
* no fake production behavior remains;
* no current-scope placeholders remain;
* validation passes.

---

# 72. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize notification, settings, privacy, personalization, and security-sensitive viewer functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List notification, preference, profile, privacy, session/security, data-management, and analytics contracts consumed.

### State and Caching

Summarize protected-route behavior, viewer-specific cache isolation, notification deduplication, account switching, logout invalidation, and mutation reconciliation.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, production build, and runtime validation.

### Integration Notes

Identify material backend-contract assumptions, external browser capabilities, or dependencies requiring server/infrastructure support.

### Out of Scope

Confirm that notification delivery infrastructure, authentication backend, privacy-compliance processing, mobile, moderation, creator studio, live streaming, and monetization were not improperly implemented.

---

# 73. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe the account settings or notification experience.

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

The result must be a real, production-grade **YouTube-style web notification, viewer settings, privacy, personalization, and account-security experience** that can be integrated with the independently generated backend and other project components through explicit contracts.
