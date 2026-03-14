# PRD - Accounting

## Document Information

| Field | Details |
|---|---|
| **Product / Feature Name** | Accounting – Car Rental System |
| **Author** | Copilot |
| **Date** | |
| **Version** | |

---

## Table of Contents

1. [Overview](#overview)
2. [Problem Statement](#problem-statement)
3. [Functional Requirements](#functional-requirements)
4. [Non-Functional Requirements](#non-functional-requirements)
5. [Dependency & Constraints](#dependency--constraints)
6. [Success Metrics](#success-metrics)

---

## Overview

### Background

The company is expanding its existing car-sales business into car rental. Unlike car sales, car rental involves recurring financial transactions—rental income collected over time, security deposits held and released, maintenance expense tracking, tax obligations, and customer refunds. None of the current systems were built for these workflows. A dedicated Accounting module is required to ensure all financial data is captured accurately, auditable, and reportable.

### Objective

Provide a centralised Accounting module within the Car Rental System that records all rental-related financial transactions, generates compliant invoices, manages deposits and refunds, integrates with third-party accounting software, and produces the financial reports that the business needs to operate and remain compliant.

### Goals

- Maintain complete and accurate financial records for every rental transaction (income, expenses, deposits, refunds, adjustments).
- Produce legally compliant invoices for individual customers, corporate clients, and recurring-rental agreements.
- Support configurable tax regimes and multiple currencies to enable future geographic expansion.
- Integrate with mainstream accounting software (e.g., QuickBooks, Xero, SAP) to avoid double-data entry.
- Provide role-based financial reports (profit/loss, outstanding payments, tax summaries) on demand.
- Enforce internal controls and approval workflows that reduce the risk of financial misstatement or fraud.
- Retain accounting records in accordance with applicable statutory data-retention periods.

---

## Problem Statement

### User Pain Point / Business Problem

Without an Accounting module the car-rental business has no reliable way to track rental income versus operating costs, manage customer deposits, or produce the financial statements required for tax filing and management decision-making. Accounting staff would have to collate data manually from booking records and bank statements, which is error-prone, slow, and does not scale.

### Who Is Affected?

| User / Stakeholder | Impact |
|---|---|
| **Accountant / Finance Staff** | Cannot close books or file taxes without accurate, consolidated financial data. |
| **Branch Manager** | Cannot see profit/loss or outstanding receivables for their branch. |
| **Customer** | Experiences delays or errors on invoices, refunds, and deposit releases. |
| **Corporate Client** | Needs consolidated, recurring invoices and credit-term management. |
| **System Administrator** | Must configure tax rates, currencies, and approval thresholds. |
| **External Auditor** | Requires a complete, immutable audit trail of all financial transactions. |

### Why Is This Important Now?

The car-rental line of business is launching imminently. Financial controls must be in place from day one to ensure regulatory compliance, protect company assets (deposits), and give management the visibility they need to run a new business unit profitably.

---

## Functional Requirements

### FR-1 – Financial Record Keeping

**Statement:** **As a** finance staff member, **I want** the system to automatically record all rental-related financial transactions (rental income, security deposits, maintenance expenses, fuel charges, late-return fees, and refunds), **so that** I have a single, accurate ledger for the car-rental business without manual data entry.

**Requirement Detail:**
- Each completed booking must generate a corresponding financial record capturing: transaction date, transaction type, amount, currency, customer/corporate reference, vehicle reference, branch, and applicable tax.
- Expense entries (maintenance, cleaning, fuel top-up) must be linkable to a specific vehicle and booking where applicable.
- All records must carry a unique transaction ID and be immutable once posted; corrections must be made via adjustment entries.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A rental booking is marked as completed | The system processes the checkout | A rental-income transaction record is created automatically with the correct amount, tax, and references |
| 2 | A maintenance cost is logged against a vehicle | The expense is saved | An expense record linked to that vehicle (and booking if applicable) appears in the ledger |
| 3 | A finance staff member attempts to edit a posted transaction directly | They submit the edit | The system rejects the edit and requires an adjustment entry instead |

---

### FR-2 – Invoicing

**Statement:** **As a** finance staff member, **I want** the system to generate invoices for individual customers, corporate clients, and recurring rental agreements, **so that** customers receive accurate, professional billing documents and accounts receivable is managed efficiently.

**Requirement Detail:**
- Individual invoices must be auto-generated at checkout and emailed to the customer.
- Corporate invoices must support consolidated billing (multiple rentals on one invoice) on a configurable billing cycle (weekly, monthly).
- Recurring rental agreements must produce scheduled invoices automatically according to the agreed schedule.
- All invoices must include: invoice number, date, itemised charges (base rental, extras, taxes, discounts), payment terms, and company registration details.
- Invoices must be available in PDF format.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | An individual customer completes a rental | The booking is closed | An itemised PDF invoice is generated and sent to the customer's registered email |
| 2 | A corporate client is configured for monthly consolidated billing | The billing cycle ends | A single consolidated invoice covering all rentals in that period is generated and sent to the corporate billing contact |
| 3 | A recurring rental agreement is active | The scheduled invoice date arrives | An invoice for the next billing period is automatically created and sent without manual intervention |

---

### FR-3 – Deposit Management

**Statement:** **As a** finance staff member, **I want** the system to record, track, and release or forfeit customer deposits according to configurable rules, **so that** deposit liabilities are accurately reflected in the accounts and customers receive timely refunds or clear forfeiture notifications.

**Requirement Detail:**
- Each deposit must be classified as refundable or non-refundable at the time of booking.
- Refundable deposits must be held as a liability until the vehicle is returned and inspected.
- Upon satisfactory return, the refundable deposit must be marked for release and a refund initiated within a configurable SLA (default: 5 business days).
- If damage or policy violations are detected, the system must allow partial or full forfeiture with a mandatory reason and approval.
- Non-refundable deposits must be recognised as income immediately upon receipt.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A refundable deposit is collected at booking | The payment is processed | The deposit is recorded as a liability and does not appear as income |
| 2 | A vehicle is returned with no damage | The return inspection is completed | The deposit is automatically queued for refund within the configured SLA |
| 3 | A vehicle is returned with damage | A manager approves partial forfeiture | The forfeited portion is transferred to income, the remainder is refunded, and a notification is sent to the customer |

---

### FR-4 – Accounting Software Integration

**Statement:** **As a** finance staff member, **I want** the system to integrate with our existing accounting software (QuickBooks, Xero, or SAP), **so that** I do not have to manually re-enter transaction data and the general ledger is always up to date.

**Requirement Detail:**
- The system must support outbound data sync to at least QuickBooks Online and Xero via their standard APIs, with SAP integration available as a configurable add-on.
- Sync must be near real-time (within 15 minutes) for income and deposit transactions; batch (nightly) sync is acceptable for expense entries.
- Mapping of the car-rental chart of accounts to the target accounting system's chart of accounts must be configurable by an administrator.
- Failed sync events must be logged, and finance staff must receive an alert for any sync failure lasting more than 30 minutes.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | QuickBooks Online integration is configured and enabled | A rental-income transaction is posted | The transaction appears in the linked QuickBooks account within 15 minutes |
| 2 | The integration API is unavailable | A transaction is posted | The transaction is queued, the failure is logged, and a finance staff alert is raised if the outage exceeds 30 minutes |
| 3 | An administrator changes the account mapping | The change is saved | All subsequent synced transactions use the new mapping |

---

### FR-5 – Financial Reporting

**Statement:** **As a** branch manager or finance staff member, **I want** to generate on-demand financial reports (profit/loss, outstanding payments, and tax summaries), **so that** I can make informed business decisions and meet regulatory filing obligations.

**Requirement Detail:**
- Available reports must include: Profit & Loss Statement, Outstanding Receivables, Tax Liability Summary, Deposit Liability Report, and Revenue by Vehicle/Branch.
- Reports must be filterable by date range, branch, customer type (individual/corporate), and currency.
- Reports must be exportable in PDF and CSV formats.
- Role-based access control must restrict sensitive reports (e.g., P&L) to authorised roles (Finance Manager, Branch Manager, Administrator).

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A finance manager selects the P&L report with a specific date range and branch filter | They click "Generate" | The report is displayed on screen and is available for download in PDF and CSV formats within 10 seconds |
| 2 | An accountant applies a tax summary report for a given quarter | The report is generated | All taxable transactions for that quarter are included, grouped by tax type, with totals matching the ledger |
| 3 | A user without the Finance Manager or Branch Manager role attempts to access the P&L report | They navigate to the report | The system denies access and displays a permission error |

---

### FR-6 – Multi-Currency and Multi-Tax Support

**Statement:** **As a** system administrator, **I want** to configure multiple currencies and tax regimes in the accounting module, **so that** the car-rental system can operate across different regions or cater to international customers without requiring code changes.

**Requirement Detail:**
- The system must support at least two active currencies simultaneously, with exchange rates updateable manually or via a configurable exchange-rate API.
- Each branch must be assignable to a tax regime (e.g., VAT, GST, Sales Tax) with configurable rates.
- Tax calculations must be applied automatically at invoice generation based on the branch's tax regime and the transaction type.
- All stored amounts must record both the original currency value and the base-currency equivalent at the time of transaction.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | Two currencies (USD and EUR) are configured with current exchange rates | An invoice is generated in EUR | The invoice shows the EUR amount, and the ledger records both the EUR value and the USD base-currency equivalent |
| 2 | A branch is configured with a 20% VAT regime | A rental invoice is generated for that branch | The invoice itemises the base rental amount and the 20% VAT amount separately |
| 3 | An administrator updates the exchange rate for EUR | The rate is saved | All subsequent transactions use the new rate; historical transactions retain their original recorded rate |

---

### FR-7 – Refunds, Adjustments, and Chargebacks

**Statement:** **As a** finance staff member, **I want** the system to process refunds, post adjustment entries, and record chargebacks in a controlled and auditable manner, **so that** the ledger remains accurate and every financial correction is traceable.

**Requirement Detail:**
- Refunds must be initiated within the system and linked to the original transaction.
- Adjustment entries must require a reason, a reference to the original transaction, and authorisation (see FR-8).
- Chargeback events (initiated by a customer's card issuer) must be recordable, linked to the original payment, and trigger an alert to finance staff for resolution.
- All refund and adjustment events must appear in the audit log.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A finance staff member initiates a partial refund against a paid invoice | The refund is submitted | The original invoice is updated to reflect the partial refund, a refund transaction record is created, and the customer is notified |
| 2 | A finance staff member posts an adjustment entry | They provide a reason and the original transaction reference | The adjustment is recorded and linked to the original transaction in the audit log |
| 3 | A chargeback event is received from a payment gateway | The event is processed | A chargeback record linked to the original payment is created, and finance staff receive an alert |

---

### FR-8 – Internal Controls and Approval Workflows

**Statement:** **As a** finance manager, **I want** to configure approval thresholds and workflows for financial transactions (refunds, write-offs, deposit forfeitures, adjustments), **so that** no high-value or sensitive transaction can be processed without proper authorisation.

**Requirement Detail:**
- Configurable approval thresholds must exist for: refunds, deposit forfeitures, write-offs, and manual adjustment entries.
- Transactions above a threshold must enter a pending queue and require approval from an authorised role (e.g., Finance Manager) before being posted.
- Approvals and rejections must be logged with the approver's identity and a timestamp.
- The system must support a two-level approval chain for transactions exceeding a higher threshold.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A refund of $500 is above the configured $200 approval threshold | A finance staff member submits the refund | The refund enters a pending queue; the Finance Manager receives an approval notification |
| 2 | A Finance Manager approves the pending refund | They click "Approve" | The refund is posted, the customer is notified, and the approval event is recorded in the audit log |
| 3 | A transaction exceeds the two-level approval threshold | The first approver approves it | The transaction enters a second pending state and a second-level approver is notified |

---

### FR-9 – Data Retention and Archival

**Statement:** **As a** system administrator, **I want** the system to retain accounting records for the period required by applicable regulations and then archive or delete them according to a configurable policy, **so that** the company meets its legal obligations without accumulating unnecessary data.

**Requirement Detail:**
- Financial records (invoices, transactions, audit logs) must be retained for a minimum configurable period (default: 7 years) before any deletion is permitted.
- After the retention period, records may be archived to cold storage or deleted in accordance with a configured policy, subject to administrator approval.
- The retention period must be configurable per record type and per jurisdiction/branch.
- Any deletion of financial records must be logged in a separate, immutable compliance audit log.

**Acceptance Criteria:**

| # | Given | When | Then |
|---|---|---|---|
| 1 | A financial record is 6 years old and the retention period is 7 years | An administrator attempts to delete it | The system blocks the deletion and displays the earliest eligible deletion date |
| 2 | A financial record has exceeded the 7-year retention period | An administrator approves its deletion | The record is deleted, and a deletion event is written to the immutable compliance audit log |
| 3 | The retention period for a specific branch is updated from 7 to 10 years | The change is saved | All existing records for that branch are evaluated against the new 10-year period, and any previously eligible records are placed back into retention |

---

## Non-Functional Requirements

*(To be defined in a subsequent iteration.)*

---

## Dependency & Constraints

- **Desktop web only** – the Accounting module is scoped to the desktop web application in this release; mobile access is out of scope.
- **Payment module dependency** – accurate deposit and refund records depend on the Payment module being implemented and providing reliable payment-status events.
- **Third-party integration availability** – accounting software integration (QuickBooks, Xero, SAP) depends on those vendors' API availability and the company obtaining the necessary API credentials.
- **Regulatory compliance** – applicable tax and data-retention rules vary by jurisdiction; the initial release targets the company's primary operating jurisdiction only. Multi-jurisdiction support requires additional configuration and legal review.
- **Exchange-rate API** – real-time currency conversion depends on a third-party exchange-rate API; procurement and SLA for that service is outside the scope of this document.
- **Chart-of-accounts alignment** – before integration with external accounting software can go live, the car-rental chart of accounts must be agreed and mapped by the Finance team.

---

## Success Metrics

- **Zero manual reconciliation effort** – finance staff spend 0 hours per week manually reconciling rental income in the first month after go-live.
- **Invoice accuracy rate ≥ 99.5%** – fewer than 0.5% of invoices require correction after issuance.
- **Deposit refund SLA adherence ≥ 95%** – at least 95% of refundable deposits are released within the configured SLA (5 business days).
- **Accounting software sync reliability ≥ 99.9%** – fewer than 0.1% of transactions fail to sync within the agreed time window over any 30-day period.
- **Report generation time ≤ 10 seconds** – all standard financial reports are generated within 10 seconds for any date range up to 12 months.
- **100% audit-trail coverage** – every financial transaction, approval, adjustment, and deletion is captured in the audit log with no gaps.
