# YouTube-Style Video Platform — Frontend Prompt — Volume 9

## 1. Prompt Identity

You are the senior frontend engineer responsible for implementing the **web monetization, paid channel memberships, purchase and checkout experiences, viewer entitlements, creator membership management, and revenue-related interfaces** of a production-grade YouTube-style video platform.

This is a bounded implementation milestone.

Your responsibility in this prompt is the web frontend for:

- paid channel memberships;
- membership tiers and benefits;
- membership enrollment;
- purchase and checkout flows;
- payment-provider integration;
- payment status presentation;
- viewer purchase history;
- membership management and cancellation;
- refunds and disputes where supported;
- entitlement-aware content presentation;
- creator membership configuration;
- creator revenue summaries;
- payout onboarding and status where supported;
- billing errors and recovery;
- accessibility;
- responsive behavior;
- security and privacy;
- testing;
- documentation.

Do not implement unrelated frontend domains.

Do not implement payment processing infrastructure, financial ledgers, payment-provider backends, tax engines, or banking integrations.

Do not fabricate payment success, membership entitlements, transactions, revenue, or payout status.

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
- moderation;
- paid memberships and monetization-capable functionality;
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

Payment and entitlement features must be implemented with particular care because mistakes can affect money, account access, recurring billing, and user trust.

---

# 3. Execution Rule

Treat this prompt as independently executable in a fresh AI coding conversation.

Do not assume access to:

- another Claude conversation;
- another AI response;
- earlier frontend prompts;
- hidden architecture decisions;
- undocumented payment APIs;
- hidden generated files;
- unverified payment-provider credentials.

If a repository is available, inspect it before modifying it.

If portable architecture, payment, membership, purchase, entitlement, or revenue contracts are supplied, use those contracts as authoritative.

If these artifacts are unavailable, inspect the existing repository for implemented contracts and follow the explicit invariants in this prompt. Do not invent incompatible financial or payment models.

Preserve compatible existing functionality.

---

# 4. Primary Objective

Implement a production-grade web experience that allows viewers to discover, purchase, manage, and understand supported paid memberships and purchases while allowing authorized creators to manage supported paid membership offerings and review revenue information.

The completed scope must support, where the backend contract provides the capability:

1. viewing paid membership offerings;
2. inspecting membership tiers and benefits;
3. enrolling in a paid membership;
4. completing a secure checkout flow;
5. handling successful, pending, failed, cancelled, and interrupted transactions;
6. viewing active membership status;
7. managing or cancelling a membership;
8. reviewing purchase and billing history;
9. viewing transaction receipts or invoices where available;
10. requesting refunds where supported;
11. displaying entitlement-aware content access;
12. managing creator membership offerings;
13. configuring membership benefits;
14. viewing creator revenue summaries;
15. completing supported payout-provider onboarding;
16. displaying payout status;
17. recovering from billing and provider errors;
18. respecting permissions and privacy;
19. using the experience accessibly and responsively.

---

# 5. Explicit Scope

Implement:

- paid membership discovery and presentation;
- creator membership tier presentation;
- membership benefits;
- checkout initiation;
- payment-provider handoff or embedded checkout integration;
- checkout return handling;
- transaction status display;
- transaction failure and cancellation handling;
- membership enrollment status;
- membership management;
- cancellation flows;
- purchase and billing history;
- receipt/invoice navigation where supported;
- refund entry points where supported;
- entitlement-aware access presentation;
- viewer billing settings;
- creator membership configuration;
- creator revenue summaries;
- supported payout onboarding and status;
- localized loading/error/empty states;
- authenticated route protection;
- secure payment-state handling;
- analytics and telemetry;
- accessibility;
- responsive behavior;
- automated tests;
- documentation.

---

# 6. Explicit Out of Scope

Do not implement:

- payment processing backends;
- financial ledgers;
- payment-provider webhook handlers;
- tax calculation engines;
- tax filing;
- banking infrastructure;
- payout execution services;
- fraud-detection services;
- chargeback processing infrastructure;
- payment-provider account provisioning backends;
- advertising exchange infrastructure;
- backend membership entitlement computation;
- monetization authorization services;
- mobile purchase flows;
- administrator financial dashboards;
- unrelated creator-studio features.

