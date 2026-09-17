# PRD - Accounting

## Document Information
- Product / Feature Name: Accounting
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Functional Requirements](#functional-requirements)
- [Non-Functional Requirements](#non-functional-requirements)
- [Dependency & Constraints](#dependency--constraints)
- [Success Metrics](#success-metrics)

## Overview

### Background
The Company is expanding from car sales into car rental, a new business line with no prior rental experience or dedicated systems. Car rental introduces financial workflows that do not exist in car sales, such as recurring/variable-duration billing, deposits and holds, damage charges, refunds, corporate credit accounts, and reconciliation between reservations, payment processors, bank deposits, and the general ledger (GL). The Company currently has no dedicated system or process to calculate rental pricing, charge customers correctly at the right time, apply the correct taxes, reconcile transactions with the accounting platform, or produce the financial reports and audit trails required to run this new business line.

### Objective
Define the accounting capabilities required to accurately price, bill, collect, record, reconcile, and report on car rental transactions, so that rental revenue, deposits, refunds, and related charges are captured correctly and flow into the Company's accounting system with a complete and auditable trail.

### Goals
- Provide a consistent way to calculate rental pricing and all related charges (insurance, fuel, tolls, mileage overage, delivery, late fees, extra driver, taxes).
- Ensure customers are charged at the correct point in the rental lifecycle (booking, pickup, return, or installments) and that deposits/holds/refunds are recorded accurately.
- Generate the billing documents needed for individual and corporate customers (estimates, invoices, receipts, credit notes, corporate statements).
- Ensure every rental transaction is mapped to the correct chart-of-accounts and synced with the accounting system(s) on a defined schedule.
- Support reconciliation between reservations, the payment processor, bank deposits, and the GL, including handling of failed payments, chargebacks, and disputes.
- Enforce approval controls and maintain an audit trail for manual price overrides, refunds, and waived fees.
- Support corporate customer credit accounts, negotiated rates, POs, consolidated invoicing, credit limits, payment terms, collections, and tax exemptions.
- Provide the financial reports and KPIs needed daily, weekly, monthly, and at period-end, including correct revenue recognition for rentals spanning multiple accounting periods.

## Problem Statement
The Company's accounting and finance teams currently have no defined process or system for handling rental-specific financial events. Without this, the following pain points occur:
- Pricing and additional charges (insurance, fuel, tolls, mileage overage, delivery, late fees, extra driver) may be calculated inconsistently or missed, leading to revenue leakage or customer billing disputes.
- There is no defined trigger for when a customer is charged (booking, pickup, return, or installments), which risks incorrect timing of revenue recognition and cash collection.
- Deposits, holds, refunds, and partial refunds have no standard recording method, risking reconciliation errors and customer disputes.
- Rental transactions have no defined chart-of-accounts mapping or sync cadence with the accounting system(s), making financial reporting unreliable.
- There is no reconciliation process between reservations, the payment processor, bank deposits, and the GL, and no defined process for failed payments, chargebacks, or disputes.
- There are no approval limits or audit trail requirements for manual price overrides, refunds, or waived fees, creating a financial control gap.
- Corporate customers (fleet accounts, businesses) have no defined credit account, negotiated rate, PO, or consolidated invoicing process.
- There is no defined set of financial reports or KPIs, and no policy for revenue recognition of rentals that span multiple accounting periods.

**Who is affected (key users):**
- Accounting / Finance team — responsible for recording, reconciling, and reporting rental transactions.
- Billing / Rental Operations staff — responsible for charging customers and issuing billing documents.
- Corporate Sales / Account Management — responsible for corporate customer credit accounts and negotiated rates.
- Finance Management — responsible for approving overrides, refunds, and reviewing reports/KPIs.
- Corporate customers — affected by invoicing accuracy, credit terms, and tax exemption handling.

**Why is this important now:**
The car rental business line is new to the Company, and no accounting workflows, controls, or reporting exist for it today. Defining these requirements now, before launch, is required to correctly bill customers, maintain financial controls, avoid revenue leakage, and produce accurate, auditable financial statements from day one of rental operations.

## Functional Requirements

### 1. Rental Pricing Calculation
**Statement:** As an Accounting team member, I want the system to calculate rental pricing based on the applicable pricing model (hourly, daily, weekly, monthly, mileage-based, seasonal, or demand-based), so that customers are charged the correct base rental amount.

**Requirement detail:** The pricing calculation must support multiple pricing models and apply the correct model based on the rental agreement, vehicle type, rental duration, and any seasonal or demand-based adjustments in effect at the time of booking.

**Acceptance criteria:**
- **Given** a rental agreement with a defined pricing model, **when** the rental is priced, **then** the correct rate (hourly, daily, weekly, monthly, or mileage-based) is applied based on the agreement terms.
- **Given** a rental occurring during a seasonal or demand-based pricing period, **when** the rental is priced, **then** the applicable seasonal/demand adjustment is applied and visible on the estimate/invoice.

### 2. Additional Charges
**Statement:** As an Accounting team member, I want additional charges (insurance, fuel, tolls, mileage overage, delivery, late fees, extra driver) to be itemized and applied to the rental, so that all billable charges are captured and communicated to the customer.

**Requirement detail:** Each additional charge type must be individually identifiable, calculated based on defined business rules (e.g., mileage overage rate per mile, late fee per day/hour), and itemized separately from the base rental charge on billing documents.

**Acceptance criteria:**
- **Given** a rental with applicable additional charges, **when** the final bill is generated, **then** each additional charge type is itemized separately with its own amount.
- **Given** a customer exceeds the agreed mileage or return time, **when** the rental is closed out, **then** the corresponding overage/late fee is automatically calculated and added to the bill.

### 3. Tax Calculation
**Statement:** As an Accounting team member, I want taxes to be calculated based on location, vehicle type, and customer type, so that the correct tax amount is charged and remitted.

**Requirement detail:** Tax rules must account for jurisdictional differences, vehicle category, and customer type (e.g., tax-exempt corporate or government customers), and must be applied consistently across estimates, invoices, and receipts.

**Acceptance criteria:**
- **Given** a rental in a specific jurisdiction, **when** the rental is billed, **then** the tax rate applicable to that location and vehicle/customer type is applied.
- **Given** a customer with a valid tax exemption, **when** the rental is billed, **then** no tax is charged and the exemption reason is recorded.

### 4. Customer Charge Timing
**Statement:** As an Accounting team member, I want the system to charge the customer at the correct point in the rental lifecycle (booking, pickup, return, or in installments), so that cash collection and revenue timing align with company policy.

**Requirement detail:** The charge trigger point must be configurable per rental type/agreement and must record the charge event, amount, and timing so it can be reconciled with revenue recognition rules.

**Acceptance criteria:**
- **Given** a rental agreement configured for a specific charge trigger (booking, pickup, return, or installment), **when** that trigger event occurs, **then** the customer is charged the corresponding amount at that time.
- **Given** an installment-based rental, **when** each installment is due, **then** the system charges the installment amount and records it against the rental agreement.

### 5. Deposits, Holds, and Refunds
**Statement:** As an Accounting team member, I want deposits, holds, refunds, and partial refunds to be recorded with full detail, so that customer funds are tracked accurately from collection through release or refund.

**Requirement detail:** Every deposit/hold placed, released, applied, or refunded (in full or in part) must be recorded with the amount, reason, and associated rental, and must be reflected in reconciliation and reporting.

**Acceptance criteria:**
- **Given** a deposit or hold is placed at booking or pickup, **when** the rental is returned, **then** the deposit/hold is released, applied to charges, or partially refunded, and each outcome is recorded.
- **Given** a partial refund is issued, **when** the refund is processed, **then** the refunded amount, reason, and remaining balance are recorded and traceable to the original transaction.

### 6. Price Adjustments for Extensions, Early Returns, and Vehicle Changes
**Statement:** As an Accounting team member, I want price adjustments for rental extensions, early returns, or vehicle changes to be recorded, so that the customer is billed the correct final amount.

**Requirement detail:** When a rental's duration or vehicle changes mid-agreement, the system must recalculate charges based on the updated terms and record the adjustment as a distinct, traceable line item.

**Acceptance criteria:**
- **Given** a rental is extended beyond its original end date, **when** the rental is closed out, **then** the additional period is billed according to the applicable pricing model.
- **Given** a rental is returned early or the vehicle is changed mid-rental, **when** the final bill is generated, **then** the price adjustment is itemized and reflected in the final amount due.

### 7. Billing Documents
**Statement:** As a Billing / Rental Operations staff member, I want to generate estimates, invoices, receipts, credit notes, and corporate statements, so that customers and corporate accounts receive the correct billing documentation for each transaction.

**Requirement detail:** Each billing document type must be generated at the appropriate point in the rental lifecycle, include all itemized charges, taxes, deposits, and adjustments, and be retrievable for audit and customer service purposes.

**Acceptance criteria:**
- **Given** a completed rental, **when** the rental is closed, **then** an invoice and receipt are generated reflecting all charges, taxes, and payments.
- **Given** a corporate account with consolidated billing, **when** the billing period ends, **then** a consolidated corporate statement is generated covering all rentals for that account in the period.
- **Given** a billing correction is needed after an invoice is issued, **when** the correction is processed, **then** a credit note is issued referencing the original invoice.

### 8. Accounting System Integration
**Statement:** As an Accounting team member, I want rental transactions to be sent to the designated accounting system(s), so that financial data is centrally recorded and available for reporting.

**Requirement detail:** All rental financial transactions (revenue, deposits, refunds, damage charges, fees) must be transmitted to the accounting system(s) of record, mapped to the correct chart-of-accounts, and synced on a defined schedule.

**Acceptance criteria:**
- **Given** a rental transaction is completed, **when** the sync process runs, **then** the transaction is transmitted to the accounting system with the correct chart-of-accounts mapping.
- **Given** a sync failure occurs, **when** the failure is detected, **then** it is flagged for review and does not result in silently lost transactions.

### 9. Reconciliation
**Statement:** As an Accounting team member, I want to reconcile reservations, payment processor records, bank deposits, and the GL, so that discrepancies are identified and resolved.

**Requirement detail:** A reconciliation process must compare transaction records across reservations, payment processor settlements, bank deposits, and GL entries, and surface discrepancies for review.

**Acceptance criteria:**
- **Given** a reconciliation period is closed, **when** reconciliation is run, **then** matched and unmatched transactions between reservations, payment processor, bank deposits, and GL are reported.
- **Given** an unmatched or failed transaction (e.g., failed payment, chargeback, dispute), **when** it is identified during reconciliation, **then** it is flagged with status and routed for resolution.

### 10. Approval Controls and Audit Trail
**Statement:** As a Finance Manager, I want manual price overrides, refunds, and waived fees to require approval within defined limits and be recorded in an audit trail, so that financial controls are enforced and adjustments are traceable.

**Requirement detail:** Approval limits must be configurable by role/amount, and every manual adjustment must capture who requested it, who approved it, the reason, and the before/after values.

**Acceptance criteria:**
- **Given** a manual price override, refund, or waived fee exceeding a user's approval limit, **when** it is submitted, **then** it is routed to an approver with sufficient authority before being applied.
- **Given** any manual financial adjustment is applied, **when** it is recorded, **then** the audit trail captures the requester, approver, reason, timestamp, and amount changed.

### 11. Corporate Customer Accounts
**Statement:** As a Corporate Account Manager, I want corporate customers to have credit accounts with negotiated rates, POs, credit limits, payment terms, and consolidated monthly invoicing, so that corporate rental relationships are billed and managed correctly.

**Requirement detail:** Corporate accounts must support negotiated pricing, PO reference capture, defined credit limits and payment terms, consolidated invoicing on a monthly (or agreed) cycle, and a collections workflow for overdue balances.

**Acceptance criteria:**
- **Given** a corporate account with a negotiated rate, **when** a rental is booked under that account, **then** the negotiated rate is applied instead of the standard rate.
- **Given** a corporate account approaches or exceeds its credit limit, **when** a new rental is booked, **then** the system flags or blocks the booking per policy.
- **Given** a corporate account with consolidated monthly invoicing, **when** the billing cycle ends, **then** all rentals for the period are combined into a single statement.

### 12. Tax Exemption Handling
**Statement:** As an Accounting team member, I want to apply tax exemptions for eligible customers, so that exempt customers are billed correctly and exemption records are retained for audit purposes.

**Requirement detail:** Tax exemption status must be recorded per customer/account, validated at the time of billing, and referenced on billing documents when applied.

**Acceptance criteria:**
- **Given** a customer with an active, valid tax exemption on file, **when** they are billed, **then** applicable taxes are not charged and the exemption reference is recorded on the invoice.
- **Given** a customer's tax exemption has expired or is invalid, **when** they are billed, **then** standard tax rules apply.

### 13. Financial Reporting and KPIs
**Statement:** As Finance Management, I want daily, weekly, monthly, and period-end financial reports along with key KPIs, so that I can monitor the financial health of the rental business.

**Requirement detail:** Reports must be available on the defined cadences and must include revenue recognized (accounting for rentals spanning multiple periods), AR aging, refunds pending, utilization, and revenue per rental day.

**Acceptance criteria:**
- **Given** a reporting period ends, **when** the corresponding report is generated, **then** it reflects revenue recognized in that period only, including proration for rentals spanning multiple periods.
- **Given** a request for KPIs, **when** the KPI dashboard/report is viewed, **then** revenue per rental day, utilization, AR aging, and refunds pending are displayed.

## Non-Functional Requirements


## Dependency & Constraints
- This document covers only the requirements gathered from the Accounting role interview; it does not define the technical design or implementation approach (see the corresponding TRD).
- The Company has no prior rental business experience or existing rental-specific accounting system; requirements assume new processes and/or systems will need to be established.
- Requirements depend on identification of the specific downstream accounting system(s) and payment processor(s) to be integrated, which are not yet finalized at the time of this PRD.
- Requirements depend on legal/tax guidance for jurisdiction-specific tax rules and corporate tax exemption policies, which are outside the scope of this document.

## Success Metrics
- Reduction in billing disputes/errors related to rental charges, taxes, and additional fees.
- 100% of rental transactions reconciled between reservations, payment processor, bank deposits, and GL within the defined reconciliation cycle.
- All manual price overrides, refunds, and waived fees have a complete, auditable approval trail.
- Corporate invoices are issued accurately and on schedule for consolidated billing cycles.
- Financial reports and KPIs (revenue/rental day, utilization, AR aging, refunds pending) are available on time for every reporting cadence (daily, weekly, monthly, period-end).

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*
