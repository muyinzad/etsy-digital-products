# Personal Finance Tracker - Formulas Reference

Complete formula guide for all tabs. Copy these into your Google Sheets.

---

## 📊 DASHBOARD Formulas

### Key Metrics (This Month)

**Total Income (This Month)**
```google_sheets
=SUMIFS('Income Tracker'!E:E, 'Income Tracker'!H:H, TEXT(TODAY(),"MMMM"))
```

**Total Expenses (This Month)**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!I:I, TEXT(TODAY(),"MMMM"))
```

**Net Cash Flow (This Month)**
```google_sheets
=Total_Income_This_Month - Total_Expenses_This_Month
```

**Savings Rate (This Month)**
```google_sheets
=IF(Total_Income>0, Net_Cash_Flow/Total_Income, 0)
```
Format as Percentage

---

### Key Metrics (YTD)

**Total Income (YTD)**
```google_sheets
=SUM('Income Tracker'!E:E)
```

**Total Expenses (YTD)**
```google_sheets
=SUM('Expense Tracker'!E:E)
```

**Net Cash Flow (YTD)**
```google_sheets
=Total_Income_YTD - Total_Expenses_YTD
```

**Savings Rate (YTD)**
```google_sheets
=IF(Total_Income_YTD>0, Net_Cash_Flow_YTD/Total_Income_YTD, 0)
```

---

### Savings Progress

**Current Amount per Goal**
```google_sheets
=SUMIF('Savings Goals'!A:A, "Emergency Fund", 'Savings Goals'!C:C)
```

**Percentage Complete**
```google_sheets
=IF(Target>0, Current/Target, 0)
```

**Progress Bar (using REPT function)**
```google_sheets
=REPT("█", ROUND(Percentage*20))&REPT("░", 20-ROUND(Percentage*20))
```

---

### Debt Payoff Progress

**Current Debt per Item**
```google_sheets
=VLOOKUP("Credit Card 1", 'Debt Payoff'!A:G, 2, FALSE)
```

**Paid Off Amount**
```google_sheets
=Original_Balance - Current_Balance
```

**Total Debt**
```google_sheets
=SUM('Debt Payoff'!B:B)
```

---

### Net Worth

**Total Assets**
```google_sheets
=SUM('Net Worth'!B:B)
```

**Total Liabilities**
```google_sheets
=SUM('Net Worth'!E:E)
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

### Spending by Category

**Budget**
```google_sheets
=VLOOKUP(Category, 'Budget Planner'!A:D, 2, FALSE)
```

**Actual**
```google_sheets
=SUMIF('Expense Tracker'!D:D, Category, 'Expense Tracker'!E:E)
```

**Difference**
```google_sheets
=Budget - Actual
```

**% of Budget**
```google_sheets
=IF(Budget>0, Actual/Budget, 0)
```

---

### Monthly Trend

**Monthly Income**
```google_sheets
=SUMIFS('Income Tracker'!E:E, 'Income Tracker'!H:H, "January")
```

**Monthly Expenses**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!I:I, "January")
```

**Net Flow**
```google_sheets
=Monthly_Income - Monthly_Expenses
```

**Savings Rate**
```google_sheets
=IF(Monthly_Income>0, Net_Flow/Monthly_Income, 0)
```

---

## 💰 INCOME TRACKER Formulas

### Summary by Category

**Total per Category**
```google_sheets
=SUMIF(D:D, "Salary", E:E)
```

**Count per Category**
```google_sheets
=COUNTIF(D:D, "Salary")
```

**% of Total**
```google_sheets
=IF(Total_Income>0, Category_Total/Total_Income, 0)
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

### Recurring Income

**Monthly Amount**
```google_sheets
=SUMIFS(E:E, F:F, "Yes")
```

**Annual Amount**
```google_sheets
=Monthly_Amount * 12
```

---

## 💸 EXPENSE TRACKER Formulas

### Summary by Category

**Total Spent**
```google_sheets
=SUMIF(D:D, "Food", E:E)
```

**Count**
```google_sheets
=COUNTIF(D:D, "Food")
```

**Difference from Budget**
```google_sheets
=Budget - Actual
```

**% of Budget**
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

**% of Expenses**
```google_sheets
=IF(Total_Expenses>0, Category_Total/Total_Expenses, 0)
```

---

## 📋 BUDGET PLANNER Formulas

### Actual Spending (auto-pulls from Expense Tracker)

**Actual per Category**
```google_sheets
=SUMIF('Expense Tracker'!D:D, "Housing", 'Expense Tracker'!E:E)
```

---

### Difference

**Difference**
```google_sheets
=Budget - Actual
```

**Status**
```google_sheets
=IF(Difference>=0, "✅ Under Budget", IF(Difference>=-50, "⚠️ At Risk", "❌ Over Budget"))
```

**% Used**
```google_sheets
=IF(Budget>0, Actual/Budget, 0)
```

---

### Budget Rule Check

**Essentials %**
```google_sheets
=IF(Total_Budget>0, Sum_Of_Essentials/Total_Budget, 0)
```

**Wants %**
```google_sheets
=IF(Total_Budget>0, Sum_Of_Wants/Total_Budget, 0)
```

**Savings/Debt %**
```google_sheets
=IF(Total_Budget>0, Sum_Of_Savings_Debt/Total_Budget, 0)
```

---

