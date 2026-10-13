# YouTube-Style Video Platform — Mobile Prompt — Volume 9

## Premium Memberships, Channel Memberships, Purchases, Subscription Management, and Entitlements

### 1. Mission and Implementation Scope

Implement the production-grade **mobile subscription, premium-benefit, channel-membership, purchase, billing-status, and entitlement experience** for the YouTube-style video platform using React Native and TypeScript on iOS and Android.

The platform targets approximately 250 million registered users and 50 million daily active users. This milestone must provide a secure, accessible, and commercially realistic mobile purchasing experience while preserving compatibility with the platform's existing account, video, creator, and billing architecture.

The mobile application must allow eligible users to discover available paid offerings, review their benefits and prices, initiate supported purchase flows, restore or reconcile eligible purchases, view their active entitlements, and manage subscription-related state. Where creator channel memberships are supported, users must also be able to discover membership tiers and access the benefits associated with their membership.

All purchase and entitlement states must reflect authoritative billing or backend information. Never manufacture successful purchases, invent subscription prices, grant paid benefits based on local UI state, or pretend that an external payment provider has confirmed a transaction.

This prompt is independently executable in a fresh coding-agent conversation. It contains the scope, implementation constraints, integration requirements, tests, and completion criteria for this milestone.

### 2. Technology and Engineering Constraints

Use the established project technology direction:

- **Mobile:** React Native and TypeScript.
- **Backend:** TypeScript and NestJS.
- **Primary database:** PostgreSQL.
- **Caching and distributed state:** Redis where appropriate to backend services.
- **Authentication:** The platform's established account, session, and authorization contracts.
- **Payments:** The platform's authoritative payment and subscription architecture, including supported native app-store billing integrations where required.
- **Entitlements:** Backend-authoritative subscription and benefit state.
- **Observability:** The project's existing structured logging, telemetry, error reporting, and correlation conventions.

Inspect the repository, API specifications, billing contracts, navigation conventions, design system, and existing mobile subscription functionality genuinely available in the execution environment.

Preserve established project terminology, models, API behavior, and architectural boundaries. Do not assume independently generated project parts share a repository or conversation history.

When payment-provider or app-store integrations are not available in the supplied artifacts, explicitly document the missing dependencies and define portable proposed contracts. Do not present a proposed integration as an operational payment system.

### 3. Required Deliverables

Implement the mobile experience for:

1. Premium subscription discovery and benefit presentation.
2. Creator channel-membership discovery and supported membership tiers.
3. Purchase initiation through the approved billing architecture.
4. Purchase processing, pending states, failures, and confirmation.
5. Server-side receipt or transaction verification integration.
6. Purchase restoration and entitlement reconciliation.
7. Premium and channel-membership status.
8. Entitlement-aware access to applicable benefits.
9. Subscription renewal, expiration, cancellation, and billing-problem states.
10. Links and navigation to supported subscription-management experiences.
11. Transaction-safe state handling, security, accessibility, and recovery.
12. Automated tests, configuration documentation, and portable integration contracts.

Use reusable components and typed repositories. Keep pricing, purchase orchestration, entitlement state, navigation, and UI rendering separated according to the existing application architecture.

### 4. Product Offerings and Purchase Catalog

Integrate with the authoritative offering catalog provided by the backend or approved billing provider.

The mobile experience may include the following offering categories where they belong to the established product scope:

- Platform-wide premium subscriptions.
- Ad-free or enhanced viewing benefits.
- Background playback or offline viewing benefits where supported.
- Creator channel memberships.
- Channel-specific membership tiers.
- Other approved paid subscriptions or recurring offerings explicitly defined by the platform.

Do not independently invent products, prices, currencies, trial periods, renewal terms, benefit definitions, or eligibility rules.

Each offering must be represented using the actual available contract fields, such as:

- Stable product or offering identifier.
- Display name and description.
- Benefit summary.
- Price and currency.
- Billing interval.
- Trial or introductory offer information, if available.
- Eligibility restrictions.
- Applicable channel or creator identifier.
- Purchase availability.
- Subscription terms and associated legal disclosures.

