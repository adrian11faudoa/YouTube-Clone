# YouTube-Style Video Platform — Backend Prompt — Volume 8

# 1. ROLE AND PURPOSE

You are the senior backend engineer responsible for implementing the eighth bounded backend milestone of the **YouTube-Style Video Platform**.

This milestone implements the platform's **monetization, payments, creator memberships, entitlements, billing, and external monetization integration boundaries**.

It is responsible for:

* creator monetization eligibility;
* monetization configuration;
* channel memberships;
* paid-access entitlements where applicable;
* payment-customer abstraction;
* payment methods through a provider abstraction;
* checkout/session orchestration;
* subscription billing;
* recurring membership billing;
* payment lifecycle;
* refunds;
* disputes;
* webhook processing;
* payout/accounting boundaries;
* monetization events;
* billing idempotency;
* entitlement enforcement;
* fraud/risk boundaries;
* creator revenue summaries;
* monetization audit records;
* monetization observability;
* security and privacy;
* tests and operational documentation.

This is a bounded implementation milestone.

It does not authorize implementation of the entire backend.

It does not authorize implementation of a full advertising exchange, ad-serving platform, tax engine, banking system, or financial ledger beyond the boundaries required by this milestone.

It does not authorize implementation of web or mobile monetization UI.

Implement only the functionality explicitly defined in this prompt.

The repository is the source of truth for actual implementation state.

Inspect the repository before making changes.

Do not rely on another AI conversation.

Do not assume that an earlier AI prompt was executed merely because it exists in the conversation.

Do not fabricate repository state.

---

# 2. PROJECT CONTEXT

## 2.1 Product

The project is an independent, production-grade video platform supporting:

* viewers;
* creators;
* channels;
* long-form video;
* short-form video;
* uploads;
* media processing;
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
* monetization-capable integrations.

This milestone adds the backend monetization infrastructure required to support paid creator relationships and other controlled revenue-generating capabilities.

## 2.2 Scale Direction

The completed platform is intended to evolve toward:

* hundreds of millions of users;
* millions of daily transactions;
* large numbers of recurring memberships;
* high-volume webhook processing;
* large creator populations;
* substantial financial-event volume.

This milestone must therefore avoid:

* synchronous payment operations inside unrelated domain transactions;
* provider-specific payment state becoming the sole source of truth;
* non-idempotent webhook processing;
* exposing payment credentials to clients;
* assuming payment success without verified provider confirmation.

---

# 3. TECHNOLOGY DIRECTION

Use the existing compatible backend stack:

* TypeScript;
* Node.js LTS;
* NestJS;
* PostgreSQL;
* Redis;
* durable queues;
* event streaming;
* REST;
* OpenAPI;
* OpenTelemetry-compatible observability.

External payment providers must remain behind explicit adapters.

The implementation must not hardcode one provider's object model into the core domain.

Provider-specific IDs must be stored as external references, not mistaken for canonical platform IDs.

---

# 4. CURRENT MILESTONE SCOPE

Implement:

1. Monetization domain.
2. Monetization eligibility.
3. Creator monetization configuration.
4. Membership/product definitions.
5. Pricing configuration.
6. Customer abstraction.
7. Payment-provider abstraction.
8. Checkout-session orchestration.
9. Recurring membership billing.
10. Membership lifecycle.
11. Entitlement lifecycle.
12. Payment transaction state.
13. Refund handling.
14. Dispute/chargeback state boundary.
15. Provider webhook ingestion.
16. Webhook signature verification boundary.
17. Webhook idempotency.
18. Payment-reconciliation jobs.
19. Revenue-event processing.
20. Creator revenue summaries.
21. Platform-fee representation.
22. Payout/accounting boundary.
23. Monetization audit logging.
24. Fraud/risk integration boundary.
25. Entitlement authorization.
26. Monetization events.
27. Notification integration events.
28. Analytics integration events.
29. Rate limiting and abuse controls.
30. Security and privacy protections.
31. Observability.
32. Unit, integration, API, concurrency, webhook, and security tests.
33. API documentation.
34. Operational documentation.

This milestone does not implement:

* full advertising auctions;
* real-time ad bidding;
* external banking infrastructure;
* tax calculation platform;
* legal entity/accounting ERP integration;
* automated payout execution without a verified provider integration;
* web monetization UI;
* mobile monetization UI.

