# YouTube-Style Video Platform — Frontend Prompt — Volume 7

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web creator studio, creator content-management, publishing, upload-management, channel-management, and creator analytics experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

* creator studio shell;
* creator dashboard;
* video-management pages;
* upload workflow UI;
* upload-session integration;
* media-processing status;
* video metadata editing;
* thumbnails;
* captions metadata;
* visibility;
* scheduling;
* playlist assignment;
* channel customization;
* creator analytics dashboards;
* content performance views;
* audience and traffic analytics views where supported;
* creator-side loading/error states;
* responsive creator tooling;
* accessibility;
* security;
* privacy;
* analytics;
* testing;
* documentation.

Do not implement unrelated frontend domains.

Do not implement backend upload processing, media transcoding, analytics computation, creator authorization services, or storage infrastructure.

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

Creator tooling must be designed as production software used for high-value content-management operations.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

* another Claude conversation;
* another AI response;
* another frontend prompt;
* hidden architecture decisions;
* undocumented APIs;
* hidden generated files.

If a repository is available, inspect it before modifying it.

If portable project contracts are available, use them as authoritative.

If compatible creator tooling already exists, extend it rather than duplicating it.

Do not infer that a creator capability exists merely because the global product supports it.

---

# 4. Primary Objective

Implement the production web creator experience.

The completed scope must allow an authorized creator to:

1. enter Creator Studio;
2. view a creator dashboard;
3. view content owned by the creator;
4. initiate video uploads;
5. track upload progress;
6. recover from interrupted uploads where supported;
7. observe media-processing state;
8. edit video metadata;
9. manage thumbnails;
10. manage captions metadata;
11. assign playlists;
12. configure visibility;
13. schedule publication;
14. inspect publication state;
15. edit channel-facing information where supported;
16. view creator analytics;
17. inspect video performance;
18. inspect channel-level analytics;
19. inspect audience/traffic information where supported;
20. handle authorization and validation errors;
21. use the creator tools responsively and accessibly;
22. maintain secure separation between creator accounts.

---

# 5. Explicit Scope

Implement:

* Creator Studio shell;
* creator navigation;
* dashboard;
* content-management page;
* content filtering and pagination;
* upload workflow;
* upload progress;
* upload-session state;
* media-processing state;
* video metadata editor;
* thumbnail management;
* captions metadata integration;
* visibility controls;
* scheduling controls;
* playlist assignment;
* publication state;
* channel customization where supported;
* creator analytics overview;
* video analytics;
* channel analytics;
* audience analytics where supported;
* traffic-source analytics where supported;
* creator-specific loading/error/empty states;
* creator route protection;
* viewer/creator permission handling;
* responsive layouts;
* accessibility;
* analytics/telemetry;
* automated testing;
* documentation.

---

# 6. Explicit Out of Scope

Do not implement:

* backend video upload services;
* multipart storage infrastructure;
* resumable-upload servers;
* object-storage provisioning;
* FFmpeg/transcoding;
* media-processing workers;
* search indexing;
* recommendation ranking;
* moderation backend;
* live-stream control plane;
* payment processing;
* monetization backend;
* advertising systems;
* mobile creator studio;
* administrator tooling;
* backend analytics aggregation.

Do not create fake upload or analytics implementations.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository;
2. identify the web application;
3. inspect authenticated route handling;
4. inspect channel/video domain models;
5. inspect API-client conventions;
6. inspect upload/media contracts;
7. inspect storage/media configuration surfaces;
8. inspect analytics contracts;
9. inspect shared form components;
10. inspect design-system primitives;
11. inspect existing video/channel cards;
12. inspect testing infrastructure.

Reuse compatible infrastructure.

Do not create parallel authentication, API-client, state-management, or form frameworks.

---

# 8. Creator Route Architecture

Implement a protected Creator Studio route structure.

A conceptual structure may be:

```text
/studio
/studio/dashboard
/studio/content
/studio/content/{videoId}
/studio/upload
/studio/analytics
/studio/analytics/video/{videoId}
/studio/analytics/channel
/studio/settings
```

The exact paths may follow repository conventions.

All creator routes must require appropriate creator authorization.

---

# 9. Creator Authorization

Creator access must be driven by the canonical authorization model.

Potential capabilities include:

