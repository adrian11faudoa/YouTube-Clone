# YouTube-Style Video Platform — Frontend Prompt — Volume 8

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web live-streaming viewer experience, live chat, creator live-stream management interface, stream-status monitoring, and live-event interaction experience** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

- live-stream discovery and entry points where supported;
- live-stream watch pages;
- live playback integration;
- live-stream status and lifecycle presentation;
- realtime live chat;
- chat moderation controls available to authorized users;
- live viewer interactions;
- creator live-stream setup;
- scheduling and stream configuration where supported;
- stream health and connection status presentation;
- live-stream start/stop controls through the canonical backend contract;
- live viewer counts and live analytics where supported;
- live-to-video-on-demand transition;
- responsive behavior;
- accessibility;
- security and privacy;
- observability and telemetry;
- automated testing;
- documentation.

Do not implement unrelated frontend domains.

Do not implement backend live-stream infrastructure, ingest servers, media processing, live-chat services, or event delivery infrastructure.

Do not fabricate backend or provider behavior.

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
- personalized discovery;
- search;
- notifications;
- creator analytics;
- live streaming;
- realtime live chat;
- moderation;
- administration;
- monetization-capable architecture;
- web and mobile clients.

The web technology direction is:

- TypeScript;
- React;
- Next.js App Router;
- responsive web;
- typed API clients;
- production server/client state management;
- browser media APIs;
- established realtime communication contracts;
- accessibility;
- observability;
- automated testing.

Live streaming introduces real-time behavior, changing lifecycle states, high-frequency events, and unpredictable network conditions. The interface must handle these without compromising playback, chat correctness, or the rest of the application.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- earlier frontend prompts;
- hidden architectural decisions;
- undocumented APIs;
- undocumented WebSocket protocols;
- hidden generated files.

If a repository is available, inspect it before modifying it.

If portable architecture, API, live-streaming, media, or realtime contracts are supplied, use those contracts as authoritative.

If those artifacts are unavailable, follow the explicit requirements in this prompt and inspect the repository for currently implemented interfaces. Do not invent incompatible contracts to compensate for missing functionality.

Preserve compatible existing behavior.

---

# 4. Primary Objective

Implement a real production web experience for viewers and creators participating in live streams.

The completed scope must allow an authorized user to:

1. discover or open a live stream through supported entry points;
2. distinguish scheduled, upcoming, live, ended, and unavailable streams;
3. watch a live stream using the project's playback architecture;
4. view live-stream metadata;
5. interact with live chat;
6. receive and send chat messages where authorized;
7. handle reconnects and temporary network failures;
8. see live viewer information where supported;
9. use available chat moderation controls according to permissions;
10. schedule a live stream where supported;
11. configure a live-stream session where supported;
12. monitor stream readiness and status;
13. start or stop a stream using real backend operations;
14. recover from supported stream or connection failures;
15. transition to archived video content where available;
16. use the experience responsively and accessibly;
17. generate appropriate live-stream telemetry without exposing sensitive information.

---

# 5. Explicit Scope

Implement:

- live-stream viewing route;
- live-stream metadata;
- lifecycle-state presentation;
- live playback integration;
- live buffering/error behavior;
- live-stream reconnection presentation;
- live chat;
- chat pagination/history initialization where supported;
- chat message composition;
- realtime chat updates;
- chat rate-limit handling;
- chat permissions;
- chat moderation controls;
- scheduled-stream presentation;
- creator live-stream setup UI;
- creator stream configuration UI;
- stream readiness/status presentation;
- start/stop control integration;
- live-session monitoring;
- live analytics display where supported;
- live viewer count display where supported;
- ended-stream behavior;
- archive/VOD navigation;
- responsive behavior;
- accessibility;
- security and privacy;
- state and cache management;
- observability and telemetry;
- automated tests;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- live ingest servers;
- RTMP ingest infrastructure;
- media transcoding workers;
- HLS/DASH packaging services;
- CDN infrastructure;
- backend live-stream orchestration;
- backend live-chat persistence;
- realtime message brokers;
- WebSocket gateways;
- backend chat moderation engines;
- recommendation ranking;
- notification delivery infrastructure;
- payment processing;
- live gifting or monetization unless a separately defined existing contract explicitly makes a narrow interaction necessary;
- mobile live-streaming applications;
- administrative moderation dashboards;
- backend analytics aggregation.

