# employee_attrition_analysis
Employee Attrition Analysis using SQL to uncover key drivers of employee turnover, including department, job role, gender, and performance, with actionable business insights.

# Employee Attrition Analysis

## Project Overview

This project analyzes employee data to understand attrition patterns and identify factors that influence employee turnover.

The goal is to uncover insights that can help organizations improve retention by examining relationships between attrition and variables such as department, job role, gender, marital status, salary, and performance.

---

## Dataset

The dataset used is the IBM HR Analytics Employee Attrition dataset.

It includes the following key fields:

* employee_id
* department
* job_role
* age
* salary
* performance_score
* gender
* marital_status
* attrition

The data was cleaned and transformed to ensure consistency and usability for SQL analysis.

---

## Data Preparation

The dataset was prepared before analysis:

* Renamed columns to lowercase for consistency
* Removed special characters from salary column
* Converted salary to numeric format
* Ensured employee_id is unique
* Structured data for efficient querying

---

## SQL Analysis

### Average Salary by Department

```sql
SELECT 
e.department,
ROUND(AVG(p.salary), 2) AS avg_salary
FROM employees e
JOIN performance p
ON e.employee_id = p.employee_id
GROUP BY e.department
ORDER BY avg_salary DESC;
```

---

### Attrition Rate by Department

```sql
SELECT 
dep.department,
ROUND(SUM(CASE WHEN emp.attrition = 'Yes' THEN 1 ELSE 0 END)* 100.0 / COUNT(*), 2)AS attrition_rate
FROM employee_datasets AS emp
JOIN department_datasets AS dep
ON emp.employee_id = dep.employee_id
GROUP BY dep.department
ORDER BY attrition_rate DESC;
```

---

### Attrition Rate by Marital Status

```sql
SELECT 
marital_status,
ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 1) AS attrition_rate
FROM employee_datasets
GROUP BY marital_status
ORDER BY attrition_rate DESC;

```

---

### Attrition Rate by Job Role

```sql
SELECT dep.job_role,
ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS attrition_rate
FROM employee_datasets AS emp
JOIN department_datasets AS dep
ON emp.employee_id = dep.employee_id
GROUP BY dep.job_role
```

---

### Attrition Rate by Gender

```sql
SELECT 
gender,
ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS attrition_rate
FROM employee_datasets
GROUP BY gender
ORDER BY attrition_rate DESC;
```

---

### Attrition Rate by Performance Score

```sql
SELECT 
performance_rating,
ROUND(SUM(CASE WHEN attrition = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*),2) AS attrition_rate
FROM employee_datasets
GROUP BY performance_rating
ORDER BY performance_rating;
```

---

## Key Insights

* Employees with single marital status show the highest attrition rate, suggesting lower retention among this group.

* The Sales Representative role records the highest attrition, indicating potential pressure or job dissatisfaction within sales roles.

* Male employees have slightly higher attrition compared to females, though this is not a major driver.

* Performance rating does not significantly impact attrition, as employees leave across all performance levels.

* The Sales department has the highest average salary, yet also experiences the highest attrition.

* This shows that higher salary alone does not guarantee employee retention, especially in demanding roles.

---

## Visualizations

The analysis was supported with visualizations created in Excel:

* Bar chart showing average salary by department
* Column chart showing attrition rate by department
* Bar Chart showing attrition rate by job role
* Column Chart showing attrition rate by gender
* Pie Chart showing attrition rate by Marital Status 

---

## Tools Used

* SQL (PostgreSQL / Supabase)
* Microsoft Excel

---

## Conclusion

The analysis shows that employee attrition is not driven by a single factor.

Sales roles and the Sales department experience the highest attrition despite having the highest average salary. This indicates that compensation alone is not enough to retain employees in high-pressure roles.

Marital status also plays a role, with single employees showing higher attrition. Gender differences exist but are not a strong driver. Performance rating does not significantly influence attrition, meaning both high and low performers leave the organization.

Overall, job role and work environment appear to have a stronger impact on attrition than salary or performance.



