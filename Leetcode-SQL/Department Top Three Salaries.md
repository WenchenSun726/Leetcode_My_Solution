# Department Top Three Salaries

185
####  MySQL

- Correlated Query - similar with 178
- too complex than dense_rank() ... just to get familar with correlated query
```mysql
SELECT d.Name as Department, 
	e.Name as Employee, 
	e.Salary as Salary
FROM Department as d 
	join Employee as e on d.Id = e.DepartmentId
WHERE 3 >   
    (SELECT COUNT(DISTINCT e1.Salary) 
    FROM Employee as e1 
    WHERE e1.DepartmentId = d.Id and e1.Salary > e.Salary)
ORDER BY Department, Salary DESC
```
####  MSSQL
- DENSE_RANK() OVER()
```mssql
SELECT d.Name AS Department, 
	e.Name AS Employee, Salary
FROM (
    SELECT Name, Salary, 
    DepartmentId, dense_rank() 
    OVER(PARTITION BY DepartmentId ORDER BY Salary DESC) 
    AS Rank
    FROM Employee) e 
    JOIN Department d on e.DepartmentId = d.Id
WHERE Rank in (1,2,3)
```