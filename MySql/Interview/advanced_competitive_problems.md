
### Problem 1: Top N Salaries

**Problem:** Write an SQL query to get the second highest salary from the `employees` table.

**Solution:**
```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```
**Explanation:** This query selects the maximum salary that is less than the highest salary, effectively giving the second highest salary.

### Problem 2: Employee Department Count

**Problem:** Write an SQL query to count the number of employees in each department.

**Solution:**
```sql
SELECT department_id, COUNT(*) AS EmployeeCount
FROM employees
GROUP BY department_id;
```
**Explanation:** This query groups the employees by department and counts the number of employees in each group.

### Problem 3: Find Duplicate Emails

**Problem:** Write an SQL query to find all duplicate email addresses in the `users` table.

**Solution:**
```sql
SELECT email, COUNT(*) AS count
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```
**Explanation:** This query groups the users by email and selects those groups where the count of emails is greater than one.

### Problem 4: Employees Earning More Than Their Managers

**Problem:** Write an SQL query to find the employees who earn more than their managers.

**Solution:**
```sql
SELECT e1.name AS Employee
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.id
WHERE e1.salary > e2.salary;
```
**Explanation:** This query joins the employees table with itself to compare the salary of each employee with their manager's salary.

### Problem 5: Department with the Highest Average Salary

**Problem:** Write an SQL query to find the department with the highest average salary.

**Solution:**
```sql
SELECT department_id
FROM employees
GROUP BY department_id
ORDER BY AVG(salary) DESC
LIMIT 1;
```
**Explanation:** This query calculates the average salary for each department, orders them in descending order, and selects the top one.

### Problem 6: Employee Salaries Difference

**Problem:** Write an SQL query to find the difference between the highest and lowest salaries in the `employees` table.

**Solution:**
```sql
SELECT MAX(salary) - MIN(salary) AS SalaryDifference
FROM employees;
```
**Explanation:** This query calculates the difference between the maximum and minimum salaries.

### Problem 7: Rank Employees by Salary

**Problem:** Write an SQL query to rank employees based on their salaries.

**Solution:**
```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```
**Explanation:** This query ranks employees by their salary in descending order using the `RANK()` window function.

### Problem 8: Consecutive Available Days

**Problem:** Write an SQL query to find all dates' Ids with consecutive available dates in the `availability` table.

**Solution:**
```sql
SELECT a.id
FROM availability a
JOIN availability b ON DATE_ADD(a.date, INTERVAL 1 DAY) = b.date;
```
**Explanation:** This query finds dates that have the next day also available by joining the table with itself on the date condition.

### Problem 9: Median Salary

**Problem:** Write an SQL query to find the median salary of the `employees` table.

**Solution:**
```sql
SELECT salary
FROM (
  SELECT salary, ROW_NUMBER() OVER (ORDER BY salary) AS row_num, COUNT(*) OVER () AS total_rows
  FROM employees
) AS subquery
WHERE row_num IN (total_rows / 2, total_rows / 2 + 1);
```
**Explanation:** This query calculates the median salary by ordering the salaries and finding the middle value(s).

### Problem 10: Manager with the Most Employees

**Problem:** Write an SQL query to find the manager who has the most employees reporting to them.

**Solution:**
```sql
SELECT manager_id, COUNT(*) AS employee_count
FROM employees
GROUP BY manager_id
ORDER BY employee_count DESC
LIMIT 1;
```
**Explanation:** This query groups employees by their manager, counts the number of employees per manager, and selects the manager with the highest count.

### Problem 11: Employee Hire Duration

**Problem:** Write an SQL query to calculate the duration each employee has been hired in days.

**Solution:**
```sql
SELECT name, DATEDIFF(CURRENT_DATE, hire_date) AS hire_duration
FROM employees;
```
**Explanation:** This query calculates the number of days each employee has been hired by subtracting the hire date from the current date.

### Problem 12: Find Employees with Nth Highest Salary

**Problem:** Write an SQL query to find the employee with the nth highest salary.