Do not redesign backend contracts merely to simplify frontend implementation.

Do not use fake streams, fake viewers, fake chat messages, or fake provider results in production paths.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. identify the web application and route conventions;
3. inspect the existing video-player architecture;
4. inspect media-source integration;
5. inspect authentication and session handling;
6. inspect existing realtime client infrastructure;
7. inspect WebSocket or server-sent-event contracts where present;
8. inspect notification and analytics conventions;
9. inspect creator authorization;
10. inspect existing creator-tooling components;
11. inspect API-client and error-handling conventions;
12. inspect shared dialogs, forms, menus, and design-system components;
13. inspect existing live-streaming functionality;
14. inspect test infrastructure.

Reuse compatible components and libraries.

Do not introduce a second media engine, realtime transport layer, or authentication system without a justified architectural reason.

---

# 8. Live-Stream Route

Implement a canonical live-stream viewing route compatible with the project's routing conventions.

A conceptual route may be:

```text
/watch?v={videoId}
```

or a dedicated live route if the product architecture defines one.

The URL must identify the canonical live-stream entity or the canonical video identity used by the backend.

Support:

- direct navigation;
- browser refresh;
- deep links;
- back/forward navigation;
- authenticated viewers;
- anonymous viewers where allowed;
- scheduled streams;
- live streams;
- ended streams;
- unavailable streams;
- restricted streams.

Do not depend exclusively on transient client-side navigation state to identify the stream.

---

# 9. Live-Stream Domain Contract

Consume the project's canonical live-stream model.

A conceptual representation may contain:

```text
streamId
videoId
channelId
title
description
thumbnail
lifecycleState
scheduledAt
actualStartedAt
actualEndedAt
visibility
playbackAvailability
chatAvailability
viewerCount
streamHealth
archiveVideoId
viewerPermissions
creatorPermissions
```

Use the authoritative property names when actual project contracts are supplied.

Do not create a parallel live-stream entity.

Do not assume all optional fields are available.

---

# 10. Live Lifecycle States

Render the canonical lifecycle states defined by the backend.

Potential states include:

```text
draft
scheduled
preparing
ready
live
ending
ended
failed
cancelled
unavailable
```

Only expose states supported by the actual contract.

The frontend must distinguish:

- a stream that has not started;
- a stream that is preparing;
- a stream currently live;
- a stream that has ended;
- a stream that has failed;
- a stream that the viewer cannot access.

Do not infer that a stream is live merely because a stream page exists.

Do not use client-side timers to fabricate authoritative lifecycle transitions.

---

# 11. Live Watch-Page Layout

Implement a responsive live-stream watch layout.

### Primary content

- live video player;
- live indicator;
- stream title;
- channel identity;
- subscription control where supported;
- stream description;
- live-viewer information where supplied;
- relevant stream metadata;
- available viewer interactions.

### Secondary content

- live chat;
- related live streams or videos where supplied;
- additional stream information.

At desktop widths, playback and chat should work together without excessive layout shifts.

On narrow screens, the layout must rearrange naturally while preserving access to playback and chat.

Do not make chat loading a prerequisite for video playback.

---

# 12. Live Playback Integration

Integrate with the project's canonical media-playback contract.

The player must consume the source, manifest, or playback authorization supplied by the appropriate backend interface.

The implementation must support the project's defined live-media formats, such as HLS or DASH where applicable.

Requirements:

- live manifest loading;
- playback authorization;
- buffering;
- stalled playback;
- live-edge handling;
- retryable network failures;
- terminal media failures;
- source expiration where applicable;
- stream-ended behavior.

Reuse the established player architecture when compatible.

Do not create a second independent player engine.

Do not implement media protocol parsers in the frontend.

---

# 13. Live-Edge Behavior

The player must handle the distinction between:

- the live edge;
- a viewer temporarily behind the live edge;
- supported DVR or time-shift playback;
- streams that do not permit seeking.

Implement live-edge controls only when supported by the stream.

When DVR is supported:

- distinguish live position from historical playback;
- provide an appropriate way to return to the live edge;
- respect server-defined seekability.

Do not claim that a viewer is watching live merely because the stream is playing.

---

# 14. Live Playback Controls

Use the existing player controls wherever appropriate.

Adapt the experience for live media:

- play/pause when supported;
- volume;
- mute;
- fullscreen;
- captions when available;
- quality selection when available;
- live-edge indicator;
- seek controls only when supported;
- return-to-live action where DVR exists;
- Picture-in-Picture where supported.

Do not expose VOD-only controls for streams that cannot support them.

---

# 15. Stream Buffering and Network Status

Handle:

- initial connection;
- buffering;
- temporary stall;
- network disconnection;
- recovery;
- authorization expiration;
- media failure.

Display understandable status information without exposing internal player diagnostics.

Do not permanently replace the player with a generic error screen for recoverable failures.

Avoid retry loops that amplify service outages.

---

# 16. Live Playback Reconnection

Implement reconnection behavior according to the playback contract and existing media engine.

The experience must:

- distinguish transient network issues from terminal failures;
- avoid duplicate player instances;
- stop retries when the viewer leaves the page;
- avoid endlessly recreating media sources;
- update status after recovery;
- clean up timers and listeners.

Do not fabricate successful playback when reconnection fails.

---

# 17. Live Metadata

Display contract-provided stream metadata, such as:

- title;
- description;
- channel;
- scheduled start time;
- actual start time;
- live status;
- viewer count;
- thumbnail;
- archive availability.

Do not assume every stream has every field.

Use a canonical timestamp model.

Display time zones appropriately for scheduled streams.

---

# 18. Live Viewer Count

If the backend supplies a live viewer count, display it according to the product design.

The frontend must:

- use the authoritative returned count;
- handle delayed or unavailable values;
- avoid arbitrary client-side increments;
- avoid assuming an exact real-time count;
- prevent duplicate realtime updates from causing incorrect state.

If the count is approximate, do not label it as exact.

Do not simulate viewer activity.

---

# 19. Live Status Refresh

If lifecycle changes are delivered through realtime events, consume the canonical event contract.

If the project uses polling, follow its defined polling strategy.

The implementation must:

- update status without requiring a page refresh;
- stop subscriptions/polling when no longer relevant;
- deduplicate repeated status events;
- handle reconnects;
- prevent stale status responses from replacing newer state.

Do not use uncontrolled high-frequency polling.

---

# 20. Live Chat Architecture

Implement a reusable live-chat component system.

A conceptual structure may be:

```text
LiveChat
  ├── LiveChatHeader
  ├── LiveChatHistory
  ├── LiveChatMessageList
  ├── LiveChatComposer
  ├── LiveChatConnectionState
  └── LiveChatModerationActions
```

Keep separate responsibilities for:

- realtime transport integration;
- message normalization;
- client state;
- rendering;
- message submission;
- moderation actions;
- telemetry.

Use the existing realtime client if the project has one.

Do not create a parallel WebSocket system.

---

# 21. Live-Chat Contract

Use the project's canonical live-chat message contract.

A conceptual message may contain:

```text
messageId
streamId
authorId
authorDisplayName
authorAvatar
messageText
createdAt
messageType
moderationState
viewerPermissions
```

Use exact contract fields when supplied.

Do not invent message identifiers, timestamps, moderation states, or permissions in production code.

---

# 22. Initial Chat History

Load initial chat content according to the backend contract.

Support:

- initial loading;
- empty history;
- unavailable chat;
- restricted chat;
- historical message retrieval where supported;
- reconnect recovery.

Do not fetch unbounded chat history.

Use the project's pagination or initialization strategy.

Do not display stale messages from a previously opened stream.

---

# 23. Realtime Chat Connection

Connect using the established realtime contract.

The client must handle:

- connecting;
- connected;
- disconnected;
- reconnecting;
- failed;
- intentionally closed.

The UI must distinguish a disconnected state from an empty chat.

Do not display the same connection error repeatedly for every reconnect attempt.

---

# 24. Chat Message Ordering

Respect the canonical message-ordering rules.

Use server-provided message IDs and timestamps where appropriate.

