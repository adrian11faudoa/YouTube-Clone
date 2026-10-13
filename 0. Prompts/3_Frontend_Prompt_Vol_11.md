# YouTube-Style Video Platform — Frontend Prompt — Volume 11

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **moderation console, trust-and-safety workflows, report management, enforcement interfaces, appeals experience, and authorized platform-administration tools** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

- moderation console;
- report queues;
- moderation case details;
- content review;
- user/channel/video/comment enforcement interfaces;
- policy-violation presentation;
- moderation decision workflows;
- appeals handling where supported;
- enforcement history;
- administrator access controls;
- audit-log viewing;
- platform-management interfaces explicitly supported by backend contracts;
- operational confirmation and error handling;
- security-sensitive administrative interactions;
- accessibility;
- responsive behavior;
- testing;
- documentation.

Do not implement unrelated frontend domains.

Do not implement moderation engines, abuse-detection models, backend enforcement systems, or administrative authorization services.

Do not fabricate moderation decisions, policy violations, audit entries, or enforcement results.

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
- notifications;
- creator studio and analytics;
- live streaming;
- paid memberships and monetization-capable functionality;
- moderation;
- administration;
- web and mobile clients.

The web technology direction is:

- TypeScript;
- React;
- Next.js App Router;
- responsive web;
- typed API clients;
- production server/client state management;
- accessibility;
- observability;
- automated testing.

Moderation and administration are security-sensitive domains. Incorrect UI behavior can cause unauthorized restrictions, exposure of private information, or irreversible actions against users and content.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- earlier frontend prompts;
- hidden architecture decisions;
- undocumented moderation APIs;
- hidden generated files;
- undocumented administrative permissions.

If a repository is available, inspect it before modifying it.

If portable moderation, authorization, audit, appeal, or administration contracts are supplied, use those contracts as authoritative.

If those artifacts are unavailable, inspect the repository for compatible implementations and follow the explicit requirements in this prompt.

Preserve compatible existing functionality.

Do not invent new backend privileges or enforcement capabilities merely to make the interface appear complete.

---

# 4. Primary Objective

Implement a secure, production-grade web console for authorized trust-and-safety personnel and administrators.

The completed scope must allow appropriately authorized personnel to:

1. inspect moderation queues;
2. filter and sort available reports;
3. open report details;
4. inspect the associated content and context;
5. review policy-relevant information supplied by the backend;
6. assign or manage cases where supported;
7. submit permitted moderation decisions;
8. enforce supported content or account restrictions;
9. review previous enforcement history;
10. handle appeals where supported;
11. view authorized audit records;
12. inspect account/channel/content details within their permission scope;
13. confirm consequential actions;
14. recover safely from failed or conflicting operations;
15. preserve a clear record of the operation requested and its confirmed outcome;
16. prevent unauthorized access to moderation tools;
17. maintain privacy and security boundaries;
18. operate the console accessibly and efficiently.

---

# 5. Explicit Scope

Implement:

- protected moderation routes;
- moderation navigation shell;
- report queues;
- case list and filtering;
- case assignment where supported;
- report details;
- related-content context panels;
- moderation decision forms;
- content enforcement interfaces;
- account/channel restriction interfaces;
- comment enforcement interfaces;
- supported live-stream enforcement entry points;
- enforcement history;
- appeals interfaces where supported;
- audit-log viewing;
- administrator account and role views where contractually supported;
- platform-management interfaces explicitly supplied by the API contracts;
- permission-aware controls;
- destructive-action confirmations;
- conflict and failure handling;
- sensitive-data display safeguards;
- observability and telemetry;
- accessibility;
- responsive behavior;
- automated testing;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- moderation decision engines;
- machine-learning classification;
- automated abuse detection;
- backend moderation queues;
- policy evaluation services;
- account restriction services;
- video/comment removal services;
- appeal adjudication engines;
- administrator authorization backends;
- audit-log persistence;
- database or event changes unrelated to this frontend scope;
- infrastructure dashboards that require nonexistent observability APIs;
- creator studio;
- viewer monetization;
- payment processing;
- mobile applications;
- unrestricted account impersonation.

