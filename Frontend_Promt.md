Using the Master Prompt above and the approved:

Architecture Prompt Volume 1
Architecture Prompt Volume 2
Backend implementation completed so far
Existing Project Index

Begin the frontend and mobile implementation phase.

Do NOT restart or regenerate the architecture.

Do NOT regenerate completed backend files.

Use the approved architecture, API contracts, event contracts, authorization model, and existing Project Index as the source of truth.

────────────────────────────────────────

IMPLEMENTATION OBJECTIVE

Build the complete production-ready frontend ecosystem for the enterprise-scale global video platform.

Implement:

1. Web Application
2. Mobile Application
3. Creator Studio / Creator Dashboard
4. Administration frontend boundaries where approved

The applications must integrate with the implemented backend APIs and approved real-time architecture.

Do not use mock APIs.

Do not use placeholder implementations.

Do not invent backend contracts that conflict with the approved architecture.

If a required backend capability is missing:

1. Identify the missing contract.
2. Implement the required backend change only if necessary.
3. Maintain backward compatibility.
4. Update the Project Index.

────────────────────────────────────────

WEB TECHNOLOGY STACK

Use:

• Next.js
• React
• TypeScript
• Strict TypeScript
• Tailwind CSS

Use the architecture-approved libraries for:

• Data fetching
• Server state
• Client state
• Forms
• Validation
• Authentication
• Video playback
• Testing

Prefer:

• Server Components where appropriate.
• Client Components only where interactivity requires them.
• Route-level code splitting.
• Lazy loading for expensive client features.
• Optimized images.
• Streaming and Suspense where appropriate.

Do not make the entire application client-rendered unnecessarily.

────────────────────────────────────────

MOBILE TECHNOLOGY STACK

Use:

• React Native
• Expo
• TypeScript

Use appropriate production-ready libraries for:

• Navigation
• Server state
• Local state
• Secure storage
• Push notifications
• Deep linking
• Media playback
• Offline storage
• Background synchronization

Support:

• iOS
• Android

────────────────────────────────────────

APPLICATION STRUCTURE

Implement the frontend according to the approved monorepo architecture.

Maintain clear boundaries between:

• Web application
• Mobile application
• Shared UI primitives where appropriate
• Shared API contracts
• Shared TypeScript types
• Shared validation schemas where appropriate
• Shared design tokens
• Shared utilities

Do not place platform-specific UI logic into a generic shared package.

Only share code when the abstraction is genuinely reusable.

────────────────────────────────────────

DESIGN SYSTEM

Create a production-ready design system.

Implement:

• Design tokens
• Typography
• Spacing
• Layout rules
• Responsive breakpoints
• Color system
• Dark mode
• Light mode
• Elevation
• Borders
• Radius
• Motion guidelines
• Focus states
• Disabled states
• Loading states
• Error states
• Empty states

Create reusable UI primitives such as:

• Button
• IconButton
• Input
• Textarea
• Select
• Checkbox
• Radio
• Switch
• Modal
• Dialog
• Dropdown
• Tooltip
• Popover
• Tabs
• Menu
• Avatar
• Badge
• Chip
• Card
• Skeleton
• Spinner
• Progress
• Toast
• Pagination
• Infinite scroll states

The design must prioritize:

• Accessibility
• Performance
• Consistency
• Keyboard navigation
• Touch targets
• Responsive design

────────────────────────────────────────

WEB APPLICATION INFORMATION ARCHITECTURE

Implement routes and layouts for:

Public:

• Home
• Explore
• Trending
• Categories
• Search
• Video Watch Page
• Channel Pages
• Playlist Pages
• Live Streams

Authenticated:

• Subscription Feed
• Watch Later
• Saved Videos
• Watch History
• Notifications
• User Settings
• Privacy Settings
• Security Settings

Creator:

• Creator Dashboard
• Channel Management
• Video Management
• Upload
• Video Editor Metadata
• Playlists
• Comments Management
• Analytics
• Monetization
• Copyright
• Live Streaming Management

Administration:

