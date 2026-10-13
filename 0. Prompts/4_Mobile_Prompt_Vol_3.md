# YouTube-Style Video Platform — Mobile Prompt — Volume 3

## 1. Prompt Identity

You are the senior React Native/mobile engineer responsible for implementing the **native search, autocomplete, discovery, personalized home feed, subscription feed, and content-browsing experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone for iOS and Android.

Your responsibility is the mobile frontend for:

- search;
- search autocomplete;
- search results;
- video and channel discovery;
- search filtering and sorting;
- personalized home feed;
- recommended content presentation;
- subscription feed;
- short-form discovery entry points;
- pagination and refresh;
- search and discovery state management;
- analytics and telemetry;
- accessibility;
- performance;
- automated testing;
- documentation.

Do not implement unrelated mobile domains.

Do not implement search indexing, recommendation-ranking algorithms, or backend discovery services.

Do not fabricate search results, recommendations, subscription feeds, or API responses.

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
- web and native mobile clients.

The mobile technology direction is:

- React Native;
- TypeScript;
- iOS and Android;
- the existing navigation and state-management architecture;
- typed API clients;
- secure authentication/session integration;
- native accessibility;
- production-quality testing;
- privacy-conscious analytics.

The mobile application must use the same canonical video, channel, identity, and discovery contracts as the rest of the platform.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- previous mobile prompts;
- hidden architectural decisions;
- undocumented API endpoints;
- generated files that are unavailable in the current environment;
- a repository shared with another AI conversation.

If a repository is available, inspect it before modifying it.

If portable architecture, API, authentication, search, discovery, or analytics contracts are supplied, use them as authoritative.

If the repository contains compatible implementations, preserve and extend them rather than creating duplicate navigation, API, state, or domain-model infrastructure.

Do not infer that a backend capability exists merely because it is part of the product vision.

---

# 4. Primary Objective

Implement the native search and discovery experience so viewers can:

1. search for videos and channels;
2. receive autocomplete suggestions;
3. submit and revise queries;
4. browse search results;
5. filter and sort results where supported;
6. load additional results;
7. navigate to videos and channels;
8. browse personalized home content;
9. open a subscription feed;
10. discover short-form videos through supported entry points;
11. refresh discovery content;
12. recover from search and discovery errors;
13. use public discovery without authentication where supported;
14. receive viewer-specific results without account-data leakage;
15. use accessible native navigation and input controls;
16. navigate reliably despite network interruptions;
17. generate appropriate analytics without exposing sensitive data.

---

# 5. Explicit Scope

Implement:

- mobile search entry point;
- search screen;
- search query input;
- autocomplete;
- query submission and normalization;
- query-state and navigation handling;
- search result lists;
- video result cards;
- channel result cards;
- supported result filters;
- supported result sorting;
- cursor-based pagination;
- personalized home feed;
- discovery-section presentation;
- video and channel browsing;
- subscription feed;
- subscription-feed authentication states;
- short-form discovery entry points;
- refresh and retry behavior;
- server-state caching;
- viewer-specific cache isolation;
- request cancellation and stale-response protection;
- connectivity-aware behavior;
- accessibility;
- performance;
- analytics and telemetry;
- automated tests;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- backend search APIs;
- search indexing infrastructure;
- recommendation algorithms;
- machine-learning pipelines;
- backend feed generation;
- native video playback internals;
- short-form swipe/player functionality;
- comments and replies;
- playlist management;
- notification center;
- creator studio;
- live-stream management;
- paid memberships and checkout;
- moderation tools;
- backend analytics aggregation;
- infrastructure provisioning.

Integrate with these domains only through existing, explicitly defined contracts.

Do not create fake production screens to make unsupported capabilities appear implemented.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. locate the React Native application;
3. inspect navigation and screen conventions;
4. inspect the existing API client;
5. inspect authentication and session handling;
6. inspect current server-state management;
7. inspect the canonical video and channel models;
8. inspect existing video/channel cards;
9. inspect the current home/discovery screen;
10. inspect search and subscription-feed APIs where available;
11. inspect cache-key and invalidation conventions;
12. inspect connectivity handling;
13. inspect analytics and telemetry;
14. inspect reusable form/input components;
15. inspect automated tests.

