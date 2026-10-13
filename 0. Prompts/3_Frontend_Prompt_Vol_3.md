# YouTube-Style Video Platform — Frontend Prompt — Volume 3

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **search, discovery, subscription-feed, browsing, and recommendation-driven content discovery experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

* search;
* search results;
* autocomplete;
* filtering and sorting;
* channel discovery;
* subscription feed;
* personalized discovery surfaces;
* related browsing surfaces;
* short-form discovery entry points where applicable;
* pagination/infinite loading;
* search state synchronization;
* discovery error and fallback behavior;
* analytics;
* accessibility;
* responsive behavior;
* performance;
* automated testing.

Do not implement unrelated frontend domains.

Do not implement backend search or recommendation infrastructure.

Do not fabricate backend responses.

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
* search;
* personalized discovery;
* recommendations;
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
* production state management;
* server/client state separation;
* accessibility;
* observability;
* automated testing.

The platform is designed for very large consumer traffic and must remain compatible with high-volume search and discovery workloads.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

* a previous AI response;
* another Claude conversation;
* another frontend prompt;
* hidden project decisions;
* undocumented backend endpoints;
* hidden generated files.

If a repository is available, inspect it first.

If portable architecture or API artifacts are available, use them as authoritative contracts.

If such artifacts are not available, follow the explicit contracts and invariants defined here while preserving any compatible implementation already present in the repository.

Do not infer that functionality is implemented merely because it is described as part of the completed product.

Inspect the repository to determine actual implementation state.

---

# 4. Primary Objective

Implement the production web discovery experience.

The finished scope must allow a viewer to:

1. search for videos;
2. search for channels;
3. receive autocomplete suggestions;
4. submit searches;
5. browse search results;
6. filter results;
7. sort results where supported;
8. paginate or continuously load additional results;
9. navigate to videos;
10. navigate to channels;
11. view subscription-driven content;
12. browse personalized discovery surfaces;
13. view recommended content candidates;
14. discover short-form content where supported;
15. recover from search/discovery failures;
16. preserve search state across navigation where appropriate;
17. use the experience anonymously where possible;
18. receive authenticated personalization where available;
19. interact with accessible responsive UI;
20. generate appropriate discovery/search telemetry.

---

# 5. Explicit Scope

Implement:

* search route;
* search input;
* search submission;
* query-state handling;
* autocomplete;
* recent-query behavior where supported;
* search results;
* video result cards;
* channel result cards;
* result filters;
* sorting;
* pagination/cursor loading;
* search loading/error/empty states;
* subscription-feed page;
* personalized home/discovery sections required by this scope;
* recommendation result presentation;
* short-form discovery entry point;
* discovery caching/state management;
* URL synchronization;
* analytics/telemetry;
* accessibility;
* responsive behavior;
* performance optimization;
* testing;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* search indexing infrastructure;
* OpenSearch/Elasticsearch infrastructure;
* recommendation ranking algorithms;
* candidate-generation backend services;
* machine-learning pipelines;
* backend subscription logic;
* backend recommendation APIs;
* backend search APIs;
* video processing;
* playback infrastructure;
* creator studio;
* live-stream control plane;
* payment systems;
* moderation backend;
* mobile applications;
* administrative dashboards.

Use the existing or defined backend contracts.

Do not create fake backend implementations to compensate for missing server functionality.

---

# 7. Repository Inspection

Before changing code:

1. inspect the repository structure;
2. identify the frontend application;
3. inspect package manager and scripts;
4. inspect Next.js routing;
5. inspect the existing component/design system;
6. inspect typed API integration;
7. inspect authentication/session handling;
8. inspect existing video/channel card components;
9. inspect existing home/discovery components;
10. inspect caching and state-management patterns;
11. inspect analytics/telemetry;
12. inspect existing test infrastructure.

Reuse compatible components and infrastructure.

Do not create duplicate implementations of existing shared primitives.

---

# 8. Search Route

Implement a canonical search experience.

A supported route should be equivalent to:

```text
/results?search_query={query}
```

If the project's routing convention uses another canonical form, preserve that convention.

The route must support:

* direct navigation;
* browser refresh;
* deep linking;
* back/forward navigation;
* encoded search terms;
* empty query handling;
* malformed query handling;
* query changes.

Search query state must remain represented in the URL for durable navigation.

Do not place transient UI state into the URL unnecessarily.

---

# 9. Search Input

Implement a reusable search input component.

Requirements:

* keyboard accessible;
* responsive;
* clear button;
* submit button;
* loading state;
* autocomplete support;
* focus management;
* empty-query handling;
* form semantics.

The component must prevent accidental duplicate submissions.

Use the project's design-system conventions when available.

Do not implement a second incompatible header search component if an existing shared search primitive can be extended.

---

# 10. Search Query State

Define explicit separation between:

* entered query;
* submitted query;
* normalized query;
* autocomplete query;
* active result filters;
* active sort order;
* loading state;
* result cursor.

Do not trigger a complete search request for every keystroke.

Typing should trigger autocomplete only according to a controlled debounce strategy.

Actual search should normally occur on:

* explicit submit;
* supported suggestion selection;
* navigation to a search URL.

---

# 11. Query Normalization

Normalize user-entered search data consistently.

Handle:

* leading/trailing whitespace;
* repeated whitespace where appropriate;
* URL encoding;
* empty strings;
* maximum query length;
* unsupported or malformed values.

Do not normalize user text so aggressively that meaningful search terms are changed.

Client-side normalization must remain compatible with backend search semantics.

---

# 12. Autocomplete

Implement autocomplete behavior.

Support:

* debounced lookup;
* suggestions;
* keyboard navigation;
* pointer selection;
* loading;
* empty suggestion list;
* errors;
* cancellation of stale requests.

Do not make autocomplete requests for every character without debouncing.

Cancel stale requests such as:

```text
query = "yo"
query = "you"
query = "youtube"
```

A response for an older query must not overwrite the newest suggestion set.

---

# 13. Autocomplete Contract

Use the project's search/autocomplete contract.

A suggestion may contain:

```text
type
text
entityId
thumbnail
channelName
metadata
```

The actual fields must follow the authoritative API contract.

The frontend must not assume every suggestion represents a video.

Support appropriate suggestion types such as:

* query;
* channel;
* video;
* playlist;

only when the backend contract supports them.

---

# 14. Search Keyboard Navigation

Autocomplete must support keyboard interaction.

At minimum:

* Arrow Up;
* Arrow Down;
* Enter;
* Escape;
* Tab where appropriate.

The active suggestion must have accessible state.

Do not trap keyboard focus unnecessarily.

Typing into the search field must remain predictable.

---

# 15. Search Result Contract

Consume a typed search-result contract capable of representing:

* video results;
* channel results;
* playlist results if supported;
* pagination cursor;
* total/result metadata only when actually provided.

A conceptual response may contain:

```text
items
nextCursor
hasMore
query
appliedFilters
appliedSort
```

Use exact project contract names when available.

Do not fabricate total result counts if the backend does not provide authoritative totals.

---

# 16. Search Result Types

Implement differentiated rendering for supported result types.

### Video results

Display:

* thumbnail;
* duration;
* title;
* channel;
* channel avatar where available;
* view count;
* publication information;
* relevant metadata.

### Channel results

Display:

* avatar;
* channel name;
* verification state where provided;
* subscriber count where provided;
* description;
* subscription action where appropriate.

### Playlist results

Only render when supported by the backend contract.

Do not create a playlist result type merely because the product contains playlists.

---

# 17. Search Result Card Architecture

Create reusable result components with explicit variants.

For example:

```text
SearchResult
  ├── VideoSearchResult
  ├── ChannelSearchResult
  └── PlaylistSearchResult
```

Avoid a single component containing complex conditionals for every domain.

Cards must remain reusable across:

* desktop;
* mobile;
* search;
* discovery;
* related surfaces where appropriate.

---

# 18. Search Filters

Implement filter UI supported by the backend contract.

Potential categories include:

* type;
* upload date;
* duration;
* features;
* live;
* short-form;
* channel;
* other backend-defined filters.

Only expose filters the backend actually supports.

