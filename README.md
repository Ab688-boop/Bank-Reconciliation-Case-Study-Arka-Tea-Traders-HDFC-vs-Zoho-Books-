
# Bank Reconciliation: Zoho Books vs HDFC Statement

A bank reconciliation case study for a tea trading company (Arka Tea Traders Pvt Ltd), done in Excel. It finds why the company's books and the bank statement disagree, classifies every mismatch, and proves the gap is fully explained.

> This is a case study based on an assessment dataset, not work done for a real client.

## The problem

For the quarter 01/01/2026 to 31/03/2026, the Zoho Books ledger and the HDFC bank statement closed at different balances.

| | Amount (INR) |
|---|---:|
| Zoho Books closing balance | 276,610.00 |
| HDFC bank closing balance | 264,823.50 |
| **Gap** | **11,786.50** |

The small net gap hides much larger errors that happen to offset each other.

## The approach

1. **Validate the data.** Opening balance plus all movements must equal the closing balance in both files.
2. **Match entries.** Each Zoho entry is paired with an unused bank entry that has the same amount and a date within 5 days. Bank narrations and Zoho descriptions differ, so matching is by amount, date and context, not by text.
3. **Classify what is left.** Every unmatched item gets a type and a root cause.
4. **Prove it.** The differences must add up to the gap, and the bank reconciliation statement (BRS) must close at 0.00.

### Classification

| Type | Meaning | Where it is fixed |
|---|---|---|
| A | Error in Zoho (missing entry, duplicate, wrong amount) | Zoho, with a correcting journal entry |
| B | Error in the bank | Raised with the bank |
| C | Timing difference (for example, a cheque not yet presented) | No correction, disclosed in the BRS |
| D | Opening balance (prior-period) issue | Zoho |

## Results

12 mismatches found: **8 Type A, 3 Type C, 1 Type D, 0 Type B**.

| Finding | Type | Amount (INR) |
|---|---|---:|
| February rent standing instruction never booked in Zoho | A | 45,000.00 |
| Opening balance difference carried from December 2025 | D | 7,850.50 |
| Cheque to Darjeeling Highland Tea issued 28/03, not yet presented | C | 22,500.00 |
| Duplicate ACT Fibernet payment | A | 4,500.00 |
| Packaging Solutions payment keyed as 36,800 instead of 38,600 | A | 1,800.00 |
| Bank interest credits (3) not booked | A | 1,225.00 |
| Quarterly bank charges (2) not booked | A | 1,062.00 |
| Two cheque deposits dated a few days earlier in Zoho than at the bank | C | 0.00 |

**Bank reconciliation statement**

| | Amount (INR) |
|---|---:|
| Balance per Zoho | 276,610.00 |
| Net corrections to Zoho (Type A and D) | (34,286.50) |
| Adjusted Zoho balance | 242,323.50 |
| Add: cheque issued but not yet presented | 22,500.00 |
| **Balance per bank** | **264,823.50** |
| Difference | 0.00 |

**Business insight:** after the corrections, the bank account was overdrawn by 22,499.50 on 10/02/2026 (for 5 days), while Zoho showed a positive balance of 10,210.00. The missing rent entry and other errors hid the overdraft.

## Repository contents

```
.
└── docs/
    ├── Part_A_Discrepancy_Register.xlsx
    ├── Part_B_Bank_Reconciliation_Statement.pdf
    ├── Part_C_Correcting_Journal_Entries.md
    └── Part_D_Memo.pdf
```

| File | What it contains |
|---|---|
| Part A (Excel) | Discrepancy register, a line-by-line matching sheet, and a proof sheet built with formulas (SUMIFS) |
| Part B (PDF) | Formal bank reconciliation statement |
| Part C | Correcting journal entries for each Zoho error |
| Part D | Memo to the Finance Head: findings, root causes, recommendations |

## Key learnings and recommendations

- Reconcile every month and have a second person review it. None of these errors survived because of difficulty, only because nobody compared the two records.
- Connect the bank feed to the accounting system so interest, charges and standing instructions are not typed by hand.
- Raise vendor payments against bills so duplicates are blocked, and keep a cheque register to track unpresented cheques.
- Set a low-balance alert so an overdrawn account is seen the same day.

## Tools

Excel (SUMIFS, COUNTIFS), Zoho Books ledger export, HDFC bank statement.

## Author

Abhishek Kumar, MBA (Business Analytics in Finance and Operations).
Linkedin - www.linkedin.com/in/abhishek-kumar-a5a819283