```text
canAccessStudio
canCreateVideo
canEditVideo
canPublishVideo
canScheduleVideo
canManageThumbnail
canManageCaptions
canManageChannel
canViewAnalytics
```

Use the actual project permission model.

Do not treat client-side ownership checks as authoritative authorization.

---

# 10. Creator Studio Shell

Implement a reusable Studio shell containing:

* creator navigation;
* current section;
* account/channel identity;
* responsive navigation;
* notifications/access controls where already supported;
* support/help entry points where contractually supported.

Conceptually:

```text
StudioShell
  ├── StudioNavigation
  ├── StudioHeader
  └── StudioContent
```

Do not duplicate the entire public application shell unnecessarily.

---

# 11. Studio Dashboard

Implement the creator dashboard.

Where supported, display:

* recent video performance;
* current watch-time metrics;
* views;
* subscribers;
* recent content;
* alerts;
* processing issues;
* creator tasks;
* analytics highlights.

All metrics must come from real backend contracts.

Do not calculate authoritative creator metrics from incomplete client-side data.

---

# 12. Dashboard Data Contract

Consume typed creator dashboard data.

A conceptual representation may contain:

```text
channel
recentVideos
summaryMetrics
alerts
processingItems
analyticsHighlights
```

Use exact project contracts when available.

Do not create multiple incompatible representations of creator metrics.

---

# 13. Creator Content Route

Implement a content-management experience for videos owned or managed by the creator.

Support:

* list;
* search/filter where backend contract supports it;
* publication status;
* visibility;
* processing status;
* views;
* comments/reactions summary where available;
* date;
* actions.

Do not expose content from channels the creator is not authorized to manage.

---

# 14. Content Filters

Support backend-defined filters such as:

* published;
* scheduled;
* draft;
* private;
* unlisted;
* processing;
* failed;
* live/archive states where applicable.

Only expose statuses represented by the authoritative video lifecycle contract.

---

# 15. Content Pagination

Use cursor pagination when provided.

Support:

* initial page;
* next page;
* loading;
* retry;
* end of list;
* duplicate prevention;
* stale-response protection.

Do not load an unbounded creator library.

---

# 16. Content Row Architecture

Create reusable creator-content rows/cards showing, where available:

* thumbnail;
* title;
* publication state;
* visibility;
* processing state;
* views;
* publication date;
* duration;
* last updated;
* available creator actions.

Actions must be permission-driven.

---

# 17. Video Editor Route

Implement an authenticated video editor route for creator-owned videos.

It must support:

* loading current metadata;
* editing supported fields;
* saving changes;
* validation;
* unsaved changes;
* save status;
* server reconciliation;
* error recovery.

Do not allow editing a video merely because the user knows its ID.

---

# 18. Video Metadata Contract

Support project-defined metadata such as:

```text
title
description
thumbnail
visibility
scheduledAt
playlistIds
category
language
tags
captionSettings
audienceSettings
publicationState
processingState
```

Only expose fields actually supported by the backend.

Do not invent undocumented metadata.

---

# 19. Title and Description Editing

Implement creator editing for:

* title;
* description.

Support:

* maximum lengths from backend/product configuration;
* validation;
* dirty state;
* save;
* cancel/reset;
* loading;
* failure;
* successful reconciliation.

Do not submit the entire object if the API supports safe partial updates and the project architecture prefers them.

---

# 20. Description Safety

Creator descriptions are untrusted content.

The editor must:

* safely handle text;
* safely display existing content;
* avoid XSS;
* validate supported URL formats;
* avoid executing markup.

If rich text is supported, use the project's explicit sanitized rich-text contract.

Do not introduce arbitrary HTML rendering.

---

# 21. Thumbnail Management

Where the project supports thumbnail management:

* display current thumbnail;
* select/upload a replacement;
* validate file type;
* validate size;
* preview safely;
* upload through the canonical media contract;
* display progress where provided;
* handle failure;
* reconcile final thumbnail.

Do not expose storage credentials.

Do not upload directly to arbitrary destinations outside the project's upload contract.

---

# 22. Thumbnail Validation

The UI must honor server/product constraints for:

* file size;
* MIME type;
* dimensions;
* supported formats.

Client validation improves usability only.

The server remains authoritative.

Do not claim an upload is valid solely because client-side checks passed.

---

# 23. Captions Metadata

Where the backend supports captions/subtitles, expose creator-facing caption management appropriate to the contract.

Potential functionality includes:

* caption language;
* availability;
* status;
* track metadata;
* add/upload entry point;
* enable/disable state.

Do not implement a complete subtitle transcoding system in the frontend.

---

# 24. Caption Upload Integration

If the platform supports caption-file upload:

* use the canonical upload contract;
* validate supported file types;
* show progress;
* associate the uploaded asset with the correct video;
* reconcile processing state;
* handle failed processing.

Never expose raw object-storage credentials.

Do not fabricate caption-processing completion.

---

# 25. Playlist Assignment

Allow creators to assign videos to supported playlists.

The UI must:

* retrieve authorized playlists;
* display current membership;
* support adding/removing;
* handle loading;
* reconcile mutations;
* prevent unauthorized playlist changes.

Do not confuse creator-owned playlists with viewer private playlists.

---

# 26. Visibility Management

Implement supported video visibility options.

Potential values may include:

```text
public
unlisted
private
```

Only expose actual project values.

Changing visibility must:

* validate permission;
* show the resulting state;
* handle server errors;
* avoid presenting unsaved state as published state.

---

# 27. Scheduling

Where supported, implement scheduled publication.

Support:

* enable/disable scheduling;
* date selection;
* time selection;
* timezone behavior;
* validation;
* save;
* cancellation/rescheduling where supported.

The frontend must use the project's canonical time model.

Do not interpret local browser time incorrectly.

---

# 28. Timezone Handling

Scheduling must distinguish:

* viewer-local timezone;
* stored canonical timestamp;
* server interpretation.

Do not send ambiguous local date/time strings.

Use the project's canonical timestamp representation.

Display timezone information clearly when scheduling has material consequences.

---

# 29. Publication State

Render authoritative lifecycle states such as:

```text
draft
uploading
processing
ready
scheduled
published
failed
blocked
```

Only render states defined by the project.

Do not infer `published` from a client save operation.

---

# 30. Upload Workflow

Implement the web upload experience using the canonical upload-session contract.

Support, where the backend provides:

1. selecting a media file;
2. validation;
3. upload-session creation;
4. upload progress;
5. pause/resume where supported;
6. retry;
7. upload completion;
8. server-side finalization;
9. processing-state tracking;
10. transition into metadata editing.

Do not implement upload transport from scratch if the project already defines a production upload abstraction.

---

# 31. Upload File Validation

Before creating an upload session:

* validate supported file types;
* validate client-known file size limits;
* provide understandable errors.

The client must never assume validation guarantees server acceptance.

Treat uploaded files as untrusted input.

---

# 32. Upload Progress

Display meaningful progress.

Track separately:

* upload progress;
* finalization state;
* processing state.

Do not present 100% upload progress as “video published.”

A media upload can complete while backend processing remains pending.

---

# 33. Resumable Uploads

Where the upload contract supports resumability:

* persist the minimum state required for recovery;
* associate state with the correct authenticated creator;
* resume from the server-confirmed position;
* handle expired sessions;
* avoid duplicate finalization.

Do not invent a resumable protocol if the backend does not provide one.

---

# 34. Upload Cancellation

Where supported:

* provide cancellation;
* confirm destructive cancellation when appropriate;
* clean up client-side state;
* invalidate upload-session state;
* avoid leaving a misleading draft marked as completed.

The server remains responsible for actual storage cleanup.

---

# 35. Upload Failure Recovery

Handle:

* network interruption;
* expired session;
* server rejection;
* storage failure;
* validation failure;
* processing failure.

Provide appropriate recovery:

* retry;
* resume;
* restart;
* edit metadata;
* report processing failure.

Do not endlessly retry permanent failures.

---

# 36. Processing State

After upload finalization, display processing state.

Possible states may include:

```text
queued
processing
ready
failed
blocked
```

Only use actual backend states.

Poll or subscribe only through the canonical contract.

Do not fabricate progress percentages when the server does not provide meaningful processing progress.

---

# 37. Processing Refresh Strategy

If the backend exposes realtime processing updates:

* consume the established realtime contract;
* deduplicate updates;
* clean up subscriptions.

If polling is the defined mechanism:

* use controlled intervals;
* stop after terminal states;
* back off when appropriate;
* stop when leaving the page.

Do not poll indefinitely after success/failure.

---

# 38. Draft Preservation

During upload/edit flows, preserve recoverable local form state where safe.

