Here are some MySQL problems with their solutions, arranged from simple to advanced levels:

### Simple Problems:
1. **Create a Database**
   - **Problem:** Create a database named `company`.
   - **Solution:**
     ```sql
     CREATE DATABASE company;
     ```

2. **Create a Table**
   - **Problem:** Create a table named `employees` with columns `id`, `name`, `position`, and `salary`.
   - **Solution:**
     ```sql
     CREATE TABLE employees (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       position VARCHAR(50) NOT NULL,
       salary DECIMAL(10, 2) NOT NULL
     );
     ```

3. **Insert Data into a Table**
   - **Problem:** Insert the following data into the `employees` table:
     ```
     | id | name     | position | salary  |
     |----|----------|----------|---------|
     | 1  | John Doe | Manager  | 75000.00|
     | 2  | Jane Doe | Developer| 65000.00|
     ```
   - **Solution:**
     ```sql
     INSERT INTO employees (name, position, salary) VALUES
     ('John Doe', 'Manager', 75000.00),
     ('Jane Doe', 'Developer', 65000.00);
     ```

4. **Select Data from a Table**
   - **Problem:** Select all columns from the `employees` table.
   - **Solution:**
     ```sql
     SELECT * FROM employees;
     ```

5. **Update Data in a Table**
   - **Problem:** Update the salary of `John Doe` to `80000.00`.
   - **Solution:**
     ```sql
     UPDATE employees
     SET salary = 80000.00
     WHERE name = 'John Doe';
     ```

### Intermediate Problems:
6. **Delete Data from a Table**
   - **Problem:** Delete the record of `Jane Doe` from the `employees` table.
   - **Solution:**
     ```sql
     DELETE FROM employees
     WHERE name = 'Jane Doe';
     ```

7. **Using JOIN to Combine Data from Two Tables**
   - **Problem:** Given a table `departments` with the following structure:
     ```sql
     CREATE TABLE departments (
       dept_id INT PRIMARY KEY,
       dept_name VARCHAR(100) NOT NULL
     );
     ```
     And the following data:
     ```sql
     INSERT INTO departments (dept_id, dept_name) VALUES
     (1, 'HR'),
     (2, 'Engineering');
     ```
     Write a query to join `employees` and `departments` tables on `position` to get department names.
   - **Solution:**
     ```sql
     SELECT e.name, e.position, d.dept_name
     FROM employees e
     JOIN departments d ON e.position = d.dept_name;
     ```

8. **Using GROUP BY with Aggregate Functions**
   - **Problem:** Find the total salary paid for each position in the `employees` table.
   - **Solution:**
     ```sql
     SELECT position, SUM(salary) AS total_salary
     FROM employees
     GROUP BY position;
     ```

9. **Using Subqueries**
   - **Problem:** Find the name of the employee with the highest salary.
   - **Solution:**
     ```sql
     SELECT name
     FROM employees
     WHERE salary = (SELECT MAX(salary) FROM employees);
     ```

10. **Using HAVING with GROUP BY**
    - **Problem:** Find the positions with a total salary greater than `100000.00`.
    - **Solution:**
      ```sql
      SELECT position, SUM(salary) AS total_salary
      FROM employees
      GROUP BY position
      HAVING total_salary > 100000.00;
      ```

### Advanced Problems:
11. **Using Transactions**
    - **Problem:** Write a transaction to insert a new employee and update the salary of an existing employee.
    - **Solution:**
      ```sql
      START TRANSACTION;
      INSERT INTO employees (name, position, salary) VALUES ('Alice Smith', 'Developer', 70000.00);
      UPDATE employees SET salary = 82000.00 WHERE name = 'John Doe';
      COMMIT;
      ```

12. **Creating and Using Stored Procedures**
    - **Problem:** Create a stored procedure to add a new employee.
    - **Solution:**
      ```sql
      DELIMITER //
      CREATE PROCEDURE AddEmployee(IN name VARCHAR(100), IN position VARCHAR(50), IN salary DECIMAL(10, 2))
      BEGIN
        INSERT INTO employees (name, position, salary) VALUES (name, position, salary);
      END //
      DELIMITER ;
      ```