Do not build UI for unsupported filtering behavior.

Filter state must be represented consistently in the URL when the filters are durable search state.

---

# 19. Search Sorting

Implement backend-supported sorting.

Examples may include:

* relevance;
* date;
* view count;
* rating/popularity where supported.

Do not invent ranking semantics.

The frontend sends the selected sort value and presents the backend result order.

---

# 20. URL Synchronization

Search URL state must include the information required to reproduce the current search.

Where appropriate encode:

```text
query
filters
sort
```

Do not encode ephemeral state such as:

* menu open state;
* hovered card;
* autocomplete visibility;
* current skeleton animation;
* internal component state.

Back/forward navigation must restore durable search state.

---

# 21. Search Pagination

Implement cursor-based or contract-defined pagination.

Prefer cursor pagination where the backend contract provides it.

Do not assume offset pagination unless explicitly required.

Support:

* initial load;
* load more;
* end of results;
* loading-more state;
* pagination failure;
* retry.

Do not create duplicate result entries when a load-more operation is retried.

Deduplicate using stable result identifiers where required.

---

# 22. Infinite Scrolling

Where product UX uses infinite scrolling, implement it with an appropriate intersection-observer mechanism.

The implementation must:

* avoid excessive network requests;
* stop when there is no next page;
* handle slow responses;
* avoid duplicate requests;
* support manual retry;
* preserve scroll position;
* remain accessible.

Do not make infinite scrolling the only way to access later results if it harms accessibility or navigation.

A clearly accessible load-more control may be used as a fallback.

---

# 23. Search Loading States

Provide meaningful states for:

* initial search;
* autocomplete loading;
* pagination;
* filter changes;
* sort changes.

Reserve layout space where possible.

Avoid flashing completely unrelated content when the query changes.

Do not show stale results as though they belonged to a newly submitted query.

---

# 24. Search Empty States

Implement differentiated empty states for:

### Empty query

Explain how to search.

### No results

Display the searched query and useful guidance.

### Filtered-out results

Indicate that active filters may have eliminated results where appropriate.

### Temporary backend failure

Do not present an infrastructure failure as “no results.”

The frontend must distinguish:

```text
no results
request failed
request unauthorized
request cancelled
```

---

# 25. Search Errors

Normalize search API failures.

Support:

* invalid query;
* unauthorized request where applicable;
* rate limiting;
* timeout;
* temporary server error;
* network failure;
* malformed response.

Provide user-facing recovery behavior.

Do not expose raw stack traces.

Do not retry indefinitely.

Do not retry a deterministic validation error.

---

# 26. Search Cancellation

When a user quickly changes queries or filters:

* cancel stale requests where supported;
* ignore stale responses;
* maintain a request identity;
* prevent previous results from overwriting current state.

This applies to:

* autocomplete;
* search;
* filters;
* sorting;
* pagination.

---

# 27. Search Cache Strategy

Cache search state using the project's server-state library.

Cache keys must account for:

* query;
* filter state;
* sort;
* authenticated viewer where personalization affects the response.

Do not share viewer-specific personalized results between users.

Do not cache signed/private content access data inappropriately.

Autocomplete may use shorter cache lifetimes than ordinary search results.

---

# 28. Personalized Discovery

Implement frontend presentation for personalized discovery endpoints where available.

The backend remains responsible for:

* candidate generation;
* ranking;
* personalization;
* safety filtering.

The frontend is responsible for:

* rendering;
* pagination;
* loading;
* errors;
* navigation;
* telemetry;
* responsive behavior.

Do not recreate ranking logic in the browser.

---

# 29. Home Discovery Integration

Extend the discovery experience to support multiple content sections when supplied by the backend.

Examples:

* recommended videos;
* continue watching;
* subscriptions;
* trending content;
* topic-based sections;
* short-form content.

Sections should be modeled as typed data rather than deeply hardcoded markup.

A conceptual section might contain:

```text
sectionId
title
items
nextCursor
presentationType
```

Use the actual project contract where available.

---

# 30. Discovery Section Architecture

Use reusable discovery primitives such as:

```text
DiscoverySection
  ├── VideoRow
  ├── VideoGrid
  ├── ShortFormRow
  └── ChannelRow
```

