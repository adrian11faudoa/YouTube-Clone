# YouTube-Style Video Platform — Mobile Prompt — Volume 1

## 1. Prompt Identity

You are the senior React Native/mobile engineer responsible for implementing the **cross-platform mobile application foundation, navigation, authentication, shared UI system, API integration, and initial home/discovery experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility is the mobile application foundation for iOS and Android, including:

- React Native application architecture;
- navigation;
- design tokens and reusable components;
- authentication and session handling;
- API integration;
- server-state management;
- local UI-state management;
- application configuration;
- home screen;
- discovery feed shell;
- video and channel cards;
- subscription-aware UI foundations;
- loading, empty, and error states;
- connectivity awareness;
- accessibility;
- telemetry;
- testing;
- documentation.

Do not implement unrelated mobile domains.

Do not implement backend services or web frontend functionality.

Do not fabricate authentication, API responses, persistence, or discovery results.

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
- administration;
- paid memberships and monetization-capable functionality;
- web and native mobile clients.

The project-wide technology direction includes:

- TypeScript;
- React Native;
- iOS and Android;
- the project's established navigation and state-management libraries;
- typed API clients;
- secure authentication/session integration;
- production-quality testing;
- observability;
- accessibility;
- responsive layouts appropriate for mobile devices.

The mobile application must integrate with the same canonical backend domain model used by the web application. It must not establish competing definitions for users, videos, channels, subscriptions, authentication, errors, or identifiers.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- earlier frontend or backend prompts;
- hidden architecture decisions;
- undocumented API endpoints;
- generated files unavailable in the current environment;
- a repository shared with another AI conversation.

If a repository is available, inspect it before modifying it.

If portable architecture, API, authentication, or data-contract artifacts are supplied, use them as authoritative.

If the repository already contains a compatible mobile application, preserve and extend it rather than creating a competing application.

If no mobile application exists, establish the native application foundation specified in this prompt.

The repository represents actual implementation state. The explicit requirements in this prompt define the current task.

---

# 4. Primary Objective

Build a maintainable, production-grade mobile foundation for a YouTube-style video platform that can be extended by independently executed mobile implementation milestones.

The completed scope must provide:

1. a working React Native application for iOS and Android;
2. a stable application architecture;
3. navigation and route organization;
4. authentication-aware navigation;
5. secure session integration;
6. a typed API client;
7. consistent API error handling;
8. server-state and client-state separation;
9. reusable design-system primitives;
10. a home/discovery screen;
11. video and channel card components;
12. real discovery API integration where the contract is available;
13. loading, empty, and recoverable failure states;
14. network-connectivity awareness;
15. accessible mobile interactions;
16. appropriate telemetry;
17. automated testing;
18. documented development and integration procedures.

---

# 5. Explicit Scope

Implement:

- mobile application foundation;
- iOS/Android configuration;
- TypeScript configuration;
- navigation architecture;
- authentication/session integration;
- API-client architecture;
- configuration and environment handling;
- design tokens;
- reusable interface primitives;
- application shell;
- shared header and navigation components;
- home screen;
- discovery screen foundation;
- video cards;
- channel cards;
- feed presentation;
- server-state management;
- local UI-state management;
- loading, empty, error, and offline states;
- account-aware cache isolation;
- analytics/telemetry foundation;
- accessibility;
- testing infrastructure;
- development documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- the complete video playback engine;
- advanced short-form feed gestures;
- complete search experience;
- full comment/reply functionality;
- complete playlist management;
- complete notification center;
- creator studio;
- live-streaming controls;
- monetization and purchases;
- moderation console;
- administrative tools;
- backend APIs;
- backend databases;
- media-processing infrastructure;
- infrastructure provisioning;
- iOS/Android store publication.

These are separate domains and must not be silently absorbed into this milestone.

The application foundation must be designed so those features can be integrated without requiring a disruptive rewrite.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. identify the existing mobile application, if present;
3. identify the package manager and scripts;
4. inspect React Native and Expo configuration where applicable;
5. inspect navigation libraries and existing routes;
6. inspect authentication/session handling;
7. inspect the API-client implementation;
8. inspect state-management dependencies;
9. inspect shared types and domain models;
10. inspect styling and reusable components;
11. inspect testing infrastructure;
12. inspect linting, formatting, and TypeScript rules;
13. inspect environment/configuration conventions;
14. inspect build and runtime configuration.