The frontend must handle:

- concurrent messages;
- duplicate delivery;
- reconnect replay;
- delayed messages;
- historical messages;
- messages arriving during pagination.

Deduplicate by canonical message identity or the project's explicit event/message deduplication contract.

Do not reorder messages arbitrarily using client arrival time when the backend defines authoritative ordering.

---

# 25. Chat Message Rendering

Render messages safely and efficiently.

Support:

- author identity;
- message content;
- message timestamp where appropriate;
- supported message types;
- moderation/deletion state;
- permitted actions.

Treat all message content as untrusted.

Do not render arbitrary message HTML.

Only implement rich content such as links, emojis, badges, or special messages when the project contract supports it.

---

# 26. Chat Composer

Implement a live-chat composer.

Support:

- authenticated and anonymous state;
- input validation;
- character limits;
- send action;
- pending state;
- successful reconciliation;
- failure feedback;
- rate-limit feedback.

Use limits defined by the backend/product contract.

Do not send messages when chat is disabled or the viewer lacks permission.

Do not submit duplicate messages because a user double-clicked or pressed Enter repeatedly.

---

# 27. Chat Submission

Sending a message must:

1. validate input;
2. verify client-side eligibility where supported;
3. submit through the canonical contract;
4. show an appropriate pending state;
5. reconcile with server-confirmed output;
6. handle failure;
7. preserve usable input after recoverable failures.

Do not generate authoritative production message IDs or pretend a message has been accepted before the contract confirms success.

---

# 28. Optimistic Chat Messages

Optimistic rendering may be used only when it is safely reconciled.

If used:

- mark the message as pending;
- distinguish temporary client state from server-confirmed state;
- replace it with the authoritative server representation;
- remove or mark failure after a rejected submission;
- prevent duplicate copies when the realtime echo arrives.

Do not leave rejected messages looking successfully sent.

---

# 29. Rate Limits and Chat Restrictions

Respect backend-provided constraints, including:

- message rate limits;
- slow mode;
- chat disabled;
- subscribers-only mode;
- members-only or other restricted modes where actually supported;
- viewer-specific restrictions.

Only expose moderation/chat modes defined by the project contract.

Do not implement restriction enforcement exclusively in the client.

---

# 30. Chat Input State

The chat composer must reflect actual permissions and availability.

Potential states include:

- signed out;
- connected and allowed;
- sending;
- slow mode;
- temporarily rate limited;
- chat disabled;
- account restricted;
- stream ended;
- connection unavailable.

Do not leave an apparently enabled send button when submission is impossible.

If the network disconnects, handle draft text deliberately rather than silently discarding it.

---

# 31. Chat Scrolling

Implement chat scrolling that respects viewer behavior.

When new messages arrive:

- follow the bottom only when the viewer is already following live chat;
- do not forcibly scroll the viewer away from older messages they are reading;
- indicate that new messages have arrived when appropriate;
- restore bottom-follow behavior on explicit user action.

Prevent excessive scroll work for every incoming message.

---

# 32. Large Chat Volumes

Live chat can generate substantial message volume.

The implementation must prevent uncontrolled DOM growth.

Use a deliberate bounded-history strategy and, where necessary, list virtualization compatible with:

- scroll position;
- accessibility;
- reconnect handling;
- historical message browsing;
- focus behavior.

Do not retain every message from a long stream indefinitely in browser memory.

---

# 33. Chat Moderation Controls

Expose moderation controls only to authorized users.

Where the contract supports them, potential controls include:

- remove a message;
- timeout/restrict a user;
- block a viewer;
- report a message;
- manage restricted chat participants.

Use the project's canonical permissions and moderation action contracts.

Do not expose moderator actions to normal viewers.

Do not invent enforcement durations or restriction semantics.

---

# 34. Chat Message Removal

When a message is removed or deleted:

- use the authoritative event or mutation response;
- update the correct message;
- reconcile duplicate events;
- avoid removing unrelated messages;
- retain a moderation placeholder only when the product contract requires one.

Do not treat message removal as equivalent to deleting every message from the same author.

---

# 35. Live-Chat Reporting

Where supported, provide a reporting interaction.

Support:

- report entry;
- category/reason selection;
- required confirmation;
- loading;
- success;
- failure.

Use the canonical report contract.

Do not display internal review or enforcement information.

---

# 36. Viewer Blocking

Where blocking is available in live chat:

- expose the action only when authorized;
- submit through the canonical backend contract;
- update affected visible state according to server results;
- handle failures;
- prevent duplicate requests.

Do not invent the consequences of blocking a viewer.

Do not assume that blocking one participant automatically removes all historical messages unless the contract defines that behavior.

---

# 37. Chat Accessibility

Live chat must support:

- keyboard-accessible message input;
- accessible send controls;
- screen-reader labels;
- visible focus;
- accessible moderation menus;
- meaningful connection-status announcements.

Do not announce every incoming message through an unrestricted live region at a rate that makes the page unusable for assistive-technology users.

Use a carefully designed accessibility strategy for high-frequency updates.

---

# 38. Creator Live-Stream Setup

Implement a creator-facing interface for creating or configuring a live stream where the backend contract supports it.

Potential fields include:

- title;
- description;
- thumbnail;
- visibility;
- scheduled time;
- chat availability;
- supported audience/settings;
- playlist assignment where supported.

Only expose fields provided by the authoritative contract.

Use the existing Creator Studio shell where compatible.

Do not duplicate the full creator dashboard.

---

# 39. Creator Live-Stream Schedule

Support scheduling where the backend contract provides the capability.

The UI must:

- validate scheduling fields;
- use canonical timestamps;
- display time zones correctly;
- create or update the scheduled stream through the canonical API;
- display the resulting schedule;
- handle rescheduling/cancellation only where supported.

Do not fabricate a scheduled stream locally.

---

# 40. Stream Readiness and Status

Where creator stream readiness is available, display the actual backend-provided status.

Potential information includes:

- not ready;
- awaiting ingest;
- preparing;
- ready;
- live;
- interrupted;
- ended;
- failed.

Only display contract-defined states.

If readiness depends on an external ingest provider, do not simulate provider success.

---

# 41. Stream Ingest Configuration

If the project exposes creator-side ingest configuration, integrate through the canonical API.

Handle credentials or stream keys as highly sensitive values.

The interface must:

- display secrets only when the backend explicitly permits it;
- avoid including secrets in URLs;
- avoid logging secrets;
- avoid sending secrets to analytics;
- avoid persisting them unnecessarily in browser storage;
- provide appropriate copy/reveal controls where supported.

Never generate fake ingest credentials or fabricate an ingest endpoint.

---

# 42. Creator Start/Stop Controls

Where the backend contract provides explicit start/stop actions:

- expose them only when the creator is authorized;
- confirm destructive or disruptive actions where appropriate;
- prevent duplicate conflicting requests;
- show pending state;
- reconcile the authoritative lifecycle response;
- handle failures.

Do not pretend the stream has started because the user clicked a button.

The backend's confirmed state is authoritative.

---

# 43. Stream Health Monitoring

Where supported, display real stream-health information.

Potential indicators include:

- ingest status;
- connection state;
- processing state;
- warnings;
- errors;
- last update time.

Do not invent bitrate, frame rate, dropped-frame counts, or other metrics when the backend does not provide them.

Use clear severity labels.

Avoid flooding creators with repeated identical warnings.

---

# 44. Creator Live-Chat Settings

Where supported, allow an authorized creator to configure live-chat settings such as:

- enable/disable chat;
- supported audience restrictions;
- slow mode;
- other backend-defined moderation controls.

Use only settings exposed by the canonical contract.

The backend remains authoritative for restrictions.

Changing settings must show pending state and reconcile the server result.

---

# 45. Live Analytics

If live analytics are available to the creator, display authoritative contract-provided values.

Potential metrics include:

- concurrent viewers;
- peak concurrent viewers;
- chat activity;
- stream duration;
- stream-health events;
- available watch-time or performance metrics.

Do not compute official analytics from incomplete frontend events.

Do not claim real-time accuracy when the backend supplies delayed aggregates.

---

# 46. Live-Stream Notifications

Where the project provides notification events for scheduled/started live streams, expose only the appropriate existing interactions.