Do not redesign backend moderation workflows solely to simplify the UI.

If a capability is not supported by the actual backend contract, do not simulate it.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. identify the web application and route conventions;
3. inspect authentication and session management;
4. inspect authorization and permission handling;
5. inspect existing administration or moderation components;
6. inspect the design system and dialog primitives;
7. inspect table, list, filter, and pagination components;
8. inspect API-client and error-normalization conventions;
9. inspect report, case, enforcement, and appeal types where present;
10. inspect audit-log integration;
11. inspect analytics and operational telemetry;
12. inspect accessibility infrastructure;
13. inspect automated tests.

Reuse compatible components.

Do not create a second authentication or authorization framework.

Do not place security-sensitive API logic directly inside presentation components when a dedicated data layer is appropriate.

---

# 8. Protected Route Architecture

Implement routes consistent with the existing application.

Conceptual routes may include:

```text
/admin
/admin/moderation
/admin/moderation/reports
/admin/moderation/cases/{caseId}
/admin/moderation/enforcement
/admin/moderation/appeals
/admin/audit-logs
/admin/accounts
/admin/platform
```

The exact paths must follow the repository's established conventions and supported backend capabilities.

Every protected route must enforce the project's authentication and authorization model.

Do not rely exclusively on client-side route guards for security.

---

# 9. Administrative Authorization

Use the canonical server-provided authorization model.

Permissions may correspond to capabilities such as:

```text
canViewReports
canReviewCases
canAssignCases
canRemoveContent
canRestrictAccounts
canManageChannels
canReviewAppeals
canViewAuditLogs
canManageRoles
canManagePlatformSettings
```

These are conceptual examples, not a replacement for the actual permission contract.

Use exact project-defined roles, scopes, and permission identifiers where available.

Do not invent a broader administrator role.

Do not assume that every moderator can perform every administrative action.

---

# 10. Permission-Aware UI

All controls must reflect the user's actual permitted capabilities.

The frontend must distinguish:

- action available;
- action unavailable;
- permission loading;
- permission denied;
- authorization expired.

Do not render privileged actions simply because a shared component supports them.

Do not use hidden buttons as a substitute for authorization.

When a user cannot perform an action, follow the product's established pattern for hiding or disabling the control and explaining the restriction where appropriate.

The backend remains the authoritative authorization boundary.

---

# 11. Moderation Console Shell

Implement a reusable moderation/admin shell.

Conceptually:

```text
AdminShell
  ├── AdminNavigation
  ├── AdminHeader
  ├── PermissionAwareActions
  └── AdminContent
```

It must support:

- current section;
- accessible navigation;
- direct route navigation;
- page titles;
- responsive layout;
- breadcrumbs where useful;
- clear distinction between ordinary viewer pages and privileged administrative pages.

Do not duplicate the public video application shell unnecessarily.

---

# 12. Report Queue

Implement a report queue for authorized moderators.

Display only the information provided by the report contract, which may include:

- report identifier;
- report category;
- reported content type;
- report creation time;
- current case status;
- assigned moderator where permitted;
- priority or severity where defined;
- relevant content identifiers;
- available actions.

Do not invent priority scores.

Do not infer that a report is valid merely because it exists in the queue.

---

# 13. Report Queue Filtering

Implement filtering and sorting supported by the backend.

Possible filters include:

- status;
- report category;
- content type;
- date range;
- assignment;
- priority where supported.

Use the canonical backend filter values.

Do not implement client-side filtering over only the currently loaded page when the user expects filtering over the complete queue.

---

# 14. Queue Pagination

Use the canonical pagination contract.

Support:

- initial loading;
- next page;
- loading-more state;
- end of results;
- retry;
- duplicate prevention;
- stale-response protection.

Prefer cursor pagination where the backend provides it.

Do not load the entire moderation queue into browser memory.

Do not issue duplicate concurrent requests for the same cursor.

---

# 15. Queue Empty and Error States

Distinguish between:

- no reports;
- no reports matching filters;
- authorization failure;
- temporary backend failure;
- network error;
- request cancellation.