Provider integration must be real where credentials/configuration are available.

When provider credentials are unavailable, implement the actual adapter boundary and test it appropriately without claiming live-provider success.

---

# 5. REPOSITORY INSPECTION

Before implementation:

1. Inspect user/account infrastructure.
2. Inspect channel ownership.
3. Inspect authorization.
4. Inspect subscriptions.
5. Inspect notifications.
6. Inspect analytics.
7. Inspect administration and audit logging.
8. Inspect event infrastructure.
9. Inspect queue infrastructure.
10. Inspect configuration.
11. Inspect existing external integration abstractions.
12. Inspect database models and migrations.
13. Inspect API documentation.
14. Inspect tests.
15. Inspect observability.

Reuse compatible infrastructure.

Do not create duplicate identity, notification, event, or audit systems.

---

# 6. MONETIZATION DOMAIN BOUNDARY

Create a dedicated monetization domain responsible for:

* monetization eligibility;
* monetization products;
* pricing;
* memberships;
* customer references;
* payment transactions;
* provider references;
* entitlements;
* refunds;
* disputes;
* revenue records;
* creator revenue summaries;
* payout/accounting boundaries.

The monetization domain does not own:

* users;
* channels;
* videos;
* subscriptions to channels;
* comments;
* playlists.

It references those entities through canonical IDs and explicit domain contracts.

---

# 7. MONETIZATION ELIGIBILITY

Implement explicit monetization eligibility.

Eligibility may depend on:

* channel status;
* account status;
* moderation state;
* creator configuration;
* supported product type;
* geographic/provider availability where configured.

Do not hardcode complex legal eligibility rules into controllers.

Represent eligibility through a domain policy.

Eligibility failures must produce deterministic domain errors.

A user must not be able to create paid products for a channel they do not control.

---

# 8. MONETIZATION PRODUCT MODEL

Implement a product model for monetizable offerings.

At minimum support a product concept such as:

* product ID;
* channel ID;
* product type;
* name;
* description;
* currency;
* price;
* billing interval where recurring;
* status;
* provider reference;
* createdAt;
* updatedAt;
* deactivatedAt where applicable.

Support product types needed for current scope, such as:

* channel membership;
* paid entitlement where explicitly supported.

Do not create arbitrary financial product types.

---

# 9. PRICING MODEL

Define pricing independently from UI.

Represent:

* amount in minor currency units;
* ISO currency;
* billing interval;
* interval count where applicable;
* effective state;
* provider price reference.

Never represent money using floating-point values.

Do not infer currency from locale.

Currency must be explicit.

Do not silently change an active customer's price.

Price changes must be versioned/effective-dated according to the billing contract.

---

# 10. CREATOR MEMBERSHIP MODEL

Implement channel membership plans.

A membership plan must identify:

* channel;
* product;
* name;
* benefits summary;
* price;
* billing interval;
* availability;
* eligibility;
* provider references.

Benefits must be represented as controlled entitlement definitions where access enforcement depends on them.

Do not rely on free-form text to authorize paid features.

---

# 11. CUSTOMER ABSTRACTION

Create a provider-neutral customer abstraction.

Represent:

* platform user ID;
* provider;
* external customer ID;
* lifecycle;
* createdAt;
* metadata required for reconciliation.

A platform user must map to a provider customer through an explicit relationship.

Do not use provider customer IDs as platform user IDs.

Do not expose provider customer identifiers through public APIs unless explicitly required.

---

# 12. PAYMENT METHOD BOUNDARY

Do not store raw payment credentials.

Create a provider abstraction for:

* adding payment method;
* listing eligible payment methods where supported;
* removing payment method;
* selecting default payment method;
* payment-method failure state.

Store only provider tokens/references that are intended for storage and are safely scoped.

Never store:

* full card numbers;
* CVVs;
* raw bank credentials;
* provider secrets.

Follow the payment provider's secure tokenization model.

---

# 13. CHECKOUT SESSION

Implement a checkout abstraction.

A checkout session must contain:

* checkout ID;
* user;
* product;
* price;
* currency;
* quantity where applicable;
* idempotency key;
* provider reference;
* status;
* expiration;
* createdAt.

The checkout session must be associated with a specific product/version/price.

Do not allow clients to submit an arbitrary amount and have the backend charge it.

The server must resolve the authoritative product price.

---