Do not bypass payment-provider requirements through a custom frontend payment form.

Do not collect or store raw card details unless an explicitly approved, compliant provider integration requires it and the architecture provides the appropriate secure fields.

---

# 7. Repository Inspection

Before implementation:

1. inspect the repository structure;
2. identify the web application;
3. inspect authentication and session handling;
4. inspect channel and creator models;
5. inspect existing subscription controls;
6. inspect payment and checkout abstractions;
7. inspect membership and entitlement contracts;
8. inspect creator analytics and revenue data;
9. inspect route protection;
10. inspect API-client and error-normalization conventions;
11. inspect supported payment-provider SDKs or hosted checkout integrations;
12. inspect forms, dialogs, and design-system components;
13. inspect state-management and caching conventions;
14. inspect automated tests.

Reuse compatible infrastructure.

Do not introduce a duplicate payment-provider integration or a competing financial data model.

---

# 8. Financial Correctness Principles

Financially sensitive frontend behavior must follow these rules:

- The backend is authoritative for prices, currencies, transaction status, membership state, refunds, revenue, and payouts.
- The frontend must never fabricate a successful payment.
- The frontend must never grant an entitlement merely because a checkout button was clicked.
- Displayed monetary values must use the currency and amount provided by the authoritative contract.
- Amounts must not be manipulated using unsafe floating-point arithmetic for financial calculations.
- The frontend must not independently calculate the amount ultimately charged.
- Every transaction must be associated with the correct canonical transaction or checkout identifier.
- Pending transactions must remain pending until an authoritative status confirms their final state.

The checkout UI may calculate presentation-only estimates when the backend explicitly supplies the necessary pricing data, but the server's final amount remains authoritative.

---

# 9. Monetization Route Architecture

Implement routes consistent with the existing application conventions.

Conceptual routes may include:

```text
/channel/{channelId}/join
/membership/checkout
/account/purchases
/account/memberships
/account/billing
/studio/monetization
/studio/monetization/memberships
/studio/monetization/revenue
/studio/monetization/payouts
```

The repository's established routing convention takes precedence.

Routes must support appropriate direct navigation and refresh behavior.

Protected pages must enforce the project's authentication model.

Do not depend exclusively on client-side navigation state for transaction identity.

---

# 10. Membership Domain Contract

Consume the canonical paid-membership contract.

A conceptual membership representation may include:

```text
membershipId
channelId
creatorId
viewerId
tierId
tierName
status
startedAt
currentPeriodStart
currentPeriodEnd
nextBillingAt
cancelAtPeriodEnd
cancelledAt
entitlements
```

Use actual project field names when authoritative contracts are provided.

Do not confuse paid channel memberships with free channel subscriptions.

The two concepts must retain separate state, APIs, permissions, and presentation.

---

# 11. Membership Tier Contract

A tier may expose fields equivalent to:

```text
tierId
channelId
name
description
price
currency
billingInterval
benefits
visibility
availability
```

Use the canonical contract.

Do not assume every tier has the same billing interval.

Do not invent benefits, prices, currencies, or billing intervals.

---

# 12. Paid Membership Discovery

Implement a paid-membership entry point from appropriate channel surfaces where supported.

The interface should allow a viewer to understand:

- that a paid membership is available;
- which creator/channel it belongs to;
- what the tiers cost;
- what the benefits are;
- what billing interval applies;
- whether the viewer already has a membership;
- whether enrollment is available.

Do not require a viewer to begin checkout simply to inspect the offering.

---

# 13. Membership Tier Selection

Provide an accessible tier-selection experience.

Support:

- available tiers;
- tier descriptions;
- pricing;
- billing intervals;
- included benefits;
- selected tier;
- unavailable tier;
- current membership state.

The user must understand which tier they are selecting before starting checkout.

Do not visually represent a tier as available if the backend marks it unavailable.

---

# 14. Membership Benefit Presentation

Render the benefits returned by the authoritative membership contract.

Potential benefits may include:

- membership badges;
- members-only content;
- other project-defined benefits.

Only present benefits actually included in the selected tier.

Do not promise features that the platform does not implement.

The presentation must distinguish between an advertised benefit and an entitlement that has already been granted to a viewer.

---

# 15. Membership Eligibility