Reuse compatible code and libraries.

Do not create a competing search architecture, API client, navigation system, authentication store, or global state-management framework.

---

# 8. Navigation and Route Architecture

Implement search and discovery routes through the established mobile navigation architecture.

The navigation model must support:

- Home;
- Search;
- Search Results;
- Subscriptions;
- video destinations;
- channel destinations;
- short-form discovery entry points supported by the application.

The fully implemented scope is limited to the search and discovery capabilities defined here.

For destinations implemented by other parts of the application, integrate with their canonical navigation routes rather than recreating those domains.

For destinations that are not yet implemented, do not create fake completed screens.

Support expected native navigation behavior, including back navigation, tab switching where applicable, and preservation of appropriate search state.

---

# 9. Canonical Search Route State

The mobile application must represent durable search state consistently.

Use route parameters or the established navigation-state convention for supported values such as:

```text
query
filters
sort
```

The exact parameter names and serialization rules must follow the project architecture.

Do not place transient UI state into durable navigation parameters unnecessarily.

Do not put credentials, private history, internal provider details, or sensitive viewer identifiers into URLs.

The search screen must remain recoverable when restored through navigation state or a supported deep link.

---

# 10. Search Screen

Implement a native search screen containing:

- accessible search input;
- submit action;
- clear action;
- autocomplete surface;
- recent-search suggestions where supported;
- initial/empty guidance;
- result navigation;
- loading and error states.

The screen must behave correctly on both iOS and Android.

Account for:

- native keyboard appearance;
- safe areas;
- text selection;
- input focus;
- keyboard submit actions;
- screen navigation;
- accessibility text scaling.

Do not let the keyboard obscure essential search controls.

---

# 11. Search Input Behavior

The search input must support:

- text entry;
- explicit submission;
- clear/reset;
- autocomplete;
- focus control;
- keyboard submission;
- validation;
- cancellation of stale requests.

Distinguish between:

- text currently being edited;
- the submitted query;
- the active autocomplete query;
- the current result query.

Do not issue a full search request for every keystroke.

Autocomplete and submitted search are separate operations with separate request lifecycles.

---

# 12. Query Normalization

Normalize search queries consistently with the backend's search semantics.

Handle:

- empty strings;
- leading/trailing whitespace;
- repeated whitespace where appropriate;
- Unicode text;
- special characters;
- URL or navigation encoding;
- maximum query length where defined.

Do not remove meaningful punctuation or characters without a contract-based reason.

Do not implement a browser/mobile-only normalization algorithm that changes the meaning of searches relative to the web client.

---

# 13. Autocomplete

Implement autocomplete through the canonical search API.

Support:

- debounced requests;
- suggestion lists;
- loading;
- no suggestions;
- request failure;
- cancellation;
- keyboard and touch selection;
- focus management;
- stale-response protection.

Do not issue an unbounded request for every character entered.

Cancel or ignore obsolete requests when the query changes.

A delayed response for an older query must never replace newer suggestions.

---

# 14. Autocomplete Contract

Consume the project's typed autocomplete contract.

A conceptual suggestion may contain:

```text
type
text
entityId
thumbnail
channelName
metadata
```

Use the exact contract fields where available.

Support suggestion categories such as query, video, channel, or playlist only when they are defined by the backend.

Do not assume every suggestion represents a video.

Do not fabricate unavailable suggestions.

---

# 15. Suggestion Navigation

When a viewer selects a suggestion:

- follow the canonical navigation behavior for its type;
- submit a search when the suggestion represents a query;
- open the appropriate video/channel destination where supported;
- dismiss the autocomplete surface;
- cancel obsolete requests;
- preserve predictable back navigation.

Do not construct backend URLs directly from suggestion labels.