This scope does not implement notification delivery infrastructure.

Do not create a parallel notification system.

Use the existing notification preferences and canonical APIs if a creator or viewer can manage notifications from the live experience.

---

# 47. Stream End and Archive Transition

When a stream ends:

- display the confirmed ended state;
- stop inappropriate live-chat submissions;
- preserve applicable historical chat presentation only where supported;
- offer the archived video when the backend provides it;
- distinguish archive processing from archive availability.

Do not assume every live stream produces an archive.

Do not redirect to a nonexistent video.

---

# 48. Live Page Navigation

Navigation between streams must prevent stale state.

When changing streams:

- dispose the previous player properly;
- close the previous realtime connection;
- stop stale polling;
- clear stream-specific pending composer state where appropriate;
- reset the current stream's message history;
- load the new stream;
- associate telemetry with the correct stream.

Do not allow messages from stream A to appear in stream B.

---

# 49. Connection Lifecycle and Cleanup

Clean up:

- WebSocket/event subscriptions;
- reconnect timers;
- polling intervals;
- media listeners;
- abort controllers;
- pending telemetry;
- temporary upload/resource state;
- visibility listeners;
- chat observers;
- stream-specific event handlers.

When the viewer leaves or the stream changes, resources belonging to the old stream must be released.

Repeated navigation between streams must not cause unbounded connection or memory growth.

---

# 50. Cache and State Management

Use the project's established server-state system.

Separate:

### Server state

- live-stream metadata;
- lifecycle state;
- creator settings;
- playback authorization;
- live analytics;
- initial chat history;
- viewer permissions.

### Realtime state

- chat messages;
- lifecycle events;
- viewer counts;
- connection state.

### Local UI state

- chat draft;
- open menus;
- pending actions;
- confirmation dialogs.

Use stream ID and other necessary context in cache keys.

Never reuse one stream's state for another stream.

---

# 51. Reconnect Reconciliation

After realtime reconnection:

- re-establish the canonical connection;
- reconcile missed messages through the defined history/sync mechanism;
- deduplicate replayed messages;
- refresh authoritative lifecycle state when required;
- avoid duplicate event handlers;
- surface persistent connection failure.

Do not assume a reopened WebSocket automatically restores messages that arrived while disconnected.

Do not invent event-replay guarantees that the transport does not provide.

---

# 52. High-Frequency Update Handling

Live systems may generate high-frequency state updates.

Use batching/throttling where appropriate for:

- viewer counts;
- connection status;
- telemetry;
- chat rendering;
- health indicators.

Do not run a complete page rerender for every incoming chat message or metric.

Preserve message correctness while optimizing rendering.

---

# 53. Security

The frontend must:

- use secure authentication mechanisms;
- respect server-side authorization;
- protect ingest credentials and stream keys;
- avoid logging tokens or signed URLs;
- safely render chat content;
- validate navigation targets;
- avoid open redirects;
- avoid unsafe HTML injection;
- prevent unauthorized stream-control actions;
- avoid exposing private stream metadata;
- follow the project's CSRF/session conventions where applicable.

Do not treat client-side permission checks as security boundaries.

---

# 54. Privacy

Live chat and live viewing behavior can expose sensitive information.

Do not unnecessarily expose:

- private participant details;
- internal moderation metadata;
- stream keys;
- provider credentials;
- internal stream identifiers not intended for viewers;
- private creator analytics.

Do not send raw chat text to analytics unless explicitly authorized by the project's privacy contract.

Use only viewer information intended for display.

---

# 55. Rate Limits and Backpressure

The interface must cooperate with server rate limits.

Handle:

- chat send limits;
- moderation-action limits;
- stream-control limits;
- realtime connection failures.

Avoid retry storms.

Do not resend a chat message repeatedly merely because an acknowledgement was delayed.

If backend backpressure or temporary unavailability is signaled, present an understandable status and recover according to the canonical contract.

---

# 56. Observability

Instrument live-stream frontend failures and important transitions.

Relevant signals may include:

- player initialization failure;
- live playback start failure;
- live playback recovery;
- realtime connection failure;
- chat send failure;
- duplicate message suppression;
- repeated connection churn;
- creator stream-control failure.