Membership enrollment must respect backend-provided eligibility.

Potential conditions include:

- channel monetization eligibility;
- creator availability;
- regional availability;
- viewer account restrictions;
- tier availability;
- policy restrictions.

Do not independently decide whether a creator or viewer qualifies.

When enrollment is unavailable, provide an appropriate explanation based on safe user-facing error or availability information.

---

# 16. Checkout Initiation

Implement checkout initiation using the canonical purchase contract.

The frontend must:

1. verify that the required selection is present;
2. submit a checkout request to the backend;
3. show the pending state;
4. receive an authoritative checkout/session response;
5. navigate to or initialize the approved payment-provider checkout;
6. preserve the canonical transaction reference needed for return handling;
7. handle initialization errors.

Use the exact request/response contract supplied by the project.

Do not create fake checkout sessions.

Do not derive a checkout URL from undocumented patterns.

---

# 17. Payment-Provider Integration

Use the provider integration selected by the project architecture.

Support the appropriate model:

- hosted checkout;
- provider SDK with secure provider-managed fields;
- another explicit provider-approved integration.

Never expose provider secret keys in the browser.

Do not embed secret credentials in client-side configuration.

Do not transmit raw payment credentials through application APIs unless the selected provider explicitly requires secure tokenization and the architecture defines that mechanism.

Do not add a second provider merely to avoid implementing the established integration.

---

# 18. Price and Currency Display

Display pricing using authoritative backend values.

Support:

- currency;
- amount;
- billing interval;
- applicable recurring/nonrecurring labeling;
- backend-supplied tax/total information where available.

Use a locale-aware monetary formatting mechanism appropriate for the application.

Do not assume every amount is denominated in the same currency.

Do not use a hardcoded currency symbol for all users.

Do not independently calculate taxes or discounts.

---

# 19. Checkout Confirmation

Before initiating payment, show the user an accurate summary where required by the provider or product contract.

The summary should make clear:

- selected channel;
- selected tier/product;
- billing interval;
- amount;
- currency;
- applicable terms and recurring nature where relevant.

Use backend-supplied pricing and product details.

Do not conceal recurring billing information.

Do not create a second, potentially conflicting price calculation in the browser.

---

# 20. Checkout Return Handling

Implement a reliable return flow for supported checkout outcomes.

Potential outcomes include:

```text
success_return
pending_return
cancelled_return
failed_return
unknown_return
```

These are presentation categories, not substitutes for the provider/backend's canonical transaction state.

On return:

- validate the transaction reference;
- query the authoritative backend for current status;
- display the confirmed status;
- handle delayed confirmation;
- prevent duplicate purchase submissions;
- remove or avoid retaining sensitive checkout parameters where appropriate.

Do not treat a success-shaped URL parameter as proof that payment succeeded.

---

# 21. Pending Transactions

Transactions may remain pending after the user returns from checkout.

The interface must:

- explain that confirmation is pending;
- retrieve status through the canonical transaction endpoint;
- refresh using a bounded, controlled strategy if supported;
- stop refreshing after a terminal state;
- offer a safe way to revisit purchase status.

Do not endlessly poll.

Do not grant benefits while the authoritative backend still marks the transaction pending unless the product's explicit entitlement contract provides a valid intermediate entitlement.

---

# 22. Payment Failure and Cancellation

Implement separate user-facing states for:

- checkout cancelled;
- payment declined;
- provider unavailable;
- transaction pending;
- authorization failure;
- expired checkout session;
- unknown transaction state.

Allow retry when supported and safe.

Do not automatically restart checkout after failure without user action.

Do not display raw provider debugging messages.

Do not claim that a cancelled checkout created a paid membership.

---

# 23. Duplicate-Purchase Prevention

Protect against duplicate purchase attempts.

The frontend must:

- disable or control duplicate submissions while checkout initiation is pending;
- preserve the canonical pending transaction reference;
- avoid launching multiple concurrent checkout sessions for the same user action;
- reconcile state after navigation interruption.

Use backend idempotency support when the contract provides it.

Client-side duplicate prevention is not a substitute for server-side idempotency.

---

# 24. Membership Activation

After checkout, retrieve the authoritative membership and entitlement state.

The UI must distinguish:

- checkout completion;
- payment confirmation;
- membership activation;
- entitlement availability.

These events may not be simultaneous.

Do not grant paid-member controls merely because the provider redirected to a return URL.

Show confirmation only when supported by authoritative backend state.

---

# 25. Entitlement-Aware Content

Integrate paid membership entitlements with the existing content-access experience.

Where supported, display appropriate states for:

- public content;
- members-only content;
- content requiring a particular tier;
- content unavailable to the current viewer;
- an active membership that provides access.

The frontend must consume authoritative entitlement information.

Do not recreate the entitlement engine in the browser.

Do not assume every membership benefit unlocks every restricted video.

---

# 26. Restricted Content Entry Points

When a viewer attempts to access paid or membership-restricted content:

- explain the access restriction;
- identify the required membership offering when the contract supports it;
- provide the appropriate membership entry point;
- preserve the canonical content destination where appropriate.

Do not expose private content metadata or signed media URLs before authorization.

Do not falsely promise that a purchase will grant access unless the backend contract establishes that relationship.

---

# 27. Existing Member Experience

When a viewer already has an active paid membership:

- display the current membership;
- show the current tier;
- display status and renewal information where available;
- provide access to included benefits;
- avoid presenting an unnecessary enrollment flow;
- offer supported management actions.

If tier changes are supported, clearly distinguish upgrades, downgrades, and any effective dates supplied by the backend.

Do not invent prorating or billing semantics.

---

# 28. Membership Management

Implement the viewer membership-management interface.

Where supported, allow the viewer to:

- inspect active membership;
- inspect tier;
- inspect status;
- view the current billing period;
- view the next billing date;
- change tier;
- cancel membership;
- review pending cancellation;
- reactivate only when the backend supports it.

Never assume a cancelled membership loses entitlements immediately.

Use the authoritative status and effective dates.

---

# 29. Cancellation Flow

Implement membership cancellation where supported.

The flow must:

- explain the action clearly;
- present applicable effective-date information;
- obtain confirmation where appropriate;
- submit the canonical cancellation request;
- display pending state;
- reconcile the server response;
- handle failure.

If cancellation takes effect at the end of a billing period, state that only when the backend confirms those semantics.

Do not locally convert an active membership to cancelled before authoritative confirmation.

---

# 30. Membership Changes

If the backend supports tier changes:

- display available alternatives;
- show authoritative pricing;
- explain effective timing using contract-provided information;
- confirm the requested change where required;
- reconcile the resulting state.

Do not independently calculate proration, credit balances, tax differences, or billing adjustments.

The backend/provider must remain authoritative for financial consequences.

---

# 31. Purchase History

Implement a viewer purchase/billing-history page where supported.

The interface should display safe contract-provided fields, potentially including:

```text
transactionId
productName
channelName
amount
currency
status
createdAt
completedAt
receiptReference
```

Use actual contract fields.

Do not expose internal payment-provider metadata unnecessarily.

---

# 32. Purchase Pagination and Filtering

Use the canonical transaction pagination model.

Where supported, provide filters for:

- status;
- date range;
- purchase type.

Support:

- loading;
- empty state;
- pagination;
- failure;
- retry;
- duplicate prevention.

Do not load an unbounded transaction history.

---

# 33. Receipt and Invoice Access

Where the backend provides receipt or invoice access:

- use the authoritative returned link or document endpoint;
- verify that the link is intended for the current viewer;
- handle expiration;
- avoid exposing private documents through shared caches;
- present unavailable-document states.

Do not manufacture receipts or tax invoices in the browser.

Do not label a generic transaction summary as a legally valid tax invoice unless the appropriate backend contract identifies it as one.

---

# 34. Refund Requests

If the backend supports viewer-initiated refund requests, provide the relevant interface.

Support:

- eligibility information supplied by the backend;
- request confirmation;
- loading;
- submitted/pending status;
- approved/denied status where available;
- failure feedback.

Do not determine refund eligibility solely through hardcoded frontend rules.

Do not claim that a refund is complete before the backend confirms its status.

Do not fabricate refund reference numbers.

---

# 35. Dispute and Failed-Transaction States

Where the backend exposes a supported status, render appropriate information for:

- payment dispute;
- refund pending;
- refund completed;
- failed transaction;
- reversed transaction;
- transaction under review.