Reuse compatible dependencies and code.

Do not create a second application entry point, API client, navigation system, authentication store, or state-management framework without a documented technical reason.

If a compatible mobile architecture already exists, extend it and document any necessary compatibility decisions.

---

# 8. Mobile Technology Direction

Use React Native and TypeScript for native iOS and Android applications.

Use Expo when it is already part of the repository or is compatible with the established project direction and required native capabilities.

If the existing project uses a bare React Native workflow, preserve it unless a well-supported technical requirement necessitates a change.

Use established libraries for:

- navigation;
- server-state management;
- secure credential storage;
- forms and validation where appropriate;
- network/connectivity awareness;
- telemetry;
- automated testing.

Do not write custom implementations of foundational platform capabilities when a maintained, compatible library already provides the required behavior.

Document material technology choices that affect later mobile implementation work.

---

# 9. Application Architecture

Establish a modular application structure.

A conceptual layout may be:

```text
mobile/
  app/
  src/
    app/
    navigation/
    api/
    auth/
    config/
    design-system/
    components/
    features/
      home/
      discovery/
      videos/
      channels/
    hooks/
    state/
    telemetry/
    utils/
    types/
    tests/
```

The actual structure may follow existing repository conventions.

Responsibilities must remain clearly separated.

Do not put API requests, authentication logic, navigation configuration, and all screen components into one large module.

Avoid circular dependencies between feature modules.

---

# 10. Navigation Architecture

Implement a maintainable navigation structure for the native application.

The initial navigation model should support the core application surfaces, including:

- Home;
- Search entry point;
- Subscriptions entry point where available;
- Notifications entry point where available;
- Library entry point where available;
- account/authentication routes.

For this milestone, the fully implemented screen content is limited to the home/discovery foundation and authentication/navigation foundation.

Other navigation destinations may only be represented when their routes and states can be integrated honestly with existing implementations. Do not create fake completed screens for features that belong to future milestones.

Use the project's established navigation convention. If no compatible convention exists, choose a maintained React Native navigation library appropriate for the application.

---

# 11. Navigation Behavior

Support:

- normal push navigation;
- tab navigation where used;
- back navigation;
- authentication-dependent routing;
- deep-link-ready route definitions;
- predictable screen lifecycle behavior;
- state preservation where appropriate.

Navigation must not depend exclusively on a previously mounted screen retaining in-memory state.

Avoid duplicate navigation actions caused by repeated taps or repeated API callbacks.

Do not introduce arbitrary screen transitions that conflict with the platform's expected navigation behavior.

---

# 12. Authentication State Model

Establish a typed authentication/session state model.

At minimum, distinguish states equivalent to:

```text
initializing
unauthenticated
authenticating
authenticated
refreshing
expired
error
```

Use the existing project session model where one exists.

The application must not treat the presence of a cached user object as sufficient proof that the current session is valid.

The backend remains authoritative for authentication and authorization.

---

# 13. Authentication Integration

Integrate with the project's canonical authentication contract.

Support the infrastructure required for:

- sign-in;
- registration entry points where supported;
- authenticated session restoration;
- token/session refresh where supported;
- logout;
- authentication errors;
- session expiration;
- protected navigation.

The application may expose the relevant authentication screens only to the extent supported by the canonical auth contract.

Do not invent an authentication protocol, endpoint, token format, or refresh behavior.

If the repository contains a working authentication implementation, reuse it and test its integration with the new navigation structure.

---

# 14. Secure Credential Storage

Use an appropriate secure native storage mechanism for session credentials, according to the project's authentication architecture.

Requirements:

- credentials must not be stored in ordinary unencrypted preferences;
- tokens must not be placed in navigation parameters;
- tokens must not be logged;
- credentials must not be included in analytics;
- logout must remove the relevant local credentials;
- account switching must invalidate old authenticated state.

Use platform-backed secure storage through the established React Native/Expo capability where appropriate.

Do not invent cryptographic storage logic.

Do not store passwords for session restoration.

---

# 15. Session Restoration

At application startup:

1. initialize configuration;
2. restore session information from the approved storage mechanism;
3. validate or refresh session state according to the canonical authentication contract;
4. identify whether the viewer is authenticated;
5. initialize the appropriate navigation state;
6. prevent sensitive authenticated screens from being exposed before session restoration has resolved.