Use the project's telemetry conventions.

Do not include:

- stream keys;
- access tokens;
- signed URLs;
- raw chat text;
- unnecessary personal information.

---

# 57. Analytics and Telemetry

Use canonical project event names where available.

Potential events include:

```text
live_stream_opened
live_playback_started
live_playback_failed
live_playback_recovered
live_stream_ended
live_archive_opened
live_chat_opened
live_chat_message_sent
live_chat_send_failed
live_chat_connection_lost
live_chat_connection_restored
live_chat_moderation_action
live_stream_scheduled
live_stream_configuration_updated
live_stream_start_requested
live_stream_stop_requested
live_stream_health_warning_viewed
live_analytics_viewed
```

Do not emit duplicate events because of reconnects, remounts, or repeated backend delivery.

Separate user actions from confirmed server outcomes.

---

# 58. Accessibility

Implement:

- semantic live-stream headings;
- accessible player controls;
- keyboard-accessible chat;
- accessible chat action menus;
- meaningful connection-state announcements;
- accessible creator controls;
- accessible scheduling forms;
- accessible status indicators;
- visible focus;
- screen-reader-compatible errors and confirmations.

Do not announce every high-frequency viewer-count update.

Do not rely on color alone to indicate stream health or live status.

---

# 59. Responsive Behavior

Support:

- mobile web;
- tablet;
- desktop;
- large desktop.

On desktop, playback and chat may occupy adjacent regions.

On smaller screens:

- playback must remain prominent;
- chat must remain accessible;
- composer controls must accommodate mobile keyboards;
- menus must fit the viewport;
- metadata must wrap correctly;
- critical stream-status information must remain visible.

Do not require desktop-only functionality to start or monitor a supported live stream.

---

# 60. Performance

Optimize:

- live-player initialization;
- initial watch-page rendering;
- realtime connection setup;
- chat message rendering;
- message-history retention;
- creator status updates;
- high-frequency analytics updates.

Do not download unlimited chat history.

Do not poll every few hundred milliseconds without an explicit technical requirement.

Do not rerender the entire page for a chat-state change.

Do not create new player or socket instances during ordinary React renders.

---

# 61. Error Isolation

Failures must be isolated where possible.

Examples:

```text
Live chat disconnected
Video playback continues
```

```text
Live analytics unavailable
Creator stream status remains usable
```

```text
Archive processing delayed
Ended-stream status remains correct
```

```text
Viewer count unavailable
Live playback remains functional
```

Do not make nonessential live features block core playback.

---

# 62. Testing Strategy

Implement automated tests for actual behavior.

### Unit tests

Cover:

- lifecycle-state mapping;
- playback-state mapping;
- chat message normalization;
- message deduplication;
- realtime reconnect state;
- rate-limit handling;
- stream-specific cache keys;
- permissions;
- telemetry construction;
- cleanup utilities;
- live/archive transition logic.

### Component tests

Cover:

- live-stream header;
- live indicator;
- live player wrapper;
- connection-status component;
- chat composer;
- message list;
- moderation menu;
- creator scheduling form;
- start/stop controls;
- stream-health indicators;
- archive state.

### Integration tests

Cover:

- live-stream metadata loading;
- playback-source initialization;
- live lifecycle updates;
- chat initialization;
- realtime message delivery;
- message submission;
- duplicate-message suppression;
- reconnect reconciliation;
- rate-limit feedback;
- moderation permissions;
- creator stream creation/configuration;
- start/stop operations;
- archive navigation.

### End-to-end tests

At minimum:

1. open a public live stream;
2. verify live-status presentation;
3. initialize live playback;
4. open chat;
5. receive a chat message;
6. send a message when authorized;
7. verify duplicate-delivery handling;
8. simulate a realtime disconnect;
9. verify reconnect behavior;
10. verify chat failure does not break playback;
11. open a scheduled stream;
12. verify correct pre-live state;
13. access creator live controls as an authorized creator;
14. verify unauthorized users cannot control a stream;
15. end a stream and verify archive behavior where available;
16. verify keyboard accessibility of chat and player controls.

Use real integration boundaries in the application and controlled mocks only in tests.

---

# 63. Browser Compatibility