Do not expose internal fraud signals or payment-provider risk scores.

Do not imply that frontend interaction itself resolves a payment dispute.

---

# 36. Billing Settings

Implement viewer-facing billing settings where supported.

Potential information includes:

- active memberships;
- billing history;
- next billing date;
- payment-provider management entry point;
- cancellation status.

Payment-method updates should use the provider's approved secure flow.

Do not collect or persist raw payment details outside the approved payment integration.

---

# 37. Payment-Method Management

If the provider supports viewer-managed payment methods through a hosted portal or secure SDK:

- launch the canonical provider flow;
- handle cancellation/return;
- refresh the authoritative billing state;
- show recoverable errors.

Do not invent a card-storage API.

Do not expose payment tokens or sensitive provider identifiers to analytics.

---

# 38. Creator Membership Management

Implement creator-facing membership configuration where supported.

Allow authorized creators to inspect and manage supported:

- membership tiers;
- tier names;
- descriptions;
- benefits;
- pricing;
- availability;
- membership status.

Only support fields and mutations defined by the backend contract.

Do not bypass server-side eligibility checks.

---

# 39. Membership Tier Configuration

For each editable tier:

- load authoritative data;
- display current configuration;
- allow supported edits;
- validate changes;
- track unsaved changes;
- submit through the canonical API;
- reconcile the updated tier;
- handle conflicts and failures.

Do not create local-only tiers that appear to be available for purchase.

---

# 40. Membership Benefit Configuration

Where supported, provide a safe creator-facing interface for configuring benefits.

The interface must:

- show valid benefits;
- use stable backend benefit identifiers;
- prevent unsupported combinations where defined by the contract;
- display validation errors;
- save and reconcile changes.

Do not advertise a membership benefit merely because its name has been entered in a text field if the platform requires a corresponding implemented entitlement.

---

# 41. Creator Membership Eligibility and Availability

Display authoritative creator eligibility and offering availability states.

If monetization is unavailable:

- show the appropriate supported explanation;
- avoid exposing internal enforcement data;
- do not allow an unavailable tier to be activated through frontend manipulation.

The backend must remain authoritative.

---

# 42. Creator Revenue Summaries

Integrate with the creator revenue-summary contract.

Where available, display:

- revenue summary;
- selected reporting period;
- membership-related revenue;
- transaction status aggregates;
- other supported monetization summaries.

Use server-provided aggregation.

Do not sum partial transaction-history pages to invent total revenue.

Do not assume gross revenue equals creator earnings or payout balance.

---

# 43. Revenue Definitions

Respect the meanings supplied by the backend.

Distinguish between available metrics such as:

- gross sales;
- refunds;
- fees;
- adjustments;
- estimated earnings;
- finalized earnings;
- payable balance;
- paid-out amount.

Only display metrics for which the API defines the meaning.

Do not derive net earnings by subtracting guessed fees or refunds.

Do not mix currencies without an explicit, authoritative conversion contract.

---

# 44. Revenue Time Ranges

Where supported, allow selection of reporting periods.

Use the canonical timezone and date model.

Display the range associated with the returned data.

Do not assume every metric is finalized at the end of the selected date range.

If data is estimated or delayed, display the status provided by the backend.

---

# 45. Payout Onboarding

If the creator platform supports payout onboarding through an external provider, integrate with the canonical onboarding flow.

Support:

- eligibility state;
- onboarding initialization;
- provider redirect or secure embedded flow;
- return handling;
- pending verification;
- completed onboarding;
- failed/requires-action state.

Do not fabricate payout onboarding completion.

Do not collect banking credentials directly in application forms unless the architecture explicitly provides an approved secure provider-managed mechanism.

---

# 46. Payout Status

Where supported, display authoritative payout state.

Possible presentation states may include:

- not configured;
- onboarding required;
- verification pending;
- eligible;
- payout pending;
- paid;
- failed;
- restricted.

Only use the statuses defined by the backend contract.

Do not infer that earnings have been paid merely because a payout request was accepted.

---

# 47. Payout History

If the backend provides payout history, render it using authoritative records.

Support:

- status;
- amount;
- currency;
- relevant timestamps;
- provider receipt/reference where safe;
- pagination;
- empty and error states.

