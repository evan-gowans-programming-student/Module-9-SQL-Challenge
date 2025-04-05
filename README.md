# SQL Employee Data Analysis Project

## Overview

This project demonstrates a detailed analysis of employee data using PostgreSQL. The objective was to answer eight business-focused questions through SQL queries while maintaining an organized workflow with raw data and query results stored separately.

---

## Project Highlights

### Data Modeling

- Raw tables were created for six CSV files (`employees`, `salaries`, `dept_emp`, `departments`, `titles`, and `dept_manager`) with appropriate data types, primary keys, and relationships.
- Result tables (`question_1_results` to `question_8_results`) were created to store answers for each query.

### Data Engineering

- Defined columns, constraints, foreign key relationships, and appropriate data types.
- `NOT NULL` constraints and value lengths were implemented where required.

### Data Analysis

- Solved eight business questions through structured SQL queries.
- Stored all query results in dedicated tables for easy validation.

---

## Business Questions Answered

Below is the list of questions and the SQL queries used to answer them:

### 1. List the employee number, last name, first name, sex, and salary of each employee.

```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.sex, salaries.salary
FROM employees
JOIN salaries ON employees.emp_no = salaries.emp_no;
```

---

### 2. List the first name, last name, and hire date for the employees who were hired in 1986.

```sql
SELECT first_name, last_name, hire_date
FROM employees
WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31';
```

---

### 3. List the manager of each department along with their department number, department name, employee number, last name, and first name.

```sql
SELECT dept_manager.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name
FROM dept_manager
JOIN departments ON dept_manager.dept_no = departments.dept_no
JOIN employees ON dept_manager.emp_no = employees.emp_no;
```

---

### 4. List the department number for each employee along with their employee number, last name, first name, and department name.

```sql
SELECT dept_emp.dept_no, employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no;
```

---

### 5. List the first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B.

```sql
SELECT first_name, last_name, sex
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%';
```

---

### 6. List each employee in the Sales department, including their employee number, last name, first name, and department name.

```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name = 'Sales';
```

---

### 7. List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.

```sql
SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees ON dept_emp.emp_no = employees.emp_no
JOIN departments ON dept_emp.dept_no = departments.dept_no
WHERE departments.dept_name IN ('Sales', 'Development');
```

---

### 8. List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name).

```sql
SELECT last_name, COUNT(*) AS frequency
FROM employees
GROUP BY last_name
ORDER BY frequency DESC;
```

---

## Repository Contents

### Raw Data

- `employees.csv`
- `salaries.csv`
- `dept_emp.csv`
- `titles.csv`
- `departments.csv`
- `dept_manager.csv`

### Question Results

- `question_1_results.csv`
- `question_2_results.csv`
- `question_3_results.csv`
- `question_4_results.csv`
- `question_5_results.csv`
- `question_6_results.csv`
- `question_7_results.csv`
- `question_8_results.csv`

### SQL Scripts

- `create_tables.sql`: Scripts to create all tables (raw and result tables).
- `queries.sql`: Scripts for running the queries to answer each question.

---

## How to Replicate the Project

1. Clone the repository:

```bash
git clone https://github.com/evan-gowans-programming-student/Module-9-SQL-Challenge
cd Module-9-SQL-Challenge
```

2. Set up a PostgreSQL database and import the raw CSV files:

- Use `create_tables.sql` to create tables.
- Import raw CSVs into PostgreSQL.
- Run the queries in `queries.sql` to replicate the analysis.
- Review the results stored in `/question_results`.
