# HR Analytics Dashboard — Project Documentation

## 1. Project Overview
The HR Analytics Dashboard is an interactive Power BI report developed to summarize and explore HR workforce data containing 6,000+ records. It focuses on employee headcount, employment status, department distribution, and base salary statistics.

## 2. Project Objectives
- Summarize the overall employee population.
- Compare active and terminated employees.
- Calculate the termination rate.
- Review minimum, maximum, and average base salary.
- Identify the five largest departments by employee count.
- Enable users to explore results using report slicers.

## 3. Tools and Technologies
- **Power BI Desktop:** report design, visuals, and interactive dashboard.
- **DAX:** measures and KPI calculations.
- **Power Query:** data preparation, where applicable. Document only the cleaning and transformation steps actually completed in your own file.

## 4. Dashboard Components
| Component | Purpose |
|---|---|
| Total Employees | Displays the total number of employee records. |
| Active Employees | Counts employees with Active status. |
| Terminated Employees | Counts employees with Terminated status. |
| Termination Rate | Shows terminated employees as a percentage of total employees. |
| Minimum Base Salary | Displays the lowest base salary. |
| Maximum Base Salary | Displays the highest base salary. |
| Average Base Salary | Displays the average base salary. |
| Top 5 Departments | Compares the five departments with the highest employee counts. |
| Department slicer | Filters report visuals by department. |
| Employment Status slicer | Filters report visuals by employment status. |

## 5. DAX Measures

The formulas below are templates based on the example model names `HR Data`, `Employment Status`, `Base Salary`, and `Employee ID`. Replace these names if your model uses different names. Also verify the exact status text in your dataset before using the Active and Terminated measures.

### 5.1 Total Employees
```DAX
Total Employees =
COUNTROWS('HR Data')
```
Counts the rows in the HR table. This is appropriate when each row represents one employee. If the table contains multiple rows per employee, use a distinct employee count instead:

```DAX
Total Employees =
DISTINCTCOUNT('HR Data'[Employee ID])
```

### 5.2 Active Employees
```DAX
Active Employees =
CALCULATE(
    [Total Employees],
    'HR Data'[Employment Status] = "Active"
)
```
Calculates the employee count for records whose employment status is `Active`.

### 5.3 Terminated Employees
```DAX
Terminated Employees =
CALCULATE(
    [Total Employees],
    'HR Data'[Employment Status] = "Terminated"
)
```
Calculates the employee count for records whose employment status is `Terminated`.

### 5.4 Termination Rate
```DAX
Termination Rate =
DIVIDE(
    [Terminated Employees],
    [Total Employees],
    0
)
```
Divides terminated employees by total employees. Format this measure as a percentage in Power BI. The `DIVIDE` function returns 0 if the denominator is zero.

### 5.5 Minimum Base Salary
```DAX
Minimum Base Salary =
MIN('HR Data'[Base Salary])
```
Returns the lowest value in the Base Salary column.

### 5.6 Maximum Base Salary
```DAX
Maximum Base Salary =
MAX('HR Data'[Base Salary])
```
Returns the highest value in the Base Salary column.

### 5.7 Average Base Salary
```DAX
Average Base Salary =
AVERAGE('HR Data'[Base Salary])
```
Returns the arithmetic mean of the Base Salary column, ignoring blank values.

## 6. Top 5 Departments Visual
To show the five departments with the largest employee counts:
1. Add `Department` to the visual's category or legend field.
2. Add an employee count to the values field. Use a distinct count of `Employee ID` if employees can appear more than once.
3. In the visual-level Filters pane, select the Department field and change the filter type to **Top N**.
4. Enter **5** in Show items.
5. Set By value to the employee-count measure, then select **Apply filter**.

## 7. Interactivity
The dashboard includes Department and Employment Status slicers. Use **Format > Edit interactions** in Power BI Desktop to check that each slicer filters the intended charts and KPI cards.

## 8. How to Open
1. Download or clone this repository.
2. Open `HR_Analytics_Dashboard.pbix` using Microsoft Power BI Desktop.
3. Refresh the data only if you have access to the original source and the required connection settings.
4. Use the slicers to explore the report.

## 9. Project Outcome
The report consolidates core workforce and salary indicators into a single interactive view. It supports quick review of employee status, department headcount, and salary ranges.

## 10. Data Privacy and Publishing
Do not publish names, contact details, employee IDs, compensation records, or other confidential or personally identifiable employee information. Before making the repository public, confirm that the source dataset is licensed for redistribution and that the PBIX does not expose restricted data or credentials.

## 11. Suggested Repository Structure
```text
HR-Analytics-PowerBI-Dashboard/
├── HR_Analytics_Dashboard.pbix
├── README.md
├── HR_Analytics_Documentation.md
└── screenshots/
    └── dashboard_overview.png
```