• Administration Dashboard
• User Management
• Channel Management
• Video Management
• Moderation
• Reports
• Appeals
• Copyright Administration
• Feature Flags
• Audit Logs

Only expose routes and actions allowed by server-side authorization.

────────────────────────────────────────

GLOBAL WEB LAYOUT

Implement:

• Responsive top navigation
• Desktop sidebar
• Collapsible navigation
• Mobile navigation
• Search entry point
• Notification access
• User menu
• Upload entry point
• Authentication-aware navigation

Support:

• Desktop
• Tablet
• Mobile web

Avoid duplicating layout logic across pages.

────────────────────────────────────────

HOME PAGE

Implement the primary personalized home experience.

Support:

• Personalized recommendations
• Video feed
• Topic filters where approved
• Infinite scrolling
• Skeleton loading
• Empty states
• Error recovery
• Refresh behavior
• Advertisement placement where approved

Implement efficient list rendering and data fetching.

Do not load the entire recommendation feed at once.

────────────────────────────────────────

VIDEO CARD SYSTEM

Create reusable video presentation components.

Support:

• Thumbnail
• Duration
• Title
• Channel
• Channel avatar
• View count
• Publication time
• Live status
• Video status where appropriate
• Context actions
• Responsive variants

Create variants for:

• Standard feed
• Compact list
• Search result
• Channel page
• Playlist
• Creator Studio
• Mobile

────────────────────────────────────────

VIDEO WATCH PAGE

Implement the complete video viewing experience.

Support:

• Video player
• Adaptive streaming
• Playback controls
• Play/pause
• Seeking
• Volume
• Mute
• Fullscreen
• Picture-in-picture where supported
• Playback speed
• Quality selection
• Subtitle selection
• Caption controls
• Audio track selection where supported
• Resume playback
• Playback progress reporting
• Theater mode where appropriate

Also implement:

• Video title
• Channel information
• Subscribe action
• Video description
• Expand/collapse description
• Tags
• Chapters
• Interaction controls
• Save
• Share
• Report
• Comments
• Related content
• Recommended content
• Advertisement presentation where approved

The player must integrate with backend playback authorization.

Do not expose protected media URLs unnecessarily.

────────────────────────────────────────

PLAYBACK STATE

Implement reliable playback state management.

Support:

• Current position
• Duration
• Playback status
• Buffering
• Selected quality
• Playback speed
• Volume
• Subtitle selection
• Resume state

Send playback events efficiently.

Do not send a network request for every tiny playback position change.

Batch or throttle events according to backend contracts.

────────────────────────────────────────

LIVE STREAMING EXPERIENCE

Implement live viewing.

Support:

• Live player
• Live indicator
• Viewer count
• Stream metadata
• Live chat
• Reactions
• Creator information
• Subscribe
• Moderation states
• Stream ended state
• Scheduled stream state
• Countdown where appropriate

Support reconnection and connection recovery.

────────────────────────────────────────

LIVE CHAT

Implement:

• Real-time messages
• Authentication-aware connections
• Reconnection
• Message sending
• Reactions
• Slow mode
• Subscriber-only mode
• Moderator indicators
• Banned user handling
• Deleted messages
• Spam/rate-limit feedback
• Auto-scroll behavior
• New-message indicators

Use the approved WebSocket architecture.

Do not create a separate incompatible real-time protocol.

────────────────────────────────────────

SEARCH EXPERIENCE

Implement:

• Search input
• Autocomplete
• Suggestions
• Recent searches where approved
• Search results
• Video results
• Channel results
• Playlist results
• Live stream results
• Filters
• Sorting
• Pagination or infinite loading
• Loading states
• Empty states
• Error states

Optimize search requests.

Do not issue unnecessary requests for every keystroke.

────────────────────────────────────────

EXPLORE AND DISCOVERY

Implement:

• Trending
• Categories
• Topics
• Popular content
• New releases
• Creator discovery
• Live discovery

Use reusable feed and card components.

────────────────────────────────────────

CHANNEL EXPERIENCE

Implement:

• Channel header
• Avatar
• Banner
• Description
• Links
• Subscribe action
• Subscriber count
• Channel navigation
• Videos
• Shorts or future short-form content boundaries
• Playlists
• Community sections where approved
• About page

Support channel visibility and privacy states.

────────────────────────────────────────

PLAYLIST EXPERIENCE

Implement:

• Playlist pages
• Playlist metadata
• Ordered videos
• Current playback
• Add/remove controls where authorized
• Reordering where authorized
• Playlist management
• Watch Later

────────────────────────────────────────

COMMENTS EXPERIENCE

Implement:

• Comment list
• Pagination
• Replies
• Thread expansion
• Create comment
• Edit
• Delete
• Reactions
• Mentions
• Report
• Pinned comments
• Moderation states

Ensure unauthorized controls are never presented as functional actions.

────────────────────────────────────────

AUTHENTICATION EXPERIENCE

Implement complete authentication flows.

Support:

• Registration
• Login
• Logout
• Email verification
• Password reset
• Password change
• OAuth where implemented
• MFA where implemented
• Passkeys where implemented
• Session management
• Device management
• Account recovery

Implement:

• Form validation
• Loading states
• Error handling
• Secure token/session handling
• Redirect handling
• Protected routes

Do not store sensitive credentials insecurely.

────────────────────────────────────────

USER SETTINGS

Implement:

• Profile settings
• Avatar management
• Account settings
• Privacy settings
• Notification preferences
• Security settings
• Session/device management
• Blocked users
• Muted users
• Watch history controls
• Recommendation/personalization controls where approved
• Data export request flow where implemented
• Account deletion flow where implemented

────────────────────────────────────────

NOTIFICATIONS

Implement:

• Notification center
• Unread counts
• Read/unread states
• Notification preferences
• Deep linking
• Empty states
• Grouping where appropriate

Support:

• New video notifications
• Comments
• Replies
• Subscription activity
• Live stream events
• Moderation actions
• Copyright events
• Security alerts

────────────────────────────────────────

VIDEO UPLOAD EXPERIENCE

Implement a production-ready upload workflow.

Support:

• File selection
• Drag and drop on web
• File validation
• Upload progress
• Multipart upload coordination
• Resumable upload where supported
• Upload cancellation
• Retry
• Recovery
• Upload status
• Processing status

Do not upload large files through an unnecessary frontend proxy.

Integrate directly with the backend-generated object-storage upload authorization.

────────────────────────────────────────

VIDEO METADATA EDITING

Implement creator controls for:

• Title
• Description
• Tags
• Category
• Thumbnail
• Visibility
• Scheduling
• Age restrictions
• Playlist assignment
• Subtitle/caption management
• Chapters
• Publishing

Validate data before submission.

Display backend validation errors correctly.

────────────────────────────────────────

VIDEO PROCESSING STATUS

Implement processing visibility.

Support states including:

• Uploading
• Uploaded
• Validating
• Processing
• Generating renditions
• Generating thumbnails
• Pending review
• Ready
• Published
• Failed
• Restricted

Support polling or approved real-time updates.

Do not create aggressive polling loops.

────────────────────────────────────────

CREATOR STUDIO

Build a production-ready Creator Studio.

Implement:

• Dashboard
• Channel overview
• Video management
• Video status
• Upload management
• Comments management
• Playlist management
• Analytics
• Audience metrics
• Revenue metrics where authorized
• Monetization settings
• Copyright management
• Live streaming management
• Channel team management

Use role and permission-aware interfaces.

────────────────────────────────────────

CREATOR ANALYTICS UI

Implement dashboards for:

• Views
• Watch time
• Audience retention
• Unique viewers
• Subscriber changes
• Traffic sources
• Geographic distribution
• Device distribution
• Revenue where authorized
• Video performance
• Live stream performance

Requirements:

• Date ranges
• Comparison periods where supported
• Loading states
• Empty states
• Error states
• Accessible charts
• Responsive visualization

Do not fabricate analytics data.

────────────────────────────────────────

MONETIZATION EXPERIENCE

Implement approved creator monetization interfaces.

Support:

• Revenue overview
• Revenue history
• Earnings status
• Payout status
• Payment account status
• Monetization eligibility
• Revenue reports

All financial data must come from authorized backend APIs.

────────────────────────────────────────

ADVERTISING EXPERIENCE

Implement approved advertiser and campaign management interfaces.

Support:

• Ad accounts
• Campaigns
• Ad groups
• Creative management
• Targeting
• Budget configuration
• Scheduling
• Campaign status
• Performance metrics

Separate advertiser interfaces from creator interfaces.

────────────────────────────────────────

LIVE CREATOR EXPERIENCE

Implement live stream management.

Support:

• Stream creation
• Stream scheduling
• Stream metadata
• Stream key display using secure interaction patterns
• Stream key rotation
• Stream health
• Stream status
• Viewer metrics
• Live chat moderation
• Stream completion
• VOD management

Never expose sensitive stream credentials unnecessarily.

────────────────────────────────────────

MODERATION INTERFACE

Implement authorized moderation tooling.

Support:

• Moderation queues
• Report review
• Video review
• Comment review
• Channel review
• Enforcement actions
• Restriction actions
• Appeals
• Moderator notes
• Evidence references
• Audit information

Every sensitive action must require confirmation where appropriate.

────────────────────────────────────────

ADMINISTRATION INTERFACE

Implement authorized administration screens.

Support:

• User administration
• Channel administration
• Video administration
• Moderation management
• Copyright management
• Advertising management
• Monetization administration
• Feature flags
• Audit logs
• System configuration where approved

Administrative interfaces must be clearly separated from consumer-facing experiences.

────────────────────────────────────────

MOBILE APPLICATION

Implement the complete React Native application.

Support major user experiences including:

• Home feed
• Video playback
• Search
• Explore
• Channels
• Subscriptions
• Playlists
• Comments
• Notifications
• User profiles
• Authentication
• Settings
• Uploads where approved
• Creator functionality appropriate for mobile
• Live streams
• Live chat

Use native platform capabilities where beneficial.

────────────────────────────────────────

MOBILE NAVIGATION

Implement appropriate navigation architecture.

Support:

• Tab navigation
• Stack navigation
• Deep links
• Authentication flows
• Modal flows
• Back navigation
• Universal links
• App links

Navigation state must remain predictable and typed.

────────────────────────────────────────

MOBILE VIDEO PLAYER

Implement production-ready video playback.

Support:

• Adaptive streaming
• HLS
• Playback controls
• Fullscreen
• Picture-in-picture where supported
• Background behavior according to platform policy
• Playback progress
• Resume playback
• Quality behavior according to available platform capabilities

Optimize memory and resource management.

────────────────────────────────────────

MOBILE OFFLINE SUPPORT

Implement approved offline capabilities.

Support:

• Cached metadata
• Recently viewed content
• Network status awareness
• Retry behavior
• Pending user actions where appropriate
• Synchronization after reconnection

Do not claim full offline video downloads unless the approved backend and product architecture explicitly support them.

────────────────────────────────────────

PUSH NOTIFICATIONS

Implement mobile push notification integration.

Support:

• Permission handling
• Token registration
• Token refresh
• Notification routing
• Deep linking
• Foreground handling
• Background handling
• Notification preferences

Use the approved notification backend contracts.

────────────────────────────────────────

DEEP LINKING

Implement deep links for:

• Videos
• Channels
• Playlists
• Live streams
• Notifications
• Search results where appropriate

Support:

• Web URLs
• Universal Links
• Android App Links

────────────────────────────────────────

STATE MANAGEMENT

Separate state correctly.

Use appropriate solutions for:

Server state:

• API data
• Caching
• Pagination
• Background refresh
• Mutation synchronization

Client state:

• UI preferences
• Player state where appropriate
• Temporary interaction state
• Local navigation state where necessary

Do not duplicate server state unnecessarily in global client stores.

────────────────────────────────────────

API CLIENT

Generate a typed API client based on approved API contracts.

Implement:

• Authentication handling
• Request cancellation
• Timeouts
• Retry behavior where appropriate
• Error normalization
• Correlation IDs
• Pagination
• File upload flows
• WebSocket authentication where required