Do not persist secrets or private account data unnecessarily.

If a creator navigates away with unsaved metadata:

* warn appropriately;
* preserve safe draft state;
* avoid silently losing significant edits.

---

# 39. Creator Channel Settings

Where supported, expose creator channel-management settings.

Potential areas include:

* channel name;
* handle;
* description;
* avatar;
* banner;
* public links;
* channel presentation.

Only implement fields covered by the creator channel-management contract.

---

# 40. Channel Customization

Where the product supports channel presentation controls:

* provide preview-safe editing;
* validate values;
* support save/cancel;
* handle server reconciliation.

Do not implement a full drag-and-drop channel-home-page builder unless the project contract explicitly includes it.

---

# 41. Creator Analytics Overview

Implement a creator analytics dashboard consuming authoritative analytics contracts.

Possible metrics:

* views;
* watch time;
* subscribers;
* likes;
* comments;
* shares;
* estimated revenue where explicitly supported;
* impressions;
* click-through rate;
* audience retention.

Only expose metrics actually supplied by the backend.

---

# 42. Analytics Time Ranges

Support backend-defined date ranges.

Potential ranges may include:

* today;
* last 7 days;
* last 28 days;
* last 90 days;
* custom range.

Do not hardcode calculations that conflict with server aggregation.

Date ranges must use the project's canonical timezone semantics.

---

# 43. Video Analytics

Implement video-level analytics views.

Potential dimensions include:

* views;
* watch time;
* average view duration;
* retention;
* likes;
* comments;
* shares;
* impressions;
* click-through rate;
* traffic sources.

Only render metrics whose definitions are supported by the analytics contract.

---

# 44. Channel Analytics

Implement channel-level analytics where supported.

Provide:

* summary cards;
* trends;
* date ranges;
* content comparisons where supported;
* subscriber changes;
* watch-time trends.

Do not infer causation from simple metric changes.

---

# 45. Audience Analytics

Where supported, render audience analytics such as:

* returning viewers;
* new viewers;
* audience geography at permitted aggregation;
* device categories;
* viewer demographics where legally/product-authorized.

Respect privacy thresholds.

Do not display overly granular audience data that the backend intentionally aggregates or suppresses.

---

# 46. Traffic Source Analytics

Where supported, display contract-defined traffic sources such as:

* browse;
* search;
* suggested/related;
* external;
* channel pages;
* other backend-defined sources.

Do not create traffic-source classifications in the frontend.

---

# 47. Analytics Visualization

Use accessible visualizations for:

* time-series data;
* category breakdowns;
* comparison views.

Every chart must have:

* accessible text summary;
* meaningful labels;
* useful empty state;
* loading state;
* error state.

Do not rely solely on color or visual position to communicate values.

---

# 48. Analytics Data Freshness

Display the freshness state supplied by the backend where available.

If metrics are delayed:

* communicate that appropriately;
* do not imply real-time accuracy.

Do not continually poll analytics unless the product contract requires it.

---

# 49. Analytics Export

Only implement analytics export when explicitly supported by the backend contract.

If export is asynchronous:

* show request state;
* pending state;
* success/failure;
* download/status link provided by the backend.

Do not generate large analytics exports entirely in the browser unless explicitly designed that way.

---

# 50. Creator Cache Isolation

Creator data must be isolated by:

* authenticated user;
* channel ID;
* managed creator identity.

Do not allow one creator's analytics or upload state to appear for another account.

Account switching must invalidate:

* creator dashboards;
* content lists;
* upload sessions;
* analytics;
* channel settings.

---

# 51. Creator Security

The frontend must:

* use secure authentication/session mechanisms;
* respect creator authorization;
* avoid exposing upload credentials;
* avoid logging signed upload/media URLs;
* avoid exposing private analytics;
* avoid exposing internal moderation or processing metadata.

Client-side authorization is not security.

---

# 52. Creator Privacy

Analytics and creator tools may contain sensitive business data.

Protect:

* revenue-related metrics where present;
* private analytics;
* unlisted/private video metadata;
* upload-session information;
* unpublished content;
* audience information.

Do not emit private creator data into public analytics.

---

# 53. Creator Route Error Isolation

A failure in analytics must not break content management.

A failed upload should not make channel settings unusable.

An unavailable thumbnail should not prevent metadata editing.

Use localized error boundaries and error states.

---

# 54. Unsaved Changes

