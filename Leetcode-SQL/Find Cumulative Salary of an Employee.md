# Find Cumulative Salary of an Employee

579 ***
####  MySQL
- recent 3 months and get rid of the most recent month
```
SELECT A.Id, 
	MAX(B.Month) as Month, 
	SUM(B.Salary) as Salary
FROM Employee A, Employee B
WHERE A.Id = B.Id 
	AND B.Month BETWEEN (A.Month-3) AND (A.Month-1)
GROUP BY A.Id, A.Month
ORDER BY Id, Month DESC
```
####  MSSQL
- Every 3 months. ROWS 2 PRECEDING indicates the number of rows or values to precede the current row (1 + 2)
```
SELECT id, month, Salary
FROM
(SELECT  id, month,
        SUM(salary) 
        OVER(PARTITION BY id  ORDER BY month 
        ROWS 2 PRECEDING) as Salary, 
        DENSE_RANK() 
        OVER(PARTITION BY id ORDER by month DESC) 
        as month_no
FROM Employee
) tmp
#exclude the most recent month
where month_no > 1 
ORDER BY id , month desc
```