## 💳 DEBT PAYOFF CALCULATOR Formulas

### Total Payment

**Total Payment per Debt**
```google_sheets
=Min_Payment + Extra_Payment
```

---

### Payoff Comparison

These require complex calculations. For simplicity, use online debt payoff calculators and enter results, or use Google Sheets' NPER function:

**Months to Pay Off (Minimum Only)**
```google_sheets
=NPER(Interest_Rate/12, -Min_Payment, Balance, 0)
```

**Total Interest**
```google_sheets
=(Months * Min_Payment) - Original_Balance
```

---

### Progress Tracker

**Paid Off**
```google_sheets
=Starting_Debt - Current_Debt
```

**Progress Bar**
```google_sheets
=REPT("█", ROUND((Paid_Off/Starting_Debt)*20))&REPT("░", 20-ROUND((Paid_Off/Starting_Debt)*20))
```

---

## 🎯 SAVINGS GOALS Formulas

### Progress Calculation

**Remaining**
```google_sheets
=Target - Current
```

**Percentage Complete**
```google_sheets
=IF(Target>0, Current/Target, 0)
```

**Progress Bar**
```google_sheets
=REPT("█", ROUND(Percentage*20))&REPT("░", 20-ROUND(Percentage*20))
```

---

### On Track Status

**Months Until Target**
```google_sheets
=DATEDIF(TODAY(), Target_Date, "M")
```

**Required Monthly Savings**
```google_sheets
=IF(Months_Until>0, Remaining/Months_Until, Remaining)
```

**On Track?**
```google_sheets
=IF(Monthly_Contribution>=Required_Monthly, "✅ Yes", "⚠️ At Risk")
```

---

### Estimated Completion

**Months to Complete**
```google_sheets
=IF(Monthly_Contribution>0, CEILING(Remaining/Monthly_Contribution), "N/A")
```

**Estimated Date**
```google_sheets
=EDATE(TODAY(), Months_to_Complete)
```

---

## 📅 BILL TRACKER Formulas

### Days Until Due

**Days Until Due**
```google_sheets
=Due_Date - TODAY()
```

---

### Bills Due This Week

Filter bills where Days Until Due <= 7 and > 0

```google_sheets
=FILTER(A:H, (G:G<=7)*(G:G>0))
```

---

### Monthly Totals

**Sum of Monthly Bills**
```google_sheets
=SUMIF(C:C, "Monthly", B:B)
```

**Sum of Annual Bills (Monthly Equivalent)**
```google_sheets
=SUMIF(C:C, "Annual", B:B)/12
```

---

## 💵 NET WORTH CALCULATOR Formulas

### Subtotals

**Cash Subtotal**
```google_sheets
=SUM(B5:B8)
```

**Investments Subtotal**
```google_sheets
=SUM(B12:B16)
```

**Real Estate Subtotal**
```google_sheets
=SUM(B20:B22)
```

---

### Total Assets

**Total Assets**
```google_sheets
=SUM(All_Subtotals)
```

---

### Total Liabilities

**Total Liabilities**
```google_sheets
=SUM(All_Liabilities)
```

---

### Net Worth

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

**% Change**
```google_sheets
=IF(Previous_Net_Worth<>0, Change/ABS(Previous_Net_Worth), 0)
```

---

## 📺 SUBSCRIPTION TRACKER Formulas

### Monthly vs Annual Cost

**Annual Cost (from Monthly)**
```google_sheets
=Monthly_Cost * 12
```

**Monthly Cost (from Annual)**
```google_sheets
=Annual_Cost / 12
```

---

### Category Totals

**Total per Category**
```google_sheets
=SUMIF(B:B, "Entertainment", D:D)
```

**Count per Category**
```google_sheets
=COUNTIF(B:B, "Entertainment")
```

---

### Potential Savings

**Sum of Cancel Recommendations**
```google_sheets
=SUMIF(J:J, "❌ Cancel", D:D)
```

---

### Shared Subscription Savings

**Your Share**
```google_sheets
=Total_Cost / Number_of_People
```

**You Save**
```google_sheets
=Total_Cost - Your_Share
```

---

## 🔧 HELPER COLUMNS

### Month Extraction

```google_sheets
=IF(A2<>"", TEXT(A2, "MMMM"), "")
```

### Year Extraction

```google_sheets
=IF(A2<>"", YEAR(A2), "")
```

---

## 📝 CONDITIONAL FORMATTING RULES

### Budget Status
- Green: Under Budget (Difference >= 0)
- Yellow: At Risk (Difference between -50 and 0)
- Red: Over Budget (Difference < -50)

### Progress Bars
- Use data bars or REPT function for visual progress

### Net Worth
- Green: Positive
- Red: Negative

### Savings Rate
- Green: >= 20%
- Yellow: 10-20%
- Red: < 10%

---

## 📌 DATA VALIDATION

### Income Categories
Data validation → List from range → Settings!A21:A29

### Expense Categories
Data validation → List from range → Settings!A33:A47

### Payment Methods
Data validation → List from range → Settings!A51:A59

### Need/Want
Data validation → List → "Need,Want"

### Status
Data validation → List → "✅ Paid,⬜ Unpaid,⏸️ Skipped"

### Keep/Cancel
Data validation → List → "✅ Keep,⚠️ Review,❌ Cancel"

---

End of Formulas Reference