13. **Creating and Using Triggers**
    - **Problem:** Create a trigger that automatically logs changes to the `employees` table into a `employee_changes` table.
    - **Solution:**
      ```sql
      CREATE TABLE employee_changes (
        change_id INT AUTO_INCREMENT PRIMARY KEY,
        employee_id INT,
        change_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        old_salary DECIMAL(10, 2),
        new_salary DECIMAL(10, 2)
      );

      DELIMITER //
      CREATE TRIGGER log_salary_change
      BEFORE UPDATE ON employees
      FOR EACH ROW
      BEGIN
        IF OLD.salary != NEW.salary THEN
          INSERT INTO employee_changes (employee_id, old_salary, new_salary)
          VALUES (OLD.id, OLD.salary, NEW.salary);
        END IF;
      END //
      DELIMITER ;
      ```

14. **Optimizing Queries with Indexes**
    - **Problem:** Create an index on the `salary` column of the `employees` table.
    - **Solution:**
      ```sql
      CREATE INDEX idx_salary ON employees(salary);
      ```

15. **Using Full-Text Search**
    - **Problem:** Add full-text search capability to the `employees` table for the `name` and `position` columns.
    - **Solution:**
      ```sql
      ALTER TABLE employees ADD FULLTEXT(name, position);

      SELECT * FROM employees
      WHERE MATCH(name, position) AGAINST('Developer');
      ```

### Complex Problems:
16. **Creating Views**
    - **Problem:** Create a view `high_salary_employees` that shows employees with salaries greater than `70000.00`.
    - **Solution:**
      ```sql
      CREATE VIEW high_salary_employees AS
      SELECT name, position, salary
      FROM employees
      WHERE salary > 70000.00;
      ```

17. **Advanced Subqueries with Joins**
    - **Problem:** Find the names of employees who earn more than the average salary of their respective positions.
    - **Solution:**
      ```sql
      SELECT name, position, salary
      FROM employees e1
      WHERE salary > (SELECT AVG(salary)
                      FROM employees e2
                      WHERE e1.position = e2.position);
      ```

18. **Partitioning Tables**
    - **Problem:** Partition the `employees` table by `position`.
    - **Solution:**
      ```sql
      ALTER TABLE employees
      PARTITION BY HASH(position) PARTITIONS 4;
      ```

19. **Handling Recursive Queries**
    - **Problem:** Create a table `employee_hierarchy` to manage employee hierarchies and write a query to get all subordinates of a given employee.
    - **Solution:**
      ```sql
      CREATE TABLE employee_hierarchy (
        emp_id INT,
        manager_id INT
      );

      INSERT INTO employee_hierarchy (emp_id, manager_id) VALUES
      (1, NULL), -- CEO
      (2, 1),
      (3, 1),
      (4, 2),
      (5, 2);

      -- Recursive query using CTE (Common Table Expressions) in MySQL 8.0+
      WITH RECURSIVE subordinates AS (
        SELECT emp_id, manager_id
        FROM employee_hierarchy
        WHERE manager_id = 1
        UNION ALL
        SELECT e.emp_id, e.manager_id
        FROM employee_hierarchy e
        INNER JOIN subordinates s ON s.emp_id = e.manager_id
      )
      SELECT emp_id FROM subordinates;
      ```

20. **Using JSON Data Type**
    - **Problem:** Create a table with a JSON column and write a query to extract a specific value from the JSON data.
    - **Solution:**
      ```sql
      CREATE TABLE employee_info (
        id INT PRIMARY KEY,
        details JSON
      );

      INSERT INTO employee_info (id, details) VALUES
      (1, '{"name": "John Doe", "position": "Manager", "salary": 75000}'),
      (2, '{"name": "Jane Doe", "position": "Developer", "salary": 65000}');

      SELECT details->>'$.name' AS name, details->>'$.position' AS position
      FROM employee_info;
      ```

These problems and solutions will help you get a good understanding of MySQL and prepare for your interview. Good luck!