Do not silently swallow API failures.

────────────────────────────────────────

ERROR HANDLING

Implement:

• Route-level error boundaries
• Component-level recovery where appropriate
• Network error handling
• Retry actions
• Authentication expiration handling
• Permission-denied states
• Not-found states
• Offline states

Provide useful user feedback without exposing internal system details.

────────────────────────────────────────

PERFORMANCE REQUIREMENTS

Optimize:

• Initial load
• Time to interactive
• Image loading
• Video thumbnails
• Route transitions
• Infinite scrolling
• Large lists
• Search
• Bundle size
• Code splitting
• Lazy loading

For mobile optimize:

• Memory usage
• List rendering
• Video resource cleanup
• Network requests
• Battery usage

Do not optimize prematurely at the expense of correctness, but avoid obvious scalability problems.

────────────────────────────────────────

ACCESSIBILITY

Implement:

• Semantic HTML
• ARIA where necessary
• Keyboard navigation
• Focus management
• Screen reader support
• Visible focus indicators
• Sufficient interaction target sizes
• Accessible forms
• Accessible error messages
• Accessible dialogs
• Reduced-motion support where appropriate

Ensure equivalent accessibility considerations on mobile.

────────────────────────────────────────

SECURITY

Frontend and mobile implementations must:

• Avoid exposing secrets.
• Avoid embedding private API credentials.
• Use secure authentication flows.
• Respect server-side authorization.
• Sanitize or safely render user-generated content.
• Avoid dangerous HTML rendering.
• Validate navigation and redirect destinations.
• Protect sensitive local storage.
• Use secure storage on mobile for sensitive tokens where required.

Do not treat frontend authorization checks as a security boundary.

────────────────────────────────────────

TESTING

Generate appropriate tests.

Web:

• Component tests
• Hook tests
• API client tests
• Integration tests
• End-to-end tests for critical flows

Mobile:

• Component tests
• Navigation tests
• State tests
• Integration tests
• End-to-end tests where tooling is available

Critical flows include:

• Registration
• Login
• Logout
• Password reset
• Video discovery
• Search
• Video playback
• Playback progress
• Subscription
• Comments
• Notifications
• Video upload
• Creator video publishing
• Live stream viewing
• Live chat
• Settings updates

────────────────────────────────────────

IMPLEMENTATION ORDER

Implement the frontend incrementally.

Use dependency-aware milestones.

Suggested milestone order:

MILESTONE GROUP 1 — FRONTEND FOUNDATION

Implement:

• Web application foundation
• Mobile application foundation
• Shared TypeScript configuration
• Shared API contracts
• API client foundation
• Environment configuration
• Design tokens
• Base UI primitives
• Layout foundation
• Routing foundation
• Error boundaries
• Loading states
• Testing foundation

────────────────────────────────────────

MILESTONE GROUP 2 — AUTHENTICATION

Implement:

• Registration
• Login
• Logout
• Email verification
• Password reset
• Password changes
• Session handling
• Protected routes
• Mobile authentication flow

────────────────────────────────────────

MILESTONE GROUP 3 — APPLICATION SHELL

Implement:

• Web navigation
• Desktop sidebar
• Mobile web navigation
• Mobile app navigation
• User menu
• Notification entry points
• Search entry points

────────────────────────────────────────

MILESTONE GROUP 4 — VIDEO DISCOVERY

Implement:

• Home
• Video cards
• Recommendation feed
• Infinite scrolling
• Loading and error states

────────────────────────────────────────

MILESTONE GROUP 5 — VIDEO PLAYBACK

Implement:

• Web video player
• Mobile video player
• Playback state
• Progress reporting
• Watch page
• Related content

────────────────────────────────────────

MILESTONE GROUP 6 — SEARCH AND EXPLORE

Implement:

• Search
• Autocomplete
• Search results
• Filters
• Trending
• Categories
• Discovery

────────────────────────────────────────

MILESTONE GROUP 7 — CHANNELS AND SUBSCRIPTIONS

Implement:

• Channel pages
• Channel navigation
• Subscribe/unsubscribe
• Subscription feed

────────────────────────────────────────

MILESTONE GROUP 8 — COMMENTS AND INTERACTIONS

Implement:

• Likes/reactions
• Comments
• Replies
• Saves
• Watch Later
• Sharing

────────────────────────────────────────

MILESTONE GROUP 9 — PLAYLISTS AND HISTORY

Implement:

• Playlists
• Watch Later
• Watch history
• Resume playback

────────────────────────────────────────

MILESTONE GROUP 10 — NOTIFICATIONS AND SETTINGS

Implement:

• Notification center
• Profile settings
• Privacy settings
• Security settings
• Device/session management

────────────────────────────────────────

MILESTONE GROUP 11 — CREATOR STUDIO FOUNDATION

Implement:

• Creator layout
• Dashboard
• Channel management
• Video management

────────────────────────────────────────

MILESTONE GROUP 12 — VIDEO UPLOAD AND PUBLISHING

Implement:

• Upload workflow
• Upload progress
• Metadata editing
• Thumbnail management
• Visibility
• Scheduling
• Processing status
• Publishing

────────────────────────────────────────

MILESTONE GROUP 13 — CREATOR ANALYTICS

Implement:

• Analytics dashboard
• Video analytics
• Audience metrics
• Performance metrics
• Responsive charts

────────────────────────────────────────

MILESTONE GROUP 14 — LIVE STREAMING

Implement:

• Live stream discovery
• Live watch page
• Live chat
• Creator live management

────────────────────────────────────────

MILESTONE GROUP 15 — MONETIZATION AND ADVERTISING

Implement approved:

• Revenue dashboards
• Payout views
• Monetization settings
• Advertiser dashboards
• Campaign management

────────────────────────────────────────

MILESTONE GROUP 16 — MODERATION AND ADMINISTRATION

Implement authorized:

• Moderation dashboard
• Reports
• Appeals
• Administration interfaces
• Feature flags
• Audit logs

────────────────────────────────────────

MILESTONE GROUP 17 — MOBILE POLISH AND PLATFORM FEATURES

Complete:

• Push notifications
• Deep linking
• Offline behavior
• Platform-specific optimization
• Accessibility improvements

────────────────────────────────────────

MILESTONE EXECUTION RULES

Begin with Frontend Milestone 1 only.

For every milestone:

1. Define the exact scope.
2. Identify files to create.
3. Identify files to modify.
4. Generate complete implementations.
5. Integrate with existing backend contracts.
6. Generate appropriate tests.
7. Verify TypeScript consistency.
8. Update the Project Index.
9. Stop.

Do not automatically begin the next milestone.

Wait for approval.

────────────────────────────────────────

CURRENT STARTING POINT

Start with:

FRONTEND MILESTONE 1 — FOUNDATION

Implement the minimum coherent production-ready foundation required for future frontend work, including:

• Web application setup
• Mobile application setup
• Shared TypeScript configuration where appropriate
• Environment configuration
• Typed API client foundation
• Authentication/session integration foundation
• Design tokens
• Base UI primitives
• Web layout foundation
• Mobile navigation foundation
• Error boundaries
• Loading states
• Empty states
• Testing foundation

Respect the approximate 20–40 file milestone limit from the Master Prompt.

If additional foundation work is required, complete it in the next milestone rather than exceeding the context limit.

────────────────────────────────────────

PROJECT INDEX

After every milestone update:

• Current phase
• Current milestone
• Completed web features
• Completed mobile features
• Generated files
• Modified files
• Integrated backend APIs
• Implemented routes
• Implemented UI components
• Tests
• Remaining work
• Exact next milestone

Never lose track of previously implemented components.

────────────────────────────────────────

STOP CONDITION

Start only with:

FRONTEND MILESTONE 1 — FOUNDATION

After completing the milestone:

• Verify integration with the approved architecture.
• Verify integration with existing backend contracts.
• Ensure generated files are internally consistent.
• Update the Project Index.
• Identify the exact next milestone.

STOP.

Wait for explicit approval before continuing.