Provide actionable but nonmisleading messages.

Do not display an empty queue as though it proves there are no outstanding reports when the request failed.

---

# 16. Report and Case Domain Models

Consume the canonical report and moderation-case contracts.

A conceptual report may contain:

```text
reportId
reporterContext
reportedEntity
reportedEntityId
reason
createdAt
status
caseId
viewerPermissions
```

A conceptual case may contain:

```text
caseId
status
assignedModerator
createdAt
updatedAt
evidence
relatedReports
availableActions
decisionHistory
```

Use actual contract names and field semantics when supplied.

Do not merge report and case entities into one frontend model if the backend treats them as distinct domains.

Do not assume every report creates a unique moderation case.

---

# 17. Case Detail Page

Implement a moderation case detail page.

Where supported, display:

- case status;
- associated reports;
- reported content;
- relevant public content metadata;
- author/channel identity;
- available evidence;
- prior decisions;
- assignment;
- case notes or reviewer notes only when explicitly supported;
- available actions permitted for the current moderator.

Keep the case's identity clear throughout review and action workflows.

Do not expose confidential reporter data unless the permission and product contract explicitly authorize it.

---

# 18. Related Content Context

Where permitted, provide safe context for reviewing reported material.

For example:

- public video metadata;
- comment content;
- channel profile;
- current content visibility;
- reported timestamps or locations where supplied;
- relevant enforcement history where authorized.

Do not fetch or reveal protected content through a viewer endpoint that bypasses administrative authorization.

Do not expose private information merely because the moderator is viewing a case.

Follow the backend's evidence and permission model.

---

# 19. Evidence Presentation

Render evidence supplied by the moderation API.

Support applicable evidence types such as:

- text;
- content references;
- timestamps;
- supported metadata;
- approved attachments or evidence links.

Only render evidence types defined by the contract.

Treat evidence as untrusted input.

Do not execute embedded scripts, render unsafe HTML, or automatically navigate to arbitrary external URLs.

Protect sensitive evidence from unnecessary caching, analytics, and logging.

---

# 20. Assignment Workflow

Where the backend supports case assignment:

- display current assignment;
- list authorized assignment options;
- update assignment through the canonical API;
- display pending state;
- handle conflicts;
- reconcile the server response.

Do not allow client-only assignment changes to appear permanent.

Do not assume every account in the user directory is eligible to review moderation cases.

---

# 21. Case Status

Render only status values defined by the authoritative contract.

Conceptual statuses may include:

```text
open
assigned
in_review
action_required
resolved
dismissed
appealed
```

Do not assume the project uses these exact values.

Map backend state to a clear user-facing label without changing its semantics.

Do not manufacture status transitions on the client.

---

# 22. Moderation Decision Interface

Implement a secure form for supported moderation decisions.

The form must:

- identify the target case and content;
- present the available decision options;
- capture required reason/category fields;
- validate required information;
- require confirmation where the action is consequential;
- submit through the canonical contract;
- display pending state;
- reconcile the server-confirmed result.

Do not assume every case has the same available decisions.

Do not use a generic unrestricted action dropdown when the contract provides a defined decision model.

---

# 23. Content Enforcement

Where supported, expose authorized actions for content such as:

- remove;
- restrict visibility;
- restore;
- other project-defined moderation actions.

Use only backend-supported actions.

For every consequential action:

- identify the target content;
- show the requested action clearly;
- require appropriate confirmation;
- submit to the canonical API;
- display the confirmed outcome;
- handle failure or conflict.

Do not treat local hiding of a content card as proof that the content was removed from the platform.

---

# 24. Account and Channel Enforcement

If authorized account/channel enforcement actions are supported, provide the corresponding UI.

Potential actions may include:

- warning;
- temporary restriction;
- suspension;
- account restriction;
- restoration;
- other explicitly supported measures.

Do not invent durations, policy categories, or enforcement consequences.

Where a duration is required, use the canonical supported values or the validation rules supplied by the backend.

Display an explicit summary of what will happen before submission where appropriate.

---

# 25. Comment Enforcement

Where comment moderation is supported:

- show the reported comment;
- show relevant context allowed by the API;
- display its current state;
- expose permitted moderation actions;
- submit decisions through the canonical contract;
- reconcile the resulting state.

Do not implement comment persistence or removal independently in the frontend.

Do not show a comment as permanently removed solely because the moderator clicked an action.

---

# 26. Video and Live-Stream Enforcement

Where supported, allow authorized personnel to review and act on reported videos or live streams.

Display:

- canonical content identity;
- current availability;
- relevant moderation status;
- supported review metadata;
- permitted actions.

Do not embed unrestricted private media playback.

Use approved review URLs or preview mechanisms supplied by the backend where privileged content access is required.

Do not assume a live stream can always be replayed for review.

---

# 27. Action Confirmation

Use confirmation dialogs for destructive or consequential actions.

The confirmation must clearly state:

- the target entity;
- the action;
- any backend-provided duration or scope;
- any material consequences known to the product.

Do not use ambiguous confirmation labels such as “Continue” when the action is destructive.

The dialog must be accessible and keyboard-operable.

Prevent accidental duplicate submissions.

---

# 28. Conflict and Concurrency Handling

The moderation interface must handle concurrent changes.

For example:

```text
Moderator A opens a case
Moderator B changes its status
Moderator A submits a decision using stale data
```

The frontend must handle backend conflicts or stale-version responses correctly.

Do not overwrite a newer server decision with a stale client response.

On conflict:

- preserve relevant user-entered information where safe;
- refresh authoritative case state;
- explain that the case changed;
- require the moderator to review the updated state before repeating a consequential action where appropriate.

Use version/updated-at fields or concurrency tokens when the backend contract provides them.

---

# 29. Double-Submission Prevention

Prevent duplicate administrative actions.

While a consequential action is pending:

- disable incompatible controls;
- preserve the target entity identity;
- prevent repeated submission;
- reconcile the outcome after network interruption.

Use backend idempotency capabilities where supplied.

If a request times out and its outcome is uncertain, retrieve authoritative status before blindly repeating the action.

Do not present an uncertain operation as definitely successful or failed.

---

# 30. Enforcement History

Where supported, display enforcement history for content, accounts, or channels.

The interface may show:

- action type;
- effective status;
- timestamps;
- appeal outcome;
- actor information where authorized;
- expiration where defined.

Do not expose internal staff identity or confidential operational details unless the contract explicitly permits them.

Use authoritative history records.

Do not manufacture a history entry from the current UI action before the backend confirms it.

---

# 31. Appeals Workflow

If the backend supports appeals, implement the corresponding moderation UI.

Potential functionality includes:

- appeal queue;
- appeal details;
- original enforcement action;
- appellant-provided explanation;
- relevant evidence;
- appeal status;
- authorized review actions;
- final decision.

Only implement capabilities defined by the actual appeal contract.

Do not create a separate appeal lifecycle that conflicts with the enforcement system.

---

# 32. Appeal Decision Safety

When submitting an appeal decision:

- identify the original decision;
- display the appeal's current status;
- collect any required decision category or explanation;
- require confirmation where appropriate;
- submit through the canonical API;
- handle conflicts;
- reconcile the server-confirmed result.

Do not automatically restore content because an appeal was opened.

Do not silently reverse an enforcement action before the backend confirms its status.

---

# 33. Administrator Account and Role Views

Where the backend contract supports user or role administration, provide the corresponding read/edit views.

Support only explicit capabilities, such as:

- listing authorized administrative accounts;
- viewing role assignments;
- reviewing permission scopes;
- making supported role changes.

Do not assume all administrators may manage other administrators.

Do not invent role names or privilege combinations.

Require confirmation for privilege changes and reconcile server responses.

---

# 34. Privilege-Change Safety

Administrative privilege changes are high-risk operations.

The frontend must:

- display the affected account;
- display the exact requested role/permission change;
- prevent accidental self-lockout where the backend contract identifies that risk;
- request confirmation where appropriate;
- handle conflicts;
- display the confirmed result.

Do not create self-service privilege escalation.

The backend remains the security authority.