Clearly distinguish platform-wide premium benefits from individual channel memberships. They must not share identifiers, entitlement ownership, renewal assumptions, or cancellation semantics unless the authoritative billing model explicitly defines that relationship.

When an offering cannot be loaded or confirmed, show an appropriate loading, unavailable, or retry state rather than a fabricated catalog entry.

### 5. Premium Subscription Discovery

Implement a mobile premium-discovery experience integrated with the existing account and viewing navigation.

The experience should explain applicable premium benefits, display available plans, and provide a clear route to review and purchase an eligible offering.

Requirements:

- Display accurate offering details.
- Explain relevant benefits using the platform's authoritative descriptions.
- Show the actual price and billing interval.
- Identify applicable trial or introductory terms when returned by the approved provider.
- Present renewal and cancellation terms accurately.
- Display relevant eligibility restrictions and unsupported-device conditions.
- Prevent duplicate purchase attempts caused by repeated taps.
- Handle unavailable, ineligible, and previously purchased offerings.
- Provide accessible loading, error, and empty states.

Do not claim that an offering includes a feature unless the authoritative product configuration grants that entitlement.

If the user already has the relevant subscription, present the actual entitlement state and appropriate management actions rather than encouraging a duplicate purchase.

### 6. Creator Channel Memberships

Implement the mobile discovery and purchase experience for channel memberships where supported by the platform's product and billing architecture.

#### 6.1 Channel membership discovery

Provide an appropriate entry point from existing channel and creator surfaces.

Display only supported membership information, including:

- Creator or channel identity.
- Membership tier name.
- Price and billing interval.
- Tier-specific benefits.
- Applicable badges, emoji, or member-only features where defined by the platform.
- Eligibility restrictions.
- Current membership status.

Use the platform's established channel and creator models.

Do not duplicate channel metadata systems or invent independent membership-tier identifiers.

#### 6.2 Membership tiers

Where multiple membership tiers are available, present them clearly and distinguish their benefits.

Requirements:

- Display the authoritative tier and pricing configuration.
- Identify the tier currently associated with the user's membership.
- Explain applicable upgrades or downgrades using the supported contract.
- Handle unavailable or retired tiers.
- Avoid granting higher-tier benefits until the corresponding entitlement is confirmed.
- Handle expired, pending, cancelled, or suspended memberships accurately.

An upgrade or downgrade may involve different billing rules depending on the provider. Do not assume immediate proration, immediate benefit changes, or a specific renewal date unless the authoritative billing contract confirms them.

#### 6.3 Membership benefits

Integrate with the existing client features that enforce channel-member benefits.

Possible benefits include member-only videos, member-only live chats, badges, or other supported channel features.

The mobile app must use the platform's authoritative entitlement result to determine eligibility. Do not treat a locally selected tier, completed animation, or unverified store callback as authorization.

Do not implement creator membership configuration tools, creator revenue dashboards, or channel-membership billing infrastructure in this milestone.

### 7. Purchase Flow Architecture

Implement a purchase orchestration layer that separates the user interface from the underlying billing provider.

Use the established billing architecture and approved mobile billing integration. Keep platform-specific behavior behind typed abstractions so billing details do not leak throughout the screen components.

A purchase flow must support the phases applicable to the real provider:

1. Load and validate the offering.
2. Confirm purchase eligibility.
3. Initiate the approved billing operation.
4. Handle user confirmation or cancellation.
5. Represent pending or deferred transactions where supported.
6. Receive the provider's transaction result.
7. Submit the appropriate transaction or verification information to the backend.
8. Wait for authoritative transaction verification and entitlement reconciliation where required.
9. Display the resulting subscription or membership status.
10. Finalize or acknowledge the transaction according to the provider's documented lifecycle.

Preserve the provider's requirements concerning transaction identifiers, product identifiers, receipt or signed-transaction information, transaction completion, retries, and acknowledgment.

Do not trust a client-side purchase callback as sufficient proof of payment when server-side verification is required.

Do not implement payment processing with fabricated provider results, locally generated transaction IDs, or hardcoded success responses.

### 8. Native Billing and Platform Requirements

