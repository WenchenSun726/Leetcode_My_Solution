# Report Contiguous Dates
1225

- CTE and window function 

#### MSSQL
- union all dates of fail and success in specific date period
- assign row_number() based on state
- **roup by state, datediff(day, rnk, date)** - similar with id-row_number() as a primary key - row_number()
```
With date AS
((SELECT 'failed' AS period_state , fail_date AS date
FROM Failed
WHERE fail_date BETWEEN '2019-01-01' AND '2019-12-31')
UNION ALL
(SELECT 'succeeded' AS period_state , success_date AS date
FROM Succeeded
WHERE success_date BETWEEN '2019-01-01' AND '2019-12-31')), 

rank AS (
SELECT *, row_number() OVER(PARTITION BY period_state ORDER BY date) AS rnk
FROM date)

SELECT period_state, MIN(date) AS start_date, MAX(date)AS end_date
FROM rank
GROUP BY period_state, DATEDIFF(day, rnk ,date)
ORDER BY 2
```