The presentation type must be driven by actual backend data or clearly defined product configuration.

Do not let a single discovery component become a monolithic component containing every surface in the application.

---

# 31. Recommendation Cards

Implement recommendation-card variants suitable for discovery.

Support:

* thumbnail;
* title;
* channel;
* views;
* time;
* duration;
* live indicators where supplied;
* short-form indicators where supplied.

Do not infer private or restricted video properties from public fields.

Navigation must use the canonical video route.

---

# 32. Subscription Feed

Implement a dedicated subscription feed experience.

The feed should display content from channels the viewer follows according to the subscription-feed API contract.

Support:

* authenticated access;
* loading;
* empty state;
* pagination;
* new-content navigation;
* refresh;
* error recovery.

Anonymous viewers should receive an appropriate sign-in state rather than a broken feed.

---

# 33. Subscription Feed Contract

Consume a feed contract containing appropriately typed entries.

A conceptual structure may include:

```text
items
nextCursor
hasMore
generatedAt
personalizationVersion
```

Do not invent feed-generation behavior in the client.

Do not assume chronological ordering unless the backend explicitly guarantees it.

---

# 34. Subscription Feed Empty State

When the viewer has no subscriptions or no available content:

* explain why the feed is empty;
* provide useful navigation toward channel discovery/search where appropriate;
* preserve the application's normal navigation shell.

Do not display fake channels or fake recommendations.

---

# 35. Personalized Feed Failure

If the recommendation or subscription service fails:

* preserve the application shell;
* show a recoverable error;
* avoid replacing unrelated working sections;
* avoid silently falling back to fabricated data.

Where an official fallback endpoint exists, use it according to the contract.

---

# 36. Short-Form Discovery

Implement the web entry point into short-form video discovery where supported.

The scope may include:

* short-form discovery section;
* vertical card presentation;
* navigation to short-form viewing;
* appropriate duration/aspect indicators.

Do not implement the full short-form playback experience if it belongs to another frontend scope.

Do not implement short-form ranking in the browser.

---

# 37. Channel Discovery

Search and discovery surfaces must support navigation to channels.

Channel cards should remain reusable.

Support:

* channel avatar;
* channel name;
* verification;
* subscriber count;
* description where available;
* subscription status where authenticated.

Do not assume every channel result is subscribable.

---

# 38. Viewer Authentication

Anonymous viewers may browse public discovery/search content.

Authentication should be required only for operations that actually depend on account state, such as:

* subscription feed;
* personalized recommendations;
* private history;
* account-specific search behavior.

Do not force login for public search.

When personalization is unavailable, use an explicitly supported anonymous discovery mode if provided by the backend.

---

# 39. Personalized Cache Isolation

Viewer-specific discovery data must never be accidentally shared between viewers.

Cache keys must account for authenticated identity where the API response varies by viewer.

Do not place user-specific discovery data in globally shared static data.

When authentication changes:

* invalidate relevant personalized caches;
* prevent leakage of previous-account content;
* reload viewer-sensitive discovery state.

---

# 40. Search History

If the product supports search-history suggestions:

* retrieve history through the appropriate contract;
* render only the data the viewer is authorized to see;
* support deletion if the product contract provides it;
* avoid cross-account leakage;
* do not persist sensitive history in uncontrolled storage.

If anonymous recent-search support is provided, clearly distinguish it from authenticated server-side search history.

---

# 41. Search History Privacy

Search history is sensitive behavioral data.

Do not send it to analytics as raw query data unless the project's privacy contract explicitly permits it.

Avoid placing sensitive query content into URLs beyond normal search navigation requirements when the product architecture does not require it.

Do not expose another viewer's search history through cached components.

---

# 42. Analytics and Telemetry

Instrument discovery and search behavior according to the project's analytics contract.

Relevant events may include:

```text
search_submitted
search_autocomplete_requested
search_suggestion_selected
search_results_viewed
search_result_clicked
search_filter_changed
search_sort_changed
search_pagination_loaded
search_no_results
discovery_section_viewed
discovery_item_clicked
subscription_feed_opened
subscription_feed_item_clicked
short_form_discovery_opened
```