Creator editors must track dirty state.

Before navigation away from materially unsaved changes:

* warn the user appropriately;
* preserve safe local state where possible;
* do not interfere with navigation when no changes exist.

Do not block navigation forever because a background autosave is occurring.

---

# 55. Autosave

Only implement autosave where explicitly supported by the product/contract.

If autosave exists:

* debounce updates;
* reconcile server responses;
* handle conflicts;
* surface save state;
* prevent stale autosave responses from overwriting newer edits.

Do not invent autosave merely for convenience.

---

# 56. Mutation Concurrency

Protect against stale mutation responses such as:

```text
Save title A
Save title B
Response B arrives
Response A arrives later
```

The older response must not restore stale state.

Use mutation sequencing, request identity, cancellation, or server versioning according to the project architecture.

---

# 57. Version Conflicts

If the backend supplies content version/updated-at information:

* include it where required;
* detect conflicts;
* provide appropriate recovery.

Do not silently overwrite another confirmed edit.

---

# 58. Analytics and Telemetry

Instrument meaningful creator actions.

Potential events include:

```text
studio_opened
studio_content_viewed
creator_video_opened
upload_started
upload_completed
upload_failed
upload_resumed
upload_cancelled
video_metadata_updated
video_visibility_changed
video_scheduled
thumbnail_updated
captions_updated
playlist_assignment_changed
creator_analytics_viewed
creator_analytics_range_changed
channel_settings_updated
```

Use canonical event names where available.

Do not transmit private analytics values unnecessarily.

Do not include signed upload URLs, access tokens, or private content data.

---

# 59. Analytics Event Privacy

Creator analytics events must not leak:

* raw private audience data;
* revenue details;
* unpublished video information;
* secrets;
* upload credentials.

Use stable opaque identifiers only where the project telemetry contract requires them.

---

# 60. Accessibility

Creator Studio must support:

* keyboard navigation;
* semantic headings;
* accessible tables;
* accessible forms;
* accessible dialogs;
* accessible upload controls;
* screen-reader progress feedback;
* accessible charts;
* visible focus;
* accessible status indicators;
* keyboard alternatives to drag/drop where applicable.

Progress updates should avoid flooding assistive technologies with excessive announcements.

---

# 61. Responsive Creator Studio

Support:

* mobile web;
* tablet;
* desktop;
* large desktop.

Creator Studio may use denser layouts on desktop, but critical functionality must remain usable on smaller screens.

Tables may become cards or horizontally scrollable regions where appropriate.

Do not make desktop-only controls the sole path to essential creator operations.

---

# 62. Performance

Optimize:

* Studio navigation;
* content lists;
* analytics rendering;
* large content collections;
* image-heavy tables/cards;
* upload UI;
* state updates.

Do not fetch every analytics dimension or every content page upfront.

Use lazy loading for lower-priority Studio sections where practical.

Avoid rerendering large content lists when one row changes.

---

# 63. File and Media Handling

Client-side media handling must:

* avoid loading entire large files into memory unnecessarily;
* use streaming/chunking mechanisms supplied by the upload architecture;
* release temporary browser resources;
* handle cancellation;
* validate file metadata where practical.

Do not implement custom binary protocols without architectural support.

---

# 64. API Error Normalization

Use the project's standard error model.

At minimum distinguish:

```text
authentication
authorization
validation
conflict
notFound
rateLimited
processingFailed
uploadFailed
temporarilyUnavailable
network
unknown
```

Map them to product-appropriate UI.

Do not expose internal stack traces.

---

# 65. Testing Strategy

Implement tests for actual creator behavior.

### Unit tests

Cover:

* permission mapping;
* upload-state transitions;
* upload retry classification;
* processing-state mapping;
* metadata validation;
* schedule serialization;
* timezone conversion;
* mutation sequencing;
* analytics range serialization;
* creator-cache isolation.

### Component tests

Cover:

* Studio navigation;
* content rows;
* upload interface;
* progress indicator;
* metadata form;
* visibility selector;
* scheduling controls;
* thumbnail management;
* playlist assignment;
* analytics cards/charts;
* channel settings;
* error states.

### Integration tests

Cover:

* creator authorization;
* content loading;
* metadata update;
* upload-session creation;
* upload completion/finalization;
* processing-state updates;
* thumbnail update;
* visibility change;
* scheduling;
* playlist assignment;
* analytics loading;
* channel customization.