---

# 35. Audit Log Interface

If the backend provides audit-log access, implement a read-only audit-log viewer unless the contract explicitly supports additional operations.

Potential fields include:

```text
auditEntryId
actor
actionType
targetEntity
targetEntityId
createdAt
result
correlationId
```

Use exact project-defined fields.

Do not fabricate audit records.

Do not expose privileged details outside the current user's authorized scope.

---

# 36. Audit Log Filtering

Support contract-defined filters such as:

- action category;
- target entity;
- actor;
- date range;
- result;
- relevant case identifier.

Use the backend's authoritative query/filter model.

Do not filter only the currently loaded page when the user expects filtering across the complete dataset.

Use cursor pagination where provided.

---

# 37. Audit Log Integrity Presentation

Audit records are historical evidence.

The frontend must:

- display stored records without silently rewriting their meaning;
- distinguish absent values from unavailable values;
- avoid inferring an operation's outcome;
- preserve authoritative timestamps;
- display partial records carefully when optional fields are absent.

Do not provide editing or deletion controls for audit entries unless the project has an explicitly authorized, auditable correction workflow.

---

# 38. Platform-Administration Boundaries

If platform-management features are available through the backend, implement only the specific interfaces within this scope and contract set.

Examples may include:

- administrative overview data;
- platform configuration values explicitly intended for administrators;
- account-management views;
- content-control settings;
- authorized operational status summaries.

Do not invent dashboard metrics.

Do not expose infrastructure secrets, raw credentials, internal environment variables, or restricted operational data.

Do not create arbitrary server configuration forms.

---

# 39. Admin Configuration Changes

Where supported administrative configuration changes exist:

- use exact contract-defined fields;
- explain the effect where supplied by product requirements;
- validate before submission;
- require confirmation for high-impact changes;
- use authoritative server responses;
- handle conflicts;
- preserve unsaved input during recoverable failures.

Do not expose settings that the backend does not permit the current administrator to modify.

Do not silently apply local configuration changes as though they were persisted.

---

# 40. Sensitive Information Handling

The moderation console may contain:

- reporter information;
- reported user details;
- private content;
- internal case notes;
- enforcement history;
- administrative account data;
- evidence attachments.

The implementation must:

- render only fields returned to the currently authorized user;
- avoid unnecessary browser persistence;
- avoid putting sensitive evidence into URLs;
- avoid logging report text or private evidence;
- avoid transmitting case details to unrelated analytics;
- use cache isolation for privileged data.

Do not invent additional privacy or access privileges based on frontend convenience.

---

# 41. Cache and State Isolation

Use the project's existing server-state system.

Cache keys must include relevant identifiers, such as:

- case ID;
- report queue filters;
- audit-log filters;
- target account/channel/content ID;
- authenticated administrative context where response content is user-specific.

After moderation actions, invalidate or reconcile only the affected case, queue, history, or target-content caches.

Do not retain privileged case details after logout or an account/role change.

Do not allow stale authorization state to keep privileged controls operational.

---

# 42. Session Expiration and Permission Changes

Handle:

- session expiration;
- account suspension;
- role revocation;
- permission-scope changes;
- authorization failure during a pending workflow.

If permissions change while the page is open:

- stop exposing actions that are no longer permitted when the change is known;
- refetch authoritative state;
- handle rejected requests correctly;
- preserve unsaved notes or form state only where safe and appropriate.

Do not retry unauthorized administrative operations indefinitely.

---

# 43. Loading, Empty, and Failure States

Every major administrative section must support:

### Loading

Show a clear pending state without misleading the reviewer.

### Empty

Explain that no matching reports, cases, appeals, or audit records are available for the current query.

### Error

Distinguish authorization failure, network failure, validation failure, stale-state conflict, and temporary backend unavailability.

### Partial

Where the API contract allows partial results, show what is available and clearly identify unavailable context.

Do not convert a failed request into an empty result.

---

# 44. Accessibility

The moderation and admin console must support:

