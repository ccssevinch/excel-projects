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
 
- **Dashboard:**  
  An interactive dashboard that consolidates:
  - **Pivot Charts:** Visualizations (e.g., line charts for Gross_Pay and Net_Pay over time).
  - **Slicers:** Allow interactive filtering (e.g., by Pay_Period_End, Payment_Status).
  - Additional key metrics and summaries for a quick, at-a-glance view of payroll performance.
 
## Key Features

- **Dynamic Calculations:**  
  Automated formulas calculate Gross_Pay, Tax_Withheld, and Net_Pay based on employee type and input data.

- **Structured Data with Validation:**  
  Employee details are maintained in an Excel Table (EmployeeTable), ensuring data integrity through structured references and drop-down lists.

- **Interactive Analysis:**  
  Pivot tables and pivot charts, coupled with slicers, enable real-time filtering and detailed analysis.

- **Clean, Professional Dashboard:**  
  The Dashboard sheet integrates key visual elements, keeping raw data and pivot tables on separate sheets to maintain clarity.

## How to Use

1. **Update Employee Data:**  
   Modify or add employee details on the `Employee_Info` sheet.

2. **Enter Payroll Data:**  
   Record payroll entries for each employee and pay period in the `Payroll_Log` sheet.

3. **Input Deductions:**  
   On the `Deductions` sheet, enter deduction amounts ensuring Employee_ID and Pay_Period_End match those in the Payroll_Log.

4. **Adjust Tax Rates:**  
   Modify tax rates as needed in the `Tax_Info` sheet.

5. **Interact with the Dashboard:**  
   Use slicers on the `Dashboard` sheet to filter the pivot charts and gain insights into payroll trends and statuses.
