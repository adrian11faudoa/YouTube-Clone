# YouTube-Style Video Platform — Frontend Prompt — Volume 1

# 1. ROLE AND PURPOSE

You are the senior frontend engineer responsible for implementing the first bounded web-frontend milestone of the **YouTube-Style Video Platform**.

This milestone establishes the production web application foundation and implements the core authenticated/public application shell required for later web milestones.

This milestone covers:

* Next.js application foundation;
* routing architecture;
* layouts;
* design system foundation;
* responsive navigation;
* authentication-aware application state;
* account/session flows;
* public/private route protection;
* shared API client;
* server/client data boundaries;
* loading states;
* error states;
* reusable UI primitives;
* accessibility foundation;
* responsive behavior;
* theme and visual foundations;
* home/discovery shell;
* channel shell;
* basic video-card infrastructure;
* shared media/image primitives;
* notification entry points;
* analytics/telemetry hooks;
* frontend testing;
* frontend documentation.

This is a bounded frontend implementation milestone.

It does not authorize implementation of the entire web application.

It does not authorize implementation of every creator workflow, watch experience, search interface, live-stream interface, monetization interface, moderation console, or administration console.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that another AI prompt was executed merely because it exists in the user's conversation.

Do not fabricate repository state.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent YouTube-style video platform supporting:

* viewers;
* creators;
* channels;
* long-form video;
* short-form video;
* uploads;
* adaptive playback;
* comments;
* reactions;
* subscriptions;
* playlists;
* search;
* recommendations;
* notifications;
* analytics;
* moderation;
* administration;
* live streaming;
* monetization-capable functionality.

The web application is a production client for these backend capabilities.

## 2.2 Web Technology

Use:

* TypeScript;
* React;
* Next.js App Router;
* accessible HTML semantics;
* responsive CSS;
* the repository's established styling strategy;
* the project's typed API contracts;
* the project's established authentication/session model.

Use compatible existing repository versions.

Do not replace a working frontend framework or build system merely for convenience.

---

# 3. CURRENT MILESTONE SCOPE

Implement:

1. Next.js application foundation.
2. Global application layout.
3. Responsive navigation shell.
4. Desktop navigation.
5. Mobile/tablet navigation behavior.
6. Header/top-bar foundation.
7. Sidebar/navigation behavior.
8. Design-token foundation.
9. Typography system.
10. Spacing/layout primitives.
11. Color/theme tokens.
12. Button/input/link/card primitives.
13. Accessible modal/dialog foundations.
14. Toast/feedback foundations.
15. Authentication-aware client state.
16. Login screen.
17. Registration screen.
18. Session restoration.
19. Logout.
20. Protected-route behavior.
21. Public-route behavior.
22. Shared typed API client.
23. API error normalization.
24. Request cancellation and timeout handling where appropriate.
25. Query/server-state foundation.
26. Home/discovery page shell.
27. Video-card component.
28. Channel-card component.
29. Feed loading/empty/error states.
30. Channel-page shell.
31. Account/profile entry points.
32. Responsive image/media primitives.
33. Accessibility foundation.
34. Analytics/telemetry hooks.
35. Frontend error boundary strategy.
36. Unit/component/integration tests.
37. Frontend documentation.

This milestone does not implement:

* full video watch-page experience;
* complete player controls;
* comments UI;
* playlist UI;
* search UI;
* full creator studio;
* upload UI;
* live-stream UI;
* monetization UI;
* moderation console;
* administration console;
* advanced recommendation controls;
* complete notification center.

Later frontend milestones will implement those bounded areas.

---

# 4. REPOSITORY INSPECTION

Before implementation:

1. Inspect the repository structure.
2. Inspect the existing Next.js application.
3. Inspect package manifests.
4. Inspect TypeScript configuration.
5. Inspect linting and formatting configuration.
6. Inspect existing styling/design-system code.
7. Inspect authentication/session code.
8. Inspect API client code.
9. Inspect generated/shared contracts.
10. Inspect existing routes.
11. Inspect tests.
12. Inspect error handling.
13. Inspect analytics/telemetry.
14. Inspect environment configuration.
15. Inspect existing assets.

Reuse compatible existing code.

Do not duplicate components or API clients already present.

If the repository contains partial implementation, preserve compatible behavior and extend it coherently.

Do not infer frontend contracts from another AI conversation.

