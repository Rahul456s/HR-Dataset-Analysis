Here is a well-organized and professional `README.md` file for your **HR Project SQL database**, ready to be used on GitHub. This includes a summary of your SQL logic, project purpose, and features.

---

# 🧑‍💼 HR Project – SQL Employee Analytics

This project represents a **Human Resources database** for analyzing employee data, performance, tenure, salary trends, and attrition rate using **SQL**. It covers data cleaning, transformation, and key HR metrics through structured queries.

---

## 📁 Database Setup

**Database Name**: `hrproject`

To get started:

```sql
CREATE DATABASE hrproject;
USE hrproject;
```

---

## 🧱 Table: `employees`

This is the core table containing employee details including:

* `EmpID`
* `FirstName`, `LastName`
* `DOB`
* `DateOfHire`
* `DateOfTermination`
* `Salary`
* `LastPerformanceReview_Date`
* `employeescurrentstatus` (added later)

---

## 🧹 Data Cleanup and Transformation

### 🔧 Modify Date and Salary Formats

```sql
-- Standardize date formats
UPDATE employees SET DOB = STR_TO_DATE(DOB, '%d-%m-%Y');
UPDATE employees SET DateOfHire = STR_TO_DATE(DateOfHire, '%d-%m-%Y');
UPDATE employees SET LastPerformanceReview_Date = STR_TO_DATE(LastPerformanceReview_Date, '%Y-%m-%d');

-- Modify column types
ALTER TABLE employees
MODIFY COLUMN DOB DATE,
MODIFY COLUMN DateOfHire DATE,
MODIFY COLUMN LastPerformanceReview_Date DATE,
MODIFY COLUMN salary DECIMAL(10,2);
```

---

## 📊 HR Analytics Queries

### 👥 Employee Overview

```sql
SELECT * FROM employees LIMIT 5;
SELECT * FROM employees ORDER BY EmpID DESC LIMIT 5;
```

### 💸 Average Salary

```sql
SELECT AVG(salary) AS avg_salary FROM employees;
```

### 🧓 Average Age

```sql
SELECT AVG(TIMESTAMPDIFF(YEAR, DOB, CURDATE())) AS Avg_Age FROM employees;
```

### 🧭 Average Tenure

```sql
SELECT AVG(TIMESTAMPDIFF(YEAR, DateOfHire, CURDATE())) AS Avg_Year_in_Company FROM employees;
```

---

## 🔄 Attrition Rate Analysis

### ➕ Add Employee Status Column

```sql
ALTER TABLE employees ADD employeescurrentstatus INT;
```

### ✅ Update Current Employee Status

```sql
SET SQL_SAFE_UPDATES = 0;

UPDATE employees
SET employeescurrentstatus = CASE
    WHEN DateOfTermination = '' THEN 1
    ELSE 0
END;
```

### 📉 Attrition Rate

```sql
SELECT 
  (CAST(COUNT(CASE WHEN employeescurrentstatus = 0 THEN 1 END) AS FLOAT) / COUNT(*)) * 100 AS Attrition_Rate
FROM employees;
```

---

## 🔍 Schema Overview

```sql
DESCRIBE employees;
```

---

## 📸 Screenshots

Include screenshots of your results or dashboards (e.g., Power BI, Tableau if used). Place images in a `screenshots/` folder and reference them like this:

```markdown
### Dashboard Overview
![Dashboard](screenshots/hr_dashboard.png)

### Attrition Rate Output
![Attrition](screenshots/attrition_rate.png)
```

---

## 🧠 Key Concepts Used

* Data Cleaning using `STR_TO_DATE`, `ALTER`, `MODIFY`
* HR Metrics: Average Age, Tenure, Attrition
* SQL Aggregates: `AVG`, `COUNT`, `CASE`
* Schema Enhancement: `ALTER TABLE`, `ADD COLUMN`
* Safe Update Bypass for Transformation

---

## 🛠 Technologies

* MySQL (or any SQL-compliant RDBMS)
* SQL Joins, Aggregates, Data Types
* HR Analytics

---

## 📄 License

This project is licensed under the MIT License.

---

## 👤 Author

**Your Name**
GitHub: [yourusername](https://github.com/Rahul456s)
Email: [youremail@example.com](mailto:Rahul456shende@gamail.com)

---

Would you like me to export this into a downloadable `README.md` file or help upload it into your GitHub repo? Let me know!
