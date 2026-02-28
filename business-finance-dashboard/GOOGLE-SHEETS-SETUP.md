# Business Finance Dashboard - Google Sheets Setup Guide

Follow these steps to build the complete template in Google Sheets.

---

## 🚀 Step-by-Step Setup (30 minutes)

### STEP 1: Create the Spreadsheet

1. Go to [sheets.google.com](https://sheets.google.com)
2. Click **+ Blank spreadsheet**
3. Rename to **Business Finance Dashboard Template**

---

### STEP 2: Create All Tabs

Create 9 tabs (click + at bottom left):

1. **Dashboard**
2. **Income Tracker**
3. **Expense Tracker**
4. **Invoice Generator**
5. **Client Database**
6. **Tax Deductions**
7. **Cash Flow Projection**
8. **Settings**
9. **Instructions**

---

### STEP 3: Build the Settings Tab (Start Here)

This tab controls all dropdowns. Build it first!

**Row 3-12: Business Information**
```
A3: Business Name:          | B3: [Your Business Name]
A4: Owner Name:             | B4: [Your Name]
A5: Business Address:       | B5: [Address]
A6: City:                   | B6: [City]
A7: State/Province:         | B7: [State]
A8: ZIP/Postal Code:        | B8: [ZIP]
A9: Country:                | B9: [Country]
A10: Phone:                 | B10: [Phone]
A11: Email:                 | B11: [Email]
A12: Tax ID:                | B12: [Tax ID]
```

**Row 15-18: Financial Settings**
```
A15: Currency Symbol:       | B15: $
A16: Currency Name:         | B16: USD
A17: Tax Year Start:        | B17: January
A18: Default Tax Rate:      | B18: 25%
```

**Row 21-30: Income Categories (Column A)**
```
A21: Services
A22: Consulting
A23: Design
A24: Retainer
A25: Product Sales
A26: Affiliate
A27: Commission
A28: Licensing
A29: Subscription
A30: Other
```

**Row 33-47: Expense Categories (Column A)**
```
A33: Software
A34: Office Supplies
A35: Travel
A36: Meals
A37: Equipment
A38: Contractors
A39: Marketing
A40: Insurance
A41: Utilities
A42: Rent
A43: Professional Services
A44: Education
A45: Banking Fees
A46: Shipping
A47: Other
```

**Row 50-59: Payment Methods (Column A)**
```
A50: Bank Transfer
A51: PayPal
A52: Credit Card
A53: Debit Card
A54: Cash
A55: Check
A56: Venmo
A57: Stripe
A58: Wise
A59: Other
```

**Row 62-66: Payment Terms (Column A)**
```
A62: Due on Receipt
A63: Net 15
A64: Net 30
A65: Net 60
A66: Custom
```

---

### STEP 4: Build Income Tracker

**Header Row (Row 1):**
```
A1: Date
B1: Invoice #
C1: Client Name
D1: Project/Description
E1: Category
F1: Amount
G1: Payment Method
H1: Status
I1: Month
J1: Notes
```

**Data Validation (Dropdowns):**
- Column E (Category): Data → Validation → List from range → Settings!A21:A30
- Column G (Payment Method): Data → Validation → List from range → Settings!A50:A59
- Column H (Status): Data → Validation → List of items → "Received,Pending,Overdue,Cancelled"

**Month Auto-Calculation (Cell I2 and down):**
```
=IF(A2<>"", TEXT(A2, "MMMM"), "")
```

**Summary Section (Below data, starting Row 50):**

Row 52: **SUMMARY BY CATEGORY**
```
A54: Services          | B54: =SUMIF(E:E,"Services",F:F)
A55: Consulting        | B55: =SUMIF(E:E,"Consulting",F:F)
A56: Design            | B56: =SUMIF(E:E,"Design",F:F)
... (repeat for each category)

A65: TOTAL INCOME      | B65: =SUM(F2:F49)
```

---

### STEP 5: Build Expense Tracker

**Header Row (Row 1):**
```
A1: Date
B1: Vendor/Store
C1: Description
D1: Category
E1: Amount
F1: Payment Method
G1: Tax Deductible
H1: Receipt?
I1: Month
J1: Reimbursable?
K1: Notes
```

**Data Validation:**
- Column D (Category): Settings!A33:A47
- Column F (Payment Method): Settings!A50:A59
- Column G (Tax Deductible): List → "Yes,No"
- Column H (Receipt?): List → "Yes,No,Digital"
- Column J (Reimbursable?): List → "Yes,No"

**Month Auto-Calculation:**
```
=IF(A2<>"", TEXT(A2, "MMMM"), "")
```

**Summary Section:**
```
Total Expenses: =SUM(E2:E49)
Tax Deductible Total: =SUMIF(G:G,"Yes",E:E)
```

---

### STEP 6: Build Client Database

**Header Row (Row 1):**
```
A1: Client Name
B1: Contact Person
C1: Email
D1: Phone
E1: Address
F1: City
G1: State
H1: ZIP
I1: Country
J1: Payment Terms
K1: Notes
```

**Data Validation:**
- Column J (Payment Terms): Settings!A62:A66

---

### STEP 7: Build Invoice Generator

**Section 1: Invoice Header (Rows 1-10)**
```
A1: INVOICE (merge A1:E1, make big and bold)

A3: FROM:                    | E3: TO:
A4: [Your Business Name]     | E4: [Client dropdown]
A5: [Address]                | E5: [Client address - VLOOKUP]
A6: [City, State ZIP]        | E6: [Client city - VLOOKUP]
A7: [Phone]                  | E7: [Client phone - VLOOKUP]
A8: [Email]                  | E8: [Client email - VLOOKUP]

A10: Invoice Number:         | B10: INV-001
C10: Invoice Date:           | D10: [date picker]
A11: Due Date:               | B11: [date picker]
C11: Payment Terms:          | D11: [dropdown]
```

**Client Auto-Fill Formulas:**
```
E4: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,1,FALSE),"")
E5: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,5,FALSE),"")
E6: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,6,FALSE)&", "&VLOOKUP(E4,'Client Database'!A:K,7,FALSE)&" "&VLOOKUP(E4,'Client Database'!A:K,8,FALSE),"")
E7: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,4,FALSE),"")
E8: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,3,FALSE),"")
D11: =IFERROR(VLOOKUP(E4,'Client Database'!A:K,10,FALSE),"Net 30")
```

**Section 2: Line Items (Rows 14-25)**
```
A14: Description             | D14: Qty | E14: Rate | F14: Amount

A15: [Description]           | D15: 1   | E15: 0    | F15: =D15*E15
A16: [Description]           | D16: 1   | E16: 0    | F16: =D16*E16
... repeat rows 17-22

A25:                         |          | Subtotal: | F25: =SUM(F15:F22)
A26:                         |          | Discount: | F26: [enter amount]
A27:                         |          | Tax (%):  | F27: [enter %]
A28:                         |          | Tax Amt:  | F28: =(F25-F26)*(F27/100)
A29:                         |          | TOTAL:    | F29: =F25-F26+F28
```

---

### STEP 8: Build Tax Deductions

This tab auto-pulls from Expense Tracker using QUERY or FILTER.

**Simple approach - manual copy or use:**
```
=FILTER('Expense Tracker'!A:K, 'Expense Tracker'!G:G="Yes")
```

**Summary by Category:**
```
=QUERY('Expense Tracker'!A:K, "SELECT D, SUM(E) WHERE G='Yes' GROUP BY D ORDER BY SUM(E) DESC")
```

---

### STEP 9: Build Cash Flow Projection

**Row 1:** Title
**Row 3:** Month names (Jan-Dec across columns B-M)

**Row 5: Opening Balance**
- B5: =[Starting Balance from Settings]
- C5: =B15 (previous month's closing)

**Row 6-9: Cash In Categories**
```
A6: Retainer Income      | B6: [enter] | C6: [enter] | ...
A7: Project Income       | B7: [enter] | C7: [enter] | ...
A8: Product Sales        | B8: [enter] | C8: [enter] | ...
A9: Other Income         | B9: [enter] | C9: [enter] | ...
```

**Row 10: Total Cash In**
```
B10: =SUM(B6:B9)
```

**Row 12-20: Cash Out Categories**
```
A12: Software            | B12: [enter] | ...
A13: Marketing           | B13: [enter] | ...
... etc.
```

**Row 21: Total Cash Out**
```
B21: =SUM(B12:B20)
```

**Row 23: Net Cash Flow**
```
B23: =B10-B21
```

**Row 25: Closing Balance**
```
B25: =B5+B23
```

---

### STEP 10: Build Dashboard

**Key Metrics Section:**
```
A3: Total Income (This Month)  | B3: =SUMIFS('Income Tracker'!F:F,'Income Tracker'!I:I,TEXT(TODAY(),"MMMM"))
A4: Total Expenses (This Month)| B4: =SUMIFS('Expense Tracker'!E:E,'Expense Tracker'!I:I,TEXT(TODAY(),"MMMM"))
A5: Net Profit (This Month)    | B5: =B3-B4
A6: Profit Margin              | B6: =IF(B3>0,B5/B3,0) [format as %]

A8: Total Income (YTD)         | B8: =SUM('Income Tracker'!F:F)
A9: Total Expenses (YTD)       | B9: =SUM('Expense Tracker'!E:E)
A10: Net Profit (YTD)          | B10: =B8-B9
A11: Profit Margin (YTD)       | B11: =IF(B8>0,B10/B8,0) [format as %]
```

**Income by Category (use QUERY):**
```
=QUERY('Income Tracker'!E:F, "SELECT E, SUM(F) WHERE E IS NOT NULL GROUP BY E ORDER BY SUM(F) DESC LIMIT 5")
```

**Monthly Trend:**
```
=QUERY('Income Tracker'!I:F, "SELECT I, SUM(F) WHERE I IS NOT NULL GROUP BY I PIVOT I")
```

---

### STEP 11: Build Instructions Tab

Copy the content from `09-instructions.csv` - it's already written!

---

### STEP 12: Add Formatting

**Color Scheme:**
- Headers: Dark blue (#1a365d) with white text
- Income/Green: #48bb78
- Expenses/Red: #f56565
- Neutral: #e2e8f0
- Accent: #3182ce

**Conditional Formatting:**
1. Profit margin: Red if <15%, Yellow if 15-30%, Green if >30%
2. Negative numbers: Red text
3. Status column: Green="Received", Yellow="Pending", Red="Overdue"

**Freeze Rows:**
- Freeze row 1 on all tabs with headers

**Protect Formulas:**
- Select formula cells → Data → Protect sheets and ranges

---

### STEP 13: Test with Sample Data

Enter 5-10 sample transactions in Income and Expense trackers. Verify:
- [ ] Dashboard updates correctly
- [ ] Categories sum properly
- [ ] Monthly trend shows data
- [ ] Invoice generator works
- [ ] Tax deductions filter correctly

---

### STEP 14: Create Template Link

1. File → Share → Get link
2. Change to "Anyone with the link can view"
3. Copy link
4. Test by opening in incognito window

**For Etsy delivery:**
"Click this link to make your own copy: [URL]&copy=true"

---

## ✅ Completion Checklist

- [ ] All 9 tabs created
- [ ] Settings tab populated
- [ ] All dropdowns working
- [ ] Formulas calculating correctly
- [ ] Conditional formatting applied
- [ ] Sample data tested
- [ ] Template link created
- [ ] Preview screenshots taken (5-10 images)
- [ ] Ready for Etsy listing!

---

## 📸 Screenshot Checklist

Take screenshots of:
1. Dashboard (full view)
2. Income Tracker with sample data
3. Expense Tracker with sample data
4. Invoice Generator (filled out)
5. Monthly trend chart
6. Settings page
7. Instructions page
8. Mobile view (if responsive)

---

You're ready to sell! 🎉
