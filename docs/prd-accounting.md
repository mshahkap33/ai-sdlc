# Product Requirements Document: Accounting

## Overview

The Accounting capability records the financial lifecycle of vehicle rentals,
integrates completed transactions with the organization's accounting platform,
and provides controlled, auditable financial reporting.

## Goals

- Calculate and document all rental-related charges accurately.
- Maintain reconciled records across reservations, payments, bank deposits, and
  the general ledger.
- Support corporate billing and collections.
- Give finance users timely financial reports and a complete audit trail.

## Users

| User | Needs |
| --- | --- |
| Accounting staff | Reconcile transactions, manage exceptions, and close accounting periods. |
| Branch staff | Create rental billing documents within authorized limits. |
| Managers | Approve financial adjustments and review operational financial performance. |
| Corporate account managers | Manage credit customers, invoices, and collections. |

## Functional Requirements

### Pricing, charges, and billing

1. The system shall calculate rental price from configurable hourly, daily,
   weekly, monthly, mileage, seasonal, and demand-based rate rules.
2. The system shall calculate and itemize insurance, fuel, toll, mileage
   overage, delivery, late-return, and extra-driver charges.
3. The system shall apply tax rules by rental location, vehicle type, and
   customer type, including eligible customer tax exemptions.
4. The system shall support charging at booking, pickup, return, and by
   installment according to the applicable rate plan or customer agreement.
5. The system shall record deposits and payment holds separately from earned
   revenue and preserve their status through release, capture, refund, or
   partial refund.
6. The system shall recalculate charges and retain the original and revised
   amounts when a rental is extended, returned early, or assigned a different
   vehicle.
7. The system shall generate estimates, invoices, receipts, credit notes, and
   consolidated corporate statements with unique document numbers.

### Accounting integration and controls

8. The system shall export rental transactions to the configured accounting
   platform using a documented chart-of-accounts mapping.
9. The mapping shall distinguish rental revenue, deposits, taxes, damage
   charges, refunds, fleet expenses, accounts receivable, and payment fees.
10. Finance administrators shall configure transaction synchronization
    frequency and view the status and errors for each synchronization run.
11. The system shall provide reconciliation views that compare reservation
    charges, payment-processor transactions, bank deposits, and general-ledger
    postings, and identify unmatched amounts.
12. The system shall record failed payments, chargebacks, and disputes with
    their lifecycle status, related rental, financial impact, and resolution.
13. The system shall enforce role-based approval limits for manual price
    overrides, refunds, and waived fees; actions over a user's limit require
    approval before posting.
14. The system shall retain an immutable audit record for every financial
    adjustment, including actor, timestamp, reason, approval, prior value, and
    resulting value.

### Corporate customers and receivables

15. The system shall support corporate credit accounts, negotiated rates,
    purchase-order references, and consolidated monthly invoicing.
16. The system shall enforce configurable credit limits and payment terms, show
    accounts-receivable aging, and track collections activities and outcomes.
17. Tax-exempt corporate customers shall require a recorded exemption reference
    and effective dates before exempt tax treatment is applied.

### Reporting and period close

18. The system shall provide daily, weekly, monthly, and period-end reports for
    revenue, taxes, deposits, refunds, receivables, and reconciliation
    exceptions.
19. For rentals spanning accounting periods, the system shall recognize
    revenue according to the configured accounting policy and retain the
    allocation used for each period.
20. The system shall report revenue per rental day, fleet utilization,
    accounts-receivable aging, and pending refunds, with filters for period,
    location, vehicle type, and customer type.

## Non-Functional Requirements

- Financial amounts shall use currency-safe decimal precision and retain the
  transaction currency.
- Posted financial records and audit events shall be access-controlled and may
  not be altered or deleted by standard users.
- Exports, reports, and reconciliation results shall be available to authorized
  users in downloadable formats suitable for finance review.
- Failed accounting integrations shall be retryable without duplicating
  postings.

## Acceptance Criteria

1. A completed rental produces an itemized invoice with applicable charges and
   taxes, and exports mapped entries to the accounting platform exactly once.
2. A partial refund produces a credit note, updates the payment and accounting
   records, and has a complete audit entry.
3. A user exceeding an approval limit cannot post a price override, refund, or
   waived fee until an authorized approver approves it.
4. A reconciliation report identifies differences between reservations,
   processor payments, bank deposits, and ledger postings.
5. A corporate account can receive one monthly invoice for multiple rentals and
   appears correctly in AR aging and collections reporting.
6. A rental spanning two periods allocates revenue to both periods according to
   the configured policy.

## Open Decisions

- Select the accounting platform(s), integration method, and synchronization
  frequency.
- Define the chart of accounts and the accounting policy for revenue
  recognition.
- Set approval roles and monetary limits.
- Define jurisdiction-specific tax rules, exemption documentation, and
  retention periods.
- Confirm supported currencies, payment processors, report formats, and
  required period-close workflow.