# 14. CHECKOUT FLOW

Implement:

```text
Client
  ↓
Create Checkout Session
  ↓
Validate Product + Eligibility
  ↓
Resolve Authoritative Price
  ↓
Create Provider Checkout
  ↓
Return Controlled Checkout Reference
  ↓
Provider Payment
  ↓
Verified Webhook
  ↓
Payment State
  ↓
Entitlement
  ↓
Notification / Analytics Events
```

Do not treat the client redirect as proof of payment.

Provider confirmation or another authoritative server-side mechanism must establish the payment result.

---

# 15. PAYMENT TRANSACTION MODEL

Implement a payment transaction model.

At minimum:

* transaction ID;
* user ID;
* product ID;
* channel ID;
* amount;
* currency;
* provider;
* external transaction ID;
* status;
* failure reason category;
* createdAt;
* updatedAt;
* completedAt;
* refundedAt where applicable.

Use canonical platform identifiers.

Provider transaction IDs must remain external references.

---

# 16. PAYMENT STATES

Implement explicit states such as:

* pending;
* requires_action;
* authorized;
* succeeded;
* failed;
* cancelled;
* partially_refunded;
* refunded;
* disputed.

Do not allow arbitrary client-controlled payment state.

Provider events and trusted reconciliation operations must drive state changes.

---

# 17. PAYMENT IDEMPOTENCY

All charge-creating operations must use idempotency.

At minimum protect:

* checkout creation;
* payment confirmation where the provider supports it;
* membership creation;
* refund creation;
* webhook processing;
* reconciliation.

A retry must not create duplicate charges.

Persist idempotency state according to the project-wide contract.

---

# 18. MEMBERSHIP SUBSCRIPTION MODEL

Implement paid membership subscriptions separately from free channel subscriptions.

Represent:

* membership subscription ID;
* user;
* channel;
* product;
* provider subscription reference;
* status;
* current period start;
* current period end;
* renewal state;
* cancellation state;
* createdAt;
* updatedAt;
* cancelledAt.

Do not overload the ordinary channel-subscription relationship with paid billing state.

---

# 19. MEMBERSHIP LIFECYCLE

Support:

* active;
* trialing where explicitly configured;
* past_due;
* paused where supported;
* cancelling;
* cancelled;
* expired.

Transitions must be provider-aware and idempotent.

Do not revoke entitlement before the authoritative billing state requires it.

Do not maintain access solely from a client-side purchase receipt.

---

# 20. ENTITLEMENT MODEL

Implement a canonical entitlement model.

An entitlement must represent:

* entitlement ID;
* user;
* channel/product;
* capability;
* status;
* source;
* start;
* expiration;
* revocation reason where applicable.

Examples of future capabilities may include:

* membership-only content;
* membership-only badges;
* membership-only chat;
* other creator-defined paid capabilities.

The entitlement model must remain independent from presentation/UI.

---

# 21. ENTITLEMENT AUTHORIZATION

Implement backend enforcement for paid capabilities where this milestone exposes them.

A request must verify:

1. authenticated user;
2. entitlement existence;
3. entitlement state;
4. entitlement expiration;
5. target resource;
6. required capability.

Do not trust the client to declare that a user is a paid member.

Entitlement checks must be server-side.

---

# 22. MEMBERSHIP BENEFIT CONFIGURATION

Define controlled membership capabilities.

Do not permit arbitrary client-generated entitlement names to create authorization privileges.

Use stable capability identifiers.

The backend must validate that a configured membership product can grant only capabilities supported by the platform.

---

# 23. REFUNDS

Implement refund orchestration.

Support:

* full refund;
* partial refund only if the provider/product contract supports it;
* refund request;
* refund pending;
* refund succeeded;
* refund failed.

Do not grant refund-related state based solely on a client request.

Verify the provider outcome.

Update membership/entitlement state according to explicit business rules.

---

# 24. REFUND ENTITLEMENT BEHAVIOR

Define how entitlements behave after:

* full refund;
* partial refund;
* cancellation;
* provider failure.

Do not silently revoke access in a way inconsistent with the product/billing policy.

Where policy is configurable, model it explicitly.

---

# 25. DISPUTES AND CHARGEBACKS

Create a dispute/chargeback boundary.

Represent:

* dispute ID;
* transaction;
* provider;
* external reference;
* status;
* reason;
* openedAt;
* resolvedAt.

