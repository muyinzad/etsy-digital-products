# Business Finance Dashboard - Formulas Reference

Complete formula guide for all tabs. Copy these into your Google Sheets.

---

## 📊 DASHBOARD Formulas

### Key Metrics Section

**Total Income (This Month)**
```google_sheets
=SUMIFS('Income Tracker'!F:F, 'Income Tracker'!I:I, MONTH(TODAY()))
```

**Total Income (YTD)**
```google_sheets
=SUM('Income Tracker'!F:F)
```

**Total Expenses (This Month)**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!I:I, MONTH(TODAY()))
```

**Total Expenses (YTD)**
```google_sheets
=SUM('Expense Tracker'!E:E)
```

**Net Profit (This Month)**
```google_sheets
=Total_Income_This_Month - Total_Expenses_This_Month
```

**Net Profit (YTD)**
```google_sheets
=Total_Income_YTD - Total_Expenses_YTD
```

**Profit Margin (This Month)**
```google_sheets
=IF(Total_Income_This_Month>0, Net_Profit_This_Month/Total_Income_This_Month, 0)
```
Format as Percentage

**Profit Margin (YTD)**
```google_sheets
=IF(Total_Income_YTD>0, Net_Profit_YTD/Total_Income_YTD, 0)
```
Format as Percentage

**Open Invoices**
```google_sheets
=SUMIFS('Income Tracker'!F:F, 'Income Tracker'!H:H, "Pending")
```

**Cash on Hand**
```google_sheets
=Starting_Balance + Net_Profit_YTD
```
(Enter starting balance in Settings)

---

### Income by Category

**Category Amount**
```google_sheets
=SUMIF('Income Tracker'!E:E, A16, 'Income Tracker'!F:F)
```
(A16 = category name cell)

**Category Percentage**
```google_sheets
=IF(Total_Income>0, Category_Amount/Total_Income, 0)
```

---

### Top Expense Categories

**Category Amount**
```google_sheets
=SUMIF('Expense Tracker'!D:D, F16, 'Expense Tracker'!E:E)
```
(F16 = category name cell)

**Category Percentage**
```google_sheets
=IF(Total_Expenses>0, Category_Amount/Total_Expenses, 0)
```

---

### Monthly Trend

**Monthly Income**
```google_sheets
=SUMIFS('Income Tracker'!F:F, 'Income Tracker'!I:I, 1)
```
(1 = January, 2 = February, etc.)

**Monthly Expenses**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!I:I, 1)
```

**Monthly Profit**
```google_sheets
=Monthly_Income - Monthly_Expenses
```

---

### Cash Flow Status (Next 30 Days)

**Expected Income**
```google_sheets
=SUMIFS('Cash Flow Projection'!B5:M5, 'Cash Flow Projection'!B3:M3, ">="&TODAY(), 'Cash Flow Projection'!B3:M3, "<="&TODAY()+30)
```

**Expected Expenses**
```google_sheets
=SUMIFS('Cash Flow Projection'!B19:M19, 'Cash Flow Projection'!B3:M3, ">="&TODAY(), 'Cash Flow Projection'!B3:M3, "<="&TODAY()+30)
```

**Projected Cash Flow**
```google_sheets
=Expected_Income - Expected_Expenses
```

---

## 💰 INCOME TRACKER Formulas

### Summary by Category

**Total Amount per Category**
```google_sheets
=SUMIF(E:E, "Services", F:F)
```
(Replace "Services" with each category name)

**Number of Transactions per Category**
```google_sheets
=COUNTIF(E:E, "Services")
```

**Total Income**
```google_sheets
=SUM(F:F)
```

**Total Transactions**
```google_sheets
=COUNTA(F:F)-1
```
(-1 to exclude header)

---

### Summary by Month

**Monthly Total**
```google_sheets
=SUMIF(I:I, "January", F:F)
```
(Replace "January" with each month)

**Monthly Transaction Count**
```google_sheets
=COUNTIF(I:I, "January")
```

---

### Status Breakdown

**Received Amount**
```google_sheets
=SUMIF(H:H, "Received", F:F)
```

**Pending Amount**
```google_sheets
=SUMIF(H:H, "Pending", F:F)
```

**Overdue Amount**
```google_sheets
=SUMIF(H:H, "Overdue", F:F)
```

---

## 💸 EXPENSE TRACKER Formulas

### Summary by Category

**Total Amount per Category**
```google_sheets
=SUMIF(D:D, "Software", E:E)
```

**Percentage of Total**
```google_sheets
=IF(Total_Expenses>0, Category_Amount/Total_Expenses, 0)
```

**Tax Deductible Amount**
```google_sheets
=SUMIFS(E:E, D:D, "Software", G:G, "Yes")
```

**Total Expenses**
```google_sheets
=SUM(E:E)
```

---

### Tax Deduction Summary

**Total Tax Deductible**
```google_sheets
=SUMIF(G:G, "Yes", E:E)
```

**Total Non-Deductible**
```google_sheets
=SUMIF(G:G, "No", E:E)
```

**Percentage Deductible**
```google_sheets
=IF(Total_Expenses>0, Total_Tax_Deductible/Total_Expenses, 0)
```

---

## 📄 INVOICE GENERATOR Formulas

### Line Items

**Amount (Quantity × Rate)**
```google_sheets
=Quantity_Cell * Rate_Cell
```
Example: `=E15*F15`

**Subtotal**
```google_sheets
=SUM(G15:G22)
```
(Range of all line item amounts)

**Discount Amount**
```google_sheets
=IF(Discount_Type="Percentage", Subtotal*(Discount_Rate/100), Discount_Amount)
```