**Solution:**
```sql
SET @n := 2;  -- Replace 2 with the desired rank
SELECT name, salary
FROM (
  SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rank
  FROM employees
) AS ranked
WHERE salary_rank = @n;
```
**Explanation:** This query ranks salaries and selects the employee with the nth highest salary.

### Problem 13: Common Employees Between Two Departments

**Problem:** Write an SQL query to find employees who work in both department A and department B.

**Solution:**
```sql
SELECT DISTINCT e1.employee_id
FROM department_employee e1
JOIN department_employee e2 ON e1.employee_id = e2.employee_id
WHERE e1.department_id = 'A' AND e2.department_id = 'B';
```
**Explanation:** This query finds employees who are listed in both department A and department B by joining the table with itself.

### Problem 14: Find Missing Dates

**Problem:** Write an SQL query to find missing dates in a sequence of dates.

**Solution:**
```sql
SELECT a.date + INTERVAL 1 DAY AS missing_date
FROM dates a
LEFT JOIN dates b ON a.date + INTERVAL 1 DAY = b.date
WHERE b.date IS NULL;
```
**Explanation:** This query finds dates where the next day is missing by performing a left join with the date incremented by one day.

### Problem 15: Employees with Highest Salary in Each Department

**Problem:** Write an SQL query to find employees with the highest salary in each department.

**Solution:**
```sql
SELECT department_id, name, salary
FROM employees e
WHERE salary = (SELECT MAX(salary)
                FROM employees
                WHERE department_id = e.department_id);
```
**Explanation:** This query selects employees whose salary is the maximum within their department.

### Problem 16: Recursive Query to Find Ancestors

**Problem:** Write an SQL query using recursive CTEs to find all ancestors of a given employee.

**Solution:**
```sql
WITH RECURSIVE ancestors AS (
  SELECT id, manager_id
  FROM employees
  WHERE id = 1  -- Replace 1 with the employee's ID
  UNION
  SELECT e.id, e.manager_id
  FROM employees e
  JOIN ancestors a ON e.id = a.manager_id
)
SELECT id
FROM ancestors;
```
**Explanation:** This query uses a recursive CTE to find all ancestors of a given employee by repeatedly joining the employees table with itself.

### Problem 17: Calculate Running Total

**Problem:** Write an SQL query to calculate the running total of employee salaries.

**Solution:**
```sql
SELECT name, salary, SUM(salary) OVER (ORDER BY hire_date) AS running_total
FROM employees;
```
**Explanation:** This query calculates a running total of salaries ordered by hire date using the `SUM()` window function.

### Problem 18: Find Orphaned Records

**Problem:** Write an SQL query to find employees without a manager.

**Solution:**
```sql
SELECT id, name
FROM employees
WHERE manager_id IS NULL;
```
**Explanation:** This query selects employees whose `manager_id` is null, indicating they have no manager.

### Problem 19: Get Top N Employees by Department

**Problem:** Write an SQL query to get the top N employees with the highest salaries in each department.

**Solution:**
```sql
SET @n := 3;  -- Replace 3 with the desired number of top employees
SELECT department_id, name, salary
FROM (
  SELECT department_id, name, salary, RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dept_rank
  FROM employees
) AS ranked
WHERE dept_rank <= @n;
```
**Explanation:** This query ranks employees by salary within each department and selects the top N employees per department.

### Problem 20: Pivot Table

**Problem:** Write an SQL query to pivot a table to show employee names as columns and their salaries as rows.

**Solution:**
```sql
SELECT 
  'Salaries' AS Description,
  MAX(CASE WHEN name = 'Alice' THEN salary END) AS Alice,
  MAX(CASE WHEN name = 'Bob' THEN salary END) AS Bob,
  MAX(CASE WHEN name = 'Charlie' THEN salary END) AS Charlie
FROM employees;
```
**Explanation:** This query uses conditional aggregation to pivot employee names as columns and display their corresponding salaries.

These explanations should help you understand the logic behind each solution and prepare effectively for your MySQL interview.