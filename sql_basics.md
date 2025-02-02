## **Introduction to SQL**

### **What is SQL?**

SQL (Structured Query Language) is a standard programming language designed for managing and manipulating relational databases. It allows users to retrieve, update, delete, and organize data stored in tables.


## **Sample Database: Employee Salaries**

Sample table: `employee_salaries`

| emp\_id | emp\_name | department | salary | hire\_date |
| ------- | --------- | ---------- | ------ | ---------- |
| 1       | Alice     | HR         | 70000  | 2018-06-01 |
| 2       | Bob       | IT         | 120000 | 2016-09-12 |
| 3       | Charlie   | IT         | 95000  | 2019-04-15 |
| 4       | David     | Finance    | 85000  | 2020-11-01 |
| 5       | Eve       | HR         | 72000  | 2021-02-20 |
| 6       | Frank     | Finance    | 78000  | 2018-05-10 |

---
# 1. Basic SQL Commands


### **SELECT Statement**

The SELECT statement is used to retrieve specific columns or entire rows from a database table.

### **Syntax:**

```sql
SELECT column1, column2, ...
FROM table_name;
```

### **Question:**

Retrieve the names and departments of all employees.

### **SQL Query:**

```sql
SELECT emp_name, department
FROM employee_salaries;
```

### **WHERE Clause**

The WHERE clause is used to filter records based on specific conditions.

### **Syntax:**

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### **Question:**

Retrieve details of employees from the IT department.

### **SQL Query:**

```sql
SELECT *
FROM employee_salaries
WHERE department = 'IT';
```


### **ORDER BY Clause**


The ORDER BY clause sorts the result set either in ascending (default) or descending order.

### **Syntax:**

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC|DESC;
```

### **Question:**

List all employees sorted by salary in descending order.

### **SQL Query:**

```sql
SELECT emp_name, salary
FROM employee_salaries
ORDER BY salary DESC;
```

### **DISTINCT Clause**

The DISTINCT clause removes duplicate records from the result set.

### **Syntax:**

```sql
SELECT DISTINCT column1
FROM table_name;
```

### **Question:**

Retrieve the unique departments from the employee\_salaries table.

### **SQL Query:**

```sql
SELECT DISTINCT department
FROM employee_salaries;
```

### **LIMIT Clause**

The LIMIT clause is used to specify the number of records to retrieve.

### **Syntax:**

```sql
SELECT column1
FROM table_name
LIMIT number;
```

### **Question:**

List the top 3 highest-paid employees.

### **SQL Query:**

```sql
SELECT emp_name, salary
FROM employee_salaries
ORDER BY salary DESC
LIMIT 3;
```

# **2. Filtering Data**

#### **AND Operator**

Used to combine multiple conditions where all conditions must be true.

##### **Question:**

List employees from the IT department earning more than 100,000.

##### **SQL Query:**

```sql
SELECT emp_name, salary, department
FROM employee_salaries
WHERE department = 'IT' AND salary > 100000;
```

#### **OR Operator**

Used to combine conditions where at least one condition is true.

##### **Question:**

List employees from the HR or Finance department.

##### **SQL Query:**

```sql
SELECT emp_name, department
FROM employee_salaries
WHERE department = 'HR' OR department = 'Finance';
```

#### **NOT Operator**

Used to negate a condition.

##### **Question:**

List employees not from the IT department.

##### **SQL Query:**

```sql
SELECT emp_name, department
FROM employee_salaries
WHERE NOT department = 'IT';
```

#### **BETWEEN Operator**

Used to filter values within a specific range.

##### **Question:**

List employees with salaries between 75,000 and 100,000.

##### **SQL Query:**

```sql
SELECT emp_name, salary
FROM employee_salaries
WHERE salary BETWEEN 75000 AND 100000;
```

#### **LIKE Operator**

Used to search for patterns in string data.

##### **Question:**

List employees whose names start with 'A'.

##### **SQL Query:**

```sql
SELECT emp_name
FROM employee_salaries
WHERE emp_name LIKE 'A%';
```

#### **IN Operator**

Used to filter results that match any value in a list.

##### **Question:**

List employees from the IT and HR departments.

##### **SQL Query:**

```sql
SELECT emp_name, department
FROM employee_salaries
WHERE department IN ('IT', 'HR');
```

#### **Example:**

List employees from the IT department earning above 90,000 or from the HR department hired after 2020.

##### **SQL Query:**

```sql
SELECT emp_name, department, salary, hire_date
FROM employee_salaries
WHERE (department = 'IT' AND salary > 90000) 
   OR (department = 'HR' AND hire_date > '2020-01-01');