**Tax Amount**
```google_sheets
=(Subtotal-Discount_Amount)*(Tax_Rate/100)
```

**Total Due**
```google_sheets
=Subtotal - Discount_Amount + Tax_Amount
```

---

### Invoice Number Auto-Generate

**Next Invoice Number**
```google_sheets
="INV-"&TEXT(COUNTA(Invoice_History_Range)+1, "000")
```

---

## 👥 CLIENT DATABASE Formulas

### Statistics

**Total Clients**
```google_sheets
=COUNTA(A:A)-1
```

**Active Clients (with transactions)**
```google_sheets
=COUNTUNIQUE('Income Tracker'!C:C)-1
```

---

### Payment Terms Breakdown

**Count per Term**
```google_sheets
=COUNTIF(J:J, "Net 30")
```

---

### Client Revenue Summary

**Total Revenue per Client**
```google_sheets
=SUMIF('Income Tracker'!C:C, Client_Name, 'Income Tracker'!F:F)
```

**Number of Projects**
```google_sheets
=COUNTIF('Income Tracker'!C:C, Client_Name)
```

**Average Project Value**
```google_sheets
=IF(Num_Projects>0, Total_Revenue/Num_Projects, 0)
```

**Last Project Date**
```google_sheets
=MAXIFS('Income Tracker'!A:A, 'Income Tracker'!C:C, Client_Name)
```

---

## 🧾 TAX DEDUCTIONS Formulas

### Deductions by Category

**Total per Category**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!D:D, "Software", 'Expense Tracker'!G:G, "Yes")
```

**Percentage of Total**
```google_sheets
=IF(Total_Deductions>0, Category_Amount/Total_Deductions, 0)
```

---

### Quarterly Summary

**Q1 (Jan-Mar)**
```google_sheets
=SUMIFS('Expense Tracker'!E:E, 'Expense Tracker'!G:G, "Yes", 'Expense Tracker'!I:I, ">=1", 'Expense Tracker'!I:I, "<=3")
```

**Estimated Tax Savings (25% bracket)**
```google_sheets
=Quarterly_Deductions * 0.25
```

---

### Home Office Deduction

**Business Use Percentage**
```google_sheets
=Business_Sq_Ft/Total_Home_Sq_Ft
```

**Home Office Deduction**
```google_sheets
=Total_Home_Expenses * Business_Use_Percentage
```

---

## 💵 CASH FLOW PROJECTION Formulas

### Opening Balance

**First Month**
```google_sheets
=Starting_Bank_Balance
```

**Subsequent Months**
```google_sheets
=Previous_Month_Closing_Balance
```

---

### Cash Flow Calculations

**Net Cash Flow**
```google_sheets
=Total_Cash_In - Total_Cash_Out
```

**Closing Balance**
```google_sheets
=Opening_Balance + Net_Cash_Flow
```

---

### Status Indicator (Conditional Formatting Rule)

Apply to Status row:
- If Closing Balance > 0 → "Positive" (green)
- If Closing Balance < 0 → "Negative" (red)

Formula:
```google_sheets
=IF(Closing_Balance>=0, "Positive", "Negative")
```

---

### Scenario Analysis

**If Income +10%**
```google_sheets
=Year_End_Balance + (Total_Income * 0.10)
```

**If Expenses -10%**
```google_sheets
=Year_End_Balance + (Total_Expenses * 0.10)
```

**Worst Month Impact**
```google_sheets
=MIN(Net_Cash_Flow_Range)
```

---

## ⚙️ SETTINGS Formulas

No formulas needed - this is a data entry tab.

---

## 🔧 HELPER COLUMNS (Hidden)

### Month Extraction

In Income/Expense trackers, add a hidden column for month number:

```google_sheets
=IF(A2<>"", MONTH(A2), "")
```

---

### Year Extraction

```google_sheets
=IF(A2<>"", YEAR(A2), "")
```

---

## 📝 CONDITIONAL FORMATTING RULES

### Profit Margin (Dashboard)
- Green: > 30%
- Yellow: 15-30%
- Red: < 15%

### Cash Flow Status
- Green: Positive
- Red: Negative

### Invoice Status
- Green: "Received"
- Yellow: "Pending"
- Red: "Overdue"

### Profit/Loss
- Green: Positive numbers
- Red: Negative numbers (use red text or red background)

---

## 🎨 DATA VALIDATION (Dropdowns)

### Income Categories
Data validation → List from range → Settings!A16:A25

### Expense Categories
Data validation → List from range → Settings!A30:A45

### Payment Methods
Data validation → List from range → Settings!A50:A60

### Payment Terms
Data validation → List from range → Settings!A65:A70

### Status
Data validation → List → "Received,Pending,Overdue,Cancelled"

### Tax Deductible
Data validation → List → "Yes,No"

---

## 📌 NOTES

1. **Named Ranges** - Consider creating named ranges for key cells to make formulas easier to read
2. **Absolute References** - Use $A$1 format when referencing fixed cells
3. **Error Handling** - Wrap division formulas in IFERROR() to avoid #DIV/0! errors
4. **Array Formulas** - Some formulas may need ARRAYFORMULA() wrapper in Google Sheets

---

## 🔄 AUTO-UPDATE TRIGGERS

For automatic updates, consider:
- Using IMPORTRANGE() for multi-sheet dashboards
- Setting up Google Apps Script for automated reports
- Using QUERY() function for dynamic data analysis

Example QUERY:
```google_sheets
=QUERY('Income Tracker'!A:I, "SELECT E, SUM(F) GROUP BY E ORDER BY SUM(F) DESC")
```

---

End of Formulas Reference