Determine the required billing path for each offering from the authoritative product specification and the applicable provider integration.

Where purchases must use native app-store billing, integrate with the approved iOS and Android billing libraries and their documented APIs.

Account for the following concerns:

- Product availability.
- Regional and account eligibility.
- Product and price retrieval.
- Purchase initiation.
- User cancellation.
- Pending or deferred payment.
- Transaction updates.
- Purchase restoration or reconciliation.
- Provider errors and service unavailability.
- Transaction acknowledgment or completion.
- Expired or revoked purchases.
- Test and production environment separation.

Do not assume the same transaction lifecycle or feature set exists identically on iOS and Android.

Where the approved architecture uses a different payment route for a specific offering, follow its authoritative implementation contract and the applicable platform rules.

Do not bypass required native purchase flows, silently redirect prohibited transactions to an alternative checkout, or assume that all offerings can be sold using the same mechanism.

Do not claim that an unavailable store integration works in production. If credentials, store configuration, product registration, or external service access are missing, implement the available integration and clearly identify what remains environment-dependent.

### 9. Server Verification and Entitlement Reconciliation

The backend is authoritative for paid access and subscription state.

Integrate with the backend's established transaction-verification and entitlement-reconciliation contracts.

The mobile app must:

- Submit only the transaction information required by the approved contract.
- Authenticate the operation as required.
- Correlate purchase attempts with their associated product and account.
- Handle pending verification.
- Display the actual verification outcome.
- Refresh entitlement state following a completed or restored purchase.
- Handle delayed backend confirmation.
- Recover from a lost response without creating a duplicate purchase.
- Reconcile native transaction updates with backend state.
- Avoid granting access based exclusively on client-side flags.

Support the provider's documented transaction lifecycle and idempotency requirements. Repeated verification of the same legitimate transaction must follow the backend's idempotency contract.

Do not include raw purchase receipts, signed transactions, authentication tokens, or other sensitive verification material in logs or analytics.

Do not implement server-side receipt verification, subscription webhooks, financial reconciliation, fraud detection, or entitlement persistence in this prompt.

If those backend contracts are unavailable, define explicit portable proposed request and response schemas, including transaction states, account association, idempotency, verification failures, and entitlement-refresh behavior.

### 10. Subscription and Membership Status

Implement a screen or section that shows the user's current premium and channel-membership status.

Display the actual information supplied by the backend, such as:

- Active subscription or membership.
- Product or tier name.
- Associated creator where applicable.
- Renewal date where authoritative information is available.
- Expiration date where applicable.
- Cancellation state.
- Billing or verification issue.
- Pending transaction or membership activation.
- Available management actions.

Distinguish among:

- A purchase that has been initiated.
- A provider transaction that is pending.
- A transaction submitted for verification.
- A verified active entitlement.
- A cancelled subscription that remains active until expiration.
- An expired entitlement.
- A refunded or revoked purchase.
- A billing issue that affects current access.

Use the actual status model and provider semantics.

Do not infer access solely from a displayed renewal date or the presence of a transaction record. Reconcile against the authoritative entitlement response.

Provide understandable explanations and next steps for relevant states.

### 11. Restore Purchases and Reconcile Transactions

Implement purchase restoration or equivalent transaction reconciliation where supported by the actual billing platform.

The restoration workflow must:

1. Initiate the approved provider's restoration or transaction-query mechanism.
2. Retrieve transactions that the provider makes available to the signed-in store account.
3. Submit the appropriate verification information to the backend when required.
4. Associate verified entitlements with the authenticated platform account according to the authoritative account-linking rules.
5. Refresh the mobile entitlement state.
6. Report the actual result to the user.

Handle:

- No restorable purchases.
- Already-restored purchases.
- Pending transaction verification.
- Provider unavailability.
- Invalid or revoked transactions.
- Mismatched platform accounts.
- Backend verification errors.
- Interrupted restoration.
- Duplicate transaction delivery.

Do not silently associate an entitlement with the wrong platform account merely because the store account has an existing transaction.

Do not promise restoration when the provider or product does not support it. Document the exact limitations of the chosen billing architecture.