- semantic headings;
- keyboard navigation;
- accessible data tables;
- accessible filters;
- accessible case actions;
- screen-reader labels;
- visible focus;
- accessible confirmation dialogs;
- meaningful status and error announcements;
- accessible audit-log navigation.

Color alone must not communicate:

- severity;
- case status;
- enforcement outcome;
- permission state.

The interface must remain usable without a mouse.

---

# 45. Responsive Behavior

Support desktop, tablet, and mobile web.

Moderation work may be optimized for desktop, but critical workflows must not become unusable on smaller screens.

Ensure:

- long case details wrap correctly;
- tables have an appropriate narrow-screen strategy;
- action controls remain reachable;
- confirmation dialogs fit the viewport;
- sensitive information is not accidentally clipped in a way that changes its meaning.

Do not make drag-only, hover-only, or desktop-only actions the sole available interaction.

---

# 46. Performance

Optimize:

- large report queues;
- case navigation;
- audit-log pagination;
- evidence presentation;
- filter changes;
- state reconciliation after actions.

Do not fetch every case or audit record upfront.

Do not keep every previously opened privileged case mounted indefinitely.

Do not rerender an entire queue when one row changes status.

Use list virtualization only when appropriate and without breaking keyboard navigation, browser behavior, or accessibility.

---

# 47. Security

The implementation must:

- respect backend authorization;
- use secure session handling;
- prevent open redirects;
- render untrusted content safely;
- avoid unsafe HTML;
- avoid exposing protected attachments;
- avoid logging secrets or private evidence;
- validate administrative navigation targets;
- protect privilege-changing actions;
- handle expired sessions safely.

Never treat a hidden frontend route or disabled button as the only authorization barrier.

---

# 48. Observability and Telemetry

Use the project's observability conventions to capture appropriate frontend failures and interaction outcomes.

Potential events include:

```text
moderation_console_opened
report_queue_viewed
moderation_case_opened
moderation_case_assigned
moderation_decision_submitted
moderation_action_failed
enforcement_history_viewed
appeal_opened
appeal_decision_submitted
audit_log_viewed
admin_permission_change_submitted
```

Use canonical event names when available.

Do not emit raw evidence, report text, private case notes, credentials, or unnecessary user information.

Administrative telemetry must not become a secondary store of confidential moderation data.

---

# 49. Testing Strategy

Implement tests for actual administrative behavior.

### Unit tests

Cover:

- permission-to-action mapping;
- report/case status mapping;
- filter serialization;
- pagination state;
- enforcement-action payload construction;
- confirmation requirements;
- stale-state conflict handling;
- duplicate-submission prevention;
- audit-log rendering;
- cache isolation;
- error normalization.

### Component tests

Cover:

- report queue;
- case detail;
- evidence panel;
- assignment control;
- moderation decision form;
- content-enforcement dialog;
- account/channel enforcement actions;
- appeals interface;
- audit-log viewer;
- role-management controls where supported;
- permission-denied states.

### Integration tests

Cover:

- protected route behavior;
- loading reports;
- filtering/pagination;
- opening a case;
- assigning a case;
- submitting a moderation decision;
- enforcement failure;
- stale-version conflict;
- appeals workflow where supported;
- audit-log filtering;
- role changes where supported;
- session expiration;
- permission revocation;
- privileged cache invalidation.

### End-to-end tests

At minimum:

1. authenticate as an authorized moderator;
2. open the report queue;
3. filter reports;
4. inspect a case;
5. view the related content context;
6. submit a supported moderation decision using a test case;
7. verify the UI reconciles authoritative server state;
8. simulate a conflicting case update;
9. verify the stale action is not silently treated as successful;
10. open enforcement history;
11. view audit logs where permitted;
12. verify an unauthorized user cannot access privileged routes;
13. verify a moderator without enforcement permission cannot execute an enforcement action;
14. verify a session/permission change removes or blocks privileged access;
15. verify keyboard accessibility of important workflows.

Use controlled test data and test boundaries. Do not perform real destructive actions against production accounts or content during ordinary automated tests.

---

# 50. Browser Compatibility

Validate the supported browser matrix.

Pay particular attention to:

- accessible tables;
- long evidence content;
- dialogs;
- keyboard navigation;
- focus restoration;
- responsive administrative workflows;
- session expiration;
- protected document navigation.

Do not rely on hover-only controls.

---

# 51. Documentation

Update documentation describing:

- protected admin routes;
- moderation console architecture;
- report/case model integration;
- authorization and permission mapping;
- supported enforcement workflows;
- appeals integration where available;
- audit-log integration;
- sensitive-data handling;
- cache isolation;
- conflict handling;
- telemetry/privacy considerations;
- accessibility;
- automated testing.

Documentation must reflect actual implemented behavior.

---

# 52. No Fake Administrative Behavior

Do not create:

- fake reports;
- fabricated policy violations;
- simulated enforcement success;
- fake audit records;
- invented moderator permissions;
- fake appeal outcomes;
- hardcoded case decisions;
- local-only account restrictions;
- fake administrative configuration persistence.

Mocks are permitted only in controlled automated tests.

The production application must use real contracts and authoritative backend state.

---

# 53. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- nonfunctional enforcement buttons;
- empty decision handlers;
- fake audit-log entries;
- placeholder permission checks;
- incomplete destructive-action confirmation;
- simulated appeal success;
- unsupported administration controls;
- “implement later” sections.

Every feature included in this prompt must be genuinely implemented within the supported contract boundaries.

---

# 54. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- production build;
- protected route access;
- report queue and filtering;
- case detail and assignment;
- moderation decision submission;
- stale-state conflict handling;
- enforcement workflows;
- appeals where supported;
- audit-log access and filtering;
- administrator permission controls where supported;
- session expiration;
- permission revocation;
- cache invalidation;
- privacy/security handling;
- responsive layouts;
- accessibility-critical workflows.

Fix issues found within the current scope.

Do not claim that backend enforcement or moderation systems were deployed or validated unless that actually occurred.

---

# 55. Definition of Done

This prompt is complete only when:

- the moderation/admin shell works;
- protected routes enforce the established authentication model;
- report queues load from real contracts;
- filtering and pagination work;
- case details render correctly;
- evidence is safely presented;
- case assignment works where supported;
- moderation decisions use real APIs;
- content enforcement works where supported;
- account/channel enforcement works where supported;
- comment/live-content enforcement entry points work where supported;
- enforcement history works where supported;
- appeals work where supported;
- audit-log viewing and filtering work where supported;
- administrator/role views work where supported;
- consequential actions require appropriate confirmation;
- duplicate submissions are prevented;
- conflicts and stale responses are handled safely;
- current permissions control the available interface;
- session and permission changes are handled;
- privileged cache state is isolated and invalidated correctly;
- confidential information is not exposed through telemetry or public routes;
- responsive behavior works;
- accessibility requirements are implemented;
- automated tests cover the defined behavior;
- documentation is updated;
- no fake production behavior remains;
- no current-scope placeholders remain;
- validation passes.

---

# 56. Completion Report

At the end of execution, provide a concise completion report containing:

### Implemented

Summarize the moderation console, report management, enforcement, appeals, and administration interfaces actually completed.

### Files

List significant files created, modified, or deleted.

### API Contracts

List report, case, enforcement, appeal, audit-log, authorization, role-management, and telemetry contracts consumed.

### State and Security

Summarize permission-aware UI, privileged cache isolation, stale-state protection, destructive-action safety, session expiration handling, and sensitive-data protections.

### Testing

List tests created and tests executed, including permission-boundary and conflict tests.

### Validation

Report type checking, linting, production build, and relevant access-control validation.

### Integration Notes

Identify unsupported backend capabilities, unresolved contract assumptions, or dependencies requiring integration by another project part.

### Out of Scope

Confirm that moderation engines, abuse detection, enforcement backends, audit persistence, infrastructure dashboards, and excluded application domains were not improperly implemented.

---

# 57. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe moderation and administration workflows.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts.

Do not fabricate reports, decisions, enforcement outcomes, permissions, or audit records.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web moderation, trust-and-safety, appeals, and platform-administration interface** that can be integrated with the independently generated backend and other project components through explicit contracts.
