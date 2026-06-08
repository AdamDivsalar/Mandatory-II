# Mandatory I - Tech Company

**Deadline**: This is mandatory I and the deadline is in `itslearning`. Mandatories are prerequisites to go to the exam.

**Hand-in**: `itslearning`, hand in a link to the SQL file in any Git repository. There will be peer assessment after the deadline.

Late hand-ins are only accepted the Assignment channel in the Teams room.

> **Bemærkning:** Jeg har kørt `tech_company.sql` op mod en `tech_company` database og skrevet mine queries i MySQL CLI. Svarene står under hvert spørgsmål. Et par steder var jeg lidt usikker på `WHERE` vs. `HAVING` og på hvordan NULL opfører sig i joins, men jeg fik det til at give mening til sidst.

---

## Single Table Assignments

1. Find the employee number for employees named `MARTIN`.

```sql
SELECT employee_number
FROM employees
WHERE employee_name = 'MARTIN';
```

2. Find the employee(s) with a salary greater than 1500.

```sql
SELECT employee_name, salary
FROM employees
WHERE salary > 1500;
```

3. List the names of salesmen that earn more than 1300.

```sql
SELECT employee_name
FROM employees
WHERE job_title = 'SALESMAN'
  AND salary > 1300;
```

4. List the names of employees that are not salesmen.

```sql
SELECT employee_name
FROM employees
WHERE job_title <> 'SALESMAN';
```

5. List the names of all clerks together with their salary with a deduction of 10%.

```sql
SELECT employee_name, salary * 0.9 AS reduced_salary
FROM employees
WHERE job_title = 'CLERK';
```

6. Find the name of employees hired before May 1981.

```sql
SELECT employee_name, hire_date
FROM employees
WHERE hire_date < '1981-05-01';
```

7. List employees sorted by salary in descending order (i.e. highest salary first).

```sql
SELECT employee_name, salary
FROM employees
ORDER BY salary DESC;
```

8. List departments sorted by location.

```sql
SELECT *
FROM departments
ORDER BY office_location;
```

9. Find name of the department located in New York.

```sql
SELECT department_name
FROM departments
WHERE office_location = 'NEW YORK';
```

10. You have proven your worth at the company. Your colleague comes to you trying to remember `what's-his-name`. It starts with a `J` and ends with `S`. Can you help her?

```sql
SELECT employee_name
FROM employees
WHERE employee_name LIKE 'J%S';
```

<!-- Giver to navne: JONES og JAMES. -->

11. Maybe that wasn't helpful. "Oh yeah, I remember now!" they say and tell you that he is a manager.

```sql
SELECT employee_name
FROM employees
WHERE employee_name LIKE 'J%S'
  AND job_title = 'MANAGER';
```

<!-- Nu står kun JONES tilbage. -->

12. How many employees are there in each department?

```sql
SELECT department_number, COUNT(*) AS number_of_employees
FROM employees
GROUP BY department_number;
```

<!--
KING har department_number = NULL, så han havner i sin egen gruppe.
Department 40 (OPERATIONS) har ingen ansatte og dukker derfor slet ikke op her,
fordi vi kun tæller rækker i employees. Det kommer igen i JOIN-opgaverne.
-->

---

## Aggregate functions

1. For the first assignment, take on the hat of a Data Analyst. You've been tasked to create a summary of interesting data.

```sql
SELECT
    MIN(salary)  AS lowest_salary,
    MAX(salary)  AS highest_salary,
    AVG(salary)  AS average_salary,
    SUM(salary)  AS total_salary
FROM employees
WHERE salary BETWEEN 800 AND 5000;
```

<!-- Hele lønspændet ligger mellem 800 (SMITH) og 5000 (KING), så BETWEEN dækker alle. -->

2. List the number of employees.

```sql
SELECT COUNT(*) AS number_of_employees
FROM employees;
```

3. List the sum of all salaries (excluding commission which are bonuses added to the base salaries).

```sql
SELECT SUM(salary) AS total_base_salary
FROM employees;
```

4. List the average salary for employees in department 20.

```sql
SELECT AVG(salary) AS avg_salary_dept_20
FROM employees
WHERE department_number = 20;
```

5. List the unique job titles in the company.

```sql
SELECT DISTINCT job_title
FROM employees;
```

6. List the number of employees in each department.

```sql
SELECT department_number, COUNT(*) AS number_of_employees
FROM employees
GROUP BY department_number;
```

7. List in decreasing order the maximum salary in each department together with the department number.

```sql
SELECT department_number, MAX(salary) AS max_salary
FROM employees
GROUP BY department_number
ORDER BY max_salary DESC;
```

8. List total sum of salary and commission for all employees.

```sql
SELECT SUM(salary) + SUM(COALESCE(commission, 0)) AS total_pay
FROM employees;
```

<!--
Commission er NULL for de fleste. Hvis man bare skriver SUM(salary + commission)
ryger de rækker ud hvor commission er NULL, så jeg pakker commission ind i
COALESCE(commission, 0), så NULL bliver behandlet som 0.
-->

9. Subquery time! Select the name and salary of employees whose salary is above average.

```sql
SELECT employee_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

## JOIN Assignments

1. Create an `INNER JOIN` between `employees` and `departments` to get the department name for each employee. Show all columns.

```sql
SELECT *
FROM employees
INNER JOIN departments
    ON employees.department_number = departments.department_number;
```

2. Continue from the last task. Show two columns. The `employee_name` and their corresponding `department_name`. Oh, and can you sort them alphabetically (A-Z)?

```sql
SELECT employees.employee_name, departments.department_name
FROM employees
INNER JOIN departments
    ON employees.department_number = departments.department_number