Use canonical event names where supplied by the project.

Do not emit:

* passwords;
* access tokens;
* session secrets;
* private media URLs;
* unnecessary personally identifying information.

Treat search queries as potentially sensitive.

---

# 43. Analytics Sampling and Frequency

Do not send excessive analytics traffic.

For high-frequency UI behavior:

* debounce where appropriate;
* aggregate repeated events;
* avoid duplicate events caused by React remounts;
* avoid firing visibility events every render.

For result impressions, use a controlled visibility strategy.

Do not instrument every pixel movement.

---

# 44. Result Impression Tracking

Where the analytics contract requires search/discovery impressions, implement an appropriate visibility mechanism.

It must:

* avoid duplicate impressions;
* associate impressions with the correct query/session context;
* remain efficient for long result lists;
* stop observing unmounted elements;
* avoid generating excessive telemetry.

If the analytics contract does not require impression events, do not invent them.

---

# 45. Search Result Navigation

When a user selects a result:

* navigate using the canonical route;
* preserve required attribution context only through supported mechanisms;
* avoid placing sensitive analytics identifiers in publicly visible URLs;
* ensure the destination can reconstruct the correct content from the canonical ID.

Do not navigate through internal backend URLs.

---

# 46. Back Navigation

Search navigation must preserve expected browser behavior.

Example:

```text
Search
  → Video
  → Back
  → Search results restored
```

Where feasible, preserve:

* query;
* filters;
* sort;
* scroll position.

Do not reload the entire search experience unnecessarily.

Do not rely on in-memory state alone for durable query state.

---

# 47. Responsive Discovery Layouts

Support:

* mobile;
* tablet;
* desktop;
* large desktop.

Use appropriate layouts:

* lists for narrow search screens;
* grids or multi-column result layouts where beneficial;
* horizontally scrolling discovery rows only when accessible;
* compact cards on small screens.

Avoid horizontal overflow.

Do not hide important search controls merely because the viewport is narrow.

---

# 48. Accessibility

Implement:

* semantic headings;
* labelled search controls;
* accessible autocomplete;
* keyboard navigation;
* accessible filter menus;
* accessible sort menus;
* focus restoration;
* screen-reader status updates;
* meaningful result announcements;
* accessible infinite-scroll fallback;
* sufficient touch targets;
* visible focus states.

When search results update after submission, move or announce focus appropriately without causing disruptive screen-reader behavior.

---

# 49. SEO and Metadata

Search and discovery routes must use appropriate metadata where applicable.

Public video/channel discovery pages may expose meaningful:

* title;
* description;
* canonical URL.

Do not generate misleading metadata from user-entered search queries.

Search-result pages should follow the product's indexing policy.

If search pages should not be indexed, implement the project's intended indexing policy rather than assuming they should be public search-engine pages.

---

# 50. Performance

Optimize:

* initial search navigation;
* autocomplete latency;
* image loading;
* card rendering;
* pagination;
* discovery section rendering;
* hydration;
* cache reuse.

Use:

* responsive images;
* lazy loading where appropriate;
* virtualization only where it provides measurable value;
* memoization where it avoids actual expensive recomputation.

Do not over-virtualize normal result lists without evidence of need.

Avoid a global rerender whenever one search-result item changes.

---

# 51. Image Optimization

Search and discovery are image-heavy.

Ensure:

* correct image dimensions;
* responsive source selection;
* lazy loading where appropriate;
* placeholder/fallback behavior;
* layout reservation;
* appropriate priority for above-the-fold media.

Do not load full-resolution thumbnails when a smaller rendition is sufficient.

---

# 52. Error Isolation

Failure in one discovery domain must not destroy others.

For example:

```text
Search works
Recommendations fail
Subscription feed still usable
```

Likewise:

```text
Home recommendations fail
Search remains functional
```

Use local error boundaries or equivalent isolation.

Do not create a single global failure state for independently retrievable discovery sections.

---

# 53. Rate Limits and Request Discipline

Respect server rate limits.

Do not:

* retry autocomplete aggressively;
* issue multiple identical searches;
* request the next page more than once concurrently;
* poll discovery endpoints unnecessarily.

Handle `429` responses appropriately.

Where the server provides retry metadata, respect it without creating excessive waiting for the user.

---

# 54. Stale Data and Revalidation

Discovery data can become stale.

Use a sensible strategy for:

* search results;
* recommendations;
* subscription feed;
* autocomplete;
* personalized sections.

Do not claim real-time freshness unless the API provides it.

When revalidating:

* retain useful content while fetching where appropriate;
* avoid flashing empty states;
* prevent stale results from replacing newer query results.

---

# 55. Data Race Protection

Protect against:

```text
Request A: query = "music"
Request B: query = "music videos"
Request C: query = "music videos 2026"
```

The latest active query must own the rendered result set.

Apply the same principle to:

* filters;
* sort changes;
* pagination;
* autocomplete;
* authenticated state changes;
* recommendation-section refreshes.

Use abort controllers, request keys, generation IDs, or equivalent mechanisms.

---

# 56. Component Boundaries

Use clear boundaries such as:

```text
search/
  page
  data
  hooks
  types
  components
  autocomplete
  filters
  results
  analytics

discovery/
  data
  hooks
  components
  sections
  cards
  subscriptions
  short-form
  analytics
```

The exact repository structure may differ.

Responsibilities must remain modular.

Do not create circular dependencies between search and discovery modules.

---

# 57. State Ownership

Separate:

### URL state

* query;
* filters;
* sort.

### Server state

* search results;
* autocomplete data;
* recommendation sections;
* subscription feed;
* channel results.

### Local UI state

* open menus;
* active suggestion;
* focused control;
* temporary filter selections;
* loading indicators.

### Persistent client preferences

Only state explicitly suitable for local persistence.

Do not put all search/discovery state into one global store.

---

# 58. Authentication Expiration

Handle authentication expiration while:

* opening subscription feed;
* retrieving personalized discovery;
* retrieving search history;
* subscribing from a channel result;
* performing viewer-specific discovery operations.

Do not create infinite token-refresh loops.

Preserve public search functionality even when account authentication becomes invalid.

---

# 59. Security

The implementation must:

* avoid unsafe HTML rendering;
* safely handle query strings;
* validate navigation targets;
* avoid open redirects;
* avoid logging sensitive search information;
* avoid leaking authorization information;
* use secure session mechanisms;
* respect server-side authorization.

Search terms and URLs must not be interpreted as executable markup.

---

# 60. Privacy

Treat search and discovery behavior as potentially sensitive.

Do not expose:

* private search history;
* private subscriptions;
* personalized recommendations;
* account identifiers

to unauthorized users.

Do not put unnecessary viewer identifiers into URLs.

Ensure telemetry respects the project's privacy model.

---

# 61. Testing Strategy

Implement tests covering actual behavior.

### Unit tests

Test:

* query normalization;
* debounce logic;
* autocomplete state;
* URL encoding;
* filter serialization;
* sort serialization;
* pagination state;
* deduplication;
* cache-key generation;
* stale-response rejection;
* analytics event construction.

### Component tests

Test:

* search input;
* autocomplete;
* keyboard navigation;
* result cards;
* filter controls;
* sort controls;
* pagination;
* empty states;
* search errors;
* discovery sections;
* subscription feed;
* short-form discovery cards.

### Integration tests

Test:

* submitting a search;
* updating query state;
* loading results;
* changing filters;
* changing sort;
* loading additional results;
* recovering after errors;
* subscription-feed loading;
* personalized discovery loading;
* anonymous search behavior;
* authenticated discovery behavior.

### End-to-end tests

At minimum:

1. open search;
2. submit a query;
3. view results;
4. select a result;
5. return to the search results;
6. use autocomplete;
7. change a filter;
8. change sorting;
9. load additional results;
10. verify empty-search behavior;
11. verify no-results behavior;
12. open subscription feed;
13. verify authenticated discovery behavior where test infrastructure supports it;
14. verify responsive/mobile search behavior;
15. verify keyboard-accessible autocomplete.

Do not replace behavior tests with superficial rendering snapshots.

