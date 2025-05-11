<h3>Adding New Employees to the Payroll Tracker</h3>

This guide explains how to add new/more employee records to the Employee_Info 
sheet of the Excel-based Payroll Tracker, specifically documenting the addition
of 200 newly generated employees. It includes the source code to generate the new employee
dataset, step-by-step instructions, and best practices. 


Here is the code used to generate the 200 employee records with consistent formatting:

```python
from faker import Faker
import pandas as pd
import random 
import re

fake = Faker()
Faker.seed(0)

num_employees = 200
existing_file_path = 'full or relative path'
employee_sheet = 'Employee_Info'


department_positions = {
    'HR': [
        'HR Specialist', 'Recruitment Assistant', 'HR Coordinator',
        'Benefits Administrator', 'Talent Acquisition Specialist',
        'HR Assistant', 'Employee Relations Associate'
    ],
    'IT': [
        'System Administrator', 'Support Engineer', 'IT Technician',
        'Help Desk Specialist', 'Network Analyst', 'DevOps Assistant',
        'Tech Support Specialist', 'Junior Sys Admin'
    ],
    'Payroll': [
        'Payroll Analyst', 'Payroll Clerk', 'Compensation Assistant',
        'Timekeeping Coordinator', 'Payroll Associate', 'Wage & Tax Specialist',
        'Payroll Technician'
    ],
    'Finance': [
        'Accountant', 'Financial Analyst', 'Junior Analyst',
        'Billing Clerk', 'Accounts Payable Assistant', 'Bookkeeper',
        'Finance Coordinator', 'Audit Support Specialist'
    ],
    'Marketing': [
        'Marketing Specialist', 'Content Coordinator', 'SEO Analyst',
        'Social Media Assistant', 'Marketing Analyst', 'Brand Assistant',
        'Campaign Associate', 'Email Marketing Coordinator'
    ]
}

pay_types = ['Hourly', 'Salaried']

def generate_position(department):
    return random.choice(department_positions.get(department, ['General Associate']))


try:
    existing_df = pd.read_excel(existing_file_path, sheet_name=employee_sheet)
    last_id = existing_df['Employee_ID'].iloc[-1]
    match = re.search(r'\d+', last_id)
    starting_index = int(match.group()) + 1 if match else 1
except Exception as e:
    print(f" ERROR: Could not read {existing_file_path} or sheet {employee_sheet}.\nPlease make sure the file exists and is not open in Excel. \nDetails: {e}")
    exit(1)

employee_data = []


for i in range(starting_index, starting_index + num_employees):
    emp_id = f"E{i:03}"
    full_name = f"{fake.first_name()} {fake.last_name()}"
    hire_date = fake.date_between(start_date='-10y', end_date='today')
    department = random.choice(list(department_positions.keys()))
    position = generate_position(department)
    pay_type = random.choice(pay_types)
    pay_rate = round(random.uniform(15, 50), 2) if pay_type == 'Hourly' else random.randint(45000, 95000)
    bank_account = f"XXXX-{fake.numerify(text='####')}"

    employee_data.append([emp_id, full_name, department, position, hire_date, pay_type, pay_rate, bank_account])

columns = [
        'Employee_ID', 'Full_Name', 'Department', 
        'Position', 'Hire_Date', 'Pay_Type', 'Pay_Rate', 'Bank_Account'
]



df = pd.DataFrame(employee_data, columns=columns)
df.to_excel("Generated_Employees_PAT.xlsx", index=False)

print(f"Generated {num_employees} employees and saved to Excel Projects folder")C
```

<h3>Step-by-Step instructions:</h3>
<h4>1. Locate the Generated Employee File</h4>
The employee records were generated using Python with the faker libary.
Default file name: Generated_Employees_PAT.xlsx
Check your local project folder or Downloads folder for this file.

<h4>2. Open Both Excel Files</h4>
Open: Payroll_Tracker.xlsx
Open: generated_employees.xlsx

<h4>3. Prepare the Data for Import</h4>
Ensure that your generated employee file has the following columns in this exact order:
| Employee_ID | Full_Name | Department | Position | Hire_Date | Pay_Type | Pay_Rate | Bank_Account | Activity_Status 

<h4>4. Import into Employee_Info Sheet</h4>
1. Go to the Employee_Info sheet in Payroll_Tracker.xlsx
2. Scroll to the bottom of the existing table
3. Select the first empty row inside the Excel Table (EmployeeTable)
4. Paste the 200 new rows from the generated file
Ensure you're pasting directly into the Excel Table so it auto-expands and inherits formatting and formulas. 

<h4>5. Confirm the Format</h4>
All columns should match the expected format
Bank accounts should appear like XXXX-1234
Pay_Type must be either Hourly or Salary 

<h4>6. Save and Test</h4>
Save the file 
Use slicers or filters on Dashboard sheet to verify the new employees appear in summaries and pivot tables 

<h3>Best Practices</h3>

Always create a backup before importing new data

Make sure the new data uses the same format and column headers as the original 

Keep your Excel Tables intact - pasting inside them ensures they expand correctly 
