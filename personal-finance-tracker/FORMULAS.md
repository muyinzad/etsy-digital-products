# Personal Finance Tracker - Formulas Reference

Complete formula guide for all tabs.

---

## 📊 DASHBOARD Formulas

### Financial Snapshot

**Total Income (This Month)**
```google_sheets
=SUMIFS('Income Tracker'!E:E, 'Income Tracker'!H:H, TEXT(TODAY(),"MMMM"))
```

**Total Income (YTD)**
```google_sheets
=SUM('Income Tracker'!E:E)
```

**Total Expenses (This Month)**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!I:I, TEXT(TODAY(),"MMMM"))
```

**Total Expenses (YTD)**
```google_sheets
=SUM('Expense Tracker'!E:E)
```

**Net Cash Flow**
```google_sheets
=Total_Income - Total_Expenses
```

**Savings Rate**
```google_sheets
=IF(Total_Income>0, Net_Cash_Flow/Total_Income, 0)
```
Format as Percentage

---

### Savings Progress

**Remaining**
```google_sheets
=Target_Amount - Current_Saved
```

**Progress Bar (using SPARKLINE)**
```google_sheets
=SPARKLINE({Current_Saved,Remaining},{"charttype","bar";"color1","#48bb78";"color2","#e2e8f0";"max",Target_Amount})
```

**Percentage Complete**
```google_sheets
=Current_Saved/Target_Amount
```

**On Track?**
```google_sheets
=IF((Remaining/Months_Left)<=Monthly_Contribution,"✅ Yes","⚠️ No")
```

---

### Debt Payoff Progress

**Paid Off**
```google_sheets
=Original_Balance - Current_Balance
```

**Progress Bar**
```google_sheets
=SPARKLINE({Paid_Off,Current_Balance},{"charttype","bar";"color1","#48bb78";"color2","#f56565";"max",Original_Balance})
```

**Total Debt**
```google_sheets
=SUM(Current_Balance_Column)
```

---

### Net Worth

**Total Assets**
```google_sheets
=SUM(All_Asset_Amounts)
```

**Total Liabilities**
```google_sheets
=SUM(All_Liability_Amounts)
```

**Net Worth**
```google_sheets
=Total_Assets - Total_Liabilities
```

**Change from Last Month**
```google_sheets
=Current_Net_Worth - Previous_Net_Worth
```

---

## 💰 INCOME TRACKER Formulas

### Summary by Category

**Total Amount per Category**
```google_sheets
=SUMIF(D:D, "Salary", E:E)
```

**Count per Category**
```google_sheets
=COUNTIF(D:D, "Salary")
```

**Percentage of Total**
```google_sheets
=IF(Total_Income>0, Category_Amount/Total_Income, 0)
```

---

### Summary by Month

**Monthly Total**
```google_sheets
=SUMIF(H:H, "January", E:E)
```

**Monthly Average**
```google_sheets
=AVERAGEIF(H:H, "January", E:E)
```

---

## 💸 EXPENSE TRACKER Formulas

### Summary by Category

**Total Spent per Category**
```google_sheets
=SUMIF(D:D, "Food", E:E)
```

**Budget Difference**
```google_sheets
=Budget_Amount - Actual_Amount
```

**Percentage of Budget**
```google_sheets
=IF(Budget>0, Actual/Budget, 0)
```

---

### Need vs Want Analysis

**Needs Total**
```google_sheets
=SUMIF(H:H, "Need", E:E)
```

**Wants Total**
```google_sheets
=SUMIF(H:H, "Want", E:E)
```

**Percentage of Expenses**
```google_sheets
=IF(Total_Expenses>0, Needs_Total/Total_Expenses, 0)
```

---

## 📋 BUDGET PLANNER Formulas

### Category Status

**Status Indicator**
```google_sheets
=IF(Actual<=Budget*0.9,"✅ Under Budget",IF(Actual<=Budget,"⚠️ At Risk","❌ Over Budget"))
```

**Percentage Used**
```google_sheets
=IF(Budget>0, Actual/Budget, 0)
```

---

### 50/30/20 Rule Check

**Essentials %**
```google_sheets
=SUM(Essentials_Actual)/Total_Income
```

**Wants %**
```google_sheets
=SUM(Wants_Actual)/Total_Income
```

**Savings/Debt %**
```google_sheets
=SUM(Savings_Debt_Actual)/Total_Income
```

**Status**
```google_sheets
=IF(ABS(Actual_Percent-Target_Percent)<0.05,"OK","Over")
```

---

## 💳 DEBT PAYOFF Formulas

### Payoff Calculations

**Monthly Interest**
```google_sheets
=Balance*(Rate/12)
```

**Principal Payment**
```google_sheets
=Total_Payment - Monthly_Interest
```

**Months to Pay Off**
```google_sheets
=NPER(Rate/12, -Payment, Balance)
```

**Total Interest**
```google_sheets
=Total_Payments - Original_Balance
```

---

### Snowball Order

```google_sheets
=RANK(Balance, All_Balances, 1)
```
(1 = ascending order for smallest first)

---

### Avalanche Order

```google_sheets
=RANK(Interest_Rate, All_Rates, 0)
```
(0 = descending order for highest rate first)

---

### Debt-Free Date

```google_sheets
=EDATE(TODAY(), Months_Until_Debt_Free)
```

---

## 🎯 SAVINGS GOALS Formulas

### Goal Calculations

**Remaining**
```google_sheets
=Target_Amount - Current_Saved
```

**Months Left**
```google_sheets
=DATEDIF(TODAY(), Target_Date, "M")
```

**On Track?**
```google_sheets
=IF(Months_Left>0, IF(Remaining/Months_Left<=Monthly_Contribution, "✅ Yes", "⚠️ No"), "✅ Complete")
```

**Progress Percentage**
```google_sheets
=MIN(Current_Saved/Target_Amount, 1)
```

---

## 📅 BILL TRACKER Formulas

### Days Until Due

```google_sheets
=Due_Date - TODAY()
```

### Monthly Equivalent (for annual bills)

```google_sheets
=IF(Frequency="Annually", Amount/12, IF(Frequency="Quarterly", Amount/3, Amount))
```

---

## 💎 NET WORTH Formulas

### Asset/Liability Calculations

**Subtotal (Cash)**
```google_sheets
=SUM(Cash_Accounts_Range)
```

**Total Assets**
```google_sheets
=SUM(All_Subtotals)
```

**Net Worth**
```google_sheets
=Total_Assets - Total_Liabilities
```

---

### Historical Tracking

**Change**
```google_sheets
=Current_Net_Worth - Previous_Net_Worth
```

---

### Goal Tracking

**Progress Percentage**
```google_sheets
=Current_Net_Worth/Target_Net_Worth
```

**Required Monthly Growth**
```google_sheets
=(Target_Net_Worth-Current_Net_Worth)/Months_To_Goal
```

---

## 📺 SUBSCRIPTION TRACKER Formulas

### Cost Calculations

**Annual Cost (Monthly subscription)**
```google_sheets
=Monthly_Cost*12
```

**Monthly Equivalent (Annual subscription)**
```google_sheets
=Annual_Cost/12
```

---

### Cancel Recommendations

**Not Used in 30 Days**
```google_sheets
=IF(Used_Last_30_Days="No", "❌ Cancel", "✅ Keep")
```

---

### Category Totals

**Monthly Total by Category**
```google_sheets
=SUMIF(Category_Column, "Streaming", Monthly_Cost_Column)
```

**Annual Total by Category**
```google_sheets
=SUMIF(Category_Column, "Streaming", Annual_Cost_Column)
```

---

### Potential Savings

```google_sheets
=SUMIFS(Annual_Cost, Keep, "❌ Cancel")
```

---

## 🔧 HELPER FORMULAS

### Month Extraction

```google_sheets
=IF(Date_Cell<>"", TEXT(Date_Cell, "MMMM"), "")
```

### Year Extraction

```google_sheets
=IF(Date_Cell<>"", YEAR(Date_Cell), "")
```

### Progress Bar (Visual)

```google_sheets
=REPT("█", ROUND(Progress*20)) & REPT("░", 20-ROUND(Progress*20))
```

---

## 🎨 CONDITIONAL FORMATTING RULES

### Budget Status
- ✅ Green: Actual ≤ 90% of Budget
- ⚠️ Yellow: 90% < Actual ≤ 100%
- ❌ Red: Actual > 100%

### Net Worth Change
- Green: Positive change
- Red: Negative change

### Bill Status
- ✅ Green: Paid
- ⬜ Gray: Unpaid
- ❌ Red: Overdue

### Savings Goal Progress
- Red: <25%
- Orange: 25-50%
- Yellow: 50-75%
- Green: >75%

---

## 📝 DATA VALIDATION (Dropdowns)

### Categories
- Income: Settings!A5:A14
- Expense: Settings!A20:A35

### Need/Want
- List: "Need,Want"

### Frequency
- List: "Monthly,Annually,Quarterly,Bi-Annually,Weekly,Bi-Weekly"

### Status
- Bills: "✅ Paid,⬜ Unpaid,⏳ Pending,❌ Overdue"
- Subscriptions: "Active,Paused,Cancelled"

---

End of Formulas Reference
