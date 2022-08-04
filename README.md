# SQL Challenge: Employee Database :technologist:

## Background
The task is to research a project on employees of the corporation from the 1980s and 1990s. All that remains of the database of employees from that period are six CSV files.
I will design the tables to hold data in the CSVs, import the CSVs into a SQL database, and answer questions about the data performing data modeling, data engineering, and data analysis.

## Data Modeling
Inspected the CSVs and sketched out an ERD of the tables

<img src="https://github.com/blancacarretero/sql-challenge/blob/main/images/ERD.png?raw=true" width="600" title="hover text">

## Data Engineering
Using the information, created a table schema for each of the six CSV files. Specified data types, primary keys, foreign keys, and other constraints. 
Imported each CSV file into the corresponding SQL table.

```
-- Data Engineering

CREATE TABLE "department" (
    "dept_no" VARCHAR   NOT NULL,
    "dept_name" VARCHAR   NOT NULL,
    CONSTRAINT "pk_department" PRIMARY KEY (
        "dept_no"
     )
);

CREATE TABLE "titles" (
    "title_id" VARCHAR   NOT NULL,
    "title" VARCHAR   NOT NULL,
    CONSTRAINT "pk_titles" PRIMARY KEY (
        "title_id"
     )
);

CREATE TABLE "dept_emp" (
    "emp_no" INT   NOT NULL,
    "dept_no" VARCHAR   NOT NULL
);

CREATE TABLE "dept_manager" (
    "dept_no" VARCHAR   NOT NULL,
    "emp_no" INT   NOT NULL
);

CREATE TABLE "employees" (
    "emp_no" INT   NOT NULL,
    "emp_title_id" VARCHAR   NOT NULL,
    "bith_date" DATE   NOT NULL,
    "first_name" VARCHAR   NOT NULL,
    "last_name" VARCHAR   NOT NULL,
    "sex" VARCHAR   NOT NULL,
    "hire_date" DATE   NOT NULL,
    CONSTRAINT "pk_employees" PRIMARY KEY (
        "emp_no"
     )
);

CREATE TABLE "salary" (
    "emp_no" INT   NOT NULL,
    "salary" INT   NOT NULL
);

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "dept_emp" ADD CONSTRAINT "fk_dept_emp_dept_no" FOREIGN KEY("dept_no")
REFERENCES "department" ("dept_no");

ALTER TABLE "dept_manager" ADD CONSTRAINT "fk_dept_manager_dept_no" FOREIGN KEY("dept_no")
REFERENCES "department" ("dept_no");

ALTER TABLE "dept_manager" ADD CONSTRAINT "fk_dept_manager_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");

ALTER TABLE "employees" ADD CONSTRAINT "fk_employees_emp_title_id" FOREIGN KEY("emp_title_id")
REFERENCES "titles" ("title_id");

ALTER TABLE "salary" ADD CONSTRAINT "fk_salary_emp_no" FOREIGN KEY("emp_no")
REFERENCES "employees" ("emp_no");
```

## Data Analysis
1. List the following details of each employee: employee number, last name, first name, sex, and salary.
```
SELECT employees.emp_no, employees.last_name, employees.first_name, employees.gender, salary.salary
FROM employees
JOIN salaries
ON employees.emp_no = salaries.emp_no;
```
3. List first name, last name, and hire date for employees who were hired in 1986.
4. List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.
5. List the department of each employee with the following information: employee number, last name, first name, and department name.
6. List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."
7. List all employees in the Sales department, including their employee number, last name, first name, and department name.
8. List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.
9. List the frequency count of employee last names (i.e., how many employees share each last name) in descending order.

