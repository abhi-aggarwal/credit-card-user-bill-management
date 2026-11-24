
# CardTrack - Python CLI Application
## Software Requirements Specification

**Version:** 1.0
**Application Type:** Python Script / CLI
**Database:** SQLite
**Interface:** Terminal / Command Line
**Frontend:** Not required

---

# 1. Project Overview

CardTrack is a Python-based command-line application
designed to manage multiple credit cards, track
monthly bills, record payments, calculate outstanding
balances, and monitor payment due dates.

The application will run locally on a computer.

There will be no web application, frontend,
web server, or graphical user interface.

## 1.1 Objectives

- Manage multiple credit cards.
- Track monthly statements.
- Record full and partial payments.
- Calculate outstanding balances.
- Track payment due dates.
- Identify overdue bills.
- Maintain payment history.
- Generate financial reports.
- Store information locally.

---

# 2. Technology Requirements

## Programming Language
Python 3.x

## Database
SQLite

## Python Standard Libraries
- sqlite3
- datetime
- decimal
- csv
- os
- pathlib
- logging

## Optional Libraries
- pytest: Automated testing
- openpyxl: Excel export
- tabulate: CLI table formatting

No frontend frameworks or web frameworks.

---

# 3. Application Architecture

The application must follow a modular structure.

## Modules

### 3.1 Main Module
Responsibilities:
- Application startup
- CLI menu
- User input
- Menu navigation
- Exit functionality

### 3.2 Database Module
Responsibilities:
- Database initialization
- Table creation
- Database connections
- CRUD operations
- Database transactions
- Data integrity

### 3.3 Card Manager
Responsibilities:
- Add credit card
- Edit credit card
- Archive credit card
- View all cards
- View individual card details

### 3.4 Bill Manager
Responsibilities:
- Create monthly bill
- Update bill information
- View bills
- Filter bills by month
- Filter bills by card
- Identify unpaid bills
- Identify overdue bills

### 3.5 Payment Manager
Responsibilities:
- Record payment
- Record partial payment
- Record full payment
- View payment history
- Correct payment records
- Handle payment reversals

### 3.6 Calculator Module
Responsibilities:
- Calculate total paid
- Calculate outstanding amount
- Calculate total outstanding across cards
- Calculate payment percentage
- Calculate monthly payment summaries

### 3.7 Reminder Manager
Responsibilities:
- Identify upcoming due dates
- Identify overdue bills
- Generate reminder lists
- Identify unpaid bills

### 3.8 Report Manager
Responsibilities:
- Monthly bill report
- Payment report
- Card-wise outstanding report
- Overdue report
- Export CSV
- Optional Excel export

---

# 4. Credit Card Management

Users must be able to:

1. Add a credit card.
2. View all cards.
3. View card details.
4. Update card information.
5. Archive a card.

## Card Fields

- Card ID
- Bank Name
- Card Nickname
- Last Four Digits
- Card Network
- Credit Limit
- Statement Generation Day
- Payment Due Day
- Billing Cycle
- Created Date
- Status

Never store full card numbers, CVVs, PINs,
or banking passwords.

---

# 5. Monthly Bill Management

Users must be able to:

1. Create a monthly bill.
2. View all bills.
3. View bills for a particular card.
4. Search bills by month.
5. Update bill information.
6. View unpaid bills.
7. View partially paid bills.
8. View overdue bills.
9. View historical bills.

## Bill Fields

- Bill ID
- Card ID
- Billing Month
- Statement Date
- Due Date
- Total Bill Amount
- Minimum Amount Due
- Created Date
- Updated Date

Bill status should be calculated using
payment records and due dates.

---

# 6. Payment Management

Users must be able to:

1. Record a payment.
2. Record multiple payments against one bill.
3. View payment history.
4. View payments for a particular card.
5. View payments for a particular month.
6. Correct payment entries.
7. Record payment reversals.

## Payment Fields

- Payment ID
- Bill ID
- Payment Date
- Payment Amount
- Payment Method
- Reference Number
- Notes
- Created Date

A payment must always be associated with
an existing bill.

---

# 7. Financial Calculations

## Remaining Amount

Remaining Amount =
Total Bill Amount - Total Valid Payments

## Total Outstanding

Total Outstanding =
Sum of Remaining Amounts Across All Bills

## Total Paid

Total Paid =
Sum of Valid Payments

## Payment Percentage

Payment Percentage =
(Total Paid / Total Bill Amount) * 100

All financial calculations must use Python Decimal.

---

# 8. Bill Status Management

Possible statuses:

- UNPAID
- PARTIALLY_PAID
- PAID
- OVERDUE

Rules:

1. No valid payments = UNPAID.
2. Some payment and remaining balance = PARTIALLY_PAID.
3. Zero outstanding = PAID.
4. Due date passed with outstanding balance = OVERDUE.

