# FINSTER BANK 2026 — Banking System (Excel)

The operational banking engine for FINASTRA 2026.

**File:** `FINSTER_2026.xlsx`
**Built for:** Google Sheets (compatible with Excel)
**Purpose:** Live financial tracking system for all participating colleges on fest day

---

## What is FINSTER BANK?

FINSTER BANK is the in-house virtual banking system that powers the financial layer of FINASTRA 2026. Every participating college is assigned a FIN Code and an opening capital of Rs. 5,00,000. Throughout the day, colleges earn and spend virtual currency based on event participation, performance, loans, and strategic reinvestments.

The college with the highest final balance at end of day wins the Best College Representative award.

This Excel file is the complete operational system used by the banking team on the day of the fest. It is designed to be run live, with operators entering data in real time across multiple counters.

---

## File Structure — 5 Sheets

---

### Sheet 1: EVENT_MASTER

The master reference table for all events. Every other sheet pulls from this via VLOOKUP.

| Column       | Description                                      |
|--------------|--------------------------------------------------|
| Event Name   | Name of the event                                |
| Category     | STANDARD or STAR                                 |
| Entry Fee    | Virtual currency charged to a college per entry  |

**Event Categories and Fees:**

| Event       | Category | Entry Fee    |
|-------------|----------|--------------|
| Quiz        | STANDARD | Rs. 80,000   |
| Debate      | STANDARD | Rs. 80,000   |
| Boardroom   | STANDARD | Rs. 80,000   |
| Profit-Folio | STANDARD | Rs. 80,000  |
| Trading     | STAR     | Rs. 1,00,000 |
| Auction     | STAR     | Rs. 1,00,000 |
| Monopoly    | STAR     | Rs. 1,00,000 |

STANDARD events charge a flat entry fee. STAR events charge a higher fee and are the designated reinvestment targets for loan capital and surplus funds.

A formula at the top right auto-counts the total number of events using `COUNTA`.

---

### Sheet 2: TRANSACTION_LOG

The primary ledger of the entire system. Every financial action — entry, loan, prize, transfer, penalty — is recorded here as a timestamped row. This is the only sheet where operators manually enter data.

**Capacity:** 1000 rows

| Column               | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Timestamp            | Date and time of entry (auto via formula)                                   |
| Counter              | Name of the operator entering the transaction (e.g. Harsh Counter-1)       |
| College Name         | Full name of the participating college                                      |
| FIN Code             | Unique college identifier (e.g. FIN2026-01)                                 |
| Event Name           | Event the transaction relates to                                            |
| Event Category       | Auto-filled via VLOOKUP from EVENT_MASTER (STANDARD or STAR)                |
| Transaction Type     | Type of transaction — see types below                                       |
| Amount               | Manually entered amount (where applicable)                                  |
| Amount (Auto Corrected) | Formula-derived corrected amount based on event fee or manual input      |
| Reference ID         | Auto-generated unique ID: FINCode-EventName-TransactionType-RowNumber      |
| Validation Check     | Formula that validates the transaction against CIBIL and loan rules         |
| Participation Count  | Running count of how many events the college has entered                    |
| Running Balance      | Live balance for the college at that point in the day                       |

**Transaction Types:**

| Type             | Direction | Description                                                    |
|------------------|-----------|----------------------------------------------------------------|
| ENTRY            | Outflow   | College registers a team for an event — entry fee is deducted  |
| LOAN_DISBURSED   | Inflow    | Loan is credited to a college's account                        |
| STAR_TRANSFER    | Outflow   | College reinvests funds into a STAR event                      |
| STAR_CHEQUE      | Inflow    | Returns credited from a STAR event win                         |
| EVENT_PRIZE      | Inflow    | Prize money credited for winning or placing in an event        |
| PENALTY          | Outflow   | Penalty charged to a college                                   |

Multiple counters operate simultaneously. Each counter is identified by name in the Counter column, allowing the banking team to track who entered each transaction.

---

### Sheet 3: COLLEGE_MASTER

The live balance sheet for all registered colleges. This sheet is fully formula-driven — operators never type here. It aggregates data from TRANSACTION_LOG automatically.

**Capacity:** 1000 rows (44+ colleges registered)

| Column                  | Description                                                             |
|-------------------------|-------------------------------------------------------------------------|
| FIN Code                | Unique identifier assigned to each college (FIN2026-01, FIN2026-02...) |
| College Name            | Full name of the institution                                            |
| Opening Capital         | Starting balance for every college — Rs. 5,00,000                      |
| Total Inflows           | Sum of all LOAN_DISBURSED + STAR_CHEQUE + EVENT_PRIZE transactions      |
| Total Outflows          | Sum of all ENTRY + STAR_TRANSFER + PENALTY transactions                 |
| Current Balance         | Live balance: Opening Capital + Inflows - Outflows                      |
| Final Settlement Balance | End-of-day balance after all loan repayments and settlements           |