Support states such as:

* opened;
* under_review;
* won;
* lost;
* closed.

Do not implement provider-specific legal workflows beyond the scoped backend boundary.

Dispute state must be auditable.

---

# 26. PAYMENT WEBHOOKS

Implement secure provider webhook ingestion.

For every webhook:

1. authenticate/verify provider signature;
2. validate payload schema;
3. identify provider event;
4. identify external resource;
5. check idempotency;
6. map to canonical domain event;
7. update canonical state;
8. emit internal events;
9. record processing result.

Do not process unauthenticated arbitrary webhook requests.

---

# 27. WEBHOOK IDEMPOTENCY

Persist processed webhook event IDs or equivalent idempotency references.

Repeated provider webhook delivery must not:

* create duplicate memberships;
* grant duplicate entitlements;
* duplicate refunds;
* duplicate revenue events;
* repeatedly apply enforcement.

Webhook processing must be safe under at-least-once delivery.

---

# 28. WEBHOOK ORDERING

Do not assume webhook delivery order.

Use:

* provider event timestamps where meaningful;
* subscription/payment version;
* current canonical state;
* sequence numbers where available.

An older webhook must not revert a newer billing state.

When provider state is ambiguous, schedule reconciliation rather than guessing.

---

# 29. PAYMENT RECONCILIATION

Implement background reconciliation jobs for:

* payment transactions;
* recurring memberships;
* refunds;
* disputes;
* entitlements.

Reconciliation must compare:

* canonical platform state;
* provider references;
* trusted provider state.

Do not blindly overwrite platform state with provider data without validating ownership and resource mapping.

Reconciliation jobs must be:

* idempotent;
* retryable;
* auditable;
* rate-limited.

---

# 30. PAYMENT FAILURE HANDLING

Classify failures such as:

* payment declined;
* expired payment method;
* provider unavailable;
* authentication required;
* invalid product;
* invalid customer;
* webhook verification failure;
* duplicate request;
* fraud/risk rejection.

Expose stable public error categories.

Do not expose provider secrets or sensitive fraud signals.

---

# 31. FRAUD AND RISK BOUNDARY

Create a provider-neutral risk evaluation boundary.

It may consume signals such as:

* repeated failed payments;
* unusual checkout activity;
* excessive account/payment-method changes;
* suspicious membership creation;
* repeated refund behavior.

Do not implement a full fraud model in this milestone.

Allow a future fraud provider or risk engine to integrate through an explicit interface.

Do not automatically impose permanent account restrictions based only on a weak heuristic.

---

# 32. REVENUE EVENTS

Publish canonical monetization events including:

* monetization.product.created;
* checkout.created;
* payment.pending;
* payment.succeeded;
* payment.failed;
* membership.created;
* membership.updated;
* membership.cancelled;
* entitlement.granted;
* entitlement.revoked;
* refund.requested;
* refund.succeeded;
* refund.failed;
* dispute.opened;
* dispute.resolved;
* payout.eligible where applicable.

Use the established event envelope.

Do not expose payment credentials in events.

---

# 33. REVENUE MODEL

Implement a revenue representation suitable for creator reporting.

At minimum represent:

* gross amount;
* platform fee where configured;
* provider fee where available;
* refunds;
* net creator amount;
* currency;
* transaction source;
* recognition state.

Do not represent money using floating-point arithmetic.

Avoid pretending this model is a complete general ledger.

It is a monetization revenue-summary model.

---

# 34. CREATOR REVENUE SUMMARIES

Implement creator-facing aggregate data for:

* gross sales;
* refunds;
* fees;
* net revenue;
* active memberships;
* new memberships;
* cancelled memberships;
* recurring revenue summaries.

Enforce:

* channel ownership;
* authorized creator roles;
* privacy.

Do not expose individual buyer identities unless the product contract explicitly permits it.

---

# 35. PAYOUT BOUNDARY

Create a payout/accounting boundary without pretending to operate a banking system.

Represent:

* creator payout account reference;
* payout status;
* eligible balance;
* payout period;
* external payout reference;
* failure state.

Do not store bank credentials.

Do not initiate a real payout unless a verified payout-provider integration is configured.

The platform must distinguish:

* revenue earned;
* revenue eligible for payout;
* payout initiated;
* payout completed.

---

