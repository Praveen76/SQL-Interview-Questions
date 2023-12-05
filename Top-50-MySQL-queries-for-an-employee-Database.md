# Q1. Top 50 MySQL queries along with answers for an employee Database?
Ans: For a Data Scientist interview focusing on MySQL queries for an employee database, you can expect questions related to data retrieval, filtering, aggregation, and data manipulation. Here are 50 MySQL queries along with answers that cover a variety of scenarios you might encounter in such an interview:

**1. Retrieve all employees from the "employees" table.**
```sql
SELECT * FROM employees;
```

**2. Retrieve the first name and last name of all employees.**
```sql
SELECT first_name, last_name FROM employees;
```

**3. Retrieve the employee with ID 101.**
```sql
SELECT * FROM employees WHERE employee_id = 101;
```

**4. Retrieve employees who have a salary greater than $50,000.**
```sql
SELECT * FROM employees WHERE salary > 50000;
```

**5. Retrieve employees who work in the "Sales" department.**
```sql
SELECT * FROM employees WHERE department = 'Sales';
```

**6. Retrieve the total number of employees.**
```sql
SELECT COUNT(*) AS total_employees FROM employees;
```

**7. Retrieve the highest salary in the company.**
```sql
SELECT MAX(salary) AS highest_salary FROM employees;
```

**8. Retrieve the lowest salary in the company.**
```sql
SELECT MIN(salary) AS lowest_salary FROM employees;
```

**9. Calculate the average salary of all employees.**
```sql
SELECT AVG(salary) AS average_salary FROM employees;
```

**10. Retrieve employees whose names start with 'A'.**
```sql
SELECT * FROM employees WHERE first_name LIKE 'A%';
```

**11. Retrieve employees who were hired in 2022.**
```sql
SELECT * FROM employees WHERE YEAR(hire_date) = 2022;
```

**12. Retrieve employees who are not in the "HR" department.**
```sql
SELECT * FROM employees WHERE department != 'HR';
```

**13. Retrieve employees sorted by their salary in descending order.**
```sql
SELECT * FROM employees ORDER BY salary DESC;
```

**14. Retrieve the top 5 highest-paid employees.**
```sql
SELECT * FROM employees ORDER BY salary DESC LIMIT 5;
```

**15. Calculate the total salary expenses for the company.**
```sql
SELECT SUM(salary) AS total_salary_expense FROM employees;
```

**16. Retrieve employees grouped by department.**
```sql
SELECT department, COUNT(*) AS employee_count FROM employees GROUP BY department;
```

**17. Retrieve the department with the highest number of employees.**
```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
ORDER BY employee_count DESC
LIMIT 1;
```

**18. Retrieve employees who have a manager (manager_id is not NULL).**
```sql
SELECT * FROM employees WHERE manager_id IS NOT NULL;
```

**19. Retrieve employees who do not have a manager (manager_id is NULL).**
```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

**20. Retrieve the average salary for each department.**
```sql
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

**21. Retrieve employees who have the same manager (e.g., manager_id = 105).**
```sql
SELECT * FROM employees WHERE manager_id = 105;
```

**22. Calculate the difference between the highest and lowest salaries in the company.**
```sql
SELECT MAX(salary) - MIN(salary) AS salary_range FROM employees;
```

**23. Retrieve employees who joined the company after 01-Jan-2020.**
```sql
SELECT * FROM employees WHERE hire_date > '2020-01-01';
```

**24. Retrieve employees who are paid a bonus (bonus is not NULL).**
```sql
SELECT * FROM employees WHERE bonus IS NOT NULL;
```

**25. Retrieve employees who are paid a bonus less than or equal to $2,000.**
```sql
SELECT * FROM employees WHERE bonus <= 2000;
```

**26. Retrieve the average bonus for employees in the "Sales" department.**
```sql
SELECT AVG(bonus) AS avg_bonus
FROM employees
WHERE department = 'Sales';
```

**27. Retrieve employees who are in the "Engineering" department and have a salary greater than $60,000.**
```sql
SELECT * FROM employees WHERE department = 'Engineering' AND salary > 60000;
```

**28. Retrieve employees who have joined in 2022 and are in the "Marketing" department.**
```sql
SELECT * FROM employees WHERE YEAR(hire_date) = 2022 AND department = 'Marketing';
```

**29. Retrieve the employee with the highest salary in the "HR" department.**
```sql
SELECT * FROM employees WHERE department = 'HR' ORDER BY salary DESC LIMIT 1;
```