ORDER BY employees.employee_name ASC;
```

3. Now is the time to make a LEFT JOIN. Let's look at `employee_name` and `department_name` only. There is one more person this time who didn't show in the previous query. Who is it and why?

```sql
SELECT employees.employee_name, departments.department_name
FROM employees
LEFT JOIN departments
    ON employees.department_number = departments.department_number;
```

<!--
Den ekstra person er KING. Hans department_number er NULL, så der findes ingen
matchende række i departments. Ved INNER JOIN forsvinder rækker uden match, men
LEFT JOIN beholder alle rækker fra venstre tabel (employees) og sætter bare
department_name til NULL når der ikke er match.
-->

4. Consider this query. One department is missing. Which one and why? (Look in the database).

```sql
SELECT departments.department_name, COUNT(employees.employee_number)
FROM employees
JOIN departments
    ON departments.department_number = employees.department_number
GROUP BY department_name;
```

<!--
OPERATIONS (department 40) mangler. Der er ingen ansatte i department 40, så ved
en almindelig (INNER) JOIN findes der ingen rækker at matche på, og afdelingen
falder helt ud af resultatet.
-->

5. To get the missing department change the previous query to use a RIGHT JOIN.

```sql
SELECT departments.department_name, COUNT(employees.employee_number)
FROM employees
RIGHT JOIN departments
    ON departments.department_number = employees.department_number
GROUP BY department_name;
```

<!--
RIGHT JOIN beholder alle rækker fra departments (højre tabel), også dem uden
ansatte. OPERATIONS kommer nu med og får COUNT = 0, fordi COUNT(employee_number)
ikke tæller NULL-værdier.
-->

6. `SCOTT` sends you this query and asks you to run it. Describe in technical terms what this query does:

```sql
SELECT *
FROM employees employee
JOIN employees manager
    ON employee.manager_id = manager.employee_number
ORDER BY employee.employee_name;
```

<!--
Det er en self join: employees joines med sig selv via to aliaser, "employee" og
"manager". For hver medarbejder slås manager_id op mod employee_number i den anden
kopi af tabellen, så man får medarbejderen ved siden af den person der er deres
chef. Resultatet sorteres alfabetisk på medarbejderens navn. Da det er en INNER
JOIN falder KING ud, fordi hans manager_id er NULL (han er PRESIDENT og har ingen
chef).
-->

7. Get two columns: employees and their managers.

```sql
SELECT employee.employee_name AS employee, manager.employee_name AS manager
FROM employees employee
LEFT JOIN employees manager
    ON employee.manager_id = manager.employee_number
ORDER BY employee.employee_name;
```

<!--
Jeg bruger LEFT JOIN i stedet for INNER, så KING også kommer med (med manager =
NULL). Hvis man kun vil have dem der faktisk har en chef, kan man bruge INNER JOIN.
-->

8. Use the `HAVING` keyword to show the departments with more than 3 employees.

```sql
SELECT department_number, COUNT(department_number) AS number_of_employees
FROM employees
GROUP BY department_number
HAVING COUNT(department_number) > 3;
```

<!--
HAVING filtrerer EFTER GROUP BY (på de aggregerede grupper), hvor WHERE filtrerer
FØR grupperingen på de enkelte rækker. Her giver det department 20 (5 ansatte) og
department 30 (6 ansatte).
-->

---

## Join Table (Many-to-many)

1. Create a new table called `leaders` and insert rows into it.

```sql
CREATE TABLE leaders (
    leader_number INTEGER PRIMARY KEY,
    leader_name   VARCHAR(30)
);

INSERT INTO leaders (leader_number, leader_name) VALUES (1, 'KING');
INSERT INTO leaders (leader_number, leader_name) VALUES (2, 'JONES');
INSERT INTO leaders (leader_number, leader_name) VALUES (3, 'BLAKE');
```

2. Create a new table called `employees_leaders` that links the `employees` and `leaders` tables (join table, many-to-many).

```sql
CREATE TABLE employees_leaders (
    employee_number INT,
    leader_number   INT,
    PRIMARY KEY (employee_number, leader_number),
    FOREIGN KEY (employee_number) REFERENCES employees(employee_number),
    FOREIGN KEY (leader_number)   REFERENCES leaders(leader_number)
);
```

<!--
Den sammensatte primærnøgle (employee_number, leader_number) sikrer at den samme
kobling ikke kan stå to gange. De to fremmednøgler binder rækken op mod henholdsvis
employees og leaders.
-->

3. Create rows in `employees_leaders` that link employees to their respective leaders.

```sql
-- SMITH har to ledere (viser many-to-many: en medarbejder kan have flere ledere)
INSERT INTO employees_leaders (employee_number, leader_number) VALUES (7369, 1);
INSERT INTO employees_leaders (employee_number, leader_number) VALUES (7369, 2);

-- ALLEN og WARD deler en leder (en leder kan have flere medarbejdere)
INSERT INTO employees_leaders (employee_number, leader_number) VALUES (7499, 3);
INSERT INTO employees_leaders (employee_number, leader_number) VALUES (7521, 3);

-- SCOTT under JONES
INSERT INTO employees_leaders (employee_number, leader_number) VALUES (7788, 2);
```

4. Create a many-to-many query between employees and leaders. It requires two JOIN statements.

```sql
SELECT employees.employee_name, leaders.leader_name
FROM employees
JOIN employees_leaders
    ON employees.employee_number = employees_leaders.employee_number
JOIN leaders
    ON employees_leaders.leader_number = leaders.leader_number
ORDER BY employees.employee_name;
```

<!--
Man starter i employees, hopper via join-tabellen employees_leaders over i leaders.
Fordi koblingerne ligger i en separat tabel, kan både "en medarbejder med flere
ledere" og "en leder med flere medarbejdere" lade sig gøre på samme tid.
-->
