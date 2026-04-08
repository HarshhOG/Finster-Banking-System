# 💰 FINSTER BANK 2026 — Financial Simulation Engine

📊 Excel-Based Banking System for FINAST₹A 2026

A real-time financial tracking and simulation system designed to manage all transactions, loans, and event-based finances during a live inter-college fest. This system powers the entire financial layer of FINAST₹A through a structured and automated Excel engine.

---

## 🌐 Context

FINSTER BANK is the core financial system behind **FINAST₹A 2026**, the flagship commerce and finance fest of THK Jain College, Kolkata.

Each participating college operates like a financial entity with capital allocation, investment decisions, and loan strategies — all tracked live through this system.

---

## 🚀 Key Highlights

* Real-time financial tracking system
* Supports 40+ colleges simultaneously
* Handles 1000+ transactions
* Automated loan & credit scoring system (CIBIL-inspired logic)
* Multi-sheet linked architecture
* Designed for live, high-pressure event execution
* Zero manual calculation — fully formula-driven

---

## 🧠 What is FINSTER BANK?

FINSTER BANK is an in-house virtual banking ecosystem where:

* Each college starts with ₹5,00,000
* Money flows based on event participation and performance
* Colleges can take loans based on participation (credit scoring system)
* Funds can be reinvested into high-risk, high-reward events
* Final profitability determines the Best College Representative

---

## 🗂️ File Structure (5 Core Sheets)

---

### 1. EVENT_MASTER

Central reference table for all events.

* Stores event name, category, and entry fees
* Used by other sheets via lookup functions
* Differentiates between STANDARD and STAR events

---

### 2. TRANSACTION_LOG

Primary ledger of the system.

* All financial activities recorded here

* Supports:

  * ENTRY (event registration)
  * LOAN_DISBURSED
  * STAR_TRANSFER
  * STAR_CHEQUE
  * EVENT_PRIZE
  * PENALTY

* Includes:

  * Auto timestamps
  * Reference ID generation
  * Validation checks
  * Running balance calculation

---

### 3. COLLEGE_MASTER

Live financial dashboard for all colleges.

* Tracks:

  * Opening capital
  * Total inflows & outflows
  * Current balance
  * Final settlement

* Fully automated — no manual input

---

### 4. CIBIL_ENGINE

Credit scoring system based on participation.

* Calculates:

  * Number of events entered
  * Participation percentage

* Determines loan eligibility

---

### 5. LOAN_ENGINE

Manages loan distribution and repayment logic.

* Calculates:

  * Maximum loan eligibility
  * Interest rate based on participation
  * Total repayment amount

* Encourages strategic participation

---

## ⚙️ How It Works

### Before the Event

* All colleges are assigned FIN codes
* Opening capital is allocated
* Event structure is pre-configured

---

### During the Event

* Operators log transactions in real-time
* All balances update automatically
* Loan eligibility updates dynamically
* Financial decisions impact live standings

---

### End of Day

* Final balances are calculated
* Loan settlements processed
* Highest balance wins Best CR Award

---

## 🧮 Formula Architecture

Built using advanced Google Sheets-compatible formulas:

* `ARRAYFORMULA` for bulk processing
* `VLOOKUP` for event mapping
* `QUERY` for aggregation
* `COUNTA` for dynamic counts
* `IFERROR` for clean fallback handling

The system is optimized for Google Sheets but remains compatible with Excel.

---

## 📊 Use Cases

* Event-based financial simulation
* Real-time transaction tracking
* Credit and loan modeling
* Educational finance simulations
* Operations and logistics management

---

## 📸 Screenshots

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/9c64f7b9-a9aa-4b5a-8ac8-dd7be1f132f3" />
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/f02a5cb5-e5f6-4a19-98db-f1be9b72fedc" />
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/e224653b-b088-45d1-a3d6-9fb009be838a" />
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/58ffd67e-f1bb-447e-a35d-4e03055a540f" />
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/df623b01-3d79-4a81-a266-1d429f92f92a" />


---

## 👨‍💻 My Contribution

* Designed complete system architecture
* Built all sheets and formulas from scratch
* Developed CIBIL-inspired credit system
* Created real-time transaction engine
* Implemented loan and interest logic
* Tested system for live execution

---

## 🚀 Future Improvements

* Dashboard visualization layer
* Automation via scripts
* Real-time multi-user input system
* Integration with web-based platform

---

## 🛠️ Tools Used

* Microsoft Excel
* Google Sheets

---

## 🏆 Project Impact

* Designed for 40+ participating colleges
* Enables real-time decision-making
* Bridges finance theory with practical execution
* Used as a live operational system

---

## 🛠️ Built By

**Harsh Binani**
Convenor — FINAST₹A 2026

---

*© 2026 FINAST₹A — THK Jain College, Kolkata*