# 36. PAYOUT EVENTS

Support events such as:

* payout.eligible;
* payout.requested;
* payout.processing;
* payout.completed;
* payout.failed.

These events must be auditable.

Do not claim bank settlement occurred merely because an internal payout job was created.

---

# 37. TAX DATA BOUNDARY

Do not implement a full tax calculation engine.

Create only the boundary needed to support:

* tax identifier reference where legally required;
* country/region information required by provider workflows;
* provider-generated tax state;
* external tax service reference.

Do not store unnecessary sensitive tax documents unless explicitly required.

Do not fabricate tax determinations.

---

# 38. CURRENCY AND MONEY SAFETY

Implement a project-wide money type.

Requirements:

* integer minor units or exact decimal representation;
* explicit ISO currency;
* no floating-point arithmetic;
* explicit rounding rules;
* immutable transaction amount after payment authorization.

Define how:

* platform fees;
* provider fees;
* refunds;
* taxes;
* creator revenue

are represented.

---

# 39. MONETIZATION CACHE

Use Redis where justified for:

* product catalog reads;
* membership status;
* entitlement lookups;
* creator revenue dashboard summaries.

Every cache must define:

* key;
* TTL;
* source of truth;
* invalidation;
* privacy boundary.

Never use a stale cache to authorize paid access after entitlement revocation without an explicitly acceptable propagation delay.

---

# 40. NOTIFICATION INTEGRATION

Publish events for existing notification workflows such as:

* membership activated;
* membership cancelled;
* payment failed;
* payment recovered;
* creator membership milestone;
* refund processed.

Do not call notification providers directly.

The notification domain remains responsible for delivery.

---

# 41. ANALYTICS INTEGRATION

Publish monetization analytics events for:

* checkout initiated;
* checkout succeeded;
* checkout failed;
* membership started;
* membership cancelled;
* refund;
* dispute;
* payout state.

Do not send payment credentials or unnecessary sensitive financial data into analytics events.

---

# 42. ADMINISTRATION AND AUDIT

All privileged monetization operations must be auditable.

Audit:

* product creation/update;
* price changes;
* eligibility changes;
* refund decisions;
* payout-state changes;
* entitlement overrides;
* reconciliation overrides;
* administrative payment actions.

Do not allow normal users to modify financial audit records.

---

# 43. SECURITY REQUIREMENTS

Protect against:

* payment tampering;
* price manipulation;
* duplicate charges;
* webhook forgery;
* entitlement escalation;
* provider-reference substitution;
* unauthorized refunds;
* unauthorized payout changes;
* cross-creator revenue access;
* leaked payment information.

The backend must resolve authoritative:

* product;
* price;
* currency;
* user;
* channel;
* entitlement

from trusted server-side state.

Never trust client-provided final pricing or payment status.

---

# 44. API SURFACE

Implement API families for:

## Monetization Products

* create product;
* update product;
* activate/deactivate;
* retrieve product.

## Memberships

* list available membership plans;
* create checkout;
* retrieve current membership;
* cancel membership;
* restore/reactivate where supported.

## Entitlements

* retrieve current user entitlement state;
* verify access where required by internal services.

## Payments

* checkout status;
* payment status where appropriate.

## Creator Revenue

* revenue summary;
* membership metrics;
* payout status.

## Webhooks

* provider-specific webhook ingestion endpoints behind secure verification.

Do not expose:

* raw payment credentials;
* arbitrary refund APIs to normal users;
* internal reconciliation controls;
* unrestricted financial data.

---

# 45. AUTHORIZATION MATRIX

Create an implementation-level matrix.

At minimum:

| Operation                      | Anonymous | Authenticated User | Channel Owner                | Moderator                         | Administrator |
| ------------------------------ | --------- | ------------------ | ---------------------------- | --------------------------------- | ------------- |
| View public membership product | Allowed   | Allowed            | Allowed                      | Allowed                           | Allowed       |
| Create membership checkout     | No        | Allowed            | Allowed                      | Privileged                        | Privileged    |
| Read own membership            | No        | Own only           | Own only                     | Privileged                        | Privileged    |
| Cancel own membership          | No        | Own only           | Own only                     | Privileged                        | Privileged    |
| Create membership product      | No        | No                 | Owner only                   | No unless explicitly permissioned | Allowed       |
| Read own creator revenue       | No        | No                 | Owner only                   | Restricted                        | Allowed       |
| Manage product price           | No        | No                 | Owner only with permission   | No                                | Allowed       |
| Refund customer                | No        | No                 | Restricted by policy         | Restricted                        | Permissioned  |
| Override entitlement           | No        | No                 | No unless explicitly allowed | Permissioned                      | Permissioned  |
| Read sensitive payment data    | No        | No                 | Restricted                   | Restricted                        | Permissioned  |

