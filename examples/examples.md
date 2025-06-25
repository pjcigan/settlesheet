# SettleSheet Worked Examples

This document provides worked example scenarios for verifying the correctness of SettleSheet-generated spreadsheets. Each example includes test transactions, expected results, and a reference to the corresponding spreadsheet generator script.

---

## Example 1: The Responsible Weekend Getaway (Single Currency)

**Participants:** Alice, Bob, Charlie, Diana  
No solo expenses in this example - everyone's actually sharing things like mature adults

**Test Transactions:**

| Date       | Description                                                    | Amount | Paid By | Participants           |
|------------|---------------------------------------------------------------|--------|---------|------------------------|
| 2024-03-15 | Airbnb (because hotels are for people with expense accounts)  | 240.00 | Alice   | All                    |
| 2024-03-15 | Group dinner at "That Instagram-Famous Place"                | 120.00 | Bob     | All                    |
| 2024-03-16 | Museum tickets (for "cultural enrichment")                   | 60.00  | Charlie | Alice, Charlie, Diana  |
| 2024-03-16 | Emergency coffee run for the group                            | 28.00  | Charlie | All                    |
| 2024-03-16 | Uber because someone wore heels to a hiking trail             | 32.00  | Alice   | Alice, Bob             |
| 2024-03-17 | Fancy brunch (the "we're definitely adults" kind)            | 80.00  | Diana   | All                    |
| 2024-03-17 | Snacks for the road trip home                                 | 36.00  | Bob     | All                    |

**Expected Results:**
- Total Expenses: $596.00
- Per-person average: $149.00

**Expected Final Balances:**
- Alice: Should receive $110.00
- Bob: Should receive $14.00
- Charlie: Should pay $58.00
- Diana: Should pay $66.00

**Expected Optimized Settlement (One potential solution):**
- Charlie pays Alice: $44.00
- Diana pays Alice: $66.00
- Charlie pays Bob: $14.00

(Total: 3 transactions instead of 6)

---

## Example 2: The Multi-Currency European Adventure

**Participants:** Alice, Bob, Charlie  
**Base Currency:** USD  
**Exchange Rates:** EUR = 1.10 USD, GBP = 1.27 USD

**Test Transactions:**

| Date       | Description                                                    | Amount Paid | Paid In | Paid By | Participants |
|------------|---------------------------------------------------------------|-------------|---------|---------|--------------|
| 2024-06-10 | London hotel (because everything's expensive here)            | 180.00      | GBP     | Alice   | All          |
| 2024-06-11 | Fish & chips (when in Rome... wait, wrong country)            | 45.00       | GBP     | Bob     | All          |
| 2024-06-12 | Train to Paris (the fancy fast one)                           | 150.00      | EUR     | Charlie | All          |
| 2024-06-13 | Parisian café breakfast (€20 for coffee is normal, right?)    | 60.00       | EUR     | Alice   | All          |
| 2024-06-13 | Museum tickets because we're "cultured"                      | 36.00       | EUR     | Bob     | Alice, Bob   |
| 2024-06-14 | Airport overpriced sandwich panic                             | 24.00       | USD     | Charlie | All          |

**Expected Results:**
- Total Expenses (USD): $580.35
- Per-person average: $193.45

**Expected Final Balances:**
- Alice: Should receive $94.55
- Bob: Should pay $103.30
- Charlie: Should receive $8.75

**Expected Currency Breakdown:**
- Alice paid: $294.60 USD (£180 + €60 converted)
- Bob paid: $96.75 USD (£45 + €36 converted)
- Charlie paid: $189.00 USD (€150 + $24)

**Expected Optimized Settlement:**
- Bob pays Alice: $94.55
- Bob pays Charlie: $8.75

(Total: 2 transactions instead of 3)


## Example 3: 8-person Group Reunion Trip

**Participants:** Alice, Bob, Charlie, Diana, Eve, Frank, Grace, Henry
Demonstration of larger groups

**Test Transactions:**

| Date | Description | Amount | Paid By | Participants |
|------|-------------|---------|---------|--------------|
| 2024-11-01 | Hotel rooms (3 nights) | 720.00 | Alice | All |
| 2024-11-01 | Rental car | 280.00 | Frank | Alice, Bob, Charlie, Diana, Eve, Frank |
| 2024-11-02 | Breakfast | 96.00 | Bob | All |
| 2024-11-02 | Theme park tickets | 400.00 | Grace | Grace, Henry, Alice, Bob, Diana |
| 2024-11-02 | Lunch at park | 85.00 | Diana | Grace, Henry, Alice, Bob, Diana |
| 2024-11-03 | Groceries for BBQ | 120.00 | Charlie | All |
| 2024-11-03 | Wine and beer | 75.00 | Eve | Charlie, Diana, Eve, Frank, Grace |
| 2024-11-04 | Gas for rental car | 48.00 | Frank | Alice, Bob, Charlie, Diana, Eve, Frank |
| 2024-11-04 | Escape room | 160.00 | Henry | Bob, Charlie, Eve, Henry |
| 2024-11-05 | Farewell dinner | 240.00 | Bob | All |

### Summary Calculations

**Total Paid by Each:**
- Alice: $720.00
- Bob: $336.00
- Charlie: $120.00
- Diana: $85.00
- Eve: $75.00
- Frank: $328.00
- Grace: $400.00
- Henry: $160.00
- **Total: $2,224.00**

**Final Balances:**
- Alice: **+$421.04** (is owed)
- Bob: **-$2.67** (owes)
- Charlie: **-$136.37** (owes)
- Diana: **-$228.67** (owes)
- Eve: **-$181.66** (owes)
- Frank: **+$111.33** (is owed)
- Grace: **+$141.00** (is owed)
- Henry: **-$124.00** (owes)

**Optimized Settlements (Greedy Method):**
1. Bob pays Alice: $2.67
2. Charlie pays Alice: $136.37
3. Diana pays Alice: $228.67
4. Eve pays Alice: $53.33
5. Eve pays Frank: $111.33
6. Eve pays Grace: $17.00
7. Henry pays Grace: $124.00

*These numbers are one possible solution, and the exact amounts paid between specific participants may differ from other valid solutions due to the optimization logic used.*

**Alternative Optimized Settlement:**
1. Bob pays Alice: $2.67
2. Charlie pays Alice: $136.37
3. Diana pays Alice: $228.67
4. Eve pays Grace: $141.00
5. Eve pays Frank: $40.66
6. Eve pays Alice: $0.00
7. Henry pays Frank: $111.33
7. Henry pays Alice: $12.67

*In this alternative, Eve pays her full negative balance split between Grace and Frank, and Henry pays most of his negative balance to Frank, with the remainder to Alice. All positive and negative balances are satisfied, but the specific payers/recipients differ from the default solution. Any settlement pattern that matches the net balances is valid as long as the total inflows and outflows for each participant match their final balance.*

---

## How to Generate These Example Spreadsheets

To generate the above example spreadsheets for verification or demonstration, run the following command from where you want the examples to be saved:

```bash
python3 .../path/to/settlesheet/examples/generate_worked_examples.py
```

This will create two files in the `examples/` directory:
- `responsible_weekend_getaway.xlsx`
- `multicurrency_european_adventure.xlsx`
- `reunion_trip.xlsx`

You can open these files in Excel, Google Sheets, or LibreOffice to verify that the calculations and settlements match the expected results above. 