### 12. Subscription Management and Cancellation

Provide accessible navigation to the appropriate subscription-management experience.

Depending on the actual billing provider, that experience may be a native account-management interface, the official app-store subscription settings, or an authorized platform billing-management screen.

Requirements:

- Display the authoritative subscription status.
- Explain the available management options.
- Open only approved, valid management destinations.
- Handle unsupported or unavailable management actions gracefully.
- Refresh entitlement state after the user returns from external management.
- Represent cancellations, renewals, expirations, and billing changes based on verified information.
- Avoid performing the same cancellation or management operation twice.

Distinguish cancellation of future renewal from immediate loss of an existing entitlement. Do not remove benefits at cancellation time when the provider and backend indicate that access remains active until the end of the paid period.

Do not build the backend subscription-management portal or financial settlement infrastructure in this milestone.

### 13. Entitlement-Aware Application Behavior

Integrate the premium and membership entitlement state with the existing mobile application.

Where supported by the product contract, entitlement-dependent experiences may include:

- Ad-free viewing.
- Background playback.
- Offline viewing.
- Premium playback features.
- Member-only video access.
- Member-only live chat.
- Channel-specific membership badges.
- Other explicitly defined paid benefits.

Requirements:

- Use the shared entitlement model.
- Reconcile entitlement state at the appropriate application lifecycle points.
- Update relevant client state after confirmed changes.
- Clear or isolate entitlement data when the authenticated account changes.
- Handle expired, revoked, pending, or unavailable states correctly.
- Preserve the existing authentication and authorization architecture.
- Avoid duplicate entitlement caches with conflicting lifetimes or semantics.

Do not independently invent how ads are inserted, how offline media is protected, or how backend media authorization is enforced.

Where the mobile client needs to adapt its experience to an entitlement, use the existing product and playback contracts. The backend remains responsible for enforcing protected content access.

### 14. Purchase Errors and Recovery

Implement clear, recoverable handling for purchase-related failures.

Cover applicable cases including:

- User cancelled the purchase.
- Store or provider unavailable.
- Product unavailable.
- Ineligible account.
- Payment pending.
- Payment declined or failed.
- Transaction already processed.
- Server verification pending.
- Server verification rejected.
- Network failure after a transaction.
- Expired authentication.
- Entitlement refresh failure.
- Restored transaction associated with another account.
- Subscription expired or revoked.

Do not treat user cancellation as a payment failure requiring repeated warnings.

When a transaction may have completed but the client did not receive the response, reconcile its status with the provider or backend before initiating a second transaction.

Show messages that explain what happened without exposing provider internals or sensitive financial information.

Retry only operations whose semantics permit retry. Use the established idempotency behavior and avoid duplicate purchases or duplicate transaction completion.

### 15. Subscription-Aware UI and Accessibility

Create a polished, accessible mobile experience consistent with the existing design system.

Implement reusable components for:

- Offering cards.
- Benefit lists.
- Tier selectors.
- Price and billing-period labels.
- Purchase and restore actions.
- Processing indicators.
- Entitlement status.
- Confirmation dialogs.
- Error and retry actions.
- Subscription-management links.

Requirements:

- Display actual price and currency from the approved provider.
- Format monetary amounts and dates using appropriate locale-aware rules.
- Keep required billing terms readable.
- Identify trial, renewal, and cancellation details accurately.
- Avoid presenting pending or unverified access as active.
- Provide screen-reader labels for pricing, status, and purchase controls.
- Support dynamic text sizes.
- Provide suitable touch targets.
- Preserve safe-area and keyboard behavior.
- Follow light and dark themes where supported.
- Handle small screens and long localized text.
- Keep loading, empty, error, pending, and confirmed states visually distinct.

Do not use placeholder prices, fabricated discount badges, fake purchase confirmations, or nonfunctional subscription-management controls in the production application.

### 16. State Management, Caching, and Account Isolation

Use the project's established server-state and application-state infrastructure.

Implement explicit state transitions for product loading, purchase initiation, pending transactions, verification, active entitlements, restoration, and error recovery.

Requirements:

- Deduplicate concurrent operations where appropriate.
- Prevent duplicate user-initiated purchase submissions.
- Avoid stale responses overwriting newer account or subscription state.
- Refresh relevant entitlement queries following confirmed purchase changes.
- Reconcile provider transaction updates and backend status.
- Use bounded retry and timeout behavior.
- Handle app foregrounding and account restoration.
- Avoid persisting sensitive purchase material unnecessarily.
- Ensure one user's entitlements cannot appear in another user's session.
- Clear or revalidate user-scoped cached state during logout and account switching.

Do not create a second source of truth for subscription status.

If a store account can be associated with a different authenticated platform account, follow the backend's explicit account-linking and recovery rules rather than inferring the correct association.

### 17. Security and Privacy

Treat transaction data, provider callbacks, purchase identifiers, app links, and API responses as untrusted until appropriately verified.

Implement these protections:

- Use the established authenticated API client.
- Avoid logging raw receipts, signed transactions, tokens, or private billing data.
- Do not store payment-card details or provider credentials in application state.
- Validate offering and entitlement identifiers.
- Follow backend authorization and account-association requirements.
- Do not grant premium access from a UI-only flag.
- Handle stale and revoked transactions.
- Prevent cross-account entitlement leakage.
- Keep purchase and verification operations behind typed service interfaces.
- Avoid placing sensitive purchase information in deep-link parameters.
- Use secure storage only where the provider or platform contract requires it.
- Do not include production secrets in source code or mobile bundles.

Client-side purchase validation is not a replacement for server-side transaction verification.

### 18. Observability and Reliability

Use the established telemetry and error-reporting system.

Capture privacy-safe diagnostics for:

- Product-catalog retrieval failures.
- Purchase initiation.
- Provider cancellation and pending results.
- Verification submission and outcomes.
- Restoration attempts.
- Entitlement refresh.
- Subscription-management return and reconciliation.
- Relevant native billing errors.
- Account-association failures.

Where permitted, use stable correlation IDs to connect a mobile purchase attempt to its corresponding backend operation.

Do not include raw receipts, signed transactions, payment credentials, authentication tokens, or unnecessary personal details in telemetry.

Instrument only states the mobile application can genuinely observe. Do not claim successful payment settlement, server verification, or entitlement activation merely because a native purchase callback occurred.

### 19. Required Automated Tests

Use the testing framework established in the application.

#### 19.1 Unit tests

Test:

- Offering and price-model parsing.
- Billing-period and status mapping.
- Purchase-state transitions.
- Duplicate-submission prevention.
- Provider-result handling.
- Transaction-verification state transitions.
- Entitlement mapping and refresh.
- Restoration and transaction deduplication.
- Account-switching and entitlement isolation.
- Cancellation and expiration semantics.
- Retry and error classification.
- Purchase-management navigation resolution.

#### 19.2 Component and screen tests

Test:

- Premium offering discovery.
- Channel-membership tiers.
- Available prices and benefit rendering.
- Already-subscribed state.
- Purchase initiation and cancellation.
- Pending transactions.
- Verification success and failure.
- Purchase restoration.
- Subscription-status rendering.
- Subscription-management navigation.
- Expired, revoked, and billing-problem states.
- Accessibility labels and important screen transitions.

#### 19.3 Integration and platform tests

Where supported by the execution environment, test:

- Billing-service abstraction behavior.
- Product retrieval and eligibility handling.
- Provider transaction updates.
- Purchase-verification API integration.
- Entitlement refresh after a purchase.
- Restoration against provider sandbox transactions.
- App foregrounding and pending-transaction reconciliation.
- Account switching during a pending transaction.
- Backend unavailable and verification-delayed states.
- Relevant iOS and Android build configurations.

Use deterministic test doubles at appropriate boundaries. They must not become the production source of purchase results or entitlements.

Do not make real charges against production accounts to validate this milestone.

Execute available type checks, linting, tests, and build validations. Report the commands executed and their actual results.

### 20. Documentation and Portable Integration Contracts

Create or update documentation describing:

- Mobile purchase architecture.
- Supported offerings and product identifiers.
- Billing-provider and platform-specific responsibilities.
- Purchase lifecycle and transaction states.
- Verification and entitlement-refresh flow.
- Purchase restoration.
- Subscription cancellation and expiration handling.
- Account-association requirements.
- Native configuration and environment requirements.
- Sandbox-testing instructions.
- Required backend APIs and schemas.
- Error handling and idempotency.
- Security and privacy constraints.
- Test commands and results.
- Known limitations and unresolved integration dependencies.

If the authoritative contracts are unavailable, provide portable proposed API and state-machine definitions that an independent implementation environment can reconcile. Clearly label all proposals and unverified assumptions.

Do not claim that native purchases, server verification, or entitlement activation are operational when the necessary external services have not been configured or tested.

### 21. Explicitly Out of Scope

Do not implement the following within this milestone:

- Backend payment processing.
- Backend billing-provider webhook consumers.
- Server-side receipt or signed-transaction verification.
- Subscription persistence or entitlement databases.
- Subscription renewal orchestration.
- Financial settlement and reconciliation systems.
- Fraud detection and chargeback systems.
- Creator revenue reporting or payout systems.
- Creator membership-tier configuration.
- Backend entitlement enforcement.
- A replacement for the platform's global authentication or account architecture.
- Unrelated video, live-stream, upload, moderation, or administration functionality.
- Unplanned architecture, QA, integration, or production-readiness prompts.

Implement the assigned mobile experience, its actual billing-client integrations, entitlement consumption, automated tests, and portable documentation. Consume backend capabilities only through authoritative or explicitly proposed contracts.

### 22. Definition of Done

This milestone is complete only when all applicable criteria are satisfied:

1. The mobile app displays real offering information from the approved catalog.
2. Premium and channel memberships are represented distinctly.
3. Available purchase flows use the appropriate billing architecture.
4. Purchase success, cancellation, pending, and failure states are handled correctly.
5. Server verification and entitlement reconciliation are integrated wherever the backend contract provides them.
6. Purchase restoration or reconciliation works where supported by the actual provider.
7. Subscription and membership screens display authoritative state.
8. Subscription-management navigation follows the supported provider workflow.
9. Relevant mobile experiences consume confirmed entitlement state.
10. Account changes do not leak or preserve inappropriate entitlement state.
11. Errors and ambiguous transactions have safe recovery paths.
12. Security and privacy protections are implemented.
13. Automated tests cover core purchase, verification, restoration, account-isolation, and failure behavior.
14. Available static checks, tests, and build validations have been executed and accurately reported.
15. Documentation identifies the actual billing integrations, configuration requirements, and outstanding external dependencies.
16. No fake payment processing, invented prices, fabricated production entitlements, hardcoded secrets, placeholder implementations, or undocumented billing assumptions remain within this scope.

### 23. Completion Report

After implementation, provide a factual completion report containing:

- **Files created**
- **Files modified**
- **Files deleted**, if any
- **Premium subscription functionality**
- **Channel-membership functionality**
- **Billing-provider integrations**
- **Purchase and restoration flows**
- **Verification and entitlement integration**
- **Subscription-management functionality**
- **Security and privacy safeguards**
- **Tests created**
- **Commands and validations actually executed**
- **iOS and Android build results**
- **Documentation updated**
- **External configuration and service requirements**
- **Known limitations**
- **Unresolved integration issues**
- **Definition of Done status**

Distinguish verified implementation from proposed contracts and unavailable services. Do not claim a successful real-world purchase or production entitlement activation without actual verification.

### 24. Final Execution Directive

Treat this prompt as the active implementation assignment for mobile premium subscriptions, channel memberships, purchases, and entitlement-aware application behavior.

Inspect the project materials genuinely available in the execution environment. Implement the complete bounded scope, preserve authoritative contracts and existing functionality, execute available tests and validations, and document the actual outcome.

Do not respond with planning alone. Do not ask the user to choose which part to implement. Do not implement unrelated features, invent unavailable payment or backend capabilities, bypass required billing flows, or create unplanned project phases.

Deliver the strongest complete and verifiable implementation supported by the execution environment.

**Begin implementation now.**