### End-to-end tests

At minimum:

1. authenticate as an authorized creator;
2. open Creator Studio;
3. view dashboard;
4. open content list;
5. open an editable video;
6. modify metadata;
7. upload or update a thumbnail where test infrastructure supports it;
8. change visibility;
9. schedule a video where supported;
10. inspect processing state;
11. open creator analytics;
12. change analytics date range;
13. open channel settings;
14. verify unauthorized viewer cannot access creator tools;
15. verify account switching does not leak creator data.

Do not replace these tests with static screenshots.

---

# 66. Browser Compatibility

Validate across the supported browser matrix.

Pay particular attention to:

* file input behavior;
* large-file upload UX;
* progress events;
* dialogs;
* date/time controls;
* responsive analytics;
* accessibility of dense creator tables.

Do not assume all browsers expose identical file APIs.

---

# 67. Documentation

Update documentation describing:

* Creator Studio routes;
* creator authorization;
* upload-session integration;
* upload lifecycle;
* processing states;
* metadata editing;
* scheduling/timezone behavior;
* thumbnail/caption integration;
* analytics contracts;
* privacy/security considerations;
* creator cache isolation;
* testing strategy.

Documentation must reflect the actual implementation.

---

# 68. No Fake Creator Functionality

Do not create:

* fake upload progress;
* fake processing states;
* fake analytics;
* fake video publication;
* fake creator permissions;
* fake thumbnails;
* fake channel settings;
* fake scheduling completion.

Mocks are permitted only inside automated tests.

The real application must use actual contracts.

---

# 69. No Placeholder Completion

Do not leave:

* TODO;
* FIXME;
* nonfunctional upload buttons;
* fake analytics charts;
* empty save handlers;
* placeholder creator controls;
* incomplete upload recovery;
* fake publication states;
* “implement later” sections.

Everything in the current scope must be genuinely implemented.

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
* creator authorization;
* content management;
* upload integration;
* upload failure handling;
* processing state;
* metadata editing;
* thumbnail handling;
* scheduling;
* playlist assignment;
* analytics;
* channel settings;
* account-switch isolation;
* responsive behavior;
* accessibility;
* stale-mutation protection.

Fix issues discovered within this scope.

Do not merely report them.

---

# 71. Definition of Done

This prompt is complete only when:

* Creator Studio routes work;
* creator authorization is enforced through project contracts;
* dashboard works;
* creator content management works;
* pagination works;
* upload-session integration works where supported;
* upload progress works;
* resumable uploads work where supported;
* cancellation works where supported;
* upload failures are recoverable;
* media-processing states are represented correctly;
* video metadata editing works;
* thumbnail management works where supported;
* caption metadata management works where supported;
* playlist assignment works;
* visibility management works;
* scheduling works where supported;
* timezone behavior is correct;
* publication state is authoritative;
* channel customization works where supported;
* creator analytics work where supported;
* date-range handling works;
* charts are accessible;
* audience/privacy thresholds are respected;
* creator data is isolated by account/channel;
* mutation races are prevented;
* unsaved changes are handled correctly;
* authentication/session expiration is handled safely;
* responsive behavior works;
* accessibility requirements are implemented;
* security/privacy requirements are respected;
* analytics telemetry is implemented safely;
* tests cover the defined behavior;
* documentation is updated;
* no fake production behavior remains;
* no current-scope placeholders remain;
* validation passes.

---

# 72. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize the Creator Studio, upload-management, content-management, channel-management, and analytics functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List creator authorization, upload-session, media-processing, video metadata, thumbnail, caption, playlist, scheduling, channel-management, analytics, and telemetry contracts consumed.

### State and Caching

Summarize creator-specific cache isolation, upload state, mutation sequencing, version/conflict handling, and account switching.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, production build, upload/content-management validation, and analytics validation.

### Integration Notes

Identify material backend/media-storage assumptions, browser capabilities, or external dependencies.

### Out of Scope

Confirm that media-processing workers, object storage, backend analytics aggregation, live streaming, monetization, moderation, mobile, and administration were not improperly implemented.

---

# 73. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe Creator Studio.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate backend, upload, media-processing, or analytics behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web Creator Studio, content-management, upload-management, channel-management, and creator-analytics experience** that can be integrated with the independently generated backend, media platform, and infrastructure through explicit contracts.