The application must not show authenticated content briefly before redirecting to sign-in because session state was initialized incorrectly.

Avoid indefinite startup loading if the session service fails.

Provide a recoverable state for session-restoration errors.

---

# 16. Logout

Implement logout through the canonical authentication integration.

On logout:

- revoke or invalidate the server session where required and supported;
- remove local session credentials;
- clear user-specific server-state caches;
- clear user-specific client state;
- reset authentication-dependent navigation;
- prevent further authenticated requests using old credentials.

A failed remote logout must not cause the application to continue presenting the user as authenticated indefinitely when the local security policy requires clearing the session.

Document the expected behavior when the device is offline during logout.

---

# 17. Authentication Expiration

Handle expired or revoked sessions.

The implementation must:

- detect the canonical authentication failure;
- attempt the approved refresh flow where supported;
- prevent concurrent requests from triggering uncontrolled refresh operations;
- prevent infinite refresh loops;
- clear invalid credentials when the contract requires it;
- redirect to the appropriate authentication state;
- preserve public navigation where possible.

Do not blindly retry every unauthorized request.

Do not automatically repeat non-idempotent mutations after refreshing a session unless the operation's retry semantics are safe.

---

# 18. Typed API Client

Create or extend a typed API-client layer.

It must provide consistent handling for:

- base URL configuration;
- request methods;
- headers;
- authentication;
- serialization;
- response parsing;
- cancellation;
- timeouts where appropriate;
- error normalization;
- request correlation identifiers where supported.

Keep transport concerns separate from screen components.

Do not write independent ad hoc network calls throughout the application.

Do not hardcode production endpoints into components.

---

# 19. API Contract Compatibility

Use canonical project contracts for:

```text
Canonical IDs
Canonical timestamps
Authentication/session
API success envelope
API error model
Pagination
Video entity
Channel entity
Discovery/feed response
Viewer-specific state
Analytics events
```

The exact contract fields and paths must follow the supplied architecture artifacts or current compatible repository implementation.

If no applicable contract exists, document the missing integration dependency and implement a typed boundary appropriate for the current scope. Do not create a fake production service to make the screen appear functional.

---

# 20. API Error Normalization

Normalize errors into a consistent frontend representation.

The mobile application must be able to distinguish relevant categories such as:

```text
network
timeout
authentication
authorization
validation
notFound
rateLimited
conflict
temporarilyUnavailable
cancelled
unknown
```

Use canonical backend error codes where supplied.

Provide safe fallback behavior for malformed or unrecognized responses.

Do not display raw stack traces, internal service details, or sensitive request information to viewers.

---

# 21. API Request Lifecycle

Requests must support:

- cancellation when a screen is no longer interested in the response;
- avoidance of stale responses;
- deduplication where appropriate;
- retry policies for safe operations;
- request timeouts where appropriate.

Do not automatically retry every request.

Do not retry a failed mutation without understanding its idempotency guarantees.

Handle application backgrounding and navigation changes where they materially affect request ownership.

---

# 22. Server-State Management

Use one consistent server-state strategy compatible with the repository.

Manage data such as:

- home discovery response;
- video metadata used by cards;
- channel metadata used by cards;
- authenticated viewer-specific state.

Support:

- query keys;
- pagination where supplied;
- cache lifetimes;
- invalidation;
- refetch;
- cancellation;
- error state;
- account-specific cache isolation.

Do not put every server response into a single global state object.

Do not create a competing state-management system alongside the existing one.

---

# 23. Client-State Management

Keep local UI state separate from server state.

Local UI state may include:

- selected navigation item;
- transient menus;
- dialogs;
- temporary form state;
- loading indicators;
- screen-specific interaction state.

Avoid introducing global state for component-local interactions.

Choose state ownership deliberately and document material decisions.

---

# 24. Account-Specific Cache Isolation

Viewer-specific data must be associated with the correct authenticated identity.

When the active user changes:

- clear user-specific cached state;
- invalidate subscriptions or library state if present;
- clear viewer-specific reaction/subscription state;
- invalidate authenticated discovery data;
- reset private navigation/state where appropriate.

Never allow one account's cached personalized content to appear after another account signs in.

Do not treat a generic cache clear as a substitute for understanding which state is user-specific.

---

# 25. Configuration Management

Implement a typed configuration layer for environment-dependent mobile settings.

Configuration may include:

- API base URL;
- environment identity;
- telemetry configuration;
- optional feature configuration;
- application/build metadata.