Do not invent payout dates or transfer confirmations.

---

# 48. Tax Information Boundaries

If creator tax onboarding or tax-document access is supported, provide only the frontend entry points defined by the backend/provider contract.

Do not implement a tax engine.

Do not collect sensitive tax information through arbitrary application forms when a secure provider flow is required.

Do not store tax identifiers in local browser storage.

Do not make legal or tax-compliance claims that the backend does not substantiate.

---

# 49. Authentication and Authorization

Viewer and creator monetization routes must respect the canonical authentication and authorization model.

Support:

- authenticated viewer;
- anonymous viewer;
- creator;
- creator with limited permissions;
- expired session;
- restricted account.

Only authorized creators may manage their offerings and revenue information.

Only the appropriate viewer may access their own purchases and memberships.

Do not trust a client-supplied user ID as proof of ownership.

---

# 50. Cache Isolation and Invalidation

Use the project's established server-state library.

Cache keys must account for:

- authenticated viewer;
- creator/channel;
- membership;
- transaction or checkout reference;
- reporting period where relevant.

After relevant mutations, invalidate or reconcile:

- membership status;
- entitlements;
- purchase history;
- billing summary;
- creator tier configuration;
- revenue summaries;
- payout status.

Do not share one viewer's billing state with another viewer.

Do not cache checkout responses or provider sessions beyond their validity.

---

# 51. Account Switching

When the authenticated user changes:

- invalidate purchase history;
- invalidate memberships;
- clear transaction-specific UI state;
- invalidate viewer entitlements;
- invalidate billing settings;
- clear creator revenue caches;
- clear payout details;
- clear private membership configuration when account/channel context changes.

No account's financial information may remain visible after account switching.

---

# 52. Mutation Concurrency

Prevent stale or conflicting financial operations.

Examples include:

```text
Start checkout
Return from checkout
Retry checkout
```

and:

```text
Cancel membership
Change tier
Refresh membership state
```

Use request identity, backend idempotency support, and state reconciliation.

Do not let an outdated response overwrite a later confirmed transaction or membership state.

---

# 53. Security Requirements

The frontend must:

- never expose payment-provider secrets;
- never log payment credentials;
- never place raw payment details in URLs;
- avoid exposing signed checkout URLs through telemetry;
- use secure authentication/session behavior;
- safely validate provider return destinations;
- prevent open redirects;
- protect private billing records;
- respect backend authorization;
- avoid rendering untrusted provider error HTML.

Do not rely on client-only checks to enforce purchase permissions or financial state.

---

# 54. Privacy Requirements

Protect sensitive information, including:

- purchase history;
- membership relationships;
- billing details;
- creator revenue;
- payout status;
- tax onboarding state;
- payment-provider references.

Do not include detailed financial data in analytics unless explicitly authorized.

Do not expose transaction identifiers publicly without a product-approved reason.

Do not persist sensitive financial state unnecessarily in browser storage.

---

# 55. Accessibility

Implement:

- semantic membership offerings;
- accessible tier selection;
- accessible checkout buttons;
- readable pricing and billing intervals;
- accessible transaction status;
- keyboard-operable dialogs;
- clear cancellation confirmation;
- accessible revenue charts;
- screen-reader-friendly pending/error messages;
- visible focus;
- responsive payment-provider return states.

Do not communicate transaction state by color alone.

Revenue visualizations must include textual summaries.

---

# 56. Responsive Behavior

Support:

- mobile web;
- tablet;
- desktop;
- large desktop.

Membership tiers must remain understandable on narrow screens.

Checkout summaries must not hide material pricing details.

Purchase-history tables should adapt to mobile layouts.

Creator revenue summaries must remain readable on smaller screens.

Destructive membership and payout actions must remain clear and accessible.

---

# 57. Error Handling and Recovery

Normalize API and provider errors into meaningful user-facing categories.

At minimum distinguish:

```text
authentication
authorization
validation
checkoutCancelled
paymentFailed
transactionPending
transactionExpired
membershipUnavailable
conflict
rateLimited
temporarilyUnavailable
network
unknown
```

Use actual backend error codes when supplied.

Do not display raw payment-provider diagnostics.

Retry only operations that are safe to retry.

