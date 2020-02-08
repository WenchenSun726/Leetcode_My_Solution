# Restaurant Growth
1321

- CTE and window function 

#### MSSQL
- calculate daily sum
- find last 6 days sum using window function (ROWS BETWEEN 6 PRECEDING AND CURRENT)
- ORDER BY + OFFSET to delete first 6 rows
```
WITH total AS (
SELECT visited_on, SUM(amount) AS total
FROM Customer
GROUP BY visited_on),
tmp AS (
SELECT visited_on, SUM(total) OVER(ORDER BY visited_on Rows between 6 PRECEDING and current row) AS amount
FROM total)

SELECT visited_on, amount, round(cast((amount/7.0) AS FLOAT),2) AS average_amount
FROM tmp
ORDER BY visited_on offset 6 rows

```