Use the project's established environment strategy.

Requirements:

- validate required configuration;
- fail clearly when essential configuration is absent;
- provide safe defaults only where justified;
- avoid scattering environment lookups across feature modules;
- distinguish public mobile configuration from secrets.

Never include backend secrets or privileged provider keys in the mobile bundle.

A value embedded in a mobile application must be treated as potentially discoverable by the application user.

---

# 26. Design Tokens

Implement a reusable design-token layer for the mobile application.

Include appropriate tokens for:

- colors;
- typography;
- spacing;
- radii;
- borders;
- elevation;
- icon sizes;
- interaction targets;
- responsive layout constants.

Use consistent conventions throughout the current scope.

Do not hardcode unrelated one-off styles in every component.

The design system should remain extendable to the full video platform without forcing all future screens into a single rigid layout.

---

# 27. Theme Support

If the project already defines light/dark themes, integrate them.

If theme selection is required by the application architecture, provide a shared theme mechanism.

The implementation must:

- use consistent tokens;
- respect the selected theme;
- avoid unreadable contrast;
- avoid inconsistent hardcoded colors;
- support native system preferences where the project requires it.

Do not create decorative theme functionality that is not actually connected to shared components.

---

# 28. Reusable UI Components

Implement foundational components required by the current scope.

Examples include:

- primary/secondary button;
- icon button;
- text/input primitives where needed;
- loading indicator;
- error state;
- empty state;
- screen container;
- safe-area-aware layout;
- video card;
- channel card;
- avatar;
- thumbnail;
- separator;
- accessible modal/dialog where necessary.

Follow the repository's existing component conventions.

Avoid making components overly generic before there is a real requirement for that abstraction.

---

# 29. Video Card

Implement a reusable video card appropriate for home/discovery surfaces.

Where supplied by the video contract, present:

- thumbnail;
- title;
- channel identity;
- duration;
- views;
- publication time;
- supported live/short-form indicators.

Support:

- loading;
- unavailable thumbnail;
- missing optional metadata;
- press feedback;
- accessible labels.

Do not render fake engagement counts.

Do not assume every video has every optional field.

---

# 30. Channel Card

Implement a reusable channel card.

Where supplied by the channel contract, show:

- avatar;
- channel name;
- verification state;
- subscriber count;
- description or relevant summary.

The card must support navigation to the canonical channel route when that screen is implemented or otherwise defined by the application architecture.

Do not invent channel identities or subscription counts.

---

# 31. Home Screen

Implement the initial production home screen.

It must include:

- application navigation;
- loading state;
- home/discovery content;
- reusable video cards;
- relevant section headings where provided;
- navigation to the supported discovery surfaces;
- recoverable API failure behavior.

Consume real discovery data through the canonical backend contract when available.

Do not populate the production screen with hardcoded video arrays.

---

# 32. Home Discovery Contract

Consume the established discovery API or feed contract.

The response may contain conceptually:

```text
sections
items
nextCursor
hasMore
generatedAt
```

Use the actual API response structure.

Do not create an incompatible home-feed model.

The frontend is responsible for rendering supplied candidates. The backend remains responsible for candidate generation, ranking, filtering, and personalization.

---

# 33. Discovery Layout

Create a maintainable discovery layout appropriate for native devices.

Support the layout rules required by the design system.

Where the backend supplies sectioned content:

- render supported sections;
- preserve contract-defined ordering;
- avoid duplicating items unnecessarily when the contract defines deduplication;
- isolate section-specific loading/failure behavior when the API supports independent retrieval.

Do not invent additional recommendation categories or ranking mechanisms.

---

# 34. Discovery Pagination

If the home/discovery contract provides pagination, implement it.

Support:

- initial data;
- loading additional content;
- terminal pagination state;
- retry;
- duplicate prevention;
- stale-response protection.

Do not issue duplicate requests for the same cursor.

Do not download the entire discovery feed in one request.

---

# 35. Refresh Behavior

Provide an appropriate refresh interaction where supported.

Refresh behavior must:

- use the canonical feed API;
- show refreshing state;
- handle errors;
- reconcile returned content;
- avoid duplicate pagination requests;
- preserve a usable screen if refresh fails.

Do not clear useful content before a refresh succeeds unless the established product behavior requires it.

---

# 36. Navigation Entry Points

Provide the shared entry points required by the mobile application structure.