Do not automatically repeat a charge or create a new purchase after an ambiguous transaction result.

---

# 58. Observability and Telemetry

Instrument meaningful monetization interactions.

Potential events include:

```text
membership_offering_viewed
membership_tier_selected
checkout_initiated
checkout_redirected
checkout_returned
checkout_cancelled
checkout_failure_viewed
transaction_status_checked
membership_activated
membership_cancellation_started
membership_cancelled
membership_tier_changed
purchase_history_viewed
refund_request_started
creator_membership_settings_viewed
creator_membership_tier_updated
creator_revenue_viewed
payout_onboarding_started
payout_status_viewed
```

Use canonical project event names where available.

Separate:

- a user action;
- a checkout redirect;
- a payment-provider callback;
- a backend-confirmed transaction;
- an entitlement grant.

Do not send raw payment data, provider secrets, tax information, or private financial values to telemetry.

---

# 59. Testing Strategy

Implement automated tests for actual behavior.

### Unit tests

Cover:

- monetary display formatting;
- billing-interval display;
- transaction-state mapping;
- membership-state mapping;
- entitlement presentation;
- checkout-return parsing;
- idempotency-aware submission state;
- price/tier serialization;
- cache-key isolation;
- account-switch invalidation;
- revenue-period serialization;
- financial error classification.

### Component tests

Cover:

- membership tier cards;
- membership offering page;
- checkout summary;
- pending transaction state;
- failure/cancellation state;
- membership management;
- cancellation confirmation;
- purchase-history rows;
- refund entry point;
- creator membership editor;
- revenue summary;
- payout onboarding states.

### Integration tests

Cover:

- loading membership offerings;
- starting checkout;
- handling provider return;
- querying transaction status;
- confirming membership activation;
- rendering entitlements;
- cancelling a membership;
- viewing purchase history;
- requesting refunds where supported;
- modifying a membership tier;
- viewing creator revenue;
- payout-onboarding return handling;
- protecting viewer/creator financial data.

### End-to-end tests

At minimum:

1. open a channel membership offering;
2. inspect tiers and benefits;
3. select a tier;
4. initiate checkout through the configured integration or test-provider boundary;
5. handle a confirmed transaction response;
6. verify entitlement state comes from the authoritative backend;
7. exercise a cancelled checkout;
8. exercise a pending transaction;
9. exercise a failed transaction;
10. open active membership management;
11. cancel a membership where supported;
12. view purchase history;
13. open creator membership configuration as an authorized creator;
14. view revenue summaries where supported;
15. verify a normal viewer cannot access creator revenue;
16. verify account switching does not leak billing data.

Use provider sandbox/test facilities where available. Do not claim that real charges were processed unless they actually were.

---

# 60. Browser and Provider Compatibility

Validate the supported browser matrix and configured payment-provider integration.

Test:

- redirect navigation;
- provider return routes;
- interrupted checkout;
- refresh on return;
- pop-up restrictions if applicable;
- mobile checkout handoff;
- session expiration;
- secure provider-managed payment fields.

Do not assume every browser or provider supports identical embedded-checkout capabilities.

---

# 61. Performance

Optimize:

- membership-offering rendering;
- purchase-history pagination;
- creator revenue rendering;
- account-route transitions;
- transaction-status refresh behavior.

Do not poll transaction endpoints indefinitely.

Do not fetch an unbounded purchase history.

Do not rerender unrelated account pages when a membership component changes.

Do not eagerly load sensitive financial data across every settings route.

---

# 62. Documentation

Update documentation describing:

- monetization routes;
- paid-membership data models;
- checkout initialization;
- provider handoff;
- checkout return handling;
- transaction-status confirmation;
- entitlement presentation;
- membership cancellation;
- purchase history;
- refund support where implemented;
- creator revenue contracts;
- payout onboarding;
- cache isolation;
- security and privacy considerations;
- test-provider configuration.

Documentation must accurately describe the real implementation.

---

# 63. No Fake Financial Functionality

Do not create:

- fake checkout success;
- fabricated transaction IDs;
- fake membership activation;
- client-generated authoritative entitlement grants;
- hardcoded purchase history;
- fabricated revenue;
- fake payout completion;
- invented refund decisions;
- simulated provider redirects in production paths.