Refine permissions to match the implemented role model.

---

# 46. RATE LIMITING

Protect:

* checkout creation;
* membership changes;
* payment-status queries;
* refund requests;
* device/payment-method changes where applicable;
* webhook endpoints;
* creator financial APIs.

Provider webhooks must have appropriate infrastructure-level and application-level abuse controls without blocking valid provider retries.

---

# 47. OBSERVABILITY

Track:

## Payments

* checkout creation;
* payment success/failure;
* provider latency;
* webhook volume;
* webhook failures;
* duplicate webhooks;
* reconciliation discrepancies;
* refund volume;
* dispute volume.

## Memberships

* activation;
* cancellation;
* renewal;
* expiration;
* entitlement failures.

## Revenue

* gross revenue;
* refunds;
* reconciliation lag;
* payout state.

Sensitive financial data must not be emitted as high-cardinality metrics or ordinary logs.

Do not log full provider webhook payloads when they contain sensitive information.

---

# 48. TESTING REQUIREMENTS

Create real tests.

## Unit Tests

Test:

* money arithmetic;
* price resolution;
* eligibility;
* membership transitions;
* entitlement decisions;
* refund rules;
* webhook mapping;
* risk policy;
* revenue calculations.

## Integration Tests

Test:

* product persistence;
* checkout creation;
* memberships;
* entitlements;
* webhook processing;
* queue workers;
* reconciliation;
* audit logging.

## Webhook Tests

Test:

* valid signature;
* invalid signature;
* duplicate webhook;
* out-of-order webhook;
* unknown event;
* malformed payload;
* provider retry.

## Concurrency Tests

Test:

* duplicate checkout;
* simultaneous membership creation;
* cancellation/renewal races;
* refund races;
* entitlement grant/revoke races;
* duplicate reconciliation.

## Security Tests

Test:

* price tampering;
* entitlement escalation;
* cross-user membership access;
* cross-creator revenue access;
* unauthorized refunds;
* webhook forgery;
* payout privilege escalation.

## Financial Correctness Tests

Test:

* currency handling;
* minor-unit arithmetic;
* fees;
* refunds;
* net revenue;
* rounding.

---

# 49. PERFORMANCE VALIDATION

Measure:

* checkout creation latency;
* membership status query;
* entitlement lookup;
* webhook processing throughput;
* reconciliation throughput;
* creator revenue query latency.

Do not claim payment-provider performance from local tests.

Report external dependency limitations honestly.

---

# 50. API DOCUMENTATION

Update OpenAPI for:

* products;
* memberships;
* checkout;
* entitlement access;
* creator revenue;
* webhook endpoints.

Document:

* authentication;
* permissions;
* error categories;
* idempotency;
* currency representation;
* state transitions.

Do not expose internal provider secrets or unrestricted financial fields.

---

# 51. OPERATIONAL DOCUMENTATION

Document:

* provider configuration;
* webhook setup;
* webhook verification;
* idempotency;
* reconciliation;
* refunds;
* disputes;
* membership lifecycle;
* entitlement recovery;
* payout boundaries;
* audit requirements;
* incident handling;
* provider outage behavior.

Do not include real production credentials.

Do not claim successful provider settlement without external confirmation.

---

# 52. EXPLICIT OUT-OF-SCOPE BOUNDARIES

Do not implement:

* a full advertising marketplace;
* real-time ad bidding;
* a banking system;
* a general ledger;
* a tax engine;
* legal entity management;
* automated banking settlement without a verified provider;
* advanced fraud ML;
* web monetization UI;
* mobile monetization UI.

Do not fabricate provider behavior.

Do not represent test-provider transactions as real production payments.

---

# 53. VALIDATION REQUIREMENTS

Before completion, verify:

## Products

* creators can only manage authorized products;
* prices are server-authoritative;
* currencies are explicit;
* price changes preserve existing billing contracts.

## Checkout

