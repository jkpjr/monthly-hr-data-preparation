# monthly-hr-data-preparation
Processes monthly workforce data using Microsoft Excel and Power Query, following HR validation rules and governance. This is a capstone project for the Coursera course "HR Data Preparation &amp; Governance".

## 1. Review and Reconcile Sources

The dataset `Monthly_Workforce_Extract.csv` was examined based on the guidelines listed in `HR_Project_Validation_Rules.xlsx` and `HR_Reference_Extract.csv`.

## 2. Design Power Query

a. Assigned appropriate data types:

| Columns | Data Types |
| :--- | :--- |
| `EmployeeID` | Text |
| `EmployeeName` | Text |
| `Department` | Text |
| `Location` | Text |
| `EmploymentStatus` | Text |
| `HireDate` | Date |
| `TerminationDate` | Date |
| `FTE` | Decimal Number |

b. Renamed columns if necessary.  
c. Trimmed whitespaces if any.  
d. Capitalized each word in text columns.  
e. Standardized text values using the approved values on specified columns:

| Columns | Approved Values |
| :--- | :--- |
| `EmploymentStatus` | Active |
| `EmploymentStatus` | Terminated |
| `EmploymentType` | Full-Time |
| `EmploymentType` | Part-Time |
| `EmploymentType` | Contractor |
| `Department` | Human Resources |
| `Department` | Finance |
| `Department` | Sales |
| `Department` | Information Technology |
| `Department` | Customer Support |
| `Department` | Operations |
| `Department` | Marketing |

f. Identical rows where no values are meaningfully different were deduplicated.  
g. Added conditional columns to identify invalid `FTE` values. A valid `FTE` value is a number between 0 and 1, inclusive.  
h. Filtered rows where `TerminationDate` is before `HireDate`.

Additionally, imputed missing values in the `Department` column based on matching `EmployeeID` from `HR_Reference_Extract`, as instructed in `HR_Project_Validation_Rules`, after loading the data.

## 3. VLOOKUP
Load `HR_Reference_Extract.csv` and use VLOOKUP() to get the region from the new dataset into a new `Region` column in the original table where it matches EmployeeID.

## 4. Pivot Table
Inserts a Pivot Table to show the full-time equivalent of the employees across regions per employment type and department, filtered by active employees.
