<h1>Purpose</h1>

This Markdown document explains all formulas used in the Payroll Tracker Excel file, covering their purpose, logic, dependencies, and where they are located. This is designed to help users, and reviewers understand the inner workings of each sheet, cell, and calculation, and to ensure easy scalability and maintenance for future updates.

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


We can also use LET() to reuse the variables and to make complex formulas readable like the following:

```excel
=LET(
    empID, B2,
    hoursWorked, E2,
    payType, XLOOKUP(empID, EmployeeTable[Employee_ID], EmployeeTable[Pay_Type]),
    payRate, XLOOKUP(empID, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate]),
    IF(payType = "Hourly", hoursWorked * payRate, payRate)
)
```