* checkout requests are idempotent;
* arbitrary client pricing is rejected;
* provider references are stored correctly.

## Payments

* valid provider events update state;
* duplicate events are safe;
* out-of-order events cannot regress state;
* failed payments are represented correctly.

## Memberships

* membership state matches authoritative billing state;
* cancellation is idempotent;
* entitlements are granted/revoked correctly.

## Refunds

* unauthorized refunds fail;
* duplicate refunds are prevented;
* refund state is reconciled.

## Revenue

* calculations use exact money arithmetic;
* creator ownership is enforced;
* refunds/fees affect summaries correctly.

## Security

* payment credentials are not stored;
* webhook signatures are verified;
* price tampering fails;
* entitlement escalation fails;
* financial data is isolated.

---

# 54. DEFINITION OF DONE

This milestone is complete only when:

1. The repository has been inspected.
2. Monetization eligibility is implemented.
3. Monetization products are implemented.
4. Pricing is implemented with exact money representation.
5. Creator membership plans are implemented.
6. Customer abstraction is implemented.
7. Payment-provider abstraction is implemented.
8. Checkout sessions are implemented.
9. Payment transaction lifecycle is implemented.
10. Idempotent payment operations are implemented.
11. Membership billing state is implemented.
12. Entitlements are implemented.
13. Entitlement authorization is implemented.
14. Refund handling is implemented.
15. Dispute state is implemented.
16. Secure webhook processing is implemented.
17. Webhook idempotency is implemented.
18. Webhook ordering protections are implemented.
19. Reconciliation jobs are implemented.
20. Fraud/risk integration boundary is implemented.
21. Revenue summaries are implemented.
22. Payout boundary is implemented.
23. Tax-data boundary is implemented where required.
24. Monetization events are implemented.
25. Notification integration events are implemented.
26. Analytics integration events are implemented.
27. Administrative audit logging is implemented.
28. Security controls are implemented.
29. Rate limits are implemented.
30. Observability is implemented.
31. Unit tests are implemented.
32. Integration tests are implemented.
33. Webhook tests are implemented.
34. Concurrency tests are implemented.
35. Security tests are implemented.
36. Financial correctness tests are implemented.
37. Performance validation has been performed.
38. API documentation is updated.
39. Operational documentation is updated.
40. No real payment capability is falsely claimed where external credentials are unavailable.
41. No hardcoded payment secrets exist.
42. No fake financial state substitutes for current-scope functionality.
43. No intentional TODO/FIXME gap substitutes for required functionality.
44. Known limitations are reported honestly.

---

# 55. COMPLETION REPORT

At the end of execution, provide a completion report containing:

## Files Created

List every new file.

## Files Modified

List every modified file.

## Files Deleted

List deleted files, or state that none were deleted.

## Monetization

Summarize:

* product model;
* pricing;
* eligibility;
* membership plans;
* entitlements.

## Payments

Summarize:

* provider abstraction;
* checkout;
* transaction lifecycle;
* webhooks;
* reconciliation;
* refunds;
* disputes.

## Revenue

Summarize:

* creator revenue;
* fees;
* payout boundary;
* financial event processing.

## Database Changes

List:

* models;
* migrations;
* indexes;
* constraints.

## Events and Jobs

List:

* monetization events;
* webhook jobs;
* reconciliation jobs;
* payout-related jobs.

## Tests

List:

* unit tests;
* integration tests;
* webhook tests;
* security tests;
* concurrency tests;
* financial correctness tests;
* performance validation.

## Documentation

List documentation created or updated.

## Known Limitations

List intentionally deferred functionality.

## Unresolved Issues

List only genuine unresolved implementation issues.

Do not claim that a live payment provider, banking system, tax engine, or payout network was provisioned unless it actually was.

# 56. FINAL EXECUTION RULE

Implement only the monetization, payment, membership, entitlement, revenue, payout-boundary, and supporting backend functionality defined by this milestone.

Do not implement unrelated future domains.

Do not redesign established contracts arbitrarily.

Do not rely on another AI prompt.

Do not fabricate repository state.

Do not store payment credentials.

Do not use fake successful payments, fake provider webhooks, fake payouts, placeholder financial calculations, pseudo-code, or intentionally incomplete current-scope implementations.

Produce real, tested, secure, privacy-aware, auditable, observable backend functionality within this milestone's scope.