Use canonical entity IDs and the application's established route helpers.

---

# 16. Recent Search Behavior

If authenticated or anonymous recent-search functionality exists, integrate through the project's explicit contract or approved local behavior.

Distinguish between:

- server-side authenticated history;
- local recent-query preferences;
- autocomplete suggestions.

Do not confuse autocomplete with persisted search history.

If query history is stored locally, use only the approved persistence mechanism and retention policy.

Do not persist sensitive queries indefinitely without a product requirement.

---

# 17. Search Results

Implement native search results using real contract-backed data.

Support relevant result types:

- video;
- channel;
- playlist where provided by the backend.

Use appropriate result-card presentations for each type.

Video results may contain:

```text
videoId
title
thumbnail
duration
channel
viewCount
publishedAt
availability
```

Channel results may contain:

```text
channelId
name
avatar
description
subscriberCount
verificationState
```

These are conceptual examples. The authoritative project contract determines the actual fields.

Do not use hardcoded production result arrays.

---

# 18. Video Result Cards

Implement reusable mobile video-result cards.

Display supported metadata such as:

- thumbnail;
- title;
- channel name;
- duration;
- view count;
- publication information;
- relevant availability/live/short-form indicators.

Requirements:

- stable navigation;
- accessible title and action labels;
- correct image aspect ratio;
- placeholder/loading behavior;
- missing-field handling;
- appropriate press feedback;
- efficient list rendering.

Do not assume that every video has every optional field.

---

# 19. Channel Result Cards

Implement reusable channel-result cards.

Where supported, display:

- channel avatar;
- name;
- verification indicator;
- subscriber count;
- description;
- subscription state or action where appropriate.

Navigate through the canonical channel route.

Use the shared subscription contract if subscription actions are available.

Do not implement a separate mobile-only subscription model.

---

# 20. Result Filters

Implement filters only when provided by the backend contract.

Potential filters may include:

- content type;
- upload date;
- duration;
- live;
- short-form;
- channel or other supported attributes.

The frontend must send canonical filter identifiers and values.

Do not implement client-side filtering over only the currently loaded page when the intended search covers the entire server-side result set.

Filter selection must trigger the appropriate search request.

---

# 21. Result Sorting

Implement supported search sorting.

Possible modes may include:

- relevance;
- date;
- views;
- other backend-defined orderings.

Only expose sorting modes that exist in the authoritative contract.

When the sort changes:

- update search state;
- reset pagination appropriately;
- cancel obsolete requests;
- clear incompatible cached pages;
- load the correct result set.

Do not invent ranking behavior on the client.

---

# 22. Search Pagination

Implement cursor pagination where provided by the backend.

Support:

- initial results;
- next-page loading;
- end-of-results;
- retry;
- duplicate prevention;
- request cancellation;
- stale-response protection.

Do not request every result at once.

Do not request the same cursor concurrently.

Do not append results returned for an outdated query to the active result list.

Use stable canonical IDs for deduplication where required.

---

# 23. Native List Performance

Use an appropriate React Native list implementation for the result volume and repository architecture.

Optimize:

- stable keys;
- item rendering;
- image loading;
- pagination triggers;
- scroll performance;
- state updates;
- retained component count.

Avoid rendering arbitrarily large collections using unbounded nested views.

Do not introduce complex virtualization merely for small lists when it does not provide a real benefit.

If a virtualized list is used, preserve:

- predictable scroll behavior;
- accessibility;
- pagination correctness;
- focus/selection behavior;
- appropriate item identity.

---

# 24. Search Loading and Failure States

Implement explicit states for:

- initial screen;
- autocomplete loading;
- search loading;
- pagination loading;
- no results;
- network error;
- authorization failure;
- rate limit;
- temporary backend failure.

Distinguish a legitimate empty result from a failed request.

Do not clear all useful results before a refresh succeeds unless that is the established product behavior.

Offer retry actions where they are safe and meaningful.

---

# 25. Search Cache Strategy

