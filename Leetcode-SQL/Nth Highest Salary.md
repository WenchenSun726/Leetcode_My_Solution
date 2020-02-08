# Nth Highest Salary

177
####  MySQL
- offset (n-1) is not allowed in MYSQL, need to defind a new variable
- Declare variable type;
	Set variable ;
```mysql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN

DECLARE M INT;
SET M = N-1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT (SELECT DISTINCT Salary FROM Employee 
      ORDER BY Salary DESC LIMIT M,1)
  );
END
```
####  MSSQL
- DENSE_RANK() OVER()
```mssql
CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
    RETURN (
       /* Write your T-SQL query statement below. */
       SELECT DISTINCT Salary 
       FROM (
       SELECT dense_rank() OVER (ORDER BY Salary DESC) 
       AS rank, Salary FROM Employee) AS a
       WHERE rank = @N
    );
END
```