Potential destinations include:

- Home;
- Search;
- Subscriptions;
- Notifications;
- Library;
- Account.

Only implement functional screens within the current scope.

For destinations assigned to future implementation milestones, use a clearly defined navigation boundary and do not present fabricated completed functionality.

Do not leave interactive controls that do nothing.

Where a destination is not implemented in this milestone, do not present it as a working feature unless an existing compatible screen already provides its behavior.

---

# 37. Authentication-Aware Home Experience

Public discovery must work without authentication where the backend supports anonymous access.

For authenticated viewers, use personalized discovery only through the appropriate authenticated API contract.

The application must not require login merely to display public content.

When personalization is unavailable, use only an explicitly supported fallback.

Do not fabricate personalized recommendations.

---

# 38. Connectivity Awareness

Implement appropriate network-connectivity awareness using a compatible maintained library or established repository infrastructure.

Distinguish:

- request-specific failure;
- offline state;
- reconnecting/available state.

Avoid assuming that a connected device has successful Internet access.

Where connectivity is unavailable:

- provide understandable feedback;
- preserve safe local navigation;
- avoid retry storms;
- retry/refetch according to deliberate policy.

Do not claim that feed content is available offline unless offline caching has been explicitly implemented and validated.

---

# 39. Loading, Empty, and Error States

Every asynchronous screen or component within this scope must define appropriate states.

### Loading

Show a meaningful native-compatible loading state.

### Empty

Explain when there is no available content or no results.

### Error

Distinguish transient network failure, authorization failure, and unavailable content where possible.

### Retry

Provide retry behavior where meaningful and safe.

Do not convert failed API requests into empty content.

Do not display endless loading indicators when a request has failed.

---

# 40. Offline and Recovery Behavior

For public home/discovery screens, handle temporary disconnection gracefully.

If the project's existing caching strategy allows previously fetched public feed data to remain visible, display it as cached/stale data when appropriate.

Do not invent offline persistence.

Do not persist sensitive authenticated data to ordinary local storage.

When connectivity returns, use controlled revalidation.

Prevent reconnection from triggering duplicate feed requests or duplicate rendered items.

---

# 41. Accessibility

The mobile application must support:

- accessible screen names;
- semantic control labels;
- appropriate accessibility roles;
- screen-reader navigation;
- visible focus where applicable;
- sufficient touch targets;
- accessible loading/error feedback;
- text scaling where practical;
- accessible navigation;
- contrast;
- reduced motion where relevant.

Video cards must expose meaningful labels that communicate the video's title and relevant creator information.

Do not rely solely on images, color, or gestures to convey essential information.

---

# 42. Performance

Optimize the current scope for real mobile devices.

Requirements include:

- efficient list rendering;
- stable keys;
- bounded rendering of long feeds;
- appropriate thumbnail loading;
- minimal unnecessary rerenders;
- manageable application startup work;
- controlled request volume;
- minimal memory retention;
- no unbounded cache growth.

Use optimized list primitives appropriate to the project.

Do not render a large discovery feed using an unbounded collection of nested views when a virtualized list is suitable.

Avoid expensive per-render computations.

---

# 43. Application Lifecycle

Handle relevant application lifecycle transitions.

Consider:

- foregrounding;
- backgrounding;
- navigation away from a screen;
- session expiration;
- connectivity changes.

The application must avoid unnecessary network polling in the background.

Do not assume that a request remains appropriate after the user has navigated away.

Release screen-specific resources when no longer needed.

---

# 44. Deep-Link Readiness

Prepare the navigation architecture for canonical deep links to:

- videos;
- channels;
- authentication routes;
- future supported destination types.

Implement only the deep-link behavior supported by the current repository and application configuration.

Route identifiers must follow the canonical project model.

Do not embed tokens, private metadata, or signed media URLs into deep links.

A URL for a public entity must remain independently navigable rather than depending on a previously mounted screen.

---

# 45. Security

The mobile application must:

- use secure credential storage;
- use approved transport security;
- avoid hardcoded secrets;
- avoid logging tokens;
- handle untrusted server-provided text safely;
- respect backend authorization;
- prevent sensitive cache leakage across accounts;
- validate configuration;
- avoid exposing private data in navigation state;
- use the project's approved authentication model.

Do not implement authoritative access-control decisions exclusively on the client.

---

# 46. Privacy

Respect the project's privacy architecture.

Do not:

- collect unnecessary personal information;
- store credentials in ordinary preferences;
- place private viewer information in URLs;
- leak authenticated data through shared caches;
- send raw private data to telemetry;
- expose private API response fields in logs.

Personalized discovery and viewer-specific state must be scoped to the active identity.

---

# 47. Telemetry and Observability

Integrate a frontend telemetry abstraction appropriate to the project.

The implementation should support relevant signals such as:

- application screen navigation;
- home-feed load success/failure;
- API errors;
- network failure;
- authentication-state transitions;
- unhandled application errors.

Potential event categories include:

```text
mobile_home_opened
mobile_discovery_loaded
mobile_discovery_failed
mobile_video_card_opened
mobile_channel_card_opened
mobile_authentication_started
mobile_authentication_completed
mobile_authentication_failed
mobile_network_state_changed
```

Use the canonical analytics event schema where available.

Do not emit:

- passwords;
- access tokens;
- refresh tokens;
- session secrets;
- raw private content;
- unnecessary personally identifying information.

Do not instrument every render as a user action.

---

# 48. Logging

Use structured, privacy-conscious application logging when the project's mobile observability system supports it.

Logs should help diagnose:

- request failures;
- application configuration problems;
- authentication integration problems;
- unexpected application errors.

Do not log sensitive headers, credentials, private API responses, or signed URLs.

Use the application's established error-reporting and correlation conventions.

Do not add a second logging/telemetry system without a documented reason.

---

# 49. Testing Strategy

Implement automated tests for actual behavior.

### Unit tests

Cover:

- authentication state transitions;
- session-state handling;
- API error normalization;
- request cancellation;
- cache-key generation;
- configuration validation;
- route/parameter handling;
- discovery-data normalization where required;
- telemetry event construction.

### Component tests

Cover:

- video card;
- channel card;
- reusable buttons and inputs;
- loading state;
- error state;
- empty state;
- home/discovery sections;
- authentication-aware navigation;
- connectivity indicator where implemented.

### Integration tests

Cover:

- session restoration;
- authenticated navigation;
- logout;
- API-client authentication;
- API failure handling;
- loading home/discovery content;
- refreshing discovery content;
- pagination where supported;
- stale-response protection;
- account-specific cache clearing.

### End-to-end tests

At minimum:

1. launch the application;
2. verify initialization and navigation;
3. open the home screen;
4. load discovery content from the configured API/test boundary;
5. open a video card through the canonical route;
6. open a channel card;
7. verify loading and failure recovery;
8. restore an authenticated session where test infrastructure supports it;
9. verify logout clears protected state;
10. simulate a network interruption;
11. verify recovery without duplicate feed content;
12. verify public discovery remains accessible anonymously;
13. verify accessibility labels on essential controls;
14. validate the application on supported iOS/Android test targets where available.

Use mocks only as controlled test boundaries. Do not use them as production implementations.

---

# 50. iOS and Android Compatibility

The application must preserve a coherent cross-platform implementation.

Account for differences in:

- status bar and safe areas;
- navigation behavior;
- keyboard handling;
- permissions;
- file/storage APIs if used by existing infrastructure;
- application lifecycle;
- network behavior;
- build configuration.

Use platform-specific code only when a real platform requirement justifies it.

Do not create two independently maintained application implementations for the same feature without a strong reason.

---

# 51. Build and Development Configuration

Provide usable development configuration for the repository's actual mobile stack.

Where applicable, ensure the project has working scripts/configuration for:

- development startup;
- TypeScript checking;
- linting;
- automated testing;
- platform builds;
- environment selection.

Do not claim that an iOS or Android build was validated unless the required runtime/toolchain was available and the build was actually executed.

Document exact external toolchain requirements when an environment limitation prevents validation.

---

# 52. Dependency Discipline

Use maintained, compatible dependencies.

Before adding a dependency:

- inspect existing dependencies;
- verify React Native compatibility;
- verify iOS and Android support;
- verify compatibility with the selected Expo/bare workflow;
- consider bundle size and runtime behavior;
- avoid duplicate libraries providing the same foundational capability.

Do not introduce a large dependency merely to solve a small UI concern.

Do not use unsupported native APIs without documenting the resulting build requirement.

---

# 53. Contract Compatibility

The mobile foundation must preserve compatibility with the platform's canonical:

```text
Identifiers
Timestamps
Authentication/session
Authorization
API envelopes
Error model
Pagination
Video entity
Channel entity
Discovery/feed model
Viewer-specific state
Configuration conventions
Analytics event model
Privacy model
```

Use authoritative contract fields when they are supplied.

Do not silently rename external fields or invent incompatible mobile-only entity definitions.

If a backend contract is missing, define a clear integration boundary and document the dependency. Do not fabricate the API's successful behavior.

---

# 54. No Fake Application Behavior

Do not create:

- hardcoded production video feeds;
- fake users;
- simulated authentication success;
- fake session persistence;
- static recommendations presented as server data;
- mock production API clients;
- fake subscription status;
- simulated network success;
- hardcoded production credentials.

Mocks are permitted only in controlled automated tests.

The real application path must use the project's actual integration interfaces.

---

# 55. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- empty button handlers;
- nonfunctional navigation entries presented as completed features;
- fake authentication handlers;
- placeholder API requests;
- incomplete loading/error handling;
- unused duplicate architecture;
- undocumented stubs for required functionality.

Features outside this milestone must remain explicit future navigation/integration boundaries rather than fake implementations.

Everything inside the current scope must be implemented.

---

# 56. Documentation

Create or update documentation covering:

- mobile application architecture;
- supported development workflow;
- React Native/Expo or bare-workflow decisions;
- navigation;
- authentication/session integration;
- secure credential storage;
- API-client design;
- environment configuration;
- design tokens;
- home/discovery integration;
- cache isolation;
- network recovery;
- telemetry and privacy;
- testing;
- iOS/Android build prerequisites.

Documentation must describe the implementation that actually exists.

Include any external credentials or service configuration needed for integration, but never include the secrets themselves.

---

# 57. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- production/native build where available;
- application startup;
- navigation;
- session restoration;
- logout;
- API-client behavior;
- home/discovery integration;
- loading/error/empty states;
- cache isolation;
- offline/reconnect behavior;
- accessibility-critical controls;
- iOS/Android compatibility where test environments are available.

Fix issues discovered within the current scope.

Do not claim unexecuted checks passed.

If a platform build cannot be run because the required toolchain or external configuration is unavailable, report the exact blocker and still complete all locally possible validation.

---

# 58. Definition of Done

This prompt is complete only when:

- a coherent React Native application exists or the compatible existing application is extended;
- iOS and Android are supported by the implemented architecture;
- navigation works;
- authentication/session integration works within the available contracts;
- secure credential storage is used where required;
- logout and cache invalidation work;
- configuration is typed and validated;
- API integration is centralized;
- API errors are normalized;
- server-state and local-state responsibilities are clear;
- the design-token layer exists;
- reusable UI primitives work;
- video cards work;
- channel cards work;
- home/discovery displays real contract-backed data;
- loading/empty/error states work;
- refresh/pagination work where supported;
- anonymous public discovery works where supported;
- viewer-specific cache isolation works;
- connectivity handling works;
- accessibility requirements are implemented;
- telemetry respects privacy;
- tests cover the defined behavior;
- documentation is updated;
- no fake production behavior remains;
- no current-scope placeholders remain;
- validation passes to the extent possible in the available environment.

---

# 59. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize the mobile application foundation, navigation, authentication, API integration, shared UI, and home/discovery functionality actually completed.

### Files

List significant files created, modified, or deleted.

### Architecture

Summarize application structure, navigation, state ownership, API-client organization, and configuration.

### Contracts

List authentication, API, discovery, video, channel, pagination, and telemetry contracts consumed.

### Testing

List tests created and tests executed.

### Validation

Report TypeScript, linting, builds, and runtime validation performed. Identify platform-specific checks that could not be executed.

### Integration Notes

Identify required environment configuration, authentication-provider setup, API dependencies, or mobile toolchain constraints.

### Out of Scope

Confirm that the full playback engine, advanced shorts, complete comments, playlists, notifications, creator studio, live streaming, monetization, moderation, and backend services were not improperly implemented.

---

# 60. Final Execution Directive

Execute this prompt as a concrete mobile implementation task.

Do not merely describe the mobile architecture.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate authentication, persistence, API, or discovery behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated mobile or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style React Native mobile application foundation with authentication, navigation, shared UI, and home/discovery functionality** that can be extended through independently generated mobile implementation milestones and integrated with the project's canonical backend contracts.