Inspect actual backend/API contracts represented in the repository or provided architecture artifacts available to the implementation environment.

---

# 5. FRONTEND ARCHITECTURE

Organize the web application into clear boundaries.

At minimum distinguish:

* app/routes;
* layouts;
* shared UI;
* design tokens;
* API/client infrastructure;
* authentication/session;
* server-state/data access;
* domain components;
* analytics;
* error handling;
* accessibility utilities.

Prefer a modular structure that allows later implementation of:

* watch;
* search;
* playlists;
* comments;
* creator studio;
* live streaming;
* monetization;
* moderation;
* administration

without turning the application into one monolithic component tree.

Do not create a separate state store for every feature.

Use server state and client state for their appropriate responsibilities.

---

# 6. NEXT.JS APP FOUNDATION

Implement the production Next.js foundation.

Configure:

* App Router;
* root layout;
* route-group strategy where appropriate;
* metadata;
* fonts;
* global styles;
* environment configuration;
* error boundaries;
* not-found behavior;
* loading boundaries.

Use server components by default when they provide a clear benefit.

Use client components only when interactivity, browser APIs, local state, or event handling requires them.

Do not turn the entire application into a client-rendered tree unnecessarily.

---

# 7. ENVIRONMENT CONFIGURATION

Define validated frontend configuration.

Separate:

* public browser configuration;
* server-only configuration;
* development configuration;
* production configuration.

Public variables must be explicitly prefixed according to the chosen framework conventions.

Never expose:

* backend secrets;
* access tokens;
* private signing keys;
* provider credentials;
* internal service credentials.

Fail clearly when required configuration is unavailable.

Do not hardcode production API URLs.

---

# 8. DESIGN SYSTEM FOUNDATION

Create a coherent design-token layer.

Define tokens for:

* color;
* typography;
* spacing;
* radii;
* shadows;
* borders;
* z-index;
* breakpoints;
* motion durations;
* focus states;
* sizing.

The design system must support a video-centric interface with:

* dense content discovery;
* large media surfaces;
* channel identity;
* interactive controls;
* readable metadata;
* responsive navigation.

Do not copy proprietary YouTube visual assets or branding.

Use an independent visual identity appropriate to this project.

---

# 9. TYPOGRAPHY

Implement typography tokens and reusable text primitives.

Define:

* display;
* heading;
* body;
* metadata;
* caption;
* label;
* button text.

Ensure:

* readable line heights;
* responsive sizing;
* truncation behavior;
* accessible contrast;
* predictable wrapping.

Do not rely on arbitrary one-off font sizes scattered through components.

---

# 10. RESPONSIVE LAYOUT SYSTEM

Implement responsive layouts for:

* desktop;
* laptop;
* tablet;
* mobile.

Define breakpoints centrally.

The application shell must remain usable across viewport sizes.

Navigation must adapt without:

* horizontal overflow;
* clipped controls;
* inaccessible drawers;
* overlapping content.

Do not solve responsiveness by duplicating entire pages for each breakpoint unless technically justified.

---

# 11. GLOBAL APPLICATION SHELL

Implement:

* top navigation;
* primary content container;
* sidebar/drawer;
* responsive mobile navigation;
* content area;
* global feedback layers;
* account entry;
* notification entry point where applicable.

The shell must support later pages without requiring redesign.

Define consistent max-width and spacing behavior for content surfaces.

---

# 12. HEADER

Implement the global header.

It should provide, as appropriate:

* product identity;
* navigation trigger;
* search entry point;
* account entry;
* notification entry point;
* creator/action entry point.

Search itself is out of scope for this milestone, but the header must expose a reusable search-entry surface that a later milestone can connect.

Do not implement a fake search feature.

---

# 13. SIDEBAR AND NAVIGATION

Implement responsive navigation.

The navigation model should support destinations such as:

* Home;
* Subscriptions;
* History;
* Playlists;
* Watch Later or equivalent;
* channel/library access;
* creator entry;
* settings;
* sign-in state.

Not every destination requires full implementation in this milestone.

Routes without current-page implementation must use an explicit controlled boundary rather than fake functionality.

The navigation must correctly reflect authenticated versus anonymous state.

---

# 14. ROUTING ARCHITECTURE

Create route boundaries suitable for later growth.

Use public and protected route conventions.

Potential route areas include:

* `/`;
* `/login`;
* `/register`;
* `/channel/[handle]`;
* `/account`;
* `/watch/[videoId]`;
* `/search`;
* `/subscriptions`;
* `/history`;
* `/playlists`;
* `/studio`;
* `/live`;
* `/settings`.

Only implement the routes within this milestone.

Later routes may have explicit boundaries rather than placeholder pages pretending to be complete.

---

# 15. AUTHENTICATION STATE

Implement authentication-aware application state.

The frontend must distinguish:

* unknown/loading;
* authenticated;
* unauthenticated;
* session-expired;
* authentication-error.

Session state must be derived from the backend authentication contract.

Do not store authorization decisions as permanently trusted client state.

The backend remains the authority for:

* identity;
* session validity;
* permissions;
* resource ownership.

---

# 16. SESSION RESTORATION

Implement session restoration when the application starts.

Handle:

* existing valid session;
* expired session;
* revoked session;
* network failure;
* server error.

Do not flash an unauthenticated UI unnecessarily while a session is still being restored.

Avoid infinite refresh loops.

Session restoration must not leak tokens to analytics, logs, or URL parameters.

---

# 17. LOGIN

Implement a production login flow.

Support:

* email/credential input;
* validation;
* submission;
* loading state;
* authentication success;
* authentication failure;
* rate-limit response;
* server validation error;
* network failure;
* accessible error messaging.

Do not perform authentication entirely on the client.

The frontend must use the actual backend contract.

Do not create fake credentials or fake login success.

---

# 18. REGISTRATION

Implement account registration.

Support:

* required fields;
* client-side validation;
* backend validation;
* loading state;
* duplicate-account error;
* password requirements;
* success state;
* email-verification boundary.

Do not implement email delivery in this milestone.

Display server-provided verification state through the canonical account contract.

---

# 19. LOGOUT

Implement real logout.

The client must:

* call the backend logout/session-revocation mechanism where required;
* clear relevant client state;
* clear sensitive cached data;
* return to the appropriate public experience.

Do not merely delete a local flag while leaving a server-side session active.

---

# 20. PROTECTED ROUTES

Implement protected-route behavior.

Protected pages must:

* preserve intended destination safely;
* redirect unauthenticated users to login;
* avoid leaking protected data before authentication;
* handle session expiration;
* avoid redirect loops.

Do not protect routes only through visual hiding.

Server-side authorization remains authoritative.

---

# 21. PUBLIC ROUTES

Public routes must work without authentication where the backend contract allows anonymous access.

Examples include:

* home/discovery;
* public channel pages.

Private states must not become visible simply because a client knows a resource ID.

---

# 22. API CLIENT

Implement a shared typed API client.

The client must handle:

* base URL;
* request methods;
* authentication;
* headers;
* request ID/correlation information;
* serialization;
* response parsing;
* timeout;
* cancellation;
* retry policy where appropriate;
* error normalization.

Do not create raw `fetch` calls independently throughout components.

Centralize HTTP behavior.

---

# 23. API ERROR NORMALIZATION

Normalize backend errors into typed frontend errors.

Support categories such as:

* validation;
* unauthenticated;
* unauthorized;
* not found;
* conflict;
* rate limited;
* unavailable;
* network failure;
* unknown error.

Preserve backend request/correlation identifiers for troubleshooting without displaying them unnecessarily.

Do not expose stack traces.

---

# 24. REQUEST CANCELLATION AND RACE CONTROL

Use request cancellation where appropriate.

Handle:

* route changes;
* component unmount;
* repeated feed requests;
* query changes;
* aborted server requests.

Prevent stale responses from overwriting newer client state.

Do not use a global mutable request flag to manage concurrency.

Use the chosen data-fetching abstraction consistently.

---

# 25. SERVER-STATE FOUNDATION

Implement the application's server-state strategy.

Use the repository's selected query/data library if one already exists.

Define:

* query keys;
* stale time;
* cache behavior;
* invalidation;
* error states;
* refetch behavior.

Do not duplicate server data unnecessarily in multiple client stores.

Server state must remain synchronized with backend state.

---

# 26. CLIENT-STATE FOUNDATION

Use client state only for local UI/application state such as:

* navigation drawer state;
* modal state;
* theme preference;
* temporary form state;
* media interaction state where later required.

Do not copy complete backend entities into a global client store without justification.

---

# 27. LOADING STATES

Create reusable loading primitives.

Support:

* skeletons;
* inline loading;
* button loading;
* page-level loading;
* navigation loading;
* content placeholder.

Loading states must preserve layout dimensions where practical to reduce layout shift.

Do not show indefinite spinners for recoverable API failures.

---

# 28. ERROR STATES

Create reusable error states for:

* page failure;
* API failure;
* authentication failure;
* network failure;
* empty result;
* unavailable content.

Provide:

* human-readable explanation;
* retry action where appropriate;
* safe fallback;
* accessible announcement.

Do not expose internal errors to users.

---

# 29. EMPTY STATES

Create coherent empty-state patterns for:

* no subscriptions;
* no history;
* no playlists;
* no channel content;
* no personalized feed;
* no account data.

Only implement empty states relevant to current milestone screens.

Do not imply a feature is fully implemented when it is not part of this milestone.

---

# 30. ACCESSIBILITY FOUNDATION

The frontend must target WCAG-aligned accessible behavior.

At minimum implement:

* semantic HTML;
* keyboard navigation;
* visible focus;
* focus trapping in dialogs;
* accessible labels;
* button semantics;
* form labels;
* validation messaging;
* sufficient contrast;
* reduced-motion support;
* screen-reader-friendly state announcements.

Do not rely on color alone to convey state.

Do not use clickable `div` elements when semantic interactive elements are appropriate.

---

# 31. BUTTONS, INPUTS, AND FORM PRIMITIVES

Create reusable accessible primitives for:

* button;
* icon button;
* text input;
* password input;
* textarea;
* select where needed;
* checkbox;
* form field;
* form error;
* form label.

Define:

* disabled state;
* loading state;
* invalid state;
* focus state;
* hover state;
* keyboard behavior.

Use these primitives consistently across authentication and future application screens.

---

# 32. CARD AND MEDIA PRIMITIVES

Create reusable components for:

* video card;
* channel card;
* thumbnail;
* avatar;
* metadata row;
* duration badge;
* visibility/status badge.

Video cards should support:

* thumbnail;
* title;
* channel;
* view/time metadata;
* duration;
* optional live/status state;
* loading state.

Do not hardcode one page's layout assumptions into the reusable component.

---

# 33. IMAGE AND MEDIA DELIVERY

Create controlled image/media components.

They must support:

* responsive sizing;
* lazy loading;
* aspect-ratio preservation;
* fallback image;
* error state;
* accessibility.

Use the project's CDN/media contract.

Do not expose private storage credentials.

Do not construct provider-specific signed URLs directly inside presentational components.

---

# 34. HOME/DISCOVERY PAGE SHELL

Implement the main home/discovery page shell.

It should consume the actual discovery API contract.

Support:

* feed retrieval;
* video-card grid/list;
* responsive layout;
* loading;
* empty;
* error;
* retry.

Do not implement advanced client-side recommendation algorithms.

The backend remains responsible for discovery ordering.

---

# 35. HOME FEED INTERACTION

Implement:

* initial loading;
* cursor-based pagination/infinite loading;
* retry;
* refresh where appropriate;
* route navigation to accessible public content.

Do not request unbounded pages.

Prevent duplicate feed requests.

Prevent stale responses from corrupting feed ordering.

---

# 36. CHANNEL PAGE SHELL

Implement a public channel page shell.

Support:

* channel identity;
* avatar/banner;
* channel name;
* handle;
* description;
* subscription state where available;
* channel content;
* loading;
* error;
* empty content.

Use the canonical backend channel contract.

Do not implement full creator studio functionality.

---

# 37. CHANNEL SUBSCRIPTION UI BOUNDARY

Expose the subscription control needed on the channel page.

It must support:

* current subscription state;
* subscribe;
* unsubscribe;
* loading;
* error;
* optimistic behavior only if safe;
* rollback on failure.

Do not implement the entire subscription management center in this milestone.

The backend remains authoritative.

---

# 38. ACCOUNT ENTRY

Implement account UI entry points.

Support:

* authenticated user identity;
* profile/avatar display;
* account menu foundation;
* logout;
* account/settings navigation entry.

Do not expose sensitive account fields.

The account menu must be keyboard accessible.

---

# 39. NOTIFICATION ENTRY POINT

Create the notification entry component in the global application shell.

It may display:

* unread count;
* loading state;
* notification icon;
* navigation to notification center.

