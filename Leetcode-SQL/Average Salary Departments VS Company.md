# Average Salary: Departments VS Company

615

- avg salary of company for each month
- avg salary of department for each month
- compare
- month: LEFT(a, 7) / DATE_FORMAT(a, '%Y-%m')
####  MySQL
```
SELECT A.pay_month, A.department_id, 
CASE WHEN A.dep_avg > B.com_avg THEN "higher"
    When A.dep_avg = B.com_avg THEN "same"
    Else "lower"
End AS 'comparison'
FROM (SELECT e1.department_id, AVG(s1.amount) as dep_avg, date_format(pay_date, '%Y-%m') as pay_month FROM salary AS s1 JOIN employee AS e1 using (employee_id)
GROUP BY e1.department_id, pay_month) as A 
JOIN
(SELECT AVG(amount) AS com_avg, date_format(pay_date, '%Y-%m') as pay_month
FROM salary 
GROUP BY pay_month) AS B
on A.pay_month = B.pay_month
ORDER BY a.pay_month DESC, a.department_id;
```
#### MSSQL
- 
```
select t.pay_month, t.department_id, 
	case when avg1=avg2 then 'same' 
		when avg1>avg2 then 'higher' else 'lower' 
		end as comparison
from
(select distinct e.department_id, 
	left(pay_date,7) pay_month,
	AVG(amount) 
	over(partition by left(pay_date,7),e.department_id) avg1,
	AVG(amount) over(partition by left(pay_date,7)) avg2
from salary s
inner join employee e 
on s.employee_id=e.employee_id) t
```