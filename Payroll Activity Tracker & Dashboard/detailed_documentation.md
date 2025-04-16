<h1>Purpose</h1>

This Markdown document explains all formulas used in the Payroll Tracker Excel file, covering their purpose, logic, dependencies, and where they are located. This is designed to help users, and reviewers understand the inner workings of each sheet, cell, and calculation, and to ensure easy scalability and maintenance for future updates.

### Formula used to calculate the Gross_Pay (Hourly & Salaried Employees):

```excel 
=IF(
  XLOOKUP(B2, EmployeeTable[Employee_ID]), EmployeeTable[Pay_Type]) = "Hourly",
  E2 * XLOOKUP(B2, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate]),
  XLOOKUP(B2, EmployeeTable[Employee_ID], EmployeeTable[Pay_Rate])
)


