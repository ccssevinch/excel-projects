<h1>Purpose</h1>

This Excel-based Payroll Tracker simulates core HRIS functionality and automates payroll operations using nested formulas, dynamic tables, and macro-driven dashboards.
This Markdown document explains all formulas used in the Payroll Tracker Excel file, covering their purpose, logic, dependencies, and where they are located. This is designed to help users, and reviewers understand the inner workings of each sheet, cell, and calculation, and to ensure easy scalability and maintenance for future updates.

I will first explain the standard formula that I have used in my project, then a refactored version with LET():

### Formula used to calculate the Gross_Pay (Hourly & Salaried Employees):

```excel 
=IF(
  XLOOKUP(B2, EmployeeTable[Employee_ID]), EmployeeTable[Pay_Type]) = "Hourly",
  E2 * XLOOKUP(B2, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate]),
  XLOOKUP(B2, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate])
)
```

### Context:

Let's assume that you're on the Payroll_Log sheet, and you want to calculate Gross_Pay using:

B2 → Employee_ID (used to look up info in EmployeeTable)

E2 → Hours_Worked

Pay_Type → Either "Hourly" or "Salary"

Pay_Rate → Either the hourly rate or fixed salary per period

### Explaining line by line:

```excel
XLOOKUP(B2, EmployeeTable[Employee_ID], EmployeeTable[Pay_Type])

This looks up the Pay_Type (Hourly or Salary) of the employee whose ID is in cell B2.
If the result = "Hourly", the employee is paid by the hour.
```
### Then the formula becomes:

```excel
= IF(
  Pay_Type = "Hourly",
  E2 * Pay_Rate,
  Pay_Rate
)
```
If the employee is Hourly: Multiply Hours_Worked (E2) × Pay_Rate

If the employee is Salary: Just return Pay_Rate (assuming this is per pay period)


### Using LET():

```excel
=LET(
    empID, B2,
    hoursWorked, E2,
    payType, XLOOKUP(empID, EmployeeTable[Employee_ID], EmployeeTable[Pay_Type]),
    payRate, XLOOKUP(empID, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate]),
    IF(payType = "Hourly", hoursWorked * payRate, payRate)
)
```

### Total_Deductions:

The following are the columns inside of the Deductions Sheet:

```excel
A -> Employee_ID
B -> Pay_Period_End 
C -> Health_Insurance
D -> Retirememt_401(k)
E -> Other
F -> Total_Deductions
```

### Formula used to calculate Total_deductions:

```excel
= C2 + D2 + E2
```
### What It Does:

Adds the Health Insurance, 401(k) Retirement, and Other deductions for the current row (row2).

This gives the total amount deducted for this pay period for this employee.


### Using LET():

```excel
= LET (
  health, C2,
  retirement, D2,
  other, E2
  total, health + retirement + other,
  total
)
```
### What It Does:

Defines short, meaningful variable names for each employment

Adds them together in a total variable

Returns total as the final result

### Tax Withheld 

F2 -> Refers to Gross Pay on the current row (F2 -> $4800)

Tax_Info!B2 -> Federal Tax Rate (0.12 or 12%)

Tax_Info!B3 -> Medicare Tax Rate (0.0145 or 1.45)

```excel
= F2 * (Tax_Info!B2 + Tax_Info!B3 + Tax_Info!B4)
```
### What this formula does:
1. Adds up all three tax rates:
   
   0.10 + 0.0145 + 0.062 = 0.1965
   
3. Multiplies that total tax rate by Gross Pay (F2):
   
   2000 * 0.1965 = 393 -> Tax Withheld

### Using LET():
```excel
grossPay, F2,
fedTax, Tax_Info!B2,
medTax, Tax_Info!B3,
ssTax, Tax_Info!B4,
totalTaxRate, fedTax + medTax + ssTax,
grossPay * totalTaxRate
```
The gives total tax amount wihheld for this pay period for this employee.


### Net_Pay:

F2 -> Gross Pay
G2 -> Total Deductions (like 401k, health, etc)
H2 -> Tax Withheld (combined federal, medicare, social security)

```excel
= F2 - G2 - H2
```
This formula subtracts:
Net_Pay = Gross_Pay - Total_Deductions - Tax_Withheld

### Using LET():

```excel
= LET (
grossPay, F2,
deductions, G2,
tax, H2,
grossPay - deductions - tax
)
```

### Refresh Macro 

To keep your dashboard charts, pivot tables, and summary views up to date after making changes to data in any of the sheets (Payroll_Log, Employee_Infor, etc.), the workbook includes a Refresh Macro. 

<h3>How It Works:</h3>

The macro automatically runs the ThisWorkbook.RefreshAll command.

When clicked, the Refresh All macro ensures that all of the following elements reflect the most up-do-date data:

Pivot Tables
Pivot Charts
Slicers
Any summary cells or formulas that are linked to these data sources (like totals, averages, or KPI indicators on the dashboard)

<h3>How to Use It:</h3>
1. Enable Macros when opening the file.

2. Click the "Refresh All" button on the Dashboard (or use the Developer tab if you're in edit mode).

3. All dashboards and summaries will update instantly.

### Macro Code:
```vba
Sub RefreshAll()
  ThisWorkbook.RefreshAll
End Sub
```
