<h1>Payroll Activity Tracker & Dashboard</h1>

This Excel-based solution is designed to track payroll activities and provide an interactive dashboard for analysis.

<h3>Project Overview</h3>

The workbook consists of several sheets, each serving a specific purpose:

- **Employee_Info (EmployeeTable):**  
  Contains detailed employee information including:
  - **Employee_ID:** Unique identifier.
  - **Full_Name, Department, Position, Hire_Date:** Basic employee details.
  - **Pay_Type & Pay_Rate:** Indicates if an employee is Hourly or Salaried and their corresponding pay.
  - **Bank_Account & Active_Status:** Additional details with data validation applied.
  
- **Payroll_Log:**  
  Tracks each payroll entry with the following columns:
  - **Employee_ID, Pay_Period_Start, Pay_Period_End:** Identifies the employee and the pay period.
  - **Hours_Worked:** Relevant for hourly employees.
  - **Gross_Pay:** Calculated dynamically (Hourly: Hours_Worked × Pay_Rate; Salaried: flat Pay_Rate).
  - **Total_Deductions:** Pulled from the Deductions sheet.
  - **Tax_Withheld:** Calculated based on tax rates provided in the Tax_Info sheet.
  - **Net_Pay:** Derived from Gross_Pay minus Total_Deductions and Tax_Withheld.
  - **Payment_Status & Date_Processed:** Allows tracking of payroll processing stages.

- **Deductions:**  
  Records deduction amounts per employee per pay period, including:
  - **Health_Insurance, Retirement_401k, Other:** Individual deduction entries.
  - **Total_Deductions:** A calculated field summing the above values.
 
- **Tax_Info:**  
  Contains tax rate information used to compute the Tax_Withheld:
  - For example, Federal Tax, Medicare, and Social Security rates.
 