---

# 62. Browser and Accessibility Validation

Validate:

* modern supported browsers;
* keyboard interaction;
* screen-reader semantics;
* focus behavior;
* touch behavior;
* responsive layouts.

Test autocomplete carefully because incorrect ARIA state or focus behavior can make search unusable for assistive-technology users.

---

# 63. Contract Compatibility

The frontend must remain compatible with project-wide contracts covering:

```text
Canonical IDs
Canonical timestamps
API envelopes
API error format
Authentication
Authorization
Video entity
Channel entity
Search result model
Autocomplete model
Pagination model
Subscription-feed model
Recommendation/discovery model
Analytics event model
Privacy model
```

When concrete project artifacts are available, use their exact field names and endpoint contracts.

Do not silently redefine backend entities.

Do not create client-only fields and pretend they are server-authoritative.

---

# 64. No Fake Search or Discovery

Do not implement:

* hardcoded result arrays;
* fake autocomplete responses;
* fake personalized recommendations;
* static subscription feeds;
* simulated search APIs;
* fake pagination.

Mocks are allowed only inside automated tests.

The application path must use the actual typed integration boundary.

---

# 65. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* empty search handlers;
* nonfunctional filters;
* fake autocomplete menus;
* buttons without behavior;
* placeholder cards;
* incomplete pagination;
* missing error states;
* “implement later” sections.

Everything inside the current scope must be genuinely implemented.

---

# 66. Documentation

Update documentation describing:

* search route;
* search query and URL semantics;
* autocomplete behavior;
* search result types;
* filter/sort state;
* pagination strategy;
* discovery-section architecture;
* subscription-feed integration;
* recommendation-data consumption;
* analytics events;
* caching;
* privacy considerations;
* accessibility behavior.

Documentation must reflect the actual implementation.

---

# 67. Validation

Before reporting completion, validate:

* TypeScript compilation;
* linting;
* unit tests;
* component tests;
* integration tests;
* end-to-end tests where available;
* production build;
* search navigation;
* autocomplete;
* filters;
* sorting;
* pagination;
* stale-request handling;
* authenticated/anonymous behavior;
* responsive behavior;
* accessibility-critical keyboard behavior;
* discovery failure isolation.

Fix issues found within the current scope rather than merely reporting them.

---

# 68. Definition of Done

This prompt is complete only when:

* search routing works;
* search input is production-ready;
* autocomplete works;
* stale autocomplete responses are prevented;
* search results render real backend data;
* video and channel result types are supported where contracted;
* filtering works where contracted;
* sorting works where contracted;
* pagination works;
* duplicate pagination results are prevented;
* search errors are handled;
* search empty states are handled;
* URL state is correctly synchronized;
* search caching is safe;
* personalized data is isolated by viewer;
* subscription feed is implemented;
* personalized discovery surfaces are implemented where contracted;
* recommendation ranking remains backend-owned;
* short-form discovery entry is implemented where contracted;
* search/discovery telemetry is integrated;
* sensitive telemetry is protected;
* responsive layouts work;
* accessibility requirements are implemented;
* security/privacy requirements are respected;
* search and discovery failures are isolated;
* stale asynchronous requests cannot overwrite newer state;
* tests cover the defined behavior;
* documentation is updated;
* no fake production data remains;
* no current-scope placeholder functionality remains;
* validation passes.

---

# 69. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize the search, discovery, subscription-feed, and browsing functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List the search, autocomplete, discovery, recommendation, subscription-feed, and analytics contracts consumed.

### State and Caching

Summarize URL state, server-state management, caching, pagination, and request-cancellation behavior.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, builds, and runtime validation performed.

### Integration Notes

Identify material backend-contract assumptions, compatibility concerns, or external dependencies.

### Out of Scope

Confirm that backend search, indexing, recommendation algorithms, mobile, playback infrastructure, creator studio, live, moderation, and monetization were not improperly implemented.

---

# 70. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe how search or discovery should work.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real APIs and real contracts.

Do not fabricate backend behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web search and discovery experience** that can be integrated with the independently generated backend and other client/infrastructure components through explicit project contracts.