Balances update automatically as new transactions are logged. The college with the highest Final Settlement Balance at end of day wins the Best CR award.

**Registered Colleges (sample):**
Adamas University, Amity University, Brainware University, Jadavpur University, Presidency University, St. Xaviers College, St. Xaviers University, Sister Nivedita University, Techno Main Salt Lake, and 35+ others across Kolkata.

---

### Sheet 4: CIBIL_ENGINE

The credit scoring engine. Determines each college's loan eligibility based on how many events they have participated in. Modelled loosely on India's CIBIL credit scoring concept.

| Column                   | Description                                                  |
|--------------------------|--------------------------------------------------------------|
| FIN Code                 | College identifier                                           |
| Total Events Participated | Count of valid ENTRY transactions for the college           |
| Participation %          | Percentage of total events the college has participated in   |

The Participation % feeds directly into the LOAN_ENGINE to determine the maximum loan amount and applicable interest rate. A college that has not participated in enough events is flagged as `INSUFFICIENT_PARTICIPATION` and cannot access loans.

---

### Sheet 5: LOAN_ENGINE

Manages the loan system for all colleges. Loan eligibility, amount, and interest rate are all dynamically calculated from CIBIL scores and transaction history.

| Column              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| FIN                 | College identifier                                                          |
| College Name        | Full name                                                                   |
| Events Participated | Pulled from CIBIL_ENGINE                                                    |
| Max Loan            | Maximum loan the college is eligible for, based on participation            |
| Loan Taken          | Total LOAN_DISBURSED amount from TRANSACTION_LOG for this college           |
| Interest %          | Interest rate determined by participation percentage                        |
| Loan Status         | ELIGIBLE or INSUFFICIENT_PARTICIPATION                                      |
| Total Payable       | Final amount the college must repay: Loan Taken + Interest                  |

Colleges must participate in a minimum number of events before they can apply for a loan. The more events a college has entered, the higher their max loan and the lower their interest rate — incentivising broader participation.

---

## How It Works on Fest Day

**Setup (before fest)**
All colleges are pre-loaded in COLLEGE_MASTER with their FIN codes and opening capital of Rs. 5,00,000. EVENT_MASTER is populated with all events and fees.

**During the fest**
Operators sit at designated counters (Counter-1, Counter-2, Counter-3, Counter-4, Counter-6). As colleges register teams for events, the operator finds the college's FIN code and logs the transaction in TRANSACTION_LOG with the FIN code, event name, and transaction type. All downstream calculations — balance updates, CIBIL scores, loan eligibility — update automatically.

When a college wants a loan, the LOAN_ENGINE is checked. If their CIBIL score is sufficient, a LOAN_DISBURSED entry is made. When prize money is awarded, EVENT_PRIZE entries are made. If a college reinvests into a STAR event, a STAR_TRANSFER entry is logged, and if they win, a STAR_CHEQUE entry credits the returns.

**End of day**
COLLEGE_MASTER shows the Final Settlement Balance for every college after loan repayments. The Best CR award goes to the college with the highest final balance.

---

## Formula Architecture

The file uses Google Sheets-native functions including `ARRAYFORMULA` and `QUERY`, which means it is designed to be run in Google Sheets. When opened in Excel, these functions fall back gracefully via `IFERROR` wrappers so the file does not break.

Key formula patterns used:
- `ARRAYFORMULA` with `VLOOKUP` and `QUERY` for aggregating transaction data per college
- Auto-generated Reference IDs combining FIN code, event, transaction type, and row number
- `IFERROR` wrappers on all aggregation formulas to handle empty rows cleanly
- `COUNTA` for dynamic event count in EVENT_MASTER
- `VLOOKUP` on EVENT_MASTER for auto-filling event category in every transaction row

---

## Important Notes

- Do not type in COLLEGE_MASTER, CIBIL_ENGINE, or LOAN_ENGINE — these are read-only formula sheets
- All data entry happens exclusively in TRANSACTION_LOG
- The FIN Code must be entered accurately — it is the key that links all sheets
- The file is optimised for Google Sheets. Open and operate in Google Sheets for full formula functionality
- Transaction rows should not be deleted mid-day as this will break running balances and reference IDs

---

## Built By

Harsh Binani — Convenor, FINASTRA 2026

---

*FINASTRA 2026 — THK Jain College, Kolkata*