```

---

## **3. Aggregating Data**

### **COUNT(), SUM(), AVG(), MAX(), and MIN()**

These aggregate functions perform calculations on multiple rows of a table and return a single value.

#### **Syntax:**

```sql
SELECT AGG_FUNCTION(column_name)
FROM table_name;
```
**COUNT()** - returns the number of rows in a set.

**SUM()** - returns the total sum of a numerical column.

**AVG()** - returns the average value of a numerical column.

**MAX()** - returns the largest value within the selected column.

**MIN()** - returns the smallest value within the selected column.


#### **Question:**

Count the total number of employees.

##### **SQL Query:**

```sql
SELECT COUNT(*) AS total_employees
FROM employee_salaries;
```

#### **Question:**

Find the highest and lowest salaries.

##### **SQL Query:**

```sql
SELECT MAX(salary) AS highest_salary, MIN(salary) AS lowest_salary
FROM employee_salaries;
```

### **GROUP BY Clause**


GROUP BY groups rows that have the same values in specified columns and allows aggregate functions to be performed on each group.

#### **Syntax:**

```sql
SELECT column_name, AGG_FUNCTION(column_name)
FROM table_name
GROUP BY column_name;
```

#### **Question:**

Find the average salary for each department.

##### **SQL Query:**

```sql
SELECT department, AVG(salary) AS average_salary
FROM employee_salaries
GROUP BY department;
```

### **HAVING Clause**


HAVING is used to filter groups of rows based on aggregate functions.

#### **Syntax:**

```sql
SELECT column_name, AGG_FUNCTION(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

#### **Question:**

Find departments with a total salary expense greater than 150,000.

##### **SQL Query:**

```sql
SELECT department, SUM(salary) AS total_salary
FROM employee_salaries
GROUP BY department
HAVING SUM(salary) > 150000;
```

### **CASE Statements**



The CASE statement allows conditional logic within SQL queries, similar to if-else statements in programming.

#### **Syntax:**

```sql
SELECT column1,
       CASE
         WHEN condition1 THEN result1
         WHEN condition2 THEN result2
         ELSE result3
       END AS new_column
FROM table_name;
```

#### **Question:**

Categorize employees based on salary levels:

- "High" for salaries above 100,000
- "Medium" for salaries between 75,000 and 100,000
- "Low" for salaries below 75,000

##### **SQL Query:**

```sql
SELECT emp_name, salary,
       CASE
         WHEN salary > 100000 THEN 'High'
         WHEN salary BETWEEN 75000 AND 100000 THEN 'Medium'
         ELSE 'Low'
       END AS salary_category
FROM employee_salaries;
```

---

## **4. Joins in SQL**

### **INNER JOIN**



An INNER JOIN returns records that have matching values in both tables.

#### **Syntax:**

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

#### **Example:**

Consider another table `employee_bonuses`:

| emp\_id | bonus |
| ------- | ----- |
| 1       | 5000  |
| 2       | 10000 |
| 3       | 7000  |
| 4       | 8500  |

Retrieve employee names along with their bonuses.

##### **SQL Query:**

```sql
SELECT e.emp_name, b.bonus
FROM employee_salaries e
INNER JOIN employee_bonuses b
ON e.emp_id = b.emp_id;
```

### **LEFT JOIN**



A LEFT JOIN returns all records from the left table and the matched records from the right table. If there is no match, NULL values are returned.

#### **Question:**

Retrieve all employees and their bonuses, if available.

##### **SQL Query:**

```sql
SELECT e.emp_name, b.bonus
FROM employee_salaries e
LEFT JOIN employee_bonuses b
ON e.emp_id = b.emp_id;
```

### **RIGHT JOIN**



A RIGHT JOIN returns all records from the right table and the matched records from the left table. If there is no match, NULL values are returned.

#### **Question:**

Retrieve all bonuses and the corresponding employee names, if available.

##### **SQL Query:**

```sql
SELECT e.emp_name, b.bonus
FROM employee_salaries e
RIGHT JOIN employee_bonuses b
ON e.emp_id = b.emp_id;
```

### **FULL JOIN**



A FULL JOIN returns all records when there is a match in either the left or right table. If there is no match, NULL values are returned.

#### **Question:**

Retrieve all employees and bonuses, including unmatched records from both tables.

##### **SQL Query:**

```sql
SELECT e.emp_name, b.bonus
FROM employee_salaries e
FULL JOIN employee_bonuses b
ON e.emp_id = b.emp_id;
```

---

## **Extra Questions**

1. Retrieve the names and departments of employees hired after 2018, categorized by salary levels using a CASE statement.

   ```sql
   SELECT emp_name, department, hire_date,
          CASE
            WHEN salary > 100000 THEN 'High'
            WHEN salary BETWEEN 75000 AND 100000 THEN 'Medium'
            ELSE 'Low'
          END AS salary_category
   FROM employee_salaries
   WHERE hire_date > '2018-01-01';
   ```

2. Retrieve the top 3 departments by total salary, including the total salary amount.

   ```sql
   SELECT department, SUM(salary) AS total_salary
   FROM employee_salaries
   GROUP BY department
   ORDER BY total_salary DESC
   LIMIT 3;
   ```
