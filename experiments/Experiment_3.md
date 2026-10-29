# Experiment 3
## Requirement Gathering and User Stories
**Course:** Software Design Principles (SDP)  
**Project:** Multi-Vendor E-Commerce Platform  
**Class / Section:** IT-B (2026-27)  
**Prepared by:** Keshav Garg  
**Roll Number:** 202401100600102  
**Repository:** https://github.com/KeshavGarg2570/2026-27_IT_B_202401100600102

## Aim
To identify marketplace stakeholders, plan requirement elicitation and prepare a preliminary requirement gathering report with testable user stories.
## Objectives
- Identify customer, vendor and administrator needs.
- Plan interviews, questionnaires, observation and document analysis.
- Capture functional and non-functional requirements.
- Define user stories, acceptance criteria and validation priorities.
## Introduction
Requirement elicitation translates user workflows into explicit system behaviour. For a marketplace, each role has different permissions and success criteria. The requirements below are proposed from scenario analysis; interviews, surveys and field observations have not yet been conducted.
## Stakeholder Identification
| Stakeholder | Role | Primary need |
|---|---|---|
| Customer | Browses and purchases | Accurate prices, safe checkout and separate delivery tracking. |
| Vendor | Lists and fulfils products | Own catalogue control, reliable inventory and private order access. |
| Administrator | Approves and moderates | Vendor approval, audit records and commission reports. |
| Payment provider | External payment integration | Verified events, idempotent requests and reconciliation. |
| Project team and evaluator | Build and review | Clear scope, test evidence and reproducible setup. |
## Requirement Elicitation Techniques
| Technique | Planned activity | Expected output |
|---|---|---|
| Interviews | Discuss listing and fulfilment with two potential sellers. | Vendor workflow and exception list. |
| Questionnaire | Ask prospective customers about discovery and checkout. | Feature priorities and usability preferences. |
| Observation | Observe a sample purchase and seller stock update. | Task sequence and sources of errors. |
| Document analysis | Study sample catalogue, invoice and order records. | Required fields and record relationships. |
| Persona workshop | Walk through customer, vendor and admin scenarios. | Stories and acceptance criteria. |
## Interview and Questionnaire Guide
1. Customer: How do you compare products, and what delivery information do you need for orders from multiple sellers?
2. Customer: What should happen if price or availability changes before checkout?
3. Vendor: How do you update stock and prevent selling the same unit twice?
4. Vendor: Which customer details are necessary to fulfil an order?
5. Administrator: What information is required before approving a vendor?
6. Administrator: How should commission changes affect existing orders?
7. All roles: Which failure messages or status updates would help you recover from a failed payment?

Record interview date, participant consent, anonymised role, answers and resulting requirement changes. Do not report the planned interviews as completed research.
## User Personas
| Persona | Goal | Pain point |
|---|---|---|
| Customer purchasing gifts | Buy several products in one session | Different sellers provide inconsistent order updates. |
| Small independent seller | Manage listings without a separate store | Manual stock tracking causes missed or duplicate orders. |
| Marketplace administrator | Maintain reliable catalogue and order records | Unverified sellers and unclear commission calculations. |
## Functional Requirements
| ID | Requirement | Description |
|---|---|---|
| FR01 | Accounts and roles | The system shall authenticate customers, vendors and administrators and enforce permissions on the server. |
| FR02 | Vendor approval | Only an administrator shall approve or suspend a vendor; unapproved or suspended vendors shall not receive new purchases. |
| FR03 | Catalogue ownership | An approved vendor shall create, edit and deactivate only its own products; price and stock shall be validated. |
| FR04 | Product discovery | Customers shall search active approved listings and filter by category and price. |
| FR05 | Cart | Customers shall add, change and remove positive integer quantities from several vendors; totals shall be calculated on the server. |
| FR06 | Atomic checkout | Checkout shall revalidate prices, approval and stock, reserve inventory and create one parent order with one suborder per vendor atomically. |
| FR07 | Payment state | The payment adapter shall support pending, paid, failed and expired states; duplicate events shall not repeat side effects. |
| FR08 | Order visibility | A customer shall see only their own orders; each vendor shall see only their own suborders and fulfilment-relevant address data. |
| FR09 | Fulfilment | The owning vendor shall move paid suborders through processing, shipped and delivered in order. |
| FR10 | Commission reporting | The system shall snapshot the commission rate and amounts at checkout and report commissions on paid orders without executing payouts. |
| FR11 | Verified reviews | A customer shall review a purchased product only after delivery, with at most one review per order item. |
| FR12 | Moderation and audit | Administrators shall moderate listings and review audit entries recording approval, suspension and fulfilment changes. |
## Non Functional Requirements
| ID | Category | Target or constraint |
|---|---|---|
| NFR01 | Security | All protected operations must pass role and resource-ownership tests; use framework password hashing, CSRF protection and HTTPS in deployment. |
| NFR02 | Integrity | In concurrency tests, inventory must never be negative and one idempotency key must create at most one checkout result. |
| NFR03 | Performance | Target p95 under 2 seconds for catalogue responses with 1,000 products and 20 concurrent users on the documented test environment; external payment latency is excluded. |
| NFR04 | Usability | A new user should complete a mixed-vendor sandbox purchase within five minutes during a recorded usability exercise. |
| NFR05 | Reliability | Payment retries and expiry retries must be idempotent; backup restoration must be demonstrated on a test database before release. |
| NFR06 | Maintainability | Separate account, catalogue, checkout and fulfilment modules; cover all FR IDs with documented acceptance tests. |
| NFR07 | Privacy | Vendors may access only fulfilment-required customer information for their suborders; logs must exclude passwords, credentials and card data. |
| NFR08 | Accessibility | Forms must have labels, keyboard-operable controls, visible focus and useful validation errors; manually test core workflows. |
## User Stories and Acceptance Criteria
### US01 Customer workflow
As a customer, I want to register and sign in so that I can access my own account.