Validate the project's supported browser matrix.

Pay particular attention to:

- HLS/DASH browser differences;
- fullscreen behavior;
- media autoplay restrictions;
- mobile keyboard behavior;
- realtime connection lifecycle;
- Picture-in-Picture where supported;
- network changes;
- page visibility changes.

Use feature detection for optional browser APIs.

Do not assume every browser supports identical live-media features.

---

# 64. Documentation

Update documentation covering:

- live-stream route conventions;
- lifecycle-state mapping;
- live playback integration;
- chat transport contract;
- chat message contract;
- reconnect/reconciliation behavior;
- rate-limit behavior;
- creator stream controls;
- scheduling/timezone behavior;
- stream health;
- archive transition;
- security/privacy considerations;
- telemetry;
- accessibility;
- testing strategy.

Documentation must reflect the actual implementation.

---

# 65. No Fake Live-Stream Behavior

Do not create:

- fake live streams;
- fabricated viewer counts;
- fake playback URLs;
- fake realtime messages;
- simulated chat persistence;
- fake ingest readiness;
- fabricated stream health;
- fake start/stop success;
- artificial archive availability.

Mocks are allowed only within automated tests.

The production application must use the actual project contracts.

---

# 66. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- empty chat submission handlers;
- fake reconnect success;
- nonfunctional creator controls;
- fake processing states;
- incomplete resource cleanup;
- missing rate-limit handling;
- unfinished error states;
- “implement later” sections.

Everything within the current scope must be genuinely implemented.

---

# 67. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- production build;
- live playback integration;
- stream lifecycle handling;
- chat send/receive behavior;
- realtime reconnection;
- message deduplication;
- permission enforcement at the UI boundary;
- creator scheduling/control integration;
- archive transition;
- cleanup after navigation;
- responsive behavior;
- accessibility-critical interactions;
- security/privacy handling.

Fix issues discovered within this scope rather than merely reporting them.

Do not claim that external ingest infrastructure or live streaming has been provisioned unless that was actually verified.

---

# 68. Definition of Done

This prompt is complete only when:

- live-stream routing works;
- lifecycle states render correctly;
- live playback uses real media contracts;
- player controls reflect supported live capabilities;
- buffering/reconnection states work;
- stream metadata works;
- viewer counts are handled correctly where supported;
- live status updates work;
- chat initializes correctly;
- chat submission works;
- realtime updates work;
- duplicate chat messages are prevented;
- reconnect reconciliation works;
- chat rate limits are handled;
- chat permissions are respected;
- moderation controls are permission-aware;
- scheduled-stream UI works where supported;
- creator live configuration works where supported;
- start/stop controls use real contracts where supported;
- stream-health information is accurate where supported;
- ended-stream and archive states work;
- resources are cleaned up correctly;
- account/stream state is isolated;
- responsive behavior works;
- accessibility requirements are implemented;
- security and privacy requirements are respected;
- telemetry is implemented appropriately;
- tests cover the defined behavior;
- documentation is updated;
- no fake production functionality remains;
- no current-scope placeholders remain;
- validation passes.

---

# 69. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize the live-stream viewer experience, chat, creator controls, stream-status handling, and archive transition actually completed.

### Files

List significant files created, modified, or deleted.

### API and Realtime Contracts

List live-stream, playback, chat, moderation, creator-control, analytics, and realtime contracts consumed.

### State and Connections

Summarize player integration, realtime connection management, message deduplication, reconnect handling, cache isolation, and cleanup.

### Testing

List tests created and tests executed.

### Validation

Report type checking, linting, production build, runtime validation, and relevant browser checks.

### Integration Notes

Identify material backend/provider assumptions, browser limitations, missing external configuration, or dependencies that need integration by another project part.

### Out of Scope

Confirm that ingest infrastructure, transcoding, CDN, backend chat, realtime gateways, monetization, administration, and mobile applications were not improperly implemented.

---

# 70. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe the live-streaming experience.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate playback, chat, stream health, ingest, or backend behavior.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web live-streaming, live-chat, and creator live-management experience** that can be integrated with the independently generated backend, media platform, realtime infrastructure, and other project components through explicit contracts.