**30. Retrieve employees who were hired before 01-Jan-2010 and after 31-Dec-2021.**
```sql
SELECT * FROM employees WHERE hire_date < '2010-01-01' OR hire_date > '2021-12-31';
```

**31. Retrieve employees whose first name is either "John" or "Jane".**
```sql
SELECT * FROM employees WHERE first_name IN ('John', 'Jane');
```

**32. Calculate the average salary for male employees and female employees.**
```sql
SELECT gender, AVG(salary) AS average_salary
FROM employees
GROUP BY gender;
```

**33. Retrieve employees whose salaries are in the top 10% of the company.**
```sql
SELECT * FROM employees WHERE salary >= (SELECT 0.9 * MAX(salary) FROM employees);
```

**34. Calculate the total salary expenses for each department.**
```sql
SELECT department, SUM(salary) AS total_salary_expense
FROM employees
GROUP BY department;
```

**35. Retrieve employees who have the same first name as their manager.**
```sql
SELECT e.* FROM employees e
JOIN employees m ON e.manager_id = m.employee_id
WHERE e.first_name = m.first_name;
```

**36. Retrieve the employee with the second-highest salary.**
```sql
SELECT * FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

**37. Calculate the average years of experience (tenure) for each department.**
```sql
SELECT department, AVG(YEAR(NOW()) - YEAR(hire_date)) AS avg_tenure
FROM employees
GROUP BY department;
```

**38. Retrieve employees who have been with the company for more than 5 years.**
```sql
SELECT * FROM employees WHERE YEAR(NOW()) - YEAR(hire_date) > 5;
```

**39. Retrieve employees who do not belong to any department (department is NULL).**
```sql
SELECT * FROM employees WHERE department IS NULL;
```

**40. Retrieve the employees with the three highest salaries in each department.**
```sql
SELECT department, first_name, last_name, salary
FROM (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
  FROM employees
) ranked
WHERE rank <= 3;
```

**41. Retrieve the employee with the highest salary in each department.**
```sql


SELECT department, first_name, last_name, salary
FROM (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
  FROM employees
) ranked
WHERE rank = 1;
```

**42. Calculate the total number of employees in each department.**
```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

**43. Retrieve employees who earn more than the average salary in their respective departments.**
```sql
SELECT e.*
FROM employees e
JOIN (
  SELECT department, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY department
) dept_avg ON e.department = dept_avg.department
WHERE e.salary > dept_avg.avg_salary;
```

**44. Retrieve the employee with the highest salary in each gender category.**
```sql
SELECT gender, first_name, last_name, salary
FROM (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY gender ORDER BY salary DESC) AS rank
  FROM employees
) ranked
WHERE rank = 1;
```

**45. Retrieve employees with the same last name but different first names.**
```sql
SELECT e1.*
FROM employees e1
JOIN employees e2 ON e1.last_name = e2.last_name
WHERE e1.first_name != e2.first_name;
```

**46. Retrieve employees with a salary that is not an even multiple of 1000 (e.g., not $40,000, $42,000, etc.).**
```sql
SELECT * FROM employees WHERE MOD(salary, 1000) != 0;
```

**47. Retrieve employees who have the same salary as their manager.**
```sql
SELECT e.*
FROM employees e
JOIN employees m ON e.manager_id = m.employee_id
WHERE e.salary = m.salary;
```

**48. Calculate the difference in salary between each employee and their manager.**
```sql
SELECT e.first_name, e.last_name, e.salary, m.first_name AS manager_first_name, m.last_name AS manager_last_name, m.salary AS manager_salary, e.salary - m.salary AS salary_difference
FROM employees e
JOIN employees m ON e.manager_id = m.employee_id;
```

**49. Retrieve employees who have joined in the same year as their manager.**
```sql
SELECT e.*
FROM employees e
JOIN employees m ON e.manager_id = m.employee_id
WHERE YEAR(e.hire_date) = YEAR(m.hire_date);
```

**50. Retrieve employees who have the same manager as their spouse (assuming there is a "spouse_id" field).**
```sql
SELECT e.first_name, e.last_name, e.manager_id AS employee_manager_id, s.first_name AS spouse_first_name, s.last_name AS spouse_last_name, s.manager_id AS spouse_manager_id
FROM employees e
JOIN employees s ON e.spouse_id = s.employee_id AND e.manager_id = s.manager_id;
```

These MySQL queries cover a wide range of scenarios you might encounter when working with an employee database, and they should help you prepare for a data scientist interview that includes SQL questions.