Overdue status takes priority over unpaid
and partially paid statuses.

Status should be calculated dynamically.

---

# 9. CLI Dashboard

The dashboard must display:

- Total number of credit cards
- Total monthly bills
- Total amount paid
- Total outstanding amount
- Upcoming payments
- Overdue payments
- Recent payment history

---

# 10. Reminder Management

The application must identify:

- Bills due within 7 days
- Bills due within 3 days
- Bills due today
- Overdue bills
- Fully paid bills

Initially, reminders will be displayed
when the user opens the application.

Automatic background notifications
are not required in the first release.

---

# 11. Database Requirements

## Table 1: credit_cards

Fields:
- id
- bank_name
- card_nickname
- last_four_digits
- card_network
- credit_limit
- statement_day
- due_day
- status
- created_at

## Table 2: bills

Fields:
- id
- card_id
- billing_month
- statement_date
- due_date
- total_amount
- minimum_due
- created_at
- updated_at

## Table 3: payments

Fields:
- id
- bill_id
- payment_date
- amount
- payment_method
- reference_number
- notes
- status
- created_at

## Table 4: transactions

Fields:
- id
- card_id
- transaction_date
- description
- transaction_type
- category
- amount
- created_at

## Table 5: reminders

Fields:
- id
- bill_id
- reminder_type
- scheduled_date
- status
- created_at

---

# 12. Database Relationships

- One credit card can have multiple bills.
- One bill can have multiple payments.
- One credit card can have multiple transactions.
- One bill can have multiple reminders.

Use foreign keys and database constraints.

Prevent accidental duplicate monthly bills
for the same card and billing period.

---

# 13. Main CLI Menu

1. Dashboard
2. Manage Credit Cards
3. Manage Monthly Bills
4. Record a Payment
5. View Payment History
6. View Outstanding Bills
7. View Upcoming Due Dates
8. View Overdue Bills
9. Generate Reports
10. Database Backup
11. Exit

---

# 14. Project Folder Structure

CardTrack/

- main.py
- config.py
- database/
  - db_manager.py
  - schema.py
- modules/
  - card_manager.py
  - bill_manager.py
  - payment_manager.py
  - calculator.py
  - reminder_manager.py
  - report_manager.py
- reports/
- backups/
- logs/
- tests/
- requirements.txt
- README.md

This is the proposed structure.
Implementation details will be decided during
development.

---

# 15. Error Handling

The application must handle:

- Invalid user input
- Invalid dates
- Invalid payment amounts
- Missing credit cards
- Missing bills
- Duplicate bills
- Database connection failures
- Duplicate payment submissions
- Invalid payment reversals

Errors must be logged appropriately.

The application must not crash because of
ordinary invalid user input.

---

# 16. Data Integrity and Security

- Use SQLite foreign key constraints.
- Use parameterized database queries.
- Use database transactions for payment operations.
- Use Decimal for financial calculations.
- Preserve payment history.
- Audit corrections and reversals.
- Back up the database regularly.
- Never store sensitive card credentials.

---

# 17. Development Phases

## Phase 1: Foundation
- Project setup
- SQLite database
- Table creation
- Database connection

## Phase 2: Credit Card Management
- Add card
- Edit card
- View cards
- Archive card

## Phase 3: Bill Management
- Create monthly bill
- View bills
- Update bills
- Filter bills

## Phase 4: Payment Management
- Record payments
- Partial payments
- Payment history
- Outstanding calculations

## Phase 5: Dashboard
- Total outstanding
- Total paid
- Upcoming bills
- Overdue bills

## Phase 6: Reports
- Monthly reports
- Card-wise reports
- CSV exports

## Phase 7: Testing
- Database tests
- Payment tests
- Calculation tests
- Date and status tests
- Error handling tests

---

# 18. First Release Acceptance Criteria

The first release is successful when:

1. Multiple cards can be added.
2. Multiple bills can be created.
3. Payments can be recorded.
4. Partial payments are supported.
5. Remaining amounts are calculated correctly.
6. Paid bills are identified.
7. Overdue bills are identified.
8. Payment history is maintained.
9. Dashboard summaries are accurate.
10. Data remains available after restarting
    the application.

---

# 19. Future Enhancements

- Credit card statement PDF import
- Automatic statement extraction
- Bank integrations
- Transaction categorization
- EMI tracking
- Interest calculation
- Advanced reporting
- Desktop graphical interface
- Web application

These are outside the initial release scope.

---

# Final Development Principle

Build a reliable Python command-line application
first.

Prioritize accurate financial calculations,
database integrity, payment history, and bill
tracking.

Do not introduce a frontend or bank integrations
until the scripting application is stable.
