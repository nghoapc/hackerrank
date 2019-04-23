# Problem:

### A company stores employee and department information in two data tables: Employee and Department. Write a query to print the respective department name and number of employees in each department for all departments in the Department table (even ones with no current employees). Sort the results by descending order of the number of employees; if two or more departments have the same number of employees, then sort those departments alphabetically by department name. Each row of the resulting output must contain the following respective attributes for a department: The name of the department The number of employees in the department DEPARTMENT.NAME COUNT_OF_EMPLOYEES_IN_THE_DEPARTMENT


```sh
SELECT DEPARTMENT.NAME, COUNT(EMPLOYEE.ID) AS COUNT_OF_EMPLOYEES_IN_DEPARTMENT
    FROM DEPARTMENT
    LEFT JOIN EMPLOYEE ON DEPARTMENT.ID = EMPLOYEE.DEPT_ID
    GROUP BY DEPARTMENT.NAME
    ORDER BY COUNT_OF_EMPLOYEES_IN_DEPARTMENT DESC, DEPARTMENT.NAME ASC
```