The full notification center is out of scope for this milestone.

The component must consume real unread-count data where the backend contract exists.

Do not fake notification counts.

---

# 40. THEME FOUNDATION

Implement the project's visual theme foundation.

Support:

* default/light appearance;
* dark appearance if configured by project requirements;
* system preference detection if supported;
* persistent user preference.

Do not duplicate theme logic throughout individual components.

Respect reduced-motion and accessibility preferences.

---

# 41. FRONTEND TELEMETRY

Implement frontend telemetry hooks.

Track appropriate non-sensitive events such as:

* page view;
* video-card impression where defined;
* channel-page view;
* search-entry interaction where supported;
* authentication success/failure categories;
* UI errors.

Do not send:

* passwords;
* access tokens;
* refresh tokens;
* private account data;
* raw sensitive API responses.

Use the backend analytics/event contract.

Do not create a second unrelated analytics schema.

---

# 42. ERROR BOUNDARIES

Implement React/Next.js error-boundary behavior for:

* route rendering failures;
* component failures;
* recoverable API failures.

Provide:

* safe error UI;
* retry/reload action;
* telemetry;
* correlation/reference information where safe.

Do not render stack traces to users.

---

# 43. PERFORMANCE REQUIREMENTS

Optimize the application foundation for:

* initial page load;
* server rendering;
* hydration;
* route transitions;
* image delivery;
* feed scrolling;
* layout stability.

Use:

* server components where appropriate;
* lazy loading;
* responsive images;
* bounded data fetching;
* route-level code splitting;
* caching;
* memoization only where justified.

Do not introduce client-side JavaScript merely for convenience.

---

# 44. SECURITY REQUIREMENTS

Protect against:

* XSS;
* token leakage;
* unsafe redirects;
* malicious query parameters;
* sensitive-data exposure;
* insecure client authorization assumptions.

Validate redirect destinations.

Do not place authentication tokens in URLs.

Do not render unsanitized user-generated HTML.

Treat video titles, channel names, descriptions, comments, and profile fields as untrusted content.

---

# 45. PRIVACY REQUIREMENTS

The frontend must:

* minimize stored personal data;
* avoid unnecessary local persistence;
* clear sensitive state on logout;
* avoid exposing private API responses through browser-visible shared caches;
* prevent private content from appearing in public UI states;
* avoid sending private user activity into generic telemetry.

Do not persist watch history or private recommendation context in an insecure global browser store.

---

# 46. RESPONSIVE ACCESSIBILITY

Verify:

## Mobile

* touch targets are sufficiently large;
* drawers can be opened/closed by keyboard-equivalent mechanisms;
* content does not overflow horizontally;
* cards remain readable.

## Tablet

* navigation remains usable;
* content density adapts.

## Desktop

* sidebar and content layout are coherent;
* keyboard navigation works;
* focus remains visible.

Do not create separate markup trees for each viewport unless there is a real accessibility or interaction reason.

---

# 47. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* API error normalization;
* auth-state transitions;
* route-protection logic;
* UI utility functions;
* pagination helpers;
* state transformations.

## Component Tests

Test:

* buttons;
* inputs;
* dialogs;
* navigation;
* video cards;
* channel cards;
* loading states;
* error states;
* subscription control;
* account menu.

## Integration Tests

Test:

* login;
* registration;
* logout;
* session restoration;
* home-feed retrieval;
* channel retrieval;
* subscription interaction;
* API error states.

## Accessibility Tests

Test:

* keyboard navigation;
* form labels;
* focus management;
* dialog behavior;
* accessible names;
* major color/contrast rules where tooling supports them.

## End-to-End Tests

Create bounded E2E coverage for:

* anonymous home;
* registration;
* login;
* protected-route redirect;
* logout;
* public channel navigation;
* authenticated subscription interaction.

Do not create E2E tests for out-of-scope pages.

---

# 48. API CONTRACT VALIDATION

The frontend must consume the actual backend contracts.

Verify:

* response schemas;
* error codes;
* authentication behavior;
* pagination;
* subscription state;
* visibility;
* channel data.

Do not silently create frontend-specific API fields that the backend does not provide.

If generated API types are available, use them.

If not, create explicit typed client models that mirror the authoritative contract.

---

# 49. DOCUMENTATION

Document:

* local web setup;
* environment variables;
* route structure;
* API client usage;
* authentication/session architecture;
* design-system organization;
* responsive breakpoints;
* accessibility conventions;
* testing;
* telemetry;
* error handling.

Documentation must describe the actual implementation.

Do not claim that future routes are implemented.

---

# 50. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement in this milestone:

* full watch page;
* production video player;
* comments UI;
* playlists UI;
* search results;
* search autocomplete;
* creator studio;
* video upload UI;
* live-stream studio;
* live chat UI;
* monetization UI;
* moderation UI;
* administration UI;
* complete notification center;
* advanced feed personalization controls.

The application shell may contain navigation entry points for these capabilities.

Those entry points must not pretend the functionality is already implemented.

---

# 51. VALIDATION REQUIREMENTS

Before completion, verify:

## Application Foundation

* application starts;
* production build succeeds;
* environment validation works;
* route boundaries work;
* error boundaries work.

## Authentication

* login works against the real backend;
* registration works;
* session restoration works;
* logout works;
* protected routes work;
* session expiration is handled safely.

## UI Foundation

* design tokens are consistent;
* shared primitives are accessible;
* responsive behavior works;
* keyboard navigation works.

## Home

* feed loads from the backend;
* pagination works;
* empty/error/loading states work;
* no duplicate requests occur.

## Channel

* channel data renders;
* visibility is respected;
* subscription state is correct;
* mutations handle errors.

## Security

* tokens are not leaked;
* redirect validation works;
* untrusted text is safely rendered;
* protected data is not exposed before authentication.

## Performance

* major shell routes render efficiently;
* images are optimized;
* unnecessary client JavaScript is avoided.

---

# 52. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Next.js foundation is functional.
3. Global layout is implemented.
4. Responsive navigation is implemented.
5. Header is implemented.
6. Sidebar/drawer behavior is implemented.
7. Design tokens are implemented.
8. Shared UI primitives are implemented.
9. Authentication state is implemented.
10. Login is implemented.
11. Registration is implemented.
12. Session restoration is implemented.
13. Logout is implemented.
14. Protected routing is implemented.
15. Public routing is implemented.
16. Typed API client is implemented.
17. Error normalization is implemented.
18. Server-state strategy is implemented.
19. Loading/error/empty states are implemented.
20. Home/discovery shell is implemented.
21. Video cards are implemented.
22. Channel cards are implemented.
23. Channel-page shell is implemented.
24. Subscription control is implemented.
25. Account entry is implemented.
26. Notification entry point is implemented where supported by the backend contract.
27. Theme foundation is implemented.
28. Accessibility foundation is implemented.
29. Frontend telemetry hooks are implemented.
30. Error boundaries are implemented.
31. Performance foundations are implemented.
32. Security requirements are implemented.
33. Privacy requirements are implemented.
34. Unit tests are implemented.
35. Component tests are implemented.
36. Integration tests are implemented.
37. Accessibility tests are implemented.
38. Bounded E2E tests are implemented.
39. API-contract compatibility is validated.
40. Documentation is updated.
41. No fake backend responses are used as production functionality.
42. No hardcoded credentials or secrets exist.
43. No intentional TODO/FIXME gap substitutes for current-scope functionality.
44. Known limitations are reported honestly.

---

# 53. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Application Foundation

Summarize:

* routing;
* layouts;
* responsive shell;
* design system.

## Authentication

Summarize:

* login;
* registration;
* session restoration;
* logout;
* protected routes.

## Home and Channels

Summarize:

* discovery shell;
* cards;
* channel page;
* subscription control.

## API/Data Layer

Summarize:

* API client;
* error normalization;
* server state;
* caching.

## Accessibility and Security

Summarize implemented protections.

## Tests

List:

* unit;
* component;
* integration;
* accessibility;
* E2E tests.

## Documentation

List documentation created or updated.

## Known Limitations

List functionality intentionally deferred to later frontend milestones.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim that out-of-scope pages or features were implemented.

# 54. FINAL EXECUTION RULE

Implement only the web-frontend foundation, authentication, application shell, shared UI system, home/discovery shell, channel shell, and supporting functionality defined by this milestone.

Do not implement unrelated future web features.

Do not redesign established backend/API contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not use fake APIs, fake authentication, placeholder pages presented as completed features, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, accessible, secure, responsive, observable frontend functionality within this milestone's scope.