Acceptance criteria: Invalid credentials fail with a generic message; the password is stored as a hash.

Traceability: FR01.

### US02 Administrator workflow
As a administrator, I want to approve a vendor application so that I can control who can sell.

Acceptance criteria: A pending vendor cannot publish; approval enables eligible listings.

Traceability: FR02.

### US03 Vendor workflow
As a vendor, I want to manage my catalogue and stock so that I can keep my listings accurate.

Acceptance criteria: Negative prices or quantities are rejected; another vendor cannot edit the product.

Traceability: FR03.

### US04 Customer workflow
As a customer, I want to search and filter products so that I can find suitable items.

Acceptance criteria: Results exclude inactive products and unapproved or suspended vendors.

Traceability: FR04.

### US05 Customer workflow
As a customer, I want to keep products from different vendors in one cart so that I can purchase conveniently.

Acceptance criteria: The cart shows vendor, quantity and server-calculated price for each item.

Traceability: FR05.

### US06 Customer workflow
As a customer, I want to place one mixed-vendor order so that I can track the complete purchase.

Acceptance criteria: Two vendors produce one parent order and two suborders; insufficient stock rolls back checkout.

Traceability: FR06.

### US07 Customer workflow
As a customer, I want to retry a payment safely so that I can avoid duplicate charges and orders.

Acceptance criteria: Repeated event IDs do not duplicate payment records or alter stock twice.

Traceability: FR07.

### US08 Vendor workflow
As a vendor, I want to view my suborders so that I can fulfil customer purchases.

Acceptance criteria: A request for another vendor's suborder is denied even when its ID is known.

Traceability: FR08.

### US09 Customer workflow
As a customer, I want to track each vendor delivery so that I can know which products have arrived.

Acceptance criteria: Each suborder displays its own status; unpaid orders cannot ship.

Traceability: FR09.

### US10 Administrator workflow
As a administrator, I want to see commission totals so that I can review marketplace income.

Acceptance criteria: Paid orders use the stored rate and immutable item amounts, with no automatic payout.

Traceability: FR10.

### US11 Customer workflow
As a customer, I want to review a delivered purchase so that I can share reliable feedback.

Acceptance criteria: Undelivered and duplicate order-item reviews are rejected.

Traceability: FR11.

### US12 Administrator workflow
As a administrator, I want to moderate inappropriate listings so that I can maintain catalogue quality.

Acceptance criteria: Deactivation hides the listing from discovery but preserves historical order items.

Traceability: FR12.

## Prioritisation and Validation
Must have: FR01 through FR09 and vendor isolation. Should have: commission reporting, verified reviews and administrative audit reporting. Could have: wishlist and promotional discounts after the core release. Real vendor payouts and automated courier booking are excluded from this prototype.

The next validation step is a stakeholder walkthrough of the mixed-vendor checkout, payment failure and vendor suspension scenarios. Any agreed change must update this report, the SRS and the corresponding acceptance test together.
## Requirement Gathering Report
Scenario analysis identifies inventory consistency, ownership enforcement and separate vendor fulfilment as the central requirements. Customers need one purchase flow with clear suborder statuses, while vendors need isolated dashboards. These proposed requirements form the initial baseline; stakeholder approval and empirical usability findings are still pending.
## Observation
User stories become useful test inputs when acceptance criteria specify both normal results and failure behaviour. Marketplace stories should explicitly test cross-vendor access, partial stock availability and repeated requests.
## Result
Stakeholders, elicitation activities, proposed requirements, personas and user stories have been documented for later stakeholder validation.