Use the project's established server-state/cache library.

Cache keys must account for:

- normalized query;
- filters;
- sort;
- pagination cursor where appropriate;
- authenticated viewer context when results are personalized.

Do not share personalized results between accounts.

Do not cache viewer-specific queries under a generic key.

Use sensible cache lifetimes for autocomplete and search results.

Invalidate or refetch state when the query, filters, sort, or relevant authentication context changes.

---

# 26. Personalized Home Feed

Implement the mobile home feed using the canonical discovery contract.

The feed may contain backend-defined sections, such as:

- recommended videos;
- continue watching;
- trending content;
- topical sections;
- short-form entry points;
- other supported discovery surfaces.

Only render sections actually supplied or defined by the project.

Do not hardcode a predetermined feed of videos.

Do not create recommendation candidates in the mobile client.

The backend remains responsible for candidate generation, ranking, eligibility, and personalization.

---

# 27. Discovery Section Contract

Consume the canonical discovery response.

A conceptual section may include:

```text
sectionId
title
presentationType
items
nextCursor
hasMore
```

Use the actual project contract.

Sections may use different supported presentations, such as horizontal rows or vertical lists.

The UI must preserve backend-defined ordering unless the product contract explicitly specifies client-side grouping.

Do not change item order to simulate personalized ranking.

---

# 28. Home Feed Presentation

Implement a maintainable native home-feed layout.

Requirements:

- section headings where supplied;
- reusable video/channel cards;
- appropriate list orientation;
- efficient thumbnail rendering;
- localized loading states;
- empty section behavior;
- section-level failure handling where the data contract supports it.

Do not put all home-feed behavior into a monolithic screen component.

Do not make one nonessential discovery section failure take down the entire home feed.

---

# 29. Home Feed Refresh

Implement pull-to-refresh or the established native refresh interaction.

The refresh must:

- request data through the canonical discovery contract;
- show an appropriate refreshing state;
- avoid duplicate requests;
- reconcile the returned result;
- handle failure;
- preserve existing useful content if refresh fails.

Do not show fresh content when the response was not successfully received.

Do not reset pagination in an inconsistent way when refreshing.

---

# 30. Discovery Pagination and Preloading

Implement incremental discovery loading where the backend contract supports it.

Support:

- initial loading;
- load-more behavior;
- terminal state;
- transient failure;
- retry;
- duplicate prevention.

Where limited preloading is useful, keep it bounded.

Do not download the entire personalized feed eagerly.

Do not introduce aggressive media preloading in this milestone.

The separate native watch and short-form player implementations remain responsible for media playback and playback-specific resource policies.

---

# 31. Subscription Feed

Implement the mobile subscription feed for authenticated viewers.

The feed must display contract-provided content from channels the viewer follows.

Support:

- initial load;
- pagination;
- refresh;
- loading;
- error;
- empty state;
- navigation to videos/channels;
- appropriate ordering as defined by the backend.

Do not assume the backend feed is chronological unless the contract guarantees it.

Do not generate subscription-feed items locally.

---

# 32. Subscription Feed Authentication

The subscription feed must correctly distinguish:

- authenticated viewer;
- unauthenticated viewer;
- session initializing;
- expired session;
- unauthorized response.

For anonymous viewers, present a clear sign-in entry point according to the product design.

Do not break the public home feed because subscription data is unavailable.

Do not redirect all discovery browsing to authentication merely because a personalized feed requires an account.

---

# 33. Subscription Feed Data Contract

Use the canonical feed contract, which may conceptually contain:

```text
items
nextCursor
hasMore
generatedAt
```

Follow the actual response structure.

Do not invent publication order, personalized ranking, or missing metadata.

Respect the backend's content visibility and authorization rules.

---

# 34. Short-Form Discovery Entry Points

Expose the short-form discovery entry points supported by the platform.

This may include:

- a home-feed section;
- a navigation destination;
- a short-form video card;
- an explicit route into the native short-form experience.

