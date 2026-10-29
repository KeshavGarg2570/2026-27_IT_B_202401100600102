# Experiment 2
## Problem Identification and Feasibility
**Course:** Software Design Principles (SDP)  
**Project:** Multi-Vendor E-Commerce Platform  
**Class / Section:** IT-B (2026-27)  
**Prepared by:** Keshav Garg  
**Roll Number:** 202401100600102  
**Repository:** https://github.com/KeshavGarg2570/2026-27_IT_B_202401100600102

## Aim
To identify the problem addressed by a multi-vendor marketplace and define its objectives, scope, and technical and operational feasibility before implementation.
## Objectives
- Identify the difficulties faced by buyers and independent sellers.
- Define a practical marketplace solution and measurable project objectives.
- Separate the academic prototype from future commercial integrations.
- Analyse feasibility, dependencies and risks.
## Introduction
A single-store website supports one seller, while a marketplace lets independent vendors sell through a shared catalogue. This creates additional design responsibilities: vendor approval, isolation of seller data, stock consistency, splitting customer purchases into vendor orders and recording commission. The proposed project addresses these responsibilities through a modular web application.
## Selected Project
Project title: Multi-Vendor E-Commerce Platform. Domain: online retail and marketplace management. Primary users: customer, vendor and administrator.
## Problem Statement
Independent sellers often manage product listings, stock and customer orders through separate messages or spreadsheets. Customers must visit different sellers to compare products and cannot conveniently track purchases in one place. A marketplace can centralise discovery and checkout, but must prevent vendors from accessing competitors' private records and must keep inventory correct when customers purchase simultaneously.

The proposed platform will allow approved vendors to manage their own listings and fulfil their own orders. Customers will browse approved products, maintain a cart containing items from several vendors, and place one parent order that is divided into vendor suborders. Administrators will approve vendors, moderate listings and review commission reports. Payment integration will initially use a simulated or sandbox provider; real money settlement is outside the first release.
## Project Objectives
- Provide separate authenticated customer, vendor and administrator workflows.
- Allow only approved vendors to publish products and update their inventory.
- Enable search, category filters and a cart containing multiple vendors' products.
- Create consistent parent orders and vendor suborders through one transaction.
- Record immutable purchase prices and a commission-rate snapshot for each vendor suborder.
- Let customers track orders and vendors update only their own fulfilment records.
- Provide test evidence for access control, stock handling and duplicate payment events.
## Project Scope
Included: registration and login, vendor approval, product and category management, stock quantities, product search, customer addresses, cart, sandbox checkout, per-vendor fulfilment, order history, delivered-order reviews and administrative commission reporting.

Excluded from the first release: live vendor payouts, production payment processing, automated courier booking, cross-border taxation, multi-currency conversion, recommendation models and microservices. Refund workflows and partial cancellation will be designed before a later production release. No real financial transactions will be processed in the academic prototype.
## Technical Feasibility Analysis
| Factor | Assessment | Implementation approach |
|---|---|---|
| Web application | Feasible | Python and Django with server-rendered templates reduce integration effort. |
| Persistence | Feasible | PostgreSQL transactions and row locks support consistent checkout. |
| Access control | Feasible with testing | Server-side role and ownership checks protect vendor resources. |
| Multi-vendor orders | Moderate complexity | Parent order, vendor suborders and immutable order items separate responsibilities. |
| Payments | Feasible for prototype | A simulated adapter supports success, failure, expiry and duplicate-event tests. |
| Inventory | Moderate complexity | Reserve stock atomically and release it once on failure or expiry. |
| Deployment | Conditional | A web service and PostgreSQL instance are needed; hosting budget is not yet fixed. |
## Operational Feasibility Analysis
| Factor | Expected benefit | Validation needed |
|---|---|---|
| Customer usability | Shared catalogue and consolidated order history | Observe users completing a mixed-vendor purchase. |
| Vendor adoption | Central product and order dashboard | Ask sellers to add products and fulfil a sample order. |
| Administrator workload | Approval queue and commission report | Review a simulated onboarding and moderation session. |
| Maintainability | Modules with explicit ownership boundaries | Code review and integration tests. |
| Training | Short task-focused instructions | Check whether new users complete tasks without assistance. |

These are feasibility expectations, not results from completed user interviews or measured trials.
## Economic and Schedule Feasibility
Local development can use open-source tools and simulated payments. Hosting, domain registration, email delivery and commercial payment charges require separate estimates before deployment; no fixed cost is assumed. A suggested 12-week prototype schedule allocates two weeks to requirements and design, three to accounts and catalogue, three to checkout and inventory, two to dashboards and two to verification and documentation.
## Risks and Mitigation
| Risk | Mitigation | Verification |
|---|---|---|
| Overselling the last unit | Lock stock rows and reserve inside one transaction | Two concurrent purchases cannot both reserve one unit. |
| Vendor data exposure | Scope every vendor query by authenticated owner | Vendor A cannot read or edit Vendor B's records. |
| Duplicate checkout or callback | Unique idempotency keys and payment event identifiers | Retrying creates no duplicate order or stock change. |
| Payment service unavailable | Show pending status and reconcile before fulfilment | Never mark a timed-out payment as paid. |
| Scope expansion | Keep real payouts and courier APIs outside release one | Review backlog against the agreed scope. |
## Analysis
The platform is feasible as a student prototype when delivered as a modular monolith with a relational database and simulated payments. The main engineering effort lies in inventory consistency and authorisation rather than visual catalogue pages. Stakeholder validation and a working implementation are still required to confirm operational benefits.
## Observation
Marketplace requirements must distinguish customer orders from vendor fulfilment and must define payment and inventory transitions together. Stating these boundaries early gives later experiments concrete requirements to specify and test.
## Result
The problem statement, objectives, scope and preliminary feasibility analysis for the Multi-Vendor E-Commerce Platform have been documented.