Mocks are permitted only within controlled automated tests.

The production application must use the project's real API and payment-provider boundaries.

---

# 64. No Placeholder Completion

Do not leave:

- TODO;
- FIXME;
- nonfunctional checkout buttons;
- fake membership management controls;
- placeholder payment status;
- incomplete error states;
- mock revenue charts in production paths;
- fake cancellation success;
- incomplete entitlement handling;
- “implement later” sections.

Everything within the current scope must be genuinely implemented.

---

# 65. Validation

Before completion, validate:

- TypeScript compilation;
- linting;
- unit tests;
- component tests;
- integration tests;
- end-to-end tests where available;
- production build;
- membership offering pages;
- checkout initiation;
- provider return handling;
- pending transaction handling;
- payment failure/cancellation handling;
- duplicate-purchase prevention;
- membership activation;
- membership cancellation;
- entitlement-aware presentation;
- purchase history;
- refund flow where supported;
- creator membership configuration;
- revenue summaries;
- payout onboarding where supported;
- viewer/creator authorization;
- account-switch isolation;
- responsive behavior;
- accessibility;
- sensitive-data handling.

Fix issues discovered within the current scope.

Do not claim that external payment-provider setup, real payment execution, payout onboarding, or banking verification has completed unless it was actually verified.

---

# 66. Definition of Done

This prompt is complete only when:

- paid membership discovery works;
- tiers and benefits display correctly;
- prices and currencies are authoritative;
- checkout initiation uses real contracts;
- the approved payment-provider integration works;
- checkout return handling is safe;
- pending transactions are handled correctly;
- failed and cancelled payments are handled correctly;
- duplicate submissions are prevented;
- membership activation is server-confirmed;
- entitlement presentation is accurate;
- active membership management works;
- cancellation works where supported;
- tier changes work where supported;
- purchase history works;
- receipts/invoices work where supported;
- refunds work where supported;
- billing settings work where supported;
- creator membership configuration works where supported;
- creator revenue summaries work where supported;
- payout onboarding/status works where supported;
- financial data is isolated by account;
- account switching does not leak financial state;
- security/privacy requirements are respected;
- accessible responsive interfaces are implemented;
- telemetry excludes prohibited sensitive information;
- tests cover the required behavior;
- documentation is updated;
- no fake production financial behavior remains;
- no current-scope placeholders remain;
- validation passes.

---

# 67. Completion Report

At the end of execution, provide a concise report containing:

### Implemented

Summarize paid memberships, checkout, viewer billing, entitlement presentation, creator membership management, and revenue-related functionality actually completed.

### Files

List significant files created, modified, or deleted.

### API and Provider Contracts

List membership, checkout, transaction, entitlement, billing, refund, creator revenue, payout, and telemetry contracts consumed.

### State and Financial Safety

Summarize transaction reconciliation, pending-state handling, duplicate-submission prevention, cache isolation, and account-switch behavior.

### Testing

List tests created and tests executed, identifying use of provider test/sandbox boundaries where applicable.

### Validation

Report type checking, linting, production build, and relevant integration validation.

### Integration Notes

Identify provider configuration requirements, external dependencies, unsupported contract capabilities, or remaining integration constraints.

### Out of Scope

Confirm that financial ledgers, payment processing backends, tax engines, payout execution, banking infrastructure, advertising systems, and mobile purchase flows were not improperly implemented.

---

# 68. Final Execution Directive

Execute this prompt as a concrete frontend implementation task.

Do not merely describe monetization or membership flows.

Do not provide a tutorial instead of implementation.

Inspect the repository first.

Implement only the scope defined by this prompt.

Preserve compatible existing behavior.

Use real project contracts and the configured payment-provider integration.

Do not fabricate transactions, payment success, memberships, entitlements, revenue, refunds, or payouts.

Do not ask what should be implemented.

Do not wait for another prompt.

Do not expand this task into unrelated frontend or backend domains.

Test and validate the implementation.

Update documentation where necessary.

Provide the required completion report after implementation.

The result must be a real, production-grade **YouTube-style web monetization, paid membership, checkout, entitlement, and creator revenue experience** that can be integrated with the independently generated backend, payment-provider integrations, and infrastructure through explicit contracts.