This milestone only provides discovery and navigation integration.

Do not implement the complete vertical short-form playback engine or gesture-based feed.

Use the canonical short-form route and video ID when the destination is available.

Do not present an unsupported destination as a functioning feature.

---

# 35. Navigation to Video and Channel Screens

Video selection must navigate using the canonical video identity and established native watch route.

Channel selection must navigate using the canonical channel identity.

The navigation integration must:

- avoid passing full private entities unnecessarily;
- avoid storing signed media URLs in route parameters;
- allow destination screens to retrieve authoritative data;
- support back navigation;
- avoid repeated navigation from duplicate touch events.

Do not create alternate mobile-only route formats that conflict with the project's navigation architecture.

---

# 36. Authentication and Personalization

Public search and public discovery must remain available to anonymous users where supported.

Personalized results must use the canonical authenticated request context.

When the viewer signs in or out:

- invalidate relevant personalized queries;
- clear viewer-specific feed state;
- refresh the appropriate discovery data;
- avoid displaying the previous viewer's feed under the new session.

Do not fabricate personalized results when authentication is absent.

Use an anonymous discovery mode only if the backend explicitly supports it.

---

# 37. Connectivity and Offline Behavior

Integrate with the existing network-connectivity mechanism.

The application must distinguish:

- offline state;
- request failure;
- temporary backend outage;
- connectivity restored.

When offline:

- preserve usable navigation;
- retain previously fetched public data only as permitted by the cache policy;
- make stale status clear where appropriate;
- avoid repeated network retry loops.

Connectivity alone does not prove that a backend is reachable.

Do not claim that search or personalized discovery works offline unless that capability has actually been implemented.

---

# 38. Cancellation and Stale Responses

Protect all asynchronous search/discovery operations against stale results.

Examples:

```text
Query A begins
Query B begins
Query B completes
Query A completes later
```

Only the active query may control the visible results.

Apply the same principle to:

- autocomplete;
- query submission;
- filter changes;
- sort changes;
- pagination;
- home-feed refresh;
- subscription-feed refresh;
- authentication changes.

Use request cancellation, query identity, generation IDs, or equivalent mechanisms.

---

# 39. API Error Normalization

Use the project's established error model.

The mobile UI must distinguish relevant categories, including:

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

Follow the actual backend error codes when supplied.

Do not expose internal stack traces or raw server exceptions.

Do not blindly retry requests that are not safe to repeat.

---

# 40. Accessibility

Implement native accessibility for search and discovery.

Requirements include:

- accessible search input;
- understandable autocomplete suggestions;
- screen-reader labels for cards;
- semantic buttons;
- correct accessibility roles;
- focus/keyboard behavior where supported;
- sufficient touch targets;
- accessible filter and sort controls;
- accessible empty/error states;
- text scaling;
- usable native navigation.

When search results update, communicate the state through appropriate accessibility mechanisms without repeatedly disrupting the viewer.

Do not rely exclusively on icons or color to explain actions.

---

# 41. Responsive and Platform Behavior

Support the native iOS and Android application layouts.

Account for:

- safe areas;
- keyboard visibility;
- status/navigation bars;
- platform-native back behavior;
- differing text rendering;
- accessibility text scaling;
- dynamic device dimensions.

Use the established design system.

Do not duplicate the entire search implementation separately for iOS and Android without a real platform-specific requirement.

---

# 42. Performance

Optimize for:

- search-input responsiveness;
- autocomplete latency;
- result-list scrolling;
- home-feed rendering;
- thumbnail loading;
- pagination;
- cache reuse;
- query cancellation;
- memory retention.

Use stable keys.

Avoid rerendering every result card on each keystroke.

Do not fetch unnecessary feed sections before they are needed unless the backend contract or architecture requires them.

Do not issue aggressive polling requests.

---

# 43. Privacy and Security

The implementation must:

- use secure session integration;
- respect server authorization;
- avoid logging tokens;
- avoid storing credentials in ordinary preferences;
- treat search queries as potentially sensitive;
- protect personalized content;
- avoid viewer-data leakage through caches;
- validate navigation destinations;
- avoid rendering untrusted server-provided text unsafely;
- exclude sensitive information from telemetry.

Do not make frontend authorization checks the authoritative access-control boundary.

Do not include raw search history in analytics unless explicitly permitted by the project privacy contract.

---

# 44. Telemetry and Analytics

Implement appropriate search and discovery telemetry using the project's canonical analytics contract.

Potential events may include:

```text
mobile_search_opened
mobile_search_submitted
mobile_search_suggestion_selected
mobile_search_results_viewed
mobile_search_result_clicked
mobile_search_filter_changed
mobile_search_sort_changed
mobile_search_pagination_loaded
mobile_search_no_results
mobile_home_discovery_viewed
mobile_discovery_section_viewed
mobile_discovery_item_clicked
mobile_subscription_feed_opened
mobile_subscription_feed_item_clicked
mobile_short_form_entry_opened
```

Use canonical event names where supplied.

Prevent duplicate events caused by component remounts, retries, and cache revalidation.

Do not transmit:

- passwords;
- access tokens;
- refresh tokens;
- private account data;
- raw search history;
- unnecessary personal identifiers.

Do not instrument every render as a user action.

---

# 45. Testing Strategy

Implement automated tests for actual behavior.

### Unit tests

Cover:

- query normalization;
- search query serialization;
- autocomplete debouncing;
- stale-request protection;
- filter serialization;
- sort serialization;
- pagination;
- result deduplication;
- viewer-aware cache-key generation;
- account-switch invalidation;
- discovery telemetry construction.

### Component tests

Cover:

- search input;
- autocomplete list;
- keyboard submission behavior where supported;
- video result card;
- channel result card;
- filter controls;
- sort controls;
- loading/error/empty states;
- home-feed sections;
- subscription-feed presentation;
- refresh controls.

### Integration tests

Cover:

- opening search;
- submitting a query;
- selecting autocomplete;
- loading search results;
- changing filters;
- changing sort;
- loading additional results;
- refreshing home discovery;
- loading personalized discovery;
- loading subscription feed;
- authentication transitions;
- cache invalidation;
- cancellation of stale requests;
- offline and recovery behavior.

### End-to-end tests

At minimum:

1. open the home feed;
2. load contract-backed discovery data;
3. open the search screen;
4. submit a query;
5. inspect the result list;
6. select a result;
7. return to the search screen;
8. use autocomplete;
9. change a supported filter;
10. change a supported sort order;
11. load additional results;
12. handle an empty result set;
13. recover from a search failure;
14. refresh the home feed;
15. open the subscription feed;
16. verify unauthenticated subscription-feed behavior;
17. verify public discovery remains usable anonymously;
18. verify account switching clears personalized state;
19. verify a stale query cannot overwrite a newer query;
20. verify accessibility labels on essential controls.

Use controlled mocks for isolated tests only. Production code must use the real project integration interfaces.

---

# 46. iOS and Android Compatibility

Validate the supported iOS and Android environments.

Pay particular attention to:

- native keyboard interaction;
- safe-area layout;
- list performance;
- pull-to-refresh;
- search submission;
- navigation restoration;
- accessibility;
- request cancellation;
- app background/foreground behavior.

Do not assume validation on one platform proves correctness on the other.

Use platform-specific code only when required by a genuine native behavior.

---

# 47. Dependency Discipline

Before introducing dependencies:

- inspect the installed libraries;
- verify React Native compatibility;
- verify iOS and Android support;
- consider native setup requirements;
- avoid duplicate list, form, navigation, and state-management libraries.

Do not add a web-only search library to the native application unless it explicitly supports the project's mobile environment.

Do not introduce a second analytics or API framework without a documented reason.

---

# 48. Documentation

Update documentation describing:

- search and discovery architecture;
- search API integration;
- autocomplete behavior;
- URL/navigation state;
- filters and sorting;
- pagination;
- home-feed sections;
- personalized discovery;
- subscription-feed integration;
- viewer-specific cache isolation;
- cancellation and stale-response protection;
- offline behavior;
- telemetry and privacy;
- accessibility;
- testing and debugging.

Documentation must accurately reflect the actual implementation.

---

# 49. No Fake Search or Discovery

Do not create:

- hardcoded search results;
- fake autocomplete suggestions;
- fake personalized recommendations;
- static subscription feeds presented as real data;
- fabricated subscriber relationships;
- simulated search persistence;
- fake pagination;
- fake backend success responses in production paths.

Mocks are allowed only in controlled automated tests.

The actual application must use real contracts and backend integrations.

---

# 50. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- empty search handlers;
- fake filter controls;
- nonfunctional result cards;
- placeholder feed items;
- unsupported sorting behavior;
- fake subscription-feed persistence;
- incomplete loading/error handling;
- unimplemented actions that appear functional.

Everything within the current scope must be genuinely implemented.

Features outside this milestone must remain explicit integration boundaries, not fake implementations.

---

# 51. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- native build where available;
- search routing and submission;
- autocomplete;
- result rendering;
- filters and sorting;
- pagination;
- request cancellation;
- home-feed loading;
- refresh behavior;
- subscription feed;
- authenticated and anonymous behavior;
- account-specific cache isolation;
- offline and recovery behavior;
- responsive/native layouts;
- accessibility-critical interactions;
- privacy/security requirements.

Fix issues discovered within this scope.

Do not claim that a native build, external API, or backend capability has been validated unless the check actually ran.

If a platform toolchain is unavailable, state the exact blocker in the completion report and finish all validation that can be performed locally.

---

# 52. Definition of Done

This prompt is complete only when:

- native search works;
- query state is handled consistently;
- autocomplete uses real contracts;
- stale autocomplete results are prevented;
- video and channel search results render correctly;
- filters work where supported;
- sorting works where supported;
- pagination works;
- refresh works;
- search failures and empty states are distinct;
- home discovery uses real backend data;
- discovery sections render according to the canonical contract;
- recommendation ranking remains backend-owned;
- subscription feed works where supported;
- unauthenticated behavior is correct;
- public discovery remains available anonymously where supported;
- short-form entry points integrate with the canonical destination where available;
- navigation between search, video, and channel screens is consistent;
- viewer-specific caches are isolated;
- account switching does not leak data;
- stale responses cannot overwrite newer state;
- connectivity failures are handled appropriately;
- telemetry is implemented without exposing prohibited sensitive information;
- accessibility requirements are implemented;
- native iOS/Android behavior is validated to the extent possible;
- tests cover the defined functionality;
- documentation is updated;
- no fake production functionality remains;
- no current-scope placeholders remain;
- validation passes.

---

# 53. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize native search, autocomplete, search results, personalized discovery, subscription feed, and short-form discovery entry points actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List search, autocomplete, video, channel, discovery, subscription-feed, pagination, and analytics contracts consumed.

### State and Caching

Summarize query-state handling, server-state management, viewer-specific cache isolation, pagination, cancellation, and account-switch behavior.

### Testing

List tests created and tests executed.

### Validation

Report TypeScript, linting, native builds, and runtime checks actually performed for iOS and Android.

### Integration Notes

Identify missing backend contracts, external configuration requirements, platform-toolchain limitations, or other dependencies.

### Out of Scope

Confirm that search indexing, recommendation algorithms, native playback internals, comments, playlist management, notifications, creator studio, live streaming, monetization, moderation, and backend services were not improperly implemented.

---

# 54. Final Execution Directive

Execute this prompt as a concrete native mobile implementation task.

Do not merely describe search and discovery.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate search results, recommendation data, subscription feeds, or API behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated mobile or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style native mobile search, discovery, personalized home feed, and subscription-feed experience for iOS and Android**, integrated with the project's canonical backend contracts.
