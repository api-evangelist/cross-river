# Cross River (cross-river)

Cross River is a regulated bank (FDIC member, Fort Lee, NJ) that delivers embedded finance and Banking-as-a-Service (BaaS) through the **Cross River Operating System (COS)** - a collection of RESTful APIs for deposit accounts, ACH, wires, instant payments (RTP, FedNow, CRNow), card issuing and processing, lending, and customer management (KYC / onboarding).

## Access model (read first)

Cross River is a **chartered, regulated bank**, and COS is **partner/enterprise-gated** - there is no open, self-service signup:

- Programs are onboarded through Cross River **sales and a relationship manager** (start at [crossriver.com/contact](https://www.crossriver.com/contact)).
- During onboarding you are provisioned **OAuth 2.0 client credentials** (`client_id` / `client_secret`) for the **sandbox** (`https://sandbox.crbcos.com`), and later for **production** at go-live.
- The **production base URL is not published** in the open documentation - it is issued as part of your program.
- The public documentation at [docs.crossriver.com](https://docs.crossriver.com/) is openly readable (paths, methods, concepts, per-module base URLs), but the **live sandbox and the full OpenAPI / Postman collection are shared only with onboarded partners**.

Because of this, the OpenAPI in this repo has **confirmed endpoint paths and methods** (from the public docs) but **modeled request/response body schemas** - clearly flagged inline. Verify field-level schemas against the partner-provided collection.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cross-river/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cross-river/refs/heads/main/apis.yml)

## Authentication

OAuth 2.0 **client credentials** grant. POST `client_id`, `client_secret`, and `grant_type=client_credentials` (optionally `audience` and `scope`) to the COS identity provider:

- Core modules (sandbox): `https://idptest.crbcos.com/connect/token`
- Lending (sandbox): `https://oauthtest.crbnj.net/connect/token`

The response is a signed **JWT** that must be sent as `Authorization: Bearer <token>` on every request.

## Tags

- Embedded Finance
- Banking as a Service
- BaaS
- Payments
- ACH
- Wire
- Push-to-Card
- Lending
- Accounts
- Cards
- Fintech
- RTP
- FedNow

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Cross River Accounts API

Open and manage COS deposit accounts (DDA) and subledgers - create accounts from a product, apply and remove restrictions, retrieve statements and tax documents, and manage time deposits (CDs). Part of the COS Core module.

- **Human URL:** [https://docs.crossriver.com/apis/accounts](https://docs.crossriver.com/apis/accounts)
- **Base URL:** `https://sandbox.crbcos.com/core`

#### Tags

- Accounts
- Deposits
- DDA

#### Properties

- [Documentation](https://docs.crossriver.com/apis/accounts)
- [API Reference](https://docs.crossriver.com/apis)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River ACH Payments API

Originate and receive ACH payments over the Federal Reserve ACH network - single payments, client batches, same-day ACH, reversals, and returns, with utilization monitoring. Part of the COS Payments module.

- **Human URL:** [https://docs.crossriver.com/apis/payments/ach](https://docs.crossriver.com/apis/payments/ach)
- **Base URL:** `https://sandbox.crbcos.com/ach`

#### Tags

- ACH
- Payments
- Same Day ACH

#### Properties

- [Documentation](https://docs.crossriver.com/apis/payments/ach)
- [API Reference](https://docs.crossriver.com/apis/payments/ach/apis/send-ach-transaction)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River Wires API

Send domestic wire transfer payments, cancel wires, and handle drawdown requests and responses. Part of the COS Payments module.

- **Human URL:** [https://docs.crossriver.com/apis/payments/wires](https://docs.crossriver.com/apis/payments/wires)
- **Base URL:** `https://sandbox.crbcos.com/wires`

#### Tags

- Wires
- Fedwire
- Payments

#### Properties

- [Documentation](https://docs.crossriver.com/apis/payments/wires)
- [API Reference](https://docs.crossriver.com/apis)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River Instant Payments API

Send and receive funds instantly 24/7 across CRNow, RTP (The Clearing House), and FedNow - initiate credit transfers, requests for payment, returns, and query supported financial institutions via the directory. Part of the COS Payments module.

- **Human URL:** [https://docs.crossriver.com/apis/payments/instant-payments](https://docs.crossriver.com/apis/payments/instant-payments)
- **Base URL:** `https://sandbox.crbcos.com/rtp`

#### Tags

- RTP
- FedNow
- Instant Payments

#### Properties

- [Documentation](https://docs.crossriver.com/apis/payments/instant-payments)
- [Documentation](https://docs.crossriver.com/concepts/payments/instant-payments/payment-networks)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River Cards API

Issue and manage debit cards - create cards, activate, suspend and unsuspend, close, replace lost/stolen/damaged cards, set the PIN, and manage spend controls. Part of the COS Card Management module.

- **Human URL:** [https://docs.crossriver.com/apis/cards](https://docs.crossriver.com/apis/cards)
- **Base URL:** `https://sandbox.crbcos.com/cardmanagement`

#### Tags

- Cards
- Card Issuing
- Debit

#### Properties

- [Documentation](https://docs.crossriver.com/apis/cards)
- [API Reference](https://docs.crossriver.com/apis)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River Lending API

Originate and service loans - create and update loan applications, attach documents, request funding payment rails, retrieve loan details, and cancel loans. Uses a separate lending host and OAuth server from the core COS modules.

- **Human URL:** [https://docs.crossriver.com/apis/lending](https://docs.crossriver.com/apis/lending)
- **Base URL:** `https://arixapisandbox.crbnj.net`

#### Tags

- Lending
- Loans
- Loan Origination

#### Properties

- [Documentation](https://docs.crossriver.com/apis/lending)
- [API Reference](https://docs.crossriver.com/apis)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cross River Customer Management API

Create and manage the customer records (KYC / onboarding) required before opening accounts or issuing cards - personal and business customers, beneficial owners, identifications, addresses, phones, email, due diligence, and profile updates. Part of the COS Core module.

- **Human URL:** [https://docs.crossriver.com/apis/customer-management](https://docs.crossriver.com/apis/customer-management)
- **Base URL:** `https://sandbox.crbcos.com/core`

#### Tags

- KYC
- Onboarding
- Customer Management

#### Properties

- [Documentation](https://docs.crossriver.com/apis/customer-management)
- [API Reference](https://docs.crossriver.com/apis)
- [OpenAPI](openapi/cross-river-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cross-river.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cross-river.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/cross-river-domain-security.yml)
- [Authentication](authentication/cross-river-authentication.yml)
- [Website](https://www.crossriver.com/)
- [Documentation](https://docs.crossriver.com/)
- [Sign Up](https://www.crossriver.com/contact)
- [LinkedIn](https://www.linkedin.com/company/cross-river-bank)
- [Plans](plans/cross-river-plans-pricing.yml)
- [Rate Limits](rate-limits/cross-river-rate-limits.yml)
- [Fin Ops](finops/cross-river-finops.yml)

## WebSocket review

**Does Cross River expose a documented public WebSocket API? No.** COS is request/response REST over HTTPS; asynchronous notifications are delivered by **COS Webhooks** (HTTP callbacks), not a `wss://` stream. See [review.yml](review.yml). No AsyncAPI document was authored.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
