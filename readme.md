# SettleSheet 📊💸

**Finally, a way to settle your... expenses... without losing friends over who owes what for that pizza from three weeks ago.**

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![Excel Compatible](https://img.shields.io/badge/Excel-Compatible-green.svg)]()
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Compatible-green.svg)]()
[![LibreOffice Compatible](https://img.shields.io/badge/LibreOffice-Compatible-green.svg)]()
[![PyPI version](https://badge.fury.io/py/settlesheet.svg)](https://badge.fury.io/py/settlesheet)
[![Downloads](https://pepy.tech/badge/settlesheet)](https://pepy.tech/project/settlesheet)
[![Sponsor](https://img.shields.io/badge/Sponsor-%F0%9F%A7%AA-blue?logo=github&style=flat)](https://github.com/sponsors/pjcigan)

![SettleSheet Logo](./images/Logo.jpg)

## What the Sheet is This?

SettleSheet is a **spreadsheet-based expense tracker**, with many templates that are ready to go.  The python script generates usable and functional Excel files for tracking and splitting group expenses. No apps to download, no accounts to create, no servers to maintain, and no "premium features" locked behind a paywall. Just pure, unadulterated spreadsheet magic.

**Why SettleSheet?** Because arguing about who owes what is more exhausting than actually paying for stuff.

### **Don't Know How to Code? No Problem!**

You have two ways to use SettleSheet:

1. **Download a Template** (Zero coding required) - Grab one of the pre-made [templates](./templates/), change the names, and start tracking expenses immediately
2. **Generate Custom Spreadsheets** (Optional Python) - Run the Python script to create customized spreadsheets with your preferred themes, currencies, and participant lists

**Pro Tip:** Create your spreadsheet, upload it to Google Sheets, and give everyone in your group access. Now anyone can add expenses in real-time from their phone during your trip. No more "I'll tell you what I spent later" excuses!

### Key Features

- **📱 Works Everywhere**: Excel, Google Sheets, LibreOffice - if it can open a spreadsheet, it can handle your financial drama
- **🤝 Real-Time Collaboration**: Upload to Google Sheets, share with your group, let everyone add expenses from their phone as they happen
- **🎬 Zero Installation Required**: Download a template and start using immediately - no coding, no apps, no hassle
- **🌍 Multi-Currency Support**: Because your European vacation involved at least 5 different currencies and you're still confused
- **🧮 Optimized Settlements**: Uses clever programming to minimize the number of transactions (because nobody wants to Venmo 47 different people)
- **🎨 Pretty Colors**: 6 visually appealing themes so your expense tracker can be as aesthetic as your Instagram
- **💡 Smart Formulas**: Automatically calculates who owes what, supports subgroups such as writing "John, Sarah" instead of "All" in the expense participants field
- **🔄 Real-Time Updates**: Change an expense amount and watch the settlement calculations update instantly

## Quick Start (Get Your Sheet Together)

### Installation

**For immediate use:** 
Download a template from [`/templates`](./templates/) folder - no other installation required!

**For custom spreadsheet generation:**

```bash
pip install settlesheet
```
**Or clone from source:**
```bash
git clone https://github.com/pjcigan/settlesheet.git
```


# CLI Usage

After installation, use the `settlesheet` command to generate a spreadsheet:

```bash
settlesheet mysheet.xlsx --participants Alice Bob Charlie --theme dark --currencies JPY GBP --native USD --rows 100
```

- `mysheet.xlsx`: Output filename
- `--participants`: List of participant names
- `--theme`: Color theme (bright, neutral, sleek, bold, dark, light)
- `--currencies`: List of foreign currency codes (optional)
- `--exchange_rates`: List of exchange rates for the currencies, in the same order (optional)
- `--native`: Native/base currency code (default: USD)
- `--rows`: Number of expense rows (default: 60)
- `--background_color`: Worksheet background color (optional)

## Exchange Rate Defaults
- If you specify `--currencies` but not `--exchange_rates`, the script uses 5-year average USD rates for common currencies **if** `--native USD`.  Otherwise currencies without specified exchange rates are set to 1.0 by default.
- Warnings/info messages will clarify which rates are used.

## Example

```bash
settlesheet eurotrip.xlsx --participants Alice Bob Charlie --theme bright --currencies EUR GBP JPY --native USD
```
When exchange rates are not specified for the input currencies by also using `--exchange_rates` ..., and native currency is set to USD, default average rates will be used for select common currencies. Otherwise, un-specified currencies have rates set to 1.0 by default.

```bash
settlesheet eurotrip.xlsx --participants Alice Bob Charlie --theme bright --currencies EUR GBP JPY --native EUR
```
This will set all rates to 1.0 unless you specify `--exchange_rates`.

---

## Usage

### **Option 1: Download & Go (Recommended for Most People)**

**The fastest way to get started:**

1. **Download a template** from the [`/templates`](./templates/) folder (or generate one using the examples below)
2. **Upload to Google Sheets** (or open in Excel/LibreOffice)
3. **Share with your group** - give everyone edit access
4. **Start adding expenses** as they happen during your trip
5. **Watch the magic** as settlements calculate automatically

**Why Google Sheets?** Everyone has a Google account, everyone has a phone, and everyone can add expenses in real-time. No more post-trip archaeology trying to remember what that €23.50 charge was for.

### **The Group Collaboration Workflow**

This is where SettleSheet really shines:

1. **Before your trip:** Create/download your expense sheet
2. **Upload to Google Sheets** and share with all participants  
3. **During your trip:** Anyone can add expenses immediately. Real-time updates, real-time settlement amounts.
4. **End of trip:** The spreadsheet automatically updates totals, everyone knows exactly who owes what. No extra steps or headaches required.

### **Option 2: Create Custom Spreadsheets (For the Python-Inclined)**

Want custom themes, specific currencies, or particular participant lists? Generate your own:

#### Installation

**Method A: Install via pip (Recommended)**
```bash
pip install settlesheet
```

**Method B: Clone from GitHub**
```bash
git clone https://github.com/pjcigan/settlesheet.git
cd settlesheet
python settlesheet.py
```

*Dependencies: openpyxl (automatically installed with pip)*


#### Basic Domestic Expenses
```python
from settlesheet import create_expense_spreadsheet

# Create a basic domestic trip spreadsheet
create_expense_spreadsheet(
    filename="weekend_trip.xlsx",
    participants=["Alice", "Bob", "Charlie"],
    exchange_rates=None  # No foreign currency conversion needed
)
```

#### International Trip with Single Currency
```python
# Single foreign currency (like a trip to Japan)
create_expense_spreadsheet(
    filename="tokyo_adventure.xlsx",
    participants=["Alice", "Bob", "Charlie", "Daisuke"],
    exchange_rates={"JPY": 1/149.25},  # 1 JPY = 0.0067 = 1/149.25 USD
    native_currency="USD",
    color_theme="sleek"
)
```

#### Multi-Country European Chaos
```python
# Multiple currencies for that epic Euro trip
create_expense_spreadsheet(
    filename="european_chaos.xlsx",
    participants=["Alice", "Bob", "Charlie", "Diana", "Enrique", "Francesca", "Giles", "Holly"],
    exchange_rates={
        "EUR": 1.10,    # 1 EUR = 1.10 USD
        "GBP": 1.27,    # 1 GBP = 1.27 USD  
        "CHF": 1.08     # 1 CHF = 1.08 USD
    },
    native_currency="USD",
    color_theme="bold",
    background_color="auto"
)
```

**💱 Exchange Rate Direction:** The rates represent how much 1 unit of the local currency equals in your native currency. For example:
- `"EUR": 1.10` means 1 Euro = 1.10 USD
- `"JPY": 0.0067` means 1 Yen = 0.0067 USD

**🔄 Rate Conversion Tip:** If you use rates quoted the other way (like "123.45 JPY = 1 USD"), just use `1/rate`:
```python
exchange_rates={"JPY": 1/149.25}  # Converts 149.25 JPY per USD to 0.0067 USD per JPY
```

### Using Your Spreadsheet

Once you've generated your spreadsheet (or downloaded one of the template files), here's how to actually use it:

#### 1. **Initial Setup**
- **Change participant names**: Edit the colored participant cells to match your group members
- **Update exchange rates** (multi-currency only): Check current rates and update the currency table
- **Choose your theme**: The spreadsheet comes pre-styled, but you can modify colors if needed

#### 2. **Adding Expenses**

Navigate to the expense table and start adding your expenses. Each row represents one expense:

| Date | Description | Amount | Paid By | Participants |
|------|-------------|---------|---------|--------------|
| 2024-03-15 | Dinner downtown | 84.50 | Alice | All |
| 2024-03-15 | Uber to hotel | 23.00 | Bob | Alice, Bob |
| 2024-03-16 | Museum tickets | 45.00 | Charlie | Alice, Charlie, Diana |
| 2024-03-16 | Alice's metro card | 12.00 | Alice | Alice |

**Key Points:**
- **Participants**: Use "All" for everyone, or list specific people: "Alice, Bob, Charlie"
- **Paid By**: Only one person per payment row (see limitations below) - if more than one person paid, just enter what each paid & who it applies to on separate rows
- **Amount**: Just the number - currency formatting is handled automatically. For multi-currency spreadsheets, also update the currency paid in.
- Single participant expenses are allowed, such as the metro card example above.  This can be useful for keeping track of your total trip expenses, even those not split among the group. 

#### 3. **Adding More Expense Rows**

When you need more rows:
1. **Insert new rows** 
2. **Copy formulas down**: Select the last expense row and copy it down to create new rows
3. **The formulas will automatically adjust** to the new row numbers


#### 4. **Reading Your Results**

The spreadsheet provides two settlement methods:

##### **Direct Settlements Matrix**
- Shows exactly what each person owes each other person
- More transactions, but very clear about individual debts
- Look for the "Settlements (Who Pays Whom)" section

##### **Optimized Settlements Matrix**  
- Uses the 'greedy' algorithm to minimize the total number of transactions among the entire group
- Fewer payments needed overall, which means they likely look different from the direct debts
- Look for the "Optimized Settlements (Minimized Transactions)" section

**Optimized settlement Example 1**: Instead of Alice paying Bob $20, Bob paying Charlie $15, and Charlie paying Alice $5, the optimized version might just show Alice paying Charlie $10.

**Optimized settlement Example 2**:  
Suppose four people (Alice, Bob, Charlie, David) share several expenses:

- Alice pays $60 for dinner (split among Alice, Bob, Charlie)
- Bob pays $30 for drinks (split among Bob, Charlie, David)
- Charlie pays $20 for dessert (split among all four)

Without optimization, there would be 7 separate payments between group members to settle up.
With direct pairwise netting, this reduces to 5 transactions, as debts are offset where possible.
With optimized settlements (greedy method), only 3 payments are needed:
- David pays $15 to Alice
- Charlie pays $15 to Alice
- Bob pays $5 to Alice

This achieves the same net result for everyone, but with the minimum number of transactions.

### Important Limitations & Workarounds

- **Even splits only**: All expenses are split evenly among the specified participants. For uneven splits, create separate line items.
  ```
  Instead of: "Dinner $100, Alice pays 50%, Bob pays 30%, Charlie pays 20%"
  Do this:    "Dinner - Alice's portion: $50, Alice, Alice"
              "Dinner - Bob's portion: $30, Alice, Bob" 
              "Dinner - Charlie's portion: $20, Alice, Charlie"
  ```

- **Single payer per row**: "Paid By" only accepts one person. If multiple people split a payment, create separate rows.
  ```
  Instead of: "Hotel $200, John, Sarah, All"  
  Do this:   "Hotel - John's half: $100, John, All"
             "Hotel - Sarah's half: $100, Sarah, All"
  ```

## Example Scenarios

### 🏠 **The Roommate Situation**
```python
create_expense_spreadsheet(
    filename="roommate_expenses.xlsx",
    participants=["Alex", "Jordan", "Casey"],
    exchange_rates=None,  # No foreign currency
    color_theme="neutral"
)
```
*Perfect for tracking groceries, utilities, and that time someone bought way too much toilet paper.*

### ✈️ **The Group Vacation**
```python
create_expense_spreadsheet(
    filename="bali_trip.xlsx",
    participants=["Sarah", "Mike", "Emma", "David", "Lisa"],
    exchange_rates={"IDR": 0.000067},  # 1 IDR = 0.000067 USD (or use 1/15000)
    native_currency="USD", 
    color_theme="bright"
)
```
*For when you're in Bali and everything costs either 50 cents or $50 and nobody can math anymore.*

### 🌍 **The Euro Trip that Broke the Bank**
```python
create_expense_spreadsheet(
    filename="euro_trip_2024.xlsx",
    participants=["Team Chaos", "Budget Destroyer", "Card Decliner"],
    exchange_rates={
        "EUR": 1.10,     # 1 EUR = 1.10 USD
        "GBP": 1.27,     # 1 GBP = 1.27 USD
        "CHF": 1.08,     # 1 CHF = 1.08 USD
        "SEK": 0.096     # 1 SEK = 0.096 USD
    },
    native_currency="USD",
    color_theme="sleek"
)
```
*When you've been to 4 countries in 5 days and your wallet is crying in multiple languages.*

## Features That'll Make You Think "Holy Sheet!"

### **Six Appealing Themes**
- **[Bright](./images/bright.png)**: For optimists and people who like colors. I'm told they exist.
- **[Neutral](./images/neutral.png)**: For adults who have their life together. I'm told they also exist, but I'm less sure.
- **[Sleek](./images/sleek.png)**: For minimalists and people with that timeless taste.
- **[Bold](./images/bold.png)**: For those who want their spreadsheet to pop.
- **[Dark](./images/dark.png)**: For night owls and Batman fans.
- **[Light](./images/light.png)**: For people who actually use white mode. (shudder)

| [![Bright](./images/bright.png)](./images/bright.png) | [![Neutral](./images/neutral.png)](./images/neutral.png) | [![Sleek](./images/sleek.png)](./images/sleek.png) |
|---|---|---|
| [![Bold](./images/bold.png)](./images/bold.png) | [![Dark](./images/dark.png)](./images/dark.png) | [![Light](./images/light.png)](./images/light.png) |

### **Two Settlement Methods**
1. **Direct Settlements**: Shows exactly what each person owes each other person
2. **Optimized Settlements**: Uses a greedy algorithm to minimize total transactions

*Example: Instead of 6 separate payments, you might only need 2. Your Venmo will thank you.*

### **Multi-Currency Magic**
- Automatically converts all expenses to your home currency
- Updates exchange rates as needed
- Handles the chaos of "Wait, was that £20 or €20?"

## Suggested Uses (When Life Gets Expensive)

### 🚗 **Road Trip Adventures**
*When someone always forgets to bring cash for gas, but never forgets to eat your snacks.*

### 🎉 **Bachelor/Bachelorette Parties**
*Because someone needs to keep track of expenses when half the group can't remember what happened after 9 PM.*

### 🎒 **Euro Backpacking Expeditions**
*For when you're 23, broke, and splitting a €4 hostel bed four ways, but also somehow spending €50 on "just one drink."*

### 🏠 **Roommate Reality**
*Groceries, utilities, and that one person who always uses everyone else's streaming passwords but never pays for any.*

### ⛷️ **Ski Trip Chaos**
*Lift tickets, lodge fees, and the inevitable "emergency" trip to the ski shop because someone forgot literally everything.*

### 🏖️ **Beach House Rentals**
*When the Airbnb costs more than your car, but everyone still argues about who should pay for the toilet paper.*

### 🎪 **Music Festival Survival**
*Water bottles for $8, questionable food truck meals, and that friend who "totally forgot their wallet" but somehow has money for merch.*

### 👰 **Wedding Planning Committees**
*For bridesmaids who didn't realize they'd need a business degree to split bachelorette party costs.*

### 🏢 **Office Lunch Orders**
*When Dave orders the most expensive thing on the menu and Sarah only gets a side salad, but somehow everyone's supposed to split it evenly.*

### 🎓 **College Group Projects**
*Pizza funds, printing costs, and that one group member who disappears until the day before it's due but still wants equal credit.*

### 🏕️ **Camping Adventures**
*Firewood, s'mores supplies, and discovering that "roughing it" still costs $200 per person somehow.*

### 🎮 **Gaming Convention Trips**
*Hotel rooms, convention passes, and the inevitable "just one more limited edition thing" purchases.*

### 🍽️ **Potluck Coordination**
*When someone always brings a bag of chips but eats like they brought the main course.*

### 👨‍👩‍👧‍👦 **Family Reunion Planning**
*Because someone has to track who paid for what, and it's definitely not going to be Uncle Bob.*

### 🎾 **Sports Team Expenses**
*Equipment, tournament fees, and post-game celebratory/consolatory drinks.*

### 📚 **Book Club Shenanigans**
*Wine, cheese, and the fact that only half the group actually read the book but everyone still shows up for the snacks.*

### 🎂 **Group Gift Coordination**
*When someone suggests "let's all chip in for something nice" and you need to track who actually chipped in.*

### 🛍️ **Group Shopping Trips**
*Costco runs where someone always ends up buying things for everyone and expecting to be reimbursed later.*

### 🍕 **Regular Friend Group Expenses**
*Pizza nights, movie tickets, and the eternal question of "wait, who paid last time?"*

## FAQ (Frequently Asked Questions)

**Q: Is this better than [insert popular expense app]?**  
A: It's a spreadsheet. It works offline, doesn't track your data, and won't suddenly start charging you $9.99/month for "premium features."

**Q: What if someone can't use Excel?**  
A: Google Sheets is free and works in any browser. If they can't figure that out, maybe they shouldn't be handling money.

**Q: Can I customize it?**  
A: It's a spreadsheet! You can customize it until your heart's content. Add more participants, change colors, add your own formulas - go wild.

**Q: What if the math is wrong?**  
A: The math is handled by Excel formulas that are more reliable than your friend who "definitely paid for dinner last time."  Still, if you do encounter a bug in the formulas, submit a bug report or pull request and I'll push a fix.

## Contributing

Found a bug? Have a feature request? Want to add more color themes? 

1. Fork the repo
2. Make your changes
3. Test that your spreadsheet actually works
4. Submit a pull request

Just remember: **With great spreadsheet power comes great responsibility.**

## License

This project is licensed under the CC-BY-SA 4.0 License - see the [LICENSE](license.md) file for details.

Designed and shared for free use by Phil Cigan under a CC-BY-SA 4.0 license.

## Support This Project

If SettleSheet helped you avoid awkward "who owes what" conversations, saved you from spreadsheet-induced migraines, or prevented a friendship from ending over $12.43 in disputed expenses — consider sponsoring. Your support helps fund the essential developer survival kit: coffee for late-night formula debugging, snacks for those "why won't Excel cooperate" moments, and the occasional AI assistant that's surprisingly good at the tasks I've been putting off because I didn't wanna.

No pressure though — this tool is completely free and always will be. But if you're feeling generous after successfully settling your group's chaotic expense situation, I'll definitely send some good financial karma your way (and maybe add that feature you've been thinking about).

[Sponsor me on GitHub](https://github.com/sponsors/pjcigan)

## Acknowledgments

Created by Phil Cigan (2025)

---

*SettleSheet: Because life's too short to argue about who owes $3.47 for coffee.*

**Made with <strike>love</strike> stubbornness and way too much time thinking